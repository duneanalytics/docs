[View code on GitHub](https://dune.com/docs/query/DuneSQL-reference/Functions-and-operators/varbinary.md)

# Varbinary Functions

This technical guide covers the helper functions available in Dune SQL for byte array manipulation and conversion. The guide is focused on the `app` folder of the Dune Docs project.

The guide starts by introducing the varbinary type used to represent byte arrays in Dune SQL. It then lists the byte array manipulation functions available in Dune SQL, including `bytearray_concat`, `bytearray_length`, `bytearray_ltrim`, `bytearray_position`, `bytearray_replace`, `bytearray_reverse`, `bytearray_rtrim`, `bytearray_starts_with`, and `bytearray_substring`. Each function is described in detail, including its input and output types, and examples are provided where appropriate.

The guide then covers the byte array to numeric functions available in Dune SQL, including `bytearray_to_integer`, `bytearray_to_bigint`, `bytearray_to_decimal`, `bytearray_to_uint256`, `bytearray_to_int256`, and `bytea2numeric`. The guide notes that these functions throw an overflow exception if the byte array is larger than the number of bytes supported of the type, even if the most significant bytes are all zero. It also recommends using `bytearray_ltrim` to trim the zero bytes from the left.

Overall, this technical guide provides a comprehensive overview of the byte array manipulation and conversion functions available in Dune SQL. It is a useful resource for developers working with byte arrays in Dune SQL and provides clear examples of how to use each function.
## Questions: 
 1. What is the purpose of Dune SQL's varbinary type and how does it relate to blockchain data? 
- The blockchain SQL analyst might want to know more about the use case for varbinary type and how it is used to represent byte arrays in Dune SQL, as this could impact how they work with blockchain data stored in byte array format.

2. How do the byte array manipulation functions in Dune SQL compare to similar functions in other SQL languages? 
- The analyst might want to compare the functionality and syntax of Dune SQL's byte array manipulation functions to those in other SQL languages they are familiar with, in order to better understand how to use them effectively.

3. What is the significance of the byte array to numeric conversion functions in Dune SQL for blockchain data analysis? 
- The analyst might want to know more about how the byte array to numeric conversion functions work and how they can be used to analyze blockchain data stored in byte array format, particularly for values such as integers and decimals.