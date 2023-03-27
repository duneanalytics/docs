[View code on GitHub](https://dune.com/blob/master/query\dunesql-changes.md)

The DuneSQL migration technical guide provides documentation on the changes made to DuneSQL on March 2nd, 2023. The guide is divided into several sections, each with a specific focus. The first section is a warning that some tables in DuneSQL are still experiencing datatype issues, and the affected tables are listed. The section also provides a temporary workaround for the issue.

The second section of the guide explains the changes made to DuneSQL. DuneSQL has exited its alpha stage and now uses the same data types as the underlying EVM blockchain. This means that addresses, transaction hashes, and other encoded data are now stored as `varbinary` datatype. The guide also explains that `uint256` and `int256` are now supported, allowing full wei-level precision calculations. Additionally, the guide explains that logs are now stored with the correct topic indexing, and the `from_hex` native function has been modified to transform varchar to varbinary.

The third section of the guide explains what the changes mean for users. The switch to the `varbinary` datatype should improve query speed, and users can get rid of all string casts and conversions, making queries more readable and easier to maintain. The introduction of `uint256` and `int256` allows for full wei-level precision calculations, and the indexing of logs topics has been corrected to match the rest of the blockchain ecosystem.

The fourth section of the guide explains what users need to do to adjust to the changes. Users need to remove the `-- dunesql_alpha_deprecated` comment from their queries, adjust all occurrences of `0x` strings to fit the new data types, and remove any `varchar -> double`, `varchar -> decimals`, or `varchar -> bigint` casts. If queries used columns from logs tables, users need to adjust the indexing of topics. The guide provides a table of common errors and fixes.

The final section of the guide explains what will happen if users do not adjust to the changes. Queries will continue to run against the old data types until March 23, 2023, after which they will no longer run. The guide provides examples of breaking queries and fixed queries. Overall, the DuneSQL migration technical guide provides comprehensive documentation on the changes made to DuneSQL and what users need to do to adjust to the changes.
## Questions: 
 1. What are the affected tables and when will they be fixed?
- The affected tables are `prices.usd`, some Spellbook tables, `flashbots.*`, `reservoir.*`, `snapshot.*`, and `cowswap.*`. The fix for `prices.usd` was on March 6th, 2023, while the fixes for `flashbots.*` and `reservoir.*` will be on March 10th, 2023. The fixes for `snapshot.*` and `cowswap.*` are still to be determined.

2. How will the switch to `varbinary` datatype affect query speed?
- Switching to the `varbinary` datatype should significantly improve the speed of queries by approximately 30%.

3. What should be done if a query has incompatible functions?
- A comment `-- dunesql_alpha_deprecated` has been appended to any query that has incompatible functions. This comment allows the query to be run against the old data types until March 23, 2023. It is recommended to remove the comment and convert the query to use compatible functions before the deprecation date.