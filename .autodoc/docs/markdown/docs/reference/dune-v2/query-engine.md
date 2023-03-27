[View code on GitHub](https://dune.com/blob/master/reference\dune-v2\query-engine.md)

The app technical guide covers the transition from PostgreSQL to Dune SQL and Spark SQL query engines in Dune V2. It provides a detailed comparison of syntax and operator differences between the three engines, including examples for various operations such as casting, indexing, type conversions, and aggregate functions.

The guide also explains the data types and functions available in Dune SQL, with a focus on numerical types, byte array functions, and byte array to numeric functions. It provides a comprehensive list of helper functions for working with byte arrays and their respective descriptions.

Additionally, the guide explains how to query queries as views in Dune SQL using the `query_<queryId>` identifier and provides an example for reference. It also highlights the limitations and requirements for using this feature.

Finally, the guide suggests using Google and the respective documentation for Spark SQL and Trino SQL to find answers to specific questions. It also recommends the #dune-sql Discord channel for community support and encourages users to provide feedback via email.
## Questions: 
 1. **What are the differences in syntax and keyword operators between PostgreSQL, Spark SQL, and Dune SQL?**

   The app technical guide provides a syntax comparison table that highlights the key differences between PostgreSQL, Spark SQL, and Dune SQL. Some examples include differences in casting hex/bytea to a number, handling decimals for prices.usd, and aggregate functions.

2. **What are the available byte array functions in Dune SQL?**

   Dune SQL offers several byte array functions such as `bytearray_concat`, `bytearray_length`, `bytearray_ltrim`, `bytearray_position`, `bytearray_replace`, `bytearray_reverse`, `bytearray_rtrim`, `bytearray_starts_with`, and `bytearray_substring`. These functions simplify interactions with byte arrays by accounting for the `0x`-prefix and using byte index instead of character index.

3. **How can I query queries as views in Dune SQL?**

   In Dune SQL, you can query non-parameterized queries as views using the identifier `query_<queryId>`. For example, `select * from query_1234`. Note that all output columns of the query being queried must be named, parameterized queries are not supported, only public queries can be queried, only saved queries can be queried, and only queries written in Dune SQL can be queried.