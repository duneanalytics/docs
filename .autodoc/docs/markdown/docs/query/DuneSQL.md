[View code on GitHub](https://dune.com/blob/master/query\DuneSQL.md)

The DuneSQL technical guide provides information on the datatypes, functions, and operators used in DuneSQL. The guide is divided into two main sections: Numerical types and Byte Array Functions. The Numerical types section covers the supported numerical types, including `INTEGER`, `BIGINT`, `DOUBLE`, `DECIMAL`, `UINT256`, and `INT256`. The Byte Array Functions section covers the helper functions used to manipulate byte arrays, including `bytearray_concat`, `bytearray_length`, `bytearray_ltrim`, `bytearray_position`, `bytearray_replace`, `bytearray_reverse`, `bytearray_rtrim`, `bytearray_starts_with`, `bytearray_substring`, and `bytearray_to_numeric`. 

The guide also provides information on how to query queries as views in Dune SQL. All non-parameterized queries written using Dune SQL can be queried as views in other queries using the identifier `query_<queryId>`. The guide provides an example query that queries a saved query using its `queryId`. 

The guide also includes a warning that Dune SQL exited alpha on March 2nd, 2023, and some changes to datatypes and column names were introduced that may cause breaking changes. The guide provides a link to the DuneSQL changes page for more details. 

Overall, the DuneSQL technical guide provides a comprehensive overview of the datatypes, functions, and operators used in DuneSQL, as well as information on how to query queries as views. The guide is a valuable resource for developers working with DuneSQL.
## Questions: 
 1. What numerical types does DuneSQL support?
- DuneSQL supports the numerical types `INTEGER`, `BIGINT`, `DOUBLE`, and fixed precision `DECIMAL` with precision up to 38 digits (i.e., `DECIMAL(38, 0)`), as well as `UINT256` for representing unsigned 256 bit integers and `INT256` for signed 256 bit integers.

2. What are the byte array manipulation functions available in DuneSQL?
- The byte array manipulation functions available in DuneSQL include `bytearray_concat`, `bytearray_length`, `bytearray_ltrim`, `bytearray_position`, `bytearray_replace`, `bytearray_reverse`, `bytearray_rtrim`, `bytearray_starts_with`, `bytearray_substring`, and `bytearray_substring`.

3. Can all queries written using DuneSQL be queried as views in other queries?
- Yes, all non-parameterized queries written using DuneSQL can be queried as views in other queries using the identifier `query_<queryId>`. However, there are some limitations, such as the requirement that all output columns of the query being queried must be named, and that only saved queries can be queried.