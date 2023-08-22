---
title: How to Write Efficient Queries on DuneSQL
description: Get the most out of DuneSQL by writing efficient queries.
---

**Writing efficient queries is essential for getting the most out of DuneSQL. This guide will help you understand how to write efficient queries on DuneSQL.**

## DuneSQL architecture

DuneSQL is a TrinoSQL-based query engine designed for handling data stored in a columnar format on Dune.com. In Dune, the data is stored using the parquet file format, which combines row-oriented and column-oriented approaches. Understanding the nuances of parquet file storage and how it impacts query efficiency is essential for creating optimized queries on DuneSQL.

### Parquet Files and Columnar Storage

In parquet files, the data is partitioned by rows into multiple parquet files, and within each file, the data is further partitioned into row groups. However, the pages inside row groups store data in columns rather than rows. As a result, the database appears row-oriented at a higher level, but it reads data from column-oriented pages when accessing specific values.

![schematic view of parquet files](images/parquet.png)

When querying for specific columns, this structure allows for efficient data access. On the other hand, if a query requires all columns of specific logical rows, multiple pages must be accessed since the data of one logical row is distributed across different pages.

![column oriented database (Spark)](images/column-oriented.png)

### Min/Max Values and Efficient Queries

Each parquet file has a footer containing min/max values for every column stored within. This pattern is also repeated on a row group level, which stores metadata for columns within a specific row group. These min/max values enable the database to efficiently skip entire parquet files or row groups within files while scanning through a table, provided that the column is correlated with the file's sorting.

However, the min/max values of strings, such as tx_hash strings and address strings in blockchain systems, are often not helpful, as they are randomly generated and not sequentially ordered. As a result, queries that reference these strings will be inefficient since all related pages need to be read into memory.

![min/max values](../query/images/minmax-schema.jpg)

### Writing Efficient Queries

To write efficient queries on DuneSQL, it's crucial to use filter conditions based on columns that are sequentially ordered and correlated with the file's sorting. Columns like `block_time` and `block_number` are suitable for this purpose. For instance, consider the following optimized query:

```sql
SELECT * FROM ethereum.transactions
WHERE block_number = 14854616
AND hash = 0xce1f1a2dd0c10fcf9385d14bc92c686c210e4accf00a3fe7ec2b5db7a5499cff;
```

By including the block_number column in the query, the engine can narrow down the search to a specific block, reducing the amount of data scanned and considerably speeding up the query.

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

9. **Make sure to join the smaller table to the larger table**: This saves on memory use and will make your queries run faster. So you should be joining erc20 transfers onto ethereum transactions (as an example). 

By following these tips, you can write more efficient queries on DuneSQL with TrinoSQL and optimize the performance of your data processing tasks. Remember that DuneSQL's unique structure, such as the parquet file format and columnar storage, should be taken into account when optimizing your queries to fully benefit from the system's capabilities.

!!! example  "Query still not running? Try materialized views (beta)"

    If your query still runs out of memory or time, try taking subquerys of it into a [materialized views](https://dune.com/docs/query/materialized-views/).
