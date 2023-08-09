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

Example:
```sql
SELECT bytearray_concat(0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2,
                        0xa0b86991c6218b36c1d19d4a2e9eb0ce3606eb48)
```

**`bytearray_concat(varchar, varchar)`** → varchar

Concatenates two byte arrays or strings.

Example:
```sql
-- concatenate varchar
-- using typeof to check the datatype
SELECT bytearray_concat('0xabcd', '0x00ab') as bytearray_varchar_concat,
       typeof(bytearray_concat('0xabcd', '0x00ab')) as bytearray_varchar_type

```

#### bytearray_length()

**``bytearray_length(varbinary)``** → bigint

Returns the length of a byte array.

Example:
```sql
 -- this will return 20
SELECT bytearray_length(0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2)
```

**``bytearray_length(varchar)``** → bigint

Returns the length of a string.

Example:
```sql
 -- this will return 20
SELECT typeof('0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2') as data_type,
       bytearray_length('0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2') varchar_length
```

#### bytearray_ltrim()

**``bytearray_ltrim(varbinary)``** → varbinary

Removes zero bytes or spaces from the beginning of a byte array

Example:
```sql
 -- this will remove the zeros at the front,
 -- returning 0xa2b80f9c09558945800ddf4f8786dcc8b1c44974
SELECT bytearray_ltrim(0x000000000000000000000000a2b80f9c09558945800ddf4f8786dcc8b1c44974)
```

**``bytearray_ltrim(varchar)``** → varchar

Removes spaces from the beginning of a string.

Example:
```sql
 -- this will remove the zeros at the front,
 -- returning 0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2
SELECT typeof('0x0000000000000000000000000000000000000000c02aaa39b223fe8d0a0e5c4f27ead9083c756cc2') as data_type,
       bytearray_ltrim('0x0000000000000000000000000000000000000000c02aaa39b223fe8d0a0e5c4f27ead9083c756cc2') varchar_ltrim
```

#### bytearray_position()

**``bytearray_position(varbinary, varbinary)``** → bigint

Returns the index of the first occurrence of a given bytearray or string (or 0 if not found) within a byte array or string.

Example:
```sql

-- get $ARKM claimers 
SELECT * FROM ethereum.transactions
WHERE block_time >= TIMESTAMP '2023-07-17' -- claim start date
AND bytearray_position(data,0x3d13f874) = 1 -- 0x3d13f874 is the methodID
AND success
LIMIT 100

```

**``bytearray_position(varchar, varchar)``** → bigint

Returns the index of the first occurrence of a given bytearray or string (or 0 if not found) within a byte array or string.

Example:
```sql
-- search for 0x6cc2 and replaced with 0xabcd
-- 0xc02aaa39b223fe8d0a0e5c4f27ead9083c75abcd as output
SELECT bytearray_replace('0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2',
                         '0x6cc2',
                         '0xabcd')   
```

#### bytearray_replace()

**``bytearray_replace(varbinary, varbinary, varbinary)``** → varbinary

Greedily replaces occurrences of a pattern within a byte array.

Example:
```sql

-- replacing the blackhole address (ETH)
-- to WETH address
SELECT bytearray_replace(0x0000000000000000000000000000000000000000,
                         0x0000000000000000000000000000000000000000,
                         0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2)  
```

**``bytearray_replace(varchar, varchar, varchar)``** → varchar

Greedily replaces occurrences of a pattern within a string.

Example:
```sql

SELECT bytearray_replace('0x0000000000000000000000000000000000000000a2b80f9c09558945800ddf4f8786dcc8b1c44974',
                         '0x0000000000000000000000000000000000000000',
                         '0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2')  
```

#### bytearray_reverse()

**``bytearray_reverse(varbinary)``** → varbinary

Reverses a given byte array.

Example:
```sql

SELECT bytearray_reverse(0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2)
```

**``bytearray_reverse(varchar)``** → varchar

Reverses a given string.

Example:
```sql
-- '0xabcdef' as original
-- '0xefcdab' as reversed
SELECT '0xabcdef' as original,
       bytearray_reverse('0xabcdef') as reversed
```

#### bytearray_rtrim()

**``bytearray_rtrim(varbinary) or bytearray_rtrim(varchar)``** → varbinary or varchar

Removes zero bytes or spaces from the end of a byte array or string.

Example:
```sql
 -- this will remove the zeros at the end,
 -- returning 0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2
SELECT bytearray_ltrim(0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc20000000000000000000000000000000000000000)
```

#### bytearray_starts_with()

**``bytearray_starts_with(varbinary, varbinary)``** → boolean

Determines whether a byte array starts with a prefix.

Example:
```sql

-- get $ARKM claimers 
-- bytearray_starts_with checks whether 
-- data starts with 0x3d13f874 (claim methodID)
SELECT * FROM ethereum.transactions
WHERE block_time >= TIMESTAMP '2023-07-17'
AND bytearray_starts_with(data,0x3d13f874) -- returns true if starts with 0x3d13f874
AND success
LIMIT 100

```

**``bytearray_starts_with(varchar, varchar)``** → boolean

Determines whether a string starts with a prefix.

Example:
```sql
-- returns true if starts with 0x3d13f874
SELECT bytearray_starts_with(0x3d13f874abcd,0x3d13f874) 

```

#### bytearray_substring()

**``bytearray_substring(varbinary, integer)``** → varbinary

Returns a suffix byte array or string starting at a given index.

Example:
```sql
-- using bytearray_substring starting from the 21th index
-- this returns 0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2 
SELECT 0x0000000000000000000000000000000000000000c02aaa39b223fe8d0a0e5c4f27ead9083c756cc2 as original_bytearray,
       bytearray_substring(0x0000000000000000000000000000000000000000c02aaa39b223fe8d0a0e5c4f27ead9083c756cc2,21) as bytearraysubstring_data
```

**``bytearray_substring(varchar, integer)``** → varchar

Returns a suffix string starting at a given index.

Returns a sub byte array or string of a given length starting at an index.

Example:
```sql
-- getting the sizeDelta using bytearray_substring
-- and converting to uint256 using bytearray_to_uint256
SELECT tx_hash,
       bytearray_substring(data,65,32) as sizeDelta,
       bytearray_to_uint256(bytearray_substring(data,65,32)) as sizeDelta_uint256
FROM optimism.logs
WHERE contract_address = 0xa1ace9ce6862e865937939005b1a6c5ac938a11f
AND topic0 = 0xc9d5ada2ea384fe04826ecd1b258955ac73c3e2e20d755108eafde90bc5588d4
-- some sample transaction hash
AND tx_hash IN (0x3e3c558e7f723e3bb7de1d8f5f920ca206e3e878984296a2b8e6af2969003a19, 
                0xccfd2033adfb1fdd14fdfc047fe554ba7549e396abc6c559e9528a4259295b89) 
```

**``bytearray_substring(varchar, integer, integer)``** → varchar

Returns a sub string of a given length starting at an index.

Example:
```sql
-- returns 	'0xabcd'
SELECT '0xabcdefabcdef' as varchar_data,
       bytearray_substring('0xabcdefabcdef',1,3) as varchar_substring
```

**``bytearray_substring(varbinary, integer, integer)``** → varbinary

Example:
```sql
-- returns  0xabcd
SELECT 0xabcdefabcdef as varbinary_data,
       bytearray_substring(0xabcdefabcdef,1,3) as varbinary_substring
```

## Byte Array to Numeric Functions

The byte array conversion functions throw an overflow exception if the byte array is larger than the number of bytes supported of the type, even if the most significant bytes are all zero. It is possible to use `bytearray_ltrim` in order to trim the zero bytes from the left.

[Here is a dashboard](https://dune.com/dune/dune-sql-byte-array-functions-uint256-int256-support) with examples covering all of the above functions.

#### bytearray_to_integer()

**``bytearray_to_integer(varbinary)``** → integer

Returns the `INTEGER` value of a big-endian byte array of length <= 4 representing the integer in two's complement. If the byte array has length < 4 it is padded with zero bytes.

Example:

```sql
-- convert bytearray to integer [result will be either 1 or 0]
-- if 1 = true, 0 = false
SELECT tx_hash,
       bytearray_to_integer(bytearray_ltrim(bytearray_substring(data,1,32))) as isQuote_number,
       CASE WHEN  bytearray_to_integer(bytearray_ltrim(bytearray_substring(data,1,32))) = 1 THEN TRUE ELSE FALSE END AS isQuote
FROM arbitrum.logs
WHERE contract_address = 0xdaf4ffb05bfcb2c328c19135e3e74e1182c88283
AND topic0 = 0xf1bc206c8d659bf05edd19865dbae82643062168ec3970d9d7c5468f900487d9
LIMIT 10
```

#### bytearray_to_bigint()

**``bytearray_to_bigint(varbinary)``** → bigint

Returns the `BIGINT` value of a big-endian byte array of length <= 8 representing the bigint in two's complement. If the byte array has length < 8 it is padded with zero bytes.

Example:
```sql
-- convert bytearray to integer [result will be either 1 or 0]
-- if 1 = true, 0 = false
SELECT tx_hash,
       bytearray_to_bigint(bytearray_ltrim(bytearray_substring(data,1,32))) as isQuote_number,
       CASE WHEN  bytearray_to_bigint(bytearray_ltrim(bytearray_substring(data,1,32))) = 1 THEN TRUE ELSE FALSE END AS isQuote
FROM arbitrum.logs
WHERE contract_address = 0xdaf4ffb05bfcb2c328c19135e3e74e1182c88283
AND topic0 = 0xf1bc206c8d659bf05edd19865dbae82643062168ec3970d9d7c5468f900487d9
LIMIT 10
```

#### bytearray_to_decimal()

**``bytearray_to_decimal(varbinary)``** → decimal(38,0)

Returns the `DECIMAL(38,0)` value of a big-endian byte array of length <= 16 representing the decimal(38,0) in two's complement. If the byte array has length < 16 it is padded with zero bytes.

Example:

```sql
-- using raw table to get usdc transfers amount
-- transfer topic0 = 0xddf252ad1be2c89b69c2b068fc378daa952ba7f163c4a11628f55a4df523b3ef
-- usdc contract_address = 0xaf88d065e77c8cc2239327c5edb3a432268e5831
SELECT tx_hash,
       data,
       bytearray_to_decimal(bytearray_ltrim(data)) as data_decimal
FROM arbitrum.logs
WHERE topic0 = 0xddf252ad1be2c89b69c2b068fc378daa952ba7f163c4a11628f55a4df523b3ef
AND contract_address = 0xaf88d065e77c8cc2239327c5edb3a432268e5831
AND block_time >= NOW() - interval '1' day
LIMIT 50
```

#### bytearray_to_uint256()

**``bytearray_to_uint256(varbinary)``** → uint256

Returns the `UINT256` of a big-endian byte array of length <= 32 representing the unsigned integer. If the byte array has length < 32 it is padded with zero bytes.

Example:
```sql
select tx_hash,
       data,
       bytearray_substring(data,97,32) as fee,
       bytearray_to_uint256(bytearray_substring(data,97,32)) as fee_uint256
from optimism.logs
where contract_address = 0xa1ace9ce6862e865937939005b1a6c5ac938a11f
and topic0 = 0xc9d5ada2ea384fe04826ecd1b258955ac73c3e2e20d755108eafde90bc5588d4
-- sample transaction hash
and tx_hash IN (0x3e3c558e7f723e3bb7de1d8f5f920ca206e3e878984296a2b8e6af2969003a19,
                0xccfd2033adfb1fdd14fdfc047fe554ba7549e396abc6c559e9528a4259295b89)
```

#### bytearray_to_int256()

**``bytearray_to_int256(varbinary)``** → int256

Returns the `INT256` of a big-endian byte array of length <= 32 representing the signed integer. If the byte array has length < 32 it is padded with zero bytes.

Example:
```sql
select tx_hash,
       data,
       bytearray_substring(data,65,32) as sizeDelta,
       bytearray_to_int256(bytearray_substring(data,65,32)) as sizeDelta_int256
from optimism.logs
where contract_address = 0xa1ace9ce6862e865937939005b1a6c5ac938a11f
and topic0 = 0xc9d5ada2ea384fe04826ecd1b258955ac73c3e2e20d755108eafde90bc5588d4
-- sample transaction hash
and tx_hash IN (0x3e3c558e7f723e3bb7de1d8f5f920ca206e3e878984296a2b8e6af2969003a19,
                0xccfd2033adfb1fdd14fdfc047fe554ba7549e396abc6c559e9528a4259295b89)
```

#### bytea2numeric()

**``bytea2numeric(varbinary)``** → bigint

This function has been deprecated. It is an alias for `bytearray_to_bigint`.
