---
title: Storage
description: Learn more about the differences and thinking behind our V2 database structure.
---

On a very high level, databases read data from storage into memory in order to allow that data to be operated on, in our case to transform and return blockchain data according to your Dune query’s logic. 

Read speed, the time it takes to load data from storage to memory, is an essential constraint of databases. In computer science this is referred to as [I/O bound](https://en.wikipedia.org/wiki/I/O_bound), and it’s one of the main challenges we are looking to tackle with our transition to a data lake in Dune V2 and separating storage and compute.

Let’s see how this happens.

## Row oriented databases

Databases store data in pages, which traditionally contain rows of information.

Multiple pages make one data file and a table will consist of one or more data files.

![row oriented database (PostgreSQL)](images/row-oriented.png)

When retrieving data from storage in order to operate on said data, a database will read data into memory by the page. Page size and the number of pages loaded are key bottlenecks for query speed as the number and size of pages loaded means longer read times and more waiting for your query results to be returned.

Since traditional databases store pages by row, they are best suited for retrieving all columns of one row or data from multiple sequential rows.

Whether we are looking to retrieve all columns from row 10 or column 3 from rows 11-25, our queries will be fast as only one page will need to be read into memory.

In contrast, querying for data which is stored in many different logical rows and therefore different physical pages is an expensive operation, as all the pages must be read from disk.

Most of the queries we run on Dune today are aggregation of data points in a column over thousands if not millions of rows.

This is because each of our rows is based on one transaction or trace from the blockchains we’re querying.

So for example, if we want to see all the swaps between ETH and USDC in the last month, transactions will be spread across thousands of transactions and thus thousands of rows - but the data will all be within one column of each of these rows.

Thus, in a row-oriented database, we end up loading many pages with unneeded data as we query for one column across thousands or millions of rows.

In PostgreSQL, we use indexes to look for specific subsets of data rather than reading entire pages/tables filled with extraneous data.

This leads to very fast and efficient Queries, but is limited to indexed columns.

Since every new index created for a table is a new database file, it is harder to update and maintain the table at scale.

Therefore, Dune V2 runs on column-oriented, rather than row-oriented tables.


## Column oriented database

![column oriented database (Spark)](images/column-oriented.png)

In Dune V2, we store our data on AWS S3 using the [parquet file format](https://github.com/apache/parquet-format).

Parquet is sometimes described as a hybrid approach between row-oriented databases and column-oriented databases since a table still consists of multiple parquet files which are themselves partitioned by rows.

Inside of the parquet files, though, the pages themselves contain columns instead of rows.

Pages are stored within row groups which partition the data by rows inside the parquet files.

Thus, the database is still roughly stored in a row oriented format but the individual values are stored in column orientation inside pages.

![schematic view of parquet files](images/parquet.png)

Even though the database at large is somewhat row-oriented, when we actually want to read data we are reading from column-oriented pages and thus are reading pages into memory by column.

In contrast, should we try to query for all columns of specific logical rows, we have to access lots of different pages as the data of one logical row is no longer stored in one page, but rather distributed across lots of different pages.

To better understand rows vs columns, check out this video on the differences:

![type:video]([https://youtu.be/Vw1fCeD06YI](https://youtu.be/Vw1fCeD06YI))


### To index, or not to index?

We were sometimes able to mimic the efficiency of column-based data in V1’s PostgreSQL by creating large amounts of structured subset data in the form of indexes, but for now this doesn't scale.

Each parquet file has a footer that contains `min/max` values for every column stored within.

This pattern is repeated on a column chunk level, which stores this metadata for the columns within a specific row group within the parquet file.

![schematic view of mix/max values](images/minmax-schema.jpg)

Using these `min/max` values, both on a file level and on a column chunk level allows the database to efficiently skip over entire parquet files or column chunks within parquet files while scanning through a table. For the min/max values to be useful, and the chunk skipping to work, the column must be correlated with the sorting of the file.

Unfortunately, the `min/max` values of strings are oftentimes not very useful.

For example, `tx_hash` strings and `address` strings in blockchain systems are not suited well for this kind of `min/max` data gathering since they are randomly generated.

So if we sort tables by `block_time` (which we do in almost all circumstances), we can’t effectively `min/max` by `tx_hash` or `address` strings as these data won’t be sequentially ordered.

That means the database won't be able to skip files or column chunks based on these strings, and Queries that reference them will therefore be quite inefficient since all related pages will need to be read into memory.

That said, since the Query engine at large is still able to read through individual columns in which these strings are stored very efficiently, most of the time this won't make a big difference in your Query execution speed.

The performance cost is mostly relevant for base tables like `ethereum.transactions`, `bnb.logs`, `erc20_ethereum.erc20_evt_transfer`, etc. which contain very large datasets that aren’t pre-filtered.

A notable exception to this is the Solana dataset `account_activity`_,_ which is ordered by `account_keys` rather than `block_time` like the EVM-based datasets.

This allows us to utilize the `min/max` values for the `account_keys` when building Queries based on [raw Solana data](../tables/raw/solana/index.md).


## Dune V2 Query examples

Equipped with the above knowledge, let's look at how some Queries on Dune V2 work.

!!! note
    These examples are written in Spark SQL.

### Querying for transaction hashes

```sql

Select * from ethereum.transactions

where hash = '0xce1f1a2dd0c10fcf9385d14bc92c686c210e4accf00a3fe7ec2b5db7a5499cff'

```

Based on the way our parquet file system works, this Query is very inefficient.

Our only filter condition here is a `hash` string so we’re asking the query engine to read all pages that store `tx_hash` column data.

The engine can skip a few column chunks where the `min/max` value stored in the parquet file footer is `0xa0 - 0xcd`, but those will be a rare exception.

Given we’re doing a full scan over the entire history of Ethereum Mainnet (billions of rows) to search for one `hash`, it's pretty impressive that this Query only takes about 6 minutes to run.

Since querying for ‘hash’ is a very common part of a Wizard’s workflow, let's think about how we can make this faster.

To do that, we just have to search based on a column that has sequential ‘min/max’ values so our query engine can skip over most pages/column chunks.

Both ‘block_time’ and ‘block_number’ are useful for this purpose.

```sql

Select * from ethereum.transactions

where block_number = 14854616

and hash = '0xce1f1a2dd0c10fcf9385d14bc92c686c210e4accf00a3fe7ec2b5db7a5499cff'

```

This Query is still not as fast as in PostgreSQL, where we can make use of [B-tree indexes](https://en.wikipedia.org/wiki/B-tree), but with a runtime of 13 seconds, we’re pretty close.

Again, by using our `where` clause to filter by block number, we’re leveraging the V2 engine’s ability to read the parquet file footers’ ‘min/max’ values and skip those that are out of bounds.

Once a parquet file that meets our condition is found, the engine simply loads into memory the relatively few pages from the column chunk with a `min` lower and a `max` greater than our specified `block_number` before finding a match to our ‘hash’ condition.

Since we are selecting all entries from the logical row in this Query, we actually need to access a few other pages as well, but this is a reasonably efficient operation if we only do this for a few rows.

**Lesson:** Define your conditions in a way in which the database is able to work with ‘min/max’ values of files and columns chunks so it can efficiently find the logical row(s) you need.


### Aggregating data over a large amount of logical rows

This is mainly a case study to illustrate how efficient DuneV2 is in aggregating data over a large set of logical rows.

```sql

Select avg(gas_used) from ethereum.transactions

```

This Query runs in an **amazing** 7 seconds.

This is mainly due to the fact that V2 doesn’t have to read the entire table since all this data is stored together in column-oriented pages across parquet files.

In V1’s PostgreSQL, each page we read into memory would have contained a lot of unneeded data.

In Dune V2, we can just read the data that we actually need.

**Lesson:** Querying for data across a large amount of logical rows is now much more efficient and a lot of Queries that were formerly sheer impossible due to timing out are now able to be executed.

Another good example to illustrate this is [@hildobby's](https://twitter.com/hildobby_) [Ethereum Overview](https://dune.com/hildobby/Ethereum-Overview) Dashboard.


## We’ll keep innovating

Some Queries that were heavily indexed on our V1 database might feel a bit awkward in Dune V2.

This is especially the case for `erc20` event transfer tables, `ethereum.transactions`, `ethereum.logs` and their counterparts on other blockchains.

This is a tradeoff we made to enable blockchain analytics on a large scale basis.

We will continue to keep innovating on these datasets and our database architecture to make every Query run as fast as possible on V2. Hopefully now you understand why Queries for data like `tx_hash` will be slow due to the tradeoffs we’ve made.

If you have any feedback or run into trouble with the new system, our #dune-sql Discord channel is the best place to get help from our team and Wizard community when Google fails you.

As you come across issues or identify areas of improvement, please send us an email at [dunesql-feedback@dune.com](mailto:dunesql-feedback@dune.com) and we’ll work with you to update and optimize!