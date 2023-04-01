[View code on GitHub](https://dune.com/docs/query/DuneSQL-reference/SQL-language/datatypes.md)

The app technical guide covers various data types used in DuneSQL, including:

- **Boolean**: Captures boolean values `true` and `false`.
- **Integer**: Different integer types such as `TINYINT`, `SMALLINT`, `INTEGER`, `BIGINT`, `UINT256`, and `INT256`.
- **Floating-point**: `REAL` and `DOUBLE` types implementing the IEEE Standard 754 for Binary Floating-Point Arithmetic.
- **Fixed-precision**: `DECIMAL` type with specified precision and scale.
- **String**: `VARCHAR`, `CHAR`, `VARBINARY`, and `JSON` types.
- **Date and time**: Various date and time types like `DATE`, `TIME`, `TIMESTAMP`, and `INTERVAL`.
- **Structural**: `ARRAY`, `MAP`, and `ROW` types for complex data structures.
- **Network address**: `IPADDRESS` type for IPv4 and IPv6 addresses.
- **UUID**: Represents a Universally Unique IDentifier.
- **HyperLogLog**: Data sketch for efficient computation of approximate distinct count.
- **SetDigest**: Data sketch for calculating Jaccard similarity coefficient between two sets.
- **Quantile digest**: Summary structure for capturing approximate distribution of data.
- **T-Digest**: Summary structure similar to qdigest with higher performance, lower memory usage, and higher accuracy at high and low percentiles.

The guide provides examples and detailed explanations for each data type, including their usage, properties, and functions.
## Questions: 
 1. **What are the differences between the `UINT256` and `INT256` data types, and when should each be used in EVM smart contracts?**

   The `UINT256` data type is a 256-bit unsigned integer, representing only non-negative integers, including very large positive integers and zero. The `INT256` data type is a 256-bit signed integer, representing a wide range of values, including very large negative and positive integers, as well as zero. In EVM smart contracts, `UINT256` is commonly used for representing balances and other quantities, while `INT256` is used when the value can be negative.

2. **How can I work with `VARBINARY` data types in DuneSQL, and are there any custom functions available for this purpose?**

   In DuneSQL, addresses, hashes, calldata, and logs are stored as `VARBINARY` data types. You can use SQL statements with the binary data prefix `0x` and hexadecimal format for working with `VARBINARY` data types. DuneSQL also provides custom functions to make it easier to work with `VARBINARY` data types, which can be found on the [varbinary functions](/querying-with-DuneSQL/functions/varbinary/) page.

3. **What are the differences between the `QDigest` and `TDigest` data structures, and when should each be used?**

   Both `QDigest` and `TDigest` are summary structures that capture the approximate distribution of data for a given input set and can be queried to retrieve approximate quantile values. However, `TDigest` has some advantages over `QDigest`, including higher performance, lower memory usage, and higher accuracy at high and low percentiles. Both structures are additive, meaning they can be merged together without losing precision. You should choose the appropriate structure based on your performance, memory, and accuracy requirements.