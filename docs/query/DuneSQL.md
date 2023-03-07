---
title: DuneSQL
description: DuneSQL datatypes, functions, and operators.
---

!!! warning
    **Dune SQL exited alpha on March 2nd, 2023. We have made some changes to datatypes and column names that introduced breaking changes.** [See DuneSQL changes ](dunesql-changes.md) for more details.  

    For help with migrating queries to compatible data types and general Dune SQL functions, the best place to ask questions is on our [#dune-sql](https://discord.gg/dunecom) Discord channel.



## Dune SQL Data Types and Functions

### Numerical types in DuneSQL
We support the [numerical types](https://trino.io/docs/current/language/types.html) `INTEGER`, `BIGINT`, `DOUBLE`, and fixed precision `DECIMAL` with precision up to 38 digits (i..e, `DECIMAL(38, 0)`). Additionally, we support `UINT256` for representing unsigned 256 bit integers and `INT256` for signed 256 bit integers, using two's complement.


### Byte Array Functions in DuneSQL

Dune SQL represents byte arrays using the `varbinary` type.

To make it simpler to work with byte arrays we have the following helper functions, which work with these two kinds of representation. They simplify interactions with byte arrays, as they automatically account for the `0x`-prefix and use byte index instead of characther index. For instance, the `bytearray_substring` methods take indexes by byte, not by characther (twice the byte array length). 

If there is an operation you need to do on byte arrays which is not covered by a function in the list below you should reach out to the Dune team. 

#### Byte Array Manipulation Functions

| Function | Return Type | Argument Types | Description |
| --- | --- | --- | --- |
| `bytearray_concat` | `varbinary` or `varchar` | `varbinary, varbinary` or `varchar, varchar` | Concatenates two byte arrays |
| `bytearray_length` | `bigint` | `varbinary` or `varchar` | Returns the length of a byte array |
| `bytearray_ltrim` | `varbinary` or `varchar` | `varbinary` or `varchar` | Removes zero bytes from the beginning of a byte array |
| `bytearray_position` | `bigint` | `varbinary, varbinary` or `varchar, varchar` | Returns the index of a given bytearray (or 0 if not found) |
| `bytearray_replace` | `varbinary` or `varchar` | `varbinary, varbinary, varbinary` or `varchar, varchar, varchar` | Greedily replaces occurrences of a pattern within a byte array |
| `bytearray_reverse` | `varbinary` or `varchar` | `varbinary` or `varchar` | Reverse a given byte array |
| `bytearray_rtrim` | `varbinary` or `varchar` | `varbinary` or `varchar` | Removes zero bytes from the end of a byte array |
| `bytearray_starts_with` | `boolean` | `varbinary, varbinary` or `varchar, varchar` | Determines whether a byte array starts with a prefix |
| `bytearray_substring` | `varbinary` or `varchar` | `varbinary, integer` or `varchar, integer` | Suffix byte array starting at a given index |
| `bytearray_substring` | `varbinary` or `varchar` | `varbinary, integer, integer` or `varchar, integer, integer` | Sub byte array of given length starting at an index |

#### Byte Array to Numeric Functions
|  Function | Description  |
|---|---|
| `bytearray_to_integer` | Returns the `INTEGER` value of a big-endian byte array of length <= 4 representing the integer in two's complement. If the byte array has length < 4 it is padded with zero bytes.  |
| `bytearray_to_bigint`  | Returns the `BIGINT` value of a big-endian byte array of length <= 8 representing the bigint in two's complement. If the byte array has length < 8 it is padded with zero bytes.  |
| `bytearray_to_decimal` | Returns the `DECIMAL(38,0)` value of a big-endian byte array of length <= 16 representing the decimal(38,0) in two's complement. If the byte array has length < 16 it is padded with zero bytes.  |
| `bytearray_to_uint256` | Returns the `UINT256` of a big-endian byte array of length <= 32 representing the unsigned integer. If the byte array has length < 32 it is padded with zero bytes.  |
| `bytearray_to_int256` | Returns the `INT256` of a big-endian byte array of length <= 32 representing the signed integer. If the byte array has length < 32 it is padded with zero bytes.  |
| `bytea2numeric` |  This function has been deprecated. It is an alias for `bytearray_to_bigint` |

The byte array conversion functions throw an overflow exception if the byte array is larger than the number of bytes supported of the type, even if the most significant bytes are all zero. It is possible to use `bytearray_ltrim` in order to trim the zero bytes from the left.

[Here is a dashboard](https://dune.com/dune/dune-sql-byte-array-functions-uint256-int256-support) with examples covering all of the above functions.
## Query queries as views in Dune SQL

All non-paramterized queries written using Dune SQL can be queried as views in other queries using the identifier `query_<queryId>`. For instance:
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


