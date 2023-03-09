---
title: Migrating Queries
description: This page provides a guide for migrating queries from Postgres to Dune SQL and from SparkSQL to DuneSQL.   
---


## Syntax and operator differences

The syntax and keyword operator differences between Postgres, Spark, and Dune SQL are quite minimal, here are a few key ones:

### Syntax Comparison

| <div style="width:90px">**Description**</div> | **V1 - PostgreSQL** | **V2 - Spark SQL** | **V2 - Dune SQL** |
| --- | --- | --- | --- |
| **`bytea2numeric`, or casting hex/bytea to a number** | `bytea2numeric` (bytea) | `bytea2numeric_v3` (string) | `bytearray_to_integer` (hex) <br> `bytearray_to_bigint` (hex) <br> `bytearray_to_decimal` (hex) <br> `bytearray_to_uint256` (hex) <br> `bytearray_to_int256` (hex) <br> More details on [Byte Array to Numeric Functions](#byte-array-to-numeric-functions)|
| **Doing math or numeric operations on a column, like value in ethereum.transactions** | sum(value) | sum(value) | sum(cast(value as double)) *soon this won't be needed as UINT and INT columns are added automatically.* |
| **0 vs 1 array based indexing** | 1 indexed | 0 indexed | 1 indexed |
| **Implicit type conversions between character and numeric types** | Available | Available | [Not available](https://trino.io/docs/current/functions/conversion.html) |
| **Addresses** | `\x2A7D...`(bytea)<br><br>Works in Postgres | `0x2a7d...` (string)<br><br>Has to be lowercase in Spark.<br><br>Can be done via `lower('0x2A7D...')` | `0x2a7d...` (Byte array) <br><br> No escape quotes should be used, and the literal does __not__ need to be lowercased. |
| **Selecting keyword columns is different** | "from" | \`from\` | "from" |
| **Alias naming is different** | as "daily active users" | as \`daily active user\` | as "daily active users" |
| **Exponentiation notation** | `x/10^y` or `x * 1e123` | `x*power(10,y)` or `x*1e123` | `x*power(10,y)` or `x * 1e123` |
| **Interval argument has different syntax** | `Interval '1day'` | `Interval '1 day'` | `Interval '1' day` |
| **Generate_series () is now sequence ()** | `generate_series('2022-05-15', CURRENT_DATE, '1 day')` | `explode(sequence(to_date('2022-01-01'), to_date('2022-02-01'), interval 1 day))` | [`unnest(sequence(date('2022-01-01'), date('2022-02-01'), interval '7' day))`](https://dune.com/queries/1764158?d=11)<br><br>Has a 10000 values limit. |
| **Handling decimals for prices.usd** | Don’t use `prices.usd decimals` | Replaced by `prices.tokens decimals` | Replaced by `tokens_[blockchain].erc20.decimals` |
| **Define NULL array** |` NULL::integer[]` | `CAST(NULL AS ARRAY&lt;int&gt;))` | `CAST(NULL AS ARRAY&lt;int&gt;))` |
| **encoding strings to hex** | `encode(string, 'hex')` | `hex(string)` | `hex(string)`<br><br>*available soon |
| **Get json object differences** | `(takerOutputUpdate->'deltaWei'->'value') decode(substring((addressSet->'baseAsset')::TEXT, 4,40), 'hex')` | `get_json_object(get_json_object(takerOutputUpdate,'\(.deltaWei'),'\).value')'0x'` | `json_query(json_query(takerOutputUpdate, 'lax $.deltaWei' omit quotes), 'lax $.value')` |
| **Group by an alias** | `SELECT date_trunc('hour',evt_block_time) as col1, COUNT(*) FROM erc721_ethereum evt_Transfer GROUP BY col1` | Same as PostgreSQL | `GROUP BY date_trunc('hour',evt_block_time)`Or: `GROUP BY 1, 2` |
| **Explicit date/time casting** | `'2021-08-08 17:00'::timestamp` | `cast('2021-08-08 17:00' as timestamp)` | `cast('2021-08-08 17:00' as timestamp)`<br><br>Or, `timestamp '2021-08-08 17:00'`<br><br>There are [many helper functions for casting to date/time types](https://trino.io/docs/current/functions/datetime.html?highlight=date), such as `date(‘2022-01-01’)` |
| **Checking if an item exists in an array** | `value = ANY (array)` | `array_contains(array, value)` | [`contains(array, value)` or `contains_sequence(array, array[values])`](https://trino.io/docs/current/functions/array.html#contains) |
| **Explode** | `SELECT unnest(array) FROM table` | `SELECT explode(array) FROM table` | `SELECT vals.val FROM table1, unnest(arrayFromTable1) as vals(val)`<br><br>you have to use `unnest` with a `cross join`, as described in this [blog post](https://theleftjoin.com/how-to-explode-arrays-with-presto/). |
| **Median** | `PERCENTILE_CONT(0.5) WITHIN GROUP(ORDER BY x)` | `PERCENTILE_CONT(0.5) WITHIN GROUP(ORDER BY x)` | `approx_percentile(x, 0.5)` |
| **Using “is True/False”** | `X is true` | `X is true` | `X = true` |
| **String Data Type** | `varchar` | `string` | `varchar` |
| **Casting as Strings** | `cast([xxx] as string)` | `cast([xxx] as string)` | `cast([xxx] as varchar)` |
| **`left()` is no longer a method available for returning substrings** | `left([string],[length])` | `left([string],[length])` | `substr([string], [start], [length])` <br><br> [Returns varchar; Positions start with 1, so use `1` for length if you want to replicate left() functionality](https://trino.io/docs/current/functions/string.html?highlight=substr#substring) `left(somestring, somenumber) -> substr(somestring, 0, somenumber)`|
| **Aggregate Functions** | `array_agg(col)`, `array_agg(distinct(col))` | `array_agg(col)` or `collect_list(col)`, `collect_set(col)` or `array_agg(distinct(col))` | `array_agg(col)`, `array_agg(distinct(col))` |
| **user generated views** | create view dune_user_generated.table | none | each query is a view, like [query_1747157](https://dune.com/queries/1747157) |
| **event logs topic indexing** | topic 1,2,3,4 | topic 1,2,3,4 | topic 0,1,2,3 |

#### Double quotes are not recommended for SparkSQL

Using double quotes is not recommended in DuneV2 SparkSQL, even when the engine runs your query without returning an error. This is because the parser sometimes treats words in double quotes as a string and sometimes it treats them as an object like a column name.

For example, referencing a column name in the `WHERE` clause using double quotes works as expected. However, the same query inside a CTE treats the column name as a string, [as can be seen here](https://dune.com/queries/1199604).
