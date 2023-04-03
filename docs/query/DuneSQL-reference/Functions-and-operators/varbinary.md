---
title: Varbinary functions (DuneSQL)
---

## Varbinary Functions

Dune SQL represents byte arrays using the varbinary type.

To make it simpler to work with byte arrays we have the following helper functions, which work with these two kinds of representation. They simplify interactions with byte arrays, as they automatically account for the `0x`-prefix and use byte index instead of character index. For instance, the bytearray_substring methods take indexes by byte, not by character (twice the byte array length).


## Byte Array Manipulation Functions

#### bytearray_concat()

**``bytearray_concat(varbinary, varbinary)``** → varbinary  

Concatenates two byte arrays or strings.

**`bytearry_concat(varchar, varchar)`** → varchar

Concatenates two byte arrays or strings.

#### bytearray_length()

**``bytearray_length(varbinary)``** → bigint

Returns the length of a byte array.

**``bytearray_length(varchar)``** → varchar

Returns the length of a string.

#### bytearray_ltrim()

**``bytearray_ltrim(varbinary)``** → varbinary

Removes zero bytes or spaces from the beginning of a byte array

**``bytearray_ltrim(varchar)``** → varchar

Removes spaces from the beginning of a string.

#### bytearray_position()

**``bytearray_position(varbinary, varbinary)``** → bigint

Returns the index of the first occurrence of a given bytearray or string (or 0 if not found) within a byte array or string.

**``bytearray_position(varchar, varchar)``** → bigint

Returns the index of the first occurrence of a given bytearray or string (or 0 if not found) within a byte array or string.

#### bytearray_replace()

**``bytearray_replace(varbinary, varbinary, varbinary)``** → varbinary

Greedily replaces occurrences of a pattern within a byte array.

**``bytearray_replace(varchar, varchar, varchar)``** → varchar

Greedily replaces occurrences of a pattern within a string.

#### bytearray_reverse()

**``bytearray_reverse(varbinary)``** → varbinary

Reverses a given byte array.

**``bytearray_reverse(varchar)``** → varchar

Reverses a given string.

#### bytearray_rtrim()

**``bytearray_rtrim(varbinary) or bytearray_rtrim(varchar)``** → varbinary or varchar

Removes zero bytes or spaces from the end of a byte array or string.

#### bytearray_starts_with()

**``bytearray_starts_with(varbinary, varbinary)``** → boolean

Determines whether a byte array starts with a prefix.

**``bytearray_starts_with(varchar, varchar)``** → boolean

Determines whether a string starts with a prefix.

#### bytearray_substring()

**``bytearray_substring(varbinary, integer)``** → varbinary

Returns a suffix byte array or string starting at a given index.

**``bytearray_substring(varchar, integer)``** → varchar

Returns a suffix string starting at a given index.

**``bytearray_substring(varbinary, integer, integer)``** → varbinary

Returns a sub byte array or string of a given length starting at an index.

**``bytearray_substring(varchar, integer, integer)``** → varchar

Returns a sub string of a given length starting at an index.

## Byte Array to Numeric Functions

The byte array conversion functions throw an overflow exception if the byte array is larger than the number of bytes supported of the type, even if the most significant bytes are all zero. It is possible to use `bytearray_ltrim` in order to trim the zero bytes from the left.

[Here is a dashboard](https://dune.com/dune/dune-sql-byte-array-functions-uint256-int256-support) with examples covering all of the above functions.

#### bytearray_to_integer()

**``bytearray_to_integer(varbinary)``** → integer

Returns the `INTEGER` value of a big-endian byte array of length <= 4 representing the integer in two's complement. If the byte array has length < 4 it is padded with zero bytes.

#### bytearray_to_bigint()

**``bytearray_to_bigint(varbinary)``** → bigint

Returns the `BIGINT` value of a big-endian byte array of length <= 8 representing the bigint in two's complement. If the byte array has length < 8 it is padded with zero bytes.

#### bytearray_to_decimal()

**``bytearray_to_decimal(varbinary)``** → decimal(38,0)

Returns the `DECIMAL(38,0)` value of a big-endian byte array of length <= 16 representing the decimal(38,0) in two's complement. If the byte array has length < 16 it is padded with zero bytes.

#### bytearray_to_uint256()

**``bytearray_to_uint256(varbinary)``** → uint256

Returns the `UINT256` of a big-endian byte array of length <= 32 representing the unsigned integer. If the byte array has length < 32 it is padded with zero bytes.

#### bytearray_to_int256()

**``bytearray_to_int256(varbinary)``** → int256

Returns the `INT256` of a big-endian byte array of length <= 32 representing the signed integer. If the byte array has length < 32 it is padded with zero bytes.

#### bytea2numeric()

**``bytea2numeric(varbinary)``** → bigint

This function has been deprecated. It is an alias for `bytearray_to_bigint`.
