[View code on GitHub](https://dune.com/docs/query/storage.md)

# Storage

The Storage section of the Dune Docs app technical guide provides an overview of the differences and thinking behind the V2 database structure. The guide explains how databases read data from storage into memory to transform and return blockchain data according to Dune queries' logic. The guide focuses on the differences between row-oriented and column-oriented databases and how they affect query speed.

The guide starts by explaining how databases store data in pages, which traditionally contain rows of information. Multiple pages make one data file, and a table consists of one or more data files. The guide then explains how databases read data into memory by the page, and page size and the number of pages loaded are key bottlenecks for query speed. The guide explains that traditional databases store pages by row and are best suited for retrieving all columns of one row or data from multiple sequential rows. 

The guide then explains that Dune V2 runs on column-oriented tables, which store data on AWS S3 using the parquet file format. The guide explains that parquet is a hybrid approach between row-oriented databases and column-oriented databases since a table still consists of multiple parquet files, which are themselves partitioned by rows. Inside the parquet files, the pages themselves contain columns instead of rows. The guide explains that the database is still roughly stored in a row-oriented format, but the individual values are stored in column orientation inside pages. 

The guide then explains how the database uses min/max values to efficiently skip over entire parquet files or column chunks within parquet files while scanning through a table. The guide explains that the performance cost is mostly relevant for base tables like ethereum.transactions, bnb.logs, erc20_ethereum.erc20_evt_transfer, etc., which contain very large datasets that aren't pre-filtered. 

The guide provides examples of Dune V2 queries and how they work. The first example queries for transaction hashes, and the guide explains how the query is inefficient because the only filter condition is a hash string. The guide explains that the query engine can skip a few column chunks where the min/max value stored in the parquet file footer is 0xa0 - 0xcd, but those will be a rare exception. The guide provides a more efficient query that filters by block number. 

The guide also provides an example of aggregating data over a large amount of logical rows. The guide explains that this is mainly a case study to illustrate how efficient DuneV2 is in aggregating data over a large set of logical rows. 

The guide concludes by stating that Dune will continue to innovate on these datasets and its database architecture to make every query run as fast as possible on V2. The guide encourages users to send feedback or identify areas of improvement to optimize the system.
## Questions: 
 1. What is the difference between row-oriented and column-oriented databases, and why did Dune V2 choose to use a column-oriented approach?
- Row-oriented databases store data in pages by row, while column-oriented databases store data in pages by column. Dune V2 chose to use a column-oriented approach because it is more efficient for querying data across a large amount of logical rows, which is common in blockchain systems.

2. How does Dune V2 handle indexing, and what are the limitations of this approach?
- Dune V2 uses the `min/max` values stored in the footer of each parquet file to efficiently skip over entire files or column chunks while scanning through a table. However, the `min/max` values of strings are oftentimes not very useful, which can make queries that reference them inefficient since all related pages will need to be read into memory.

3. How does Dune V2 make querying for data across a large amount of logical rows more efficient?
- Dune V2 stores data in column-oriented pages across parquet files, which allows it to read only the data that is actually needed for a query. This makes querying for data across a large amount of logical rows much more efficient and enables queries that were formerly impossible due to timing out.