---
title: REWORK
description: Get the most out of DuneSQL by writing efficient queries.
---

**Writing efficient queries is essential for getting the most out of Dune. This guide will help you understand how to write efficient queries on DuneSQL.**

In order to write efficient queries on DuneSQL, it's important to understand the underlying architecture of the system. This guide will help you understand how DuneSQL works under the hood so you can write more efficient queries and get the most out of Dune. 

## Understanding DuneSQL

DuneSQL is a TrinoSQL-based query engine designed for handling data stored in a columnar format. More spcifically, we use Parquet files as the underlying storage format. This allows for efficient data access and query processing, as well as fast data loading and data compression.

### Short Introduction to Databases

Let's start with a short introduction into databases so we can understand what we need to optimize for when writing queries on DuneSQL.

At their core, databases are sophisticated systems designed to store, retrieve, and manage data. Their primary goal is to provide fast, efficient, and reliable access to vast amounts of structured information. You can think of a database as a collection of tables, where each table is a collection of rows and columns. Conceptually, these tables exist in two ways:

- **Logical**: The logical view of a table is the way the data is organized and presented to the user. This is the view you see when you query a table.
- **Physical**: The physical view of a table is the way the data is stored on disk. This is the view you see when you look at the underlying files that make up the table.

Databases are designed to optimize for the logical view of a table, which is the view that users interact with. However, the physical view of a table is also important, as it determines how the data is stored and accessed. In order to optimize the usability of the logical view of a table, databases use a variety of techniques to optimize the physical view of a table. These techniques include:

- **Data partitioning**: Data partitioning is a technique that divides data into smaller chunks called partitions. This reduces the amount of data that needs to be stored and accessed, which improves performance.
- **Data indexing**: Data indexing is a technique that creates a data structure called an index. This data structure contains information about the data in a table, which allows the database to quickly find the data it needs.
- **Data storage layout**: Data storage layout relates to how the data is stored on disk. This includes the file format, how the data is physically stored on disk, and how the data is organized in memory. The right data storage layout can significantly improve performance. 
- **Data compression**: Data compression is a technique that reduces the size of data by removing redundant information. This reduces the amount of data that needs to be stored and accessed, which improves performance.
- **Data caching**: Data caching is a technique that stores frequently accessed data in memory. This reduces the amount of data that needs to be stored and accessed, which improves performance.

For the most part, these techniques are employed in the background and are not visible to the user. However, understanding how **data partitioning**, **data indexing** and the **data storage layout** work is essential for writing efficient queries on DuneSQL.

Databases employ these techniques to combat their most significant challenge: **the I/O bound nature of data storage**. I/O bound refers to the fact that the speed of data access is limited by the speed of the storage device. Read speed, the time it takes to load data from storage to memory, is an essential constraint of databases.

Every time you query a table, the database needs to read the data from disk into memory. This happens in a unit called a page. Pages are the smallest unit of data that can be read from disk into memory. Since reading pages from disk is slow, databases try to minimize the number of pages that need to be read into memory when querying a table. This is where data partitioning and data indexing come into play. In the next section, we'll take a closer look at how DuneSQL works and how you can write queries that minimize the number of pages that need to be read into memory. 

**To quickly summarize:** The goal of a database is to provide fast, efficient, and reliable access to vast amounts of structured information. In the end, we want to access the logical view of a table as quickly as possible. To do this, database administrators use a variety of techniques to optimize the physical view of a table. These techniques include data partitioning, data indexing, data compression, and data caching. The goal of these techniques is to minimize the number of pages that need to be read into memory when querying a table.

### DuneSQL Architecture

Now that we understand how databases work, let's take a look at how DuneSQL works under the hood. Specifically, let's look at how data is stored and accessed in DuneSQL.

Dune stores data in parquet files, which are first and foremost columnar storage files, but also ultilize some of the advantages of row-oriented storage. Data in parquet systems is partitioned by rows into multiple parquet files, and within each file, the data is further partitioned into row groups. However, the pages inside of row groups store data in columns rather than rows. As a result, the database appears row-oriented at a higher level, but it reads data from column-oriented pages when accessing specific values. Additionally, each parquet file contains metadata about the data it stores, mainly **min/max** column statistics for each column. This allows the database to efficiently skip entire parquet files or row groups within files while scanning through a table, provided that the column contains values that are not random and can be ordered.

In a very simplified schematic view, our `ethereum.transactions` table is stored in a parquet file that looks like this:

<p align="center">
  <img src="/docs/query/images/minmax-schema2.jpeg" alt="Parquet file schema" title="Parquet schema" /><br />
  <em>Example of contents of a parquet file</em>
</p>

Please note that this is a simplified view, usually there are hundreds or thousands of rows in a row group and hundreds of row groups in a parquet file.

The Parquet File consists of multiple row groups, each row group contains multiple column chunks, and each column chunk contains multiple pages. The pages are the smallest unit of data that can be read from disk into memory. The column chunks contain the actual data that is needed for the query. Each file has a footer that contains metadata about the data it stores, mainly **min/max** column statistics for each column. This allows the database to efficiently skip entire parquet files or row groups within files while scanning through a table, provided that the column contains values that are not random and can be ordered. **Writing queries that take advantage of this is essential for writing efficient queries on DuneSQL.**  
 


<p align="center">
  <img src="/docs/query/images/parquet.png" alt="Parquet file schema" title="Parquet schema" /><br />
  <em>Schematic view of a parquet file</em>
</p>

What's important to understand here is that the traditional index structure of a database is not needed in DuneSQL. Instead, the ``min/max`` values of each column are used to efficiently skip entire parquet files or row groups within files while scanning through a table, provided that the column contains values that are not random and can be ordered. This is a key difference between DuneSQL and e.g. Snowflake.

If you query a table in DuneSQL, the system will access the data in the following order:

1. **File Level:** At the foundational level, the query engine locates the specific parquet files associated with the table or a portion of the table being queried. It reads the metadata contained in the footer of each parquet file to determine whether it might contain the data needed for the query. It will skip any files that do not contain the data needed for the query. 

2. **Row Group Level:** Once the appropriate Parquet file is identified, the engine will access the relevant row groups within the file, based on the query conditions. Again, it will first read the metadata of each row group to determine whether it might contain the data needed for the query. If the row group does not contain the data needed for the query, it will skip the row group and move on to the next one.

3. **Column Chunk Level:** Once the appropriate row group is identified, the system will access the relevant column chunks within the row group, based on the query conditions. The column chunks contain the actual data that is needed for the query. The database will only read the column chunks that contain the data needed for the query. It will not read the logical row - saving time and resources.

4. **Page Level:** Within the column chunk, the data is further segmented into pages. The database reads these pages into memory, benefiting from any compression or encoding optimizations.


The engine will repeat this process for each parquet file and row group that might contain the data needed for the query. Once all the data is read into memory, the system will process the data and return the results to the user.    
If the query is too large to fit in memory, the data will "spill" from memory to disk. This is called a "spill to disk" and is a common occurrence in databases. This will negatively impact query performance, as reading data from disk is much slower than reading data from memory. To avoid this issue, it's important to write efficient queries that minimize the amount of data that needs to be read into memory.

### Tips for Writing Efficient Queries on DuneSQL 

To write efficient queries on DuneSQL, it's crucial to use filter conditions based on columns that are are not random and can be ordered. Columns like `block_time` and `block_number` are the best candidates for this, as they are sequentially ordered and can be used to efficiently skip entire parquet files or row groups within files while scanning through a table.

Let's take a look at an example. Say you want to query the `ethereum.transactions` table for a specific transaction hash. The query would usually look like this:

```sql
SELECT * FROM ethereum.transactions
WHERE hash = 0xce1f1a2dd0c10fcf9385d14bc92c686c210e4accf00a3fe7ec2b5db7a5499cff;
```

using the steps above the query engine would do the following:

1. **File Level:** The query engine tries to locate the specific parquet files associated with the table or a portion of the table being queried. It reads the metadata contained in the footer of each parquet file to determine whether it might contain the data needed for the query. It will try to skip any files that do not contain the data needed for the query. However, since the query is based on a random hash, the engine will not be able to skip any files. It will have to read all the files associated with the table.

We can stop going through the steps here, as the query engine will have to read almost all the files and row groups associated with the table. This will negatively impact query performance, as having to read all pages from all column chunks in all row groups in all parquet files is very inefficient. There might be some very unlikely edge cases where the engine can skip some files, but in general, the engine will have to read all the files associated with the table. An example of a row group or column chunk that can be skipped for this query is if the hash column for a row group or file miraculously contains only values from ``0xd... - 0xz...``. In that case, since our hash is ``0xc...``, there is no way that the row group or file contains the hash we are looking for, and the engine can skip it. However, this is very unlikely to happen, and most likely the engine will have to read all the files associated with the table.

Now let's take a look at a query that uses a column that is not random and can be ordered, such as `block_number`:

```sql
SELECT * FROM ethereum.transactions
WHERE block_number = 14854616
AND hash = 0xce1f1a2dd0c10fcf9385d14bc92c686c210e4accf00a3fe7ec2b5db7a5499cff
``` 

using the steps above the query engine would do the following:

1. **File Level:** The query engine tries to locate the specific parquet files associated with the table or a portion of the table being queried. It reads the metadata contained in the footer of each parquet file to determine whether it might contain the data needed for the query. In this case, the engine will check whether the `block_number` we are searching for is within the range of `min/max` values for the `block_number` column in the footer of each parquet file. For example, if the engine starts reading the first parquet file and sees that the `min/max` values for the `block_number` column are `14854600` and `14854620`, it will know that the file does not contain the data needed for the query. It will skip the file and move on to the next one. This will significantly reduce the amount of data that needs to be read into memory, which will improve query performance.

2. **Row Group Level:** Once the appropriate Parquet file is identified, the engine will access the relevant row groups within the file, based on the query conditions. Again, it will first read the metadata of each row group to determine whether it might contain the data needed for the query. If the row group does not contain the data needed for the query, it will skip the row group and move on to the next one. This will further reduce the amount of data that needs to be read into memory, which will improve query performance.

3. **Column Chunk Level:** Once the appropriate row group is identified, the system will access the relevant column chunks within the row group, based on the query conditions. The column chunks contain the actual data that is needed for the query. The database will only read the column chunks that contain the data needed for the query. It will not read the logical row - saving time and resources.

4. **Page Level:** Within the column chunk, the data is further segmented into pages. The database reads these pages into memory, benefiting from any compression or encoding optimizations.

As you can see, the query engine can skip entire parquet files and row groups within files while scanning through a table, provided that the column contains values that are not random and can be ordered. This is why it's important to use filter conditions based on columns that are not random and can be ordered, such as `block_number` and `block_time`.

The above example is pretty theoretical, as you will most likely not be querying the `ethereum.transactions` table for a specific transaction hash. However, the same principle applies to other tables and queries. For example, if we want to query `ethereum.transactions` for all transactions to a specific smart contract, we can use `block_number` or `block_time` to skip entire parquet files and row groups within files while scanning through the table. 

Usually you would write a query like this:

```sql
Select 
  *
FROM ethereum.traces
WHERE to = 0x510100D5143e011Db24E2aa38abE85d73D5B2177
```

With our new knowledge, we can deduct that this query will be very inefficient, as the engine will have to read almost all the files and row groups associated with the table. Instead, we can write the query like this:

```sql
Select 
  *
FROM ethereum.traces
where block_number > 17580247
and to = 0x510100D5143e011Db24E2aa38abE85d73D5B2177
```

By including the `block_number` column in the query, the engine can quickly narrow down the search to files and row groups that have a `block_number` greater than `17580247`. This significantly reduces the amount of data that needs to be read, thereby improving query performance.

We can also apply the same principle to join tables. For example, if we want to join the `ethereum.transactions` on `uniswap_v3_ethereum.Pair_evt_Swap` table, we can write the query like this:

```sql
Select
  to,
  "from",
  value,
  block_time,
  sqrt_price_x96,
FROM
  uniswap_v3_ethereum.Pair_evt_Swap swap
  join ethereum.transactions t 
    on swap.evt_tx_hash = t.hash
    and swap.evt_block_number = t.block_number
where
  swap.contract_address = 0x510100D5143e011Db24E2aa38abE85d73D5B2177
```

By including the `block_number` column in the join condition, the engine can quickly narrow down the search in `ethereum.transactions` to files and row groups that contain the `block_number` contained in a specific row in `uniswap_v3_ethereum.Pair_evt_Swap`. This significantly reduces the amount of data that needs to be read, thereby improving query performance.

Now for variousreasons that only the TrinoSQL developers know, it also makes a difference whether we join `ethereum.transactions` on `uniswap_v3_ethereum.Pair_evt_Swap` or the other way around. The following query will be even faster:

```sql
Select
  to,
  "from",
  value,
  block_time,
  sqrt_price_x96
FROM ethereum.transactions t
join uniswap_v3_ethereum.Pair_evt_Swap swap
  on t.hash = swap.evt_tx_hash
  and t.block_number = swap.evt_block_number
where
  swap.contract_address = 0x510100D5143e011Db24E2aa38abE85d73D5B2177
```

This join order optimization is related to the size of the tables. **You should always join the smaller table on the bigger table**. In this case, `ethereum.transactions` is much bigger than `uniswap_v3_ethereum.Pair_evt_Swap`, so we should join `uniswap_v3_ethereum.Pair_evt_Swap` on `ethereum.transactions`. 

Additionally, to enjoy these optimizations, **you will have to use inner joins**. Left joins and right joins will not benefit in the same way.


### Exceptions
A notable exception to the general rule of using sequentially ordered columns is the Solana dataset `account_activity`, which is ordered by `account_keys` rather than `block_time`. This allows for utilizing the min/max values for `account_keys` when building queries based on raw Solana data.

## Additional Tips for Writing Efficient Queries on DuneSQL

In addition to leveraging the columnar storage format and using sequentially ordered columns, as discussed in the previous section, here are more tips to help you write efficient queries on DuneSQL with TrinoSQL:

1. **Limit the columns in the SELECT clause**: Only request the columns you need, as it reduces the amount of data the query engine needs to process.

2. **Use the LIMIT clause**: If you're only interested in a specific number of rows, use the LIMIT clause to avoid processing more data than necessary.

3. **Leverage partition pruning**: If your data is partitioned, use partition keys in the WHERE clause to help the query engine prune unnecessary partitions and reduce the amount of data scanned. In Dune almost all tables are partitioned by time and/or block number.

4. **Filter early and use predicate pushdown**: Apply filters as early as possible in the query to reduce the amount of data being processed. This takes advantage of predicate pushdown, which pushes filter conditions down to the storage layer, reducing the amount of data read from storage.

5. **Use window functions**: Window functions can be more efficient than self-joins or subqueries for computing aggregations over a set of rows related to the current row.

6. **Avoid using DISTINCT when possible**: DISTINCT can be computationally expensive, especially on large datasets. If you can use GROUP BY or other aggregation methods to achieve the same result, it may improve query performance. Try using approx_distinct instead.

7. **Optimize subqueries**: Subqueries can sometimes cause performance issues. Consider using Common Table Expressions (CTEs) or rewriting the query using JOINs to optimize subqueries.

8. **Optimize data types**: Use appropriate data types for your columns, as it can improve query performance by reducing the amount of data processed. For example, varbinary operations are faster that varchar so be careful casting around too much.

By following these tips, you can write more efficient queries on DuneSQL with TrinoSQL and optimize the performance of your data processing tasks. Remember that DuneSQL's unique structure, such as the parquet file format and columnar storage, should be taken into account when optimizing your queries to fully benefit from the system's capabilities.
