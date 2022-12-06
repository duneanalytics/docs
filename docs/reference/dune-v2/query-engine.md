---
title: V2 Query Engines
description: Dune V2 uses Spark and Dune SQL query engines. Learn how they work here!
hide:
  - toc
---

With Dune V2 we’re moving away from a [PostgreSQL](https://www.postgresql.org/) query engine to:

1. [Apache Spark](https://www.databricks.com/glossary/what-is-apache-spark) hosted on [Databricks](https://docs.databricks.com/getting-started/introduction/index.html).
2. A self hosted instance of [Trino](https://trino.io/). 

## Syntax and operator differences

The syntax and keyword operator differences between Postgres, Spark, and Dune SQL are quite minimal, however there are a few to be aware of.

!!! warning
    **Dune SQL is still in alpha!** If you find any other changes in Spark or Dune SQL that are important to note, please feel free to [submit a PR to this docs page on GitHub](https://github.com/duneanalytics/docs/edit/master/docs/reference/dune-v2/query-engine.md) or let us know in #dune-sql.

### Double quotes are not recommended

Using double quotes is not recommended in DuneV2, even when the engine runs your query without returning an error.

This is because the parser sometimes treats words in double quotes as a string and sometimes it treats them as an object like a column name.

For example, referencing a column name in the `WHERE` clause using double quotes works as expected. However, the same query inside a CTE treats the column name as a string, [as can be seen here](https://dune.com/queries/1199604).

### Syntax Comparison

| <div style="width:290px">**Description**</div> | **V1 - PostgreSQL** | **V2 - Dune SQL** | **V2 - Spark SQL** |
| --- | --- | --- | --- |
| **`bytea2numeric` does not exist in Spark.** | `bytea2numeric` (bytea) | `bytea2numeric` (string) | `bytea2numeric_v2` (string) |
| **0 vs 1 array based indexing** | 1 indexed | 1 indexed | 0 indexed |
| **Implicit type conversions between character and numeric types** | Available | [Not available](https://trino.io/docs/current/functions/conversion.html) | Available |
| **bytea vs string for address, tx hash, etc…** | `\x2a7d...` (bytea) | depending on [bytearray outcome](https://docs.google.com/document/d/1X47-aJs6Yw0h-HZD9O2q1Hs6H1yGZZfOM2E47sPh05M/edit#heading=h.wz929gyolmil) | `0x2a7d...` (string) |
| **Addresses (strings) are lower case in dune v2** | `\x2A7D...`(bytea)<br><br>Works in Postgres | depending on [bytearray outcome](https://docs.google.com/document/d/1X47-aJs6Yw0h-HZD9O2q1Hs6H1yGZZfOM2E47sPh05M/edit#heading=h.wz929gyolmil) | `0x2a7d...` (string)<br><br>Has to be lowercase in Spark.<br><br>Can be done via `lower('0x2A7D...')` |
| **Selecting keyword columns is different** | `"from"` | `"from"` | `'from'` |
| **Alias naming is different** | as `"daily active users"` | as `"daily active users"` | as `'daily active user'` |
| **Exponentiation notation** | `x/10^y` or `x * 1e123` | `x*power(10,y)` or `x * 1e123` | `x*power(10,y)` or `x*1e123` |
| **Interval argument has different syntax** | `Interval '1day'` | `Interval '1' day` | `Interval '1 day'` |
| **Generate_series () is now sequence ()** | `generate_series('2022-05-15', CURRENT_DATE, '1 day')` | `values(sequence(cast('2022-01-01' as date) - interval '7' day,cast('2022-02-01' as date),interval '1' day))`<br><br>Has a 10000 values limit. | `explode(sequence(to_date('2022-01-01'), to_date('2022-02-01'), interval 1 day))` |
| **Decimals are no longer in prices.usd** | Don’t use `prices.usd decimals` | Replaced by `tokens_blockchain.erc20.decimals` | Replaced by `prices.tokens decimals` |
| **Define NULL array** |` NULL::integer[]` | `CAST(NULL AS ARRAY&lt;int&gt;))` | `CAST(NULL AS ARRAY&lt;int&gt;))` |
| **encoding strings to hex** | `encode(string, 'hex')` | `hex(string)`<br><br>*available soon | `hex(string)` |
| **Get json object differences** | `("takerOutputUpdate"->'deltaWei'->'value') decode(substring(("addressSet"->'baseAsset')::TEXT, 4,40), 'hex')` | `json_query(json_query(takerOutputUpdate, 'lax $.deltaWei' omit quotes), 'lax $.value')` | `get_json_object(get_json_object(takerOutputUpdate,'\(.deltaWei'),'\).value')'0x'` |
| **Group by an alias** | `SELECT date_trunc('hour',evt_block_time) as col1, COUNT(*) FROM erc721_ethereum evt_Transfer GROUP BY col1` | `GROUP BY date_trunc('hour',evt_block_time)`Or: `GROUP BY 1, 2` | Same as PostgreSQL |
| **Explicit date/time casting** | `'2021-08-08 17:00'::timestamp` | `cast('2021-08-08 17:00' as timestamp)`<br><br>Or, `timestamp '2021-08-08 17:00'`<br><br>There are [many helper functions for casting to date/time types](https://trino.io/docs/current/functions/datetime.html?highlight=date), such as `date(‘2022-01-01’)` | `cast('2021-08-08 17:00' as timestamp)` |
| **Checking if an item exists in an array** | `value = ANY (array)` | `contains(array,value)` | array_contains(array, value)` |
| **Explode** | `SELECT unnest(array) FROM table` | `SELECT vals.val FROM table1, unnest(arrayFromTable1) as vals(val)`<br><br>you have to use `unnest` with a `cross join`, as described in this [blog post](https://theleftjoin.com/how-to-explode-arrays-with-presto/). | `SELECT explode(array) FROM table` |
| **Median** | `PERCENTILE_CONT(0.5) WITHIN GROUP(ORDER BY x)` | `approx_percentile(x, 0.5)` | `PERCENTILE_CONT(0.5) WITHIN GROUP(ORDER BY x)` |
| **Using “is True/False”** | `X is true` | `X = true` | `X is true` |