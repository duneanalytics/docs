[View code on GitHub](https://dune.com/docs/query/dunesql-changes.md)

# DuneSQL migration

This technical guide provides documentation regarding the changes to DuneSQL that occurred on March 2nd, 2023. The guide is divided into several sections, each of which covers a specific aspect of the migration. 

The first section of the guide explains the changes that were made to DuneSQL. Specifically, DuneSQL now uses the same data types as the underlying EVM blockchain. This means that addresses, transaction hashes, and other encoded data are now stored as `varbinary` datatype. Additionally, `uint256` and `int256` are now supported, allowing for full wei-level precision calculations. The guide also explains that logs are now indexed from 0 instead of 1, and the `from_hex` native function has been modified to transform varchar to varbinary.

The second section of the guide explains what these changes mean for users. The switch to the `varbinary` datatype should significantly improve query speed, and the removal of string casts and conversions should make queries more readable and easier to maintain. Additionally, the introduction of `uint256` and `int256` allows for full wei-level precision calculations. 

The third section of the guide explains what users need to do to adjust to these changes. Specifically, users need to remove the `-- dunesql_alpha_deprecated` comment from their queries, adjust all occurrences of `0x` strings to fit the new data types, and remove any `varchar -> double`, `varchar -> decimals`, or `varchar -> bigint` casts. If queries used any columns from logs tables, users will need to adjust the indexing of topics. 

The fourth section of the guide explains what will happen if users do not adjust their queries. If the `-- dunesql_alpha_deprecated` comment is not removed from a query, it will continue to run against the old data types until March 23, 2023. After that date, the query will no longer run, and users will need to update it to use compatible functions.

The fifth section of the guide provides a table of common errors and fixes that users may encounter. 

Overall, this technical guide provides a comprehensive overview of the changes that were made to DuneSQL and what users need to do to adjust to these changes. It also provides examples of queries that need to be adjusted and common errors that users may encounter.
## Questions: 
 1. What are the current issues with datatypes in some tables in DuneSQL and when are they expected to be resolved?
- The current issues with datatypes in some tables in DuneSQL are affecting some Spellbook tables, `snapshot.*` and `cowswap.*`, and can be temporarily fixed by casting the columns which are incorrectly still `varchar` to `varbinary` with `from_hex(x)`. The issue is still to be resolved and there is no expected date for the resolution.

2. What are the benefits of switching to the `varbinary` datatype in DuneSQL?
- Switching to the `varbinary` datatype should significantly improve the speed of queries by approximately 30%. Additionally, it eliminates the need for string casts and conversions, making queries more readable and easier to maintain. Finally, the introduction of `uint256` and `int256` allows for full wei-level precision calculations.

3. What are some common errors and fixes that might be encountered when using DuneSQL after the changes?
- Some common errors and fixes that might be encountered when using DuneSQL after the changes include needing to cast varchar to varbinary using `from_hex(x)`, casting to `uint256` using `cast(xxx as uint256)`, using `bytearray_substring` and `bytearray_starts_with` instead of LIKE expression, and adjusting the indexing of topics in logs tables from `Topic1` to `Topic0`, `Topic2` to `Topic1`, etc.