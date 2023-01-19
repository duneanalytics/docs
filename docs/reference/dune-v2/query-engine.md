---
title: V2 Query Engines
description: Dune V2 uses Spark and Dune SQL query engines. Learn how they work here!
hide:
  - toc
---

With Dune V2 we’re moving away from a [PostgreSQL](https://www.postgresql.org/) query engine to:

1. Spark SQL - [Apache Spark](https://www.databricks.com/glossary/what-is-apache-spark) hosted on [Databricks](https://docs.databricks.com/getting-started/introduction/index.html).
2. Dune SQL - A self hosted instance of [Trino](https://trino.io/)(**currently in alpha**). 

## Syntax and operator differences

The syntax and keyword operator differences between Postgres, Spark, and Dune SQL are quite minimal, however there are a few to be aware of.

!!! warning
    **Dune SQL is still in alpha!** If you find any other changes in Spark or Dune SQL that are important to note, please feel free to [submit a PR to this docs page on GitHub](https://github.com/duneanalytics/docs/edit/master/docs/reference/dune-v2/query-engine.md) or let us know in #dune-sql. 
    **If you're running into errors using `||`, `concat()`, `replace()`, `trim()`, `length()`, or other operators on bytearrays (things like addresses, transactions, etc)** then check out the [Byte Array Functions](#byte-array-functions-in-dune-sql) section.

### Syntax Comparison

| <div style="width:290px">**Description**</div> | **V1 - PostgreSQL** | **V2 - Spark SQL** | **V2 - Dune SQL** |
| --- | --- | --- | --- |
| **`bytea2numeric` does not exist in Spark.** | `bytea2numeric` (bytea) | `bytea2numeric_v2` (string) | `bytearray_to_integer` (hex) <br> `bytearray_to_bigint` (hex) <br> `bytearray_to_decimal` (hex) <br> `bytearray_to_uint256` (hex) <br> More details on [Byte Array to Numeric Functions](#byte-array-to-numeric-functions)|
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


### Double quotes are not recommended

Using double quotes is not recommended in DuneV2, even when the engine runs your query without returning an error.

This is because the parser sometimes treats words in double quotes as a string and sometimes it treats them as an object like a column name.

For example, referencing a column name in the `WHERE` clause using double quotes works as expected. However, the same query inside a CTE treats the column name as a string, [as can be seen here](https://dune.com/queries/1199604).

## Numerical types
We support the [numerical types](https://trino.io/docs/current/language/types.html) `INTEGER`, `BIGINT`, `DOUBLE`, and fixed precision `DECIMAL` with precision up to 38 digits (i..e, `DECIMAL(38, 0)`). Additionally, we support `UINT256` for representing unsigned 256 bit integers.

## Byte Array to Numeric Functions
- `bytearray_to_integer`, returns the `INTEGER` value of a big-endian byte array of length <= 4 representing the integer in two's complement. If the byte array has length < 4 it is padded with zero bytes.
- `bytearray_to_bigint`, returns the `BIGINT` value of a big-endian byte array of length <= 8 representing the bigint in two's complement. If the byte array has length < 8 it is padded with zero bytes.
- `bytearray_to_decimal`, returns the `DECIMAL(38,0)` value of a big-endian byte array of length <= 16 representing the decimal(38,0) in two's complement. If the byte array has length < 16 it is padded with zero bytes.
- `bytearray_to_uint256`, returns the `UINT256` of a big-endian byte array of length <= 32 representing the unsigned integer. If the byte array has length < 32 it is padded with zero bytes.
- `bytea2numeric` has been deprecated. It is an alias for `bytearray_to_bigint`.

The byte array conversion functions throw an overflow exception if the byte array is larger than the number of bytes supported of the type, even if the most significant bytes are all zero. It is possible to use `bytearray_ltrim` in order to trim the zero bytes from the left.

[Here is an example query](https://dune.com/queries/1847704?d=11) that covers all of the above functions.


## Byte Array Functions in Dune SQL

Dune SQL currently represents byte arrays as `0x`-prefixed strings. In the future we will represent byte arrays using the `varbinary`. To make it simpler to work with byte arrays we have the following helper functions. They simplify interactions with byte arrays, as they automatically account for the `0x`-prefix and use byte index instead of characther index. For instance, the `bytearray_substring` methods take indexes by byte, not by characther (twice the byte array length). If there is an operation you need to do on byte arrays which is not covered by a function in the list below you should reach out to the Dune team. 

*Operators like `||` and functions like `concat()` will no longer work with bytearrays, you will need to `cast(some_bytearray as varchar)` first.*

| Function | Return Type | Argument Types | Description |
| --- | --- | --- | --- |
| bytearray_concat | varchar | varchar, varchar | Concatenates two byte arrays |
| bytearray_length | bigint | varchar | Returns the length of a byte array |
| bytearray_ltrim | varchar | varchar | Removes zero bytes from the beginning of a byte array |
| bytearray_position | bigint | varchar, varchar | Returns the index of a given bytearray (or 0 if not found) |
| bytearray_replace | varchar | varchar, varchar, varchar | Greedily replaces occurrences of a pattern within a byte array |
| bytearray_reverse | varchar | varchar | Reverse a given byte array |
| bytearray_rtrim | varchar | varchar | Removes zero bytes from the end of a byte array |
| bytearray_starts_with | boolean | varchar, varchar | Determines whether a byte array starts with a prefix |
| bytearray_substring | varchar | varchar, integer | Suffix byte array starting at a given index |
| bytearray_substring | varchar | varchar, integer, integer | Sub byte array of given length starting at an index |


## Query queries as views in Dune SQL

All queries written using Dune SQL can be queried as views in other queries using the identifier `query_<queryId>`. For instance:
```
select * from query_1234
```
[Here is an example query](https://dune.com/queries/1746224) which queries [this query](https://dune.com/queries/1746191).
The `queryId` is part of the URL of a query.

**Note**:

- All output columns of the query being queried must be named. That is, you cannot query `select 1` or `select count(*) from ethereum.transactions`, but you can query `select 1 as v` and `select count(*) as total from ethereum.transactions`.
- Parametrized queries are not supported.
- Only public queries can be queried. Support for querying private queries will be added in the future.
- Only saved queries can be queried.
- Only queries written in Dune SQL can be queried.

## Other questions and feedback

As ever, Google is a great friend in answering your SQL questions.

With Dune V2, instead of googling “PGSQL median”, you should now google “Spark SQL median” (for Spark SQL) or “Trino SQL median” (for Dune SQL). 

Both also have well documented index of built in functions on their website:

* [Spark - Spark SQL Language Reference](https://spark.apache.org/docs/latest/sql-programming-guide.html)
* [Trino - Functions and Operators](https://trino.io/docs/current/functions.html)

Our [#dune-sql Discord channel](https://discord.com/channels/757637422384283659/1051871389432422491) is the best place to get help from our team and Wizard community when Google fails you.

As you come across issues or identify areas of improvement, please send us an email at [dunesql-feedback@dune.com](mailto:dunesql-feedback@dune.com) and we’ll work with you to update and optimize!
