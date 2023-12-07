---
title: Varbinary functions (DuneSQL)
---

## Varbinary Functions

Dune SQL represents varbinarys using the varbinary type.

To make it simpler to work with varbinarys we have the following helper functions, which work with these two kinds of representation. They simplify interactions with varbinarys, as they automatically account for the `0x`-prefix and use byte index instead of character index. For instance, the varbinary_substring methods take indexes by byte, not by character (twice the varbinary length).


You can use these function to extract data from undecoded events logs, or calldata. For instance, if you have a function that takes a `uint256` as an argument, you can use `varbinary_to_uint256` to extract the value from the calldata. You'll oftentimes need to use `varbinary_substring` to extract the correct part of the calldata or use other bytearray manipulation functions to get the correct value.

```sql
select tx_hash,
       data,
       varbinary_substring(data,97,32) as fee,
       varbinary_to_uint256(varbinary_substring(data,97,32)) as fee_uint256
from optimism.logs
where contract_address = 0xa1ace9ce6862e865937939005b1a6c5ac938a11f
and topic0 = 0xc9d5ada2ea384fe04826ecd1b258955ac73c3e2e20d755108eafde90bc5588d4
-- sample transaction hash
and tx_hash IN (0x3e3c558e7f723e3bb7de1d8f5f920ca206e3e878984296a2b8e6af2969003a19,
                0xccfd2033adfb1fdd14fdfc047fe554ba7549e396abc6c559e9528a4259295b89)
```





## Varbinary to Numeric Functions

The varbinary conversion functions throw an overflow exception if the varbinary is larger than the number of bytes supported of the type, even if the most significant bytes are all zero. It is possible to use `varbinary_ltrim` in order to trim the zero bytes from the left.

[Here is a dashboard](https://dune.com/dune/dune-sql-byte-array-functions-uint256-int256-support) with examples covering all of the below functions. For a more comprehensive look at all special DuneSQL functions, use this [dashboard](https://dune.com/cryptuschrist/dunesql-functions) from [cryptuschrist](https://dune.com/cryptuschrist). 



#### varbinary_to_integer()

**``varbinary_to_integer(varbinary)``** → integer

Returns the `INTEGER` value of a big-endian varbinary of length <= 4 representing the integer in two's complement. If the varbinary has length < 4 it is padded with zero bytes.

```sql
-- convert bytearray to integer [result will be either 1 or 0]
-- if 1 = true, 0 = false
SELECT tx_hash,
       varbinary_to_integer(varbinary_ltrim(varbinary_substring(data,1,32))) as isQuote_number,
       CASE WHEN  varbinary_to_integer(varbinary_ltrim(varbinary_substring(data,1,32))) = 1 THEN TRUE ELSE FALSE END AS isQuote
FROM arbitrum.logs
WHERE contract_address = 0xdaf4ffb05bfcb2c328c19135e3e74e1182c88283
AND topic0 = 0xf1bc206c8d659bf05edd19865dbae82643062168ec3970d9d7c5468f900487d9
LIMIT 10
```

#### varbinary_to_bigint()

**``varbinary_to_bigint(varbinary)``** → bigint

Returns the `BIGINT` value of a big-endian varbinary of length <= 8 representing the bigint in two's complement. If the varbinary has length < 8 it is padded with zero bytes.


```sql
-- convert bytearray to integer [result will be either 1 or 0]
-- if 1 = true, 0 = false
SELECT tx_hash,
       varbinary_to_bigint(varbinary_ltrim(varbinary_substring(data,1,32))) as isQuote_number,
       CASE WHEN  varbinary_to_bigint(varbinary_ltrim(varbinary_substring(data,1,32))) = 1 THEN TRUE ELSE FALSE END AS isQuote
FROM arbitrum.logs
WHERE contract_address = 0xdaf4ffb05bfcb2c328c19135e3e74e1182c88283
AND topic0 = 0xf1bc206c8d659bf05edd19865dbae82643062168ec3970d9d7c5468f900487d9
LIMIT 10
```

#### varbinary_to_decimal()

**``varbinary_to_decimal(varbinary)``** → decimal(38,0)

Returns the `DECIMAL(38,0)` value of a big-endian varbinary of length <= 16 representing the decimal(38,0) in two's complement. If the varbinary has length < 16 it is padded with zero bytes.



```sql
-- using raw table to get usdc transfers amount
-- transfer topic0 = 0xddf252ad1be2c89b69c2b068fc378daa952ba7f163c4a11628f55a4df523b3ef
-- usdc contract_address = 0xaf88d065e77c8cc2239327c5edb3a432268e5831
SELECT tx_hash,
       data,
       varbinary_to_decimal(varbinary_ltrim(data)) as data_decimal
FROM arbitrum.logs
WHERE topic0 = 0xddf252ad1be2c89b69c2b068fc378daa952ba7f163c4a11628f55a4df523b3ef
AND contract_address = 0xaf88d065e77c8cc2239327c5edb3a432268e5831
AND block_time >= NOW() - interval '1' day
LIMIT 50
```

#### varbinary_to_uint256()

**``varbinary_to_uint256(varbinary)``** → uint256

Returns the `UINT256` of a big-endian varbinary of length <= 32 representing the unsigned integer. If the varbinary has length < 32 it is padded with zero bytes.


```sql
select tx_hash,
       data,
       varbinary_substring(data,97,32) as fee,
       varbinary_to_uint256(varbinary_substring(data,97,32)) as fee_uint256
from optimism.logs
where contract_address = 0xa1ace9ce6862e865937939005b1a6c5ac938a11f
and topic0 = 0xc9d5ada2ea384fe04826ecd1b258955ac73c3e2e20d755108eafde90bc5588d4
-- sample transaction hash
and tx_hash IN (0x3e3c558e7f723e3bb7de1d8f5f920ca206e3e878984296a2b8e6af2969003a19,
                0xccfd2033adfb1fdd14fdfc047fe554ba7549e396abc6c559e9528a4259295b89)
```

#### varbinary_to_int256()

**``varbinary_to_int256(varbinary)``** → int256

Returns the `INT256` of a big-endian varbinary of length <= 32 representing the signed integer. If the varbinary has length < 32 it is padded with zero bytes.


```sql
select tx_hash,
       data,
       varbinary_substring(data,65,32) as sizeDelta,
       varbinary_to_int256(varbinary_substring(data,65,32)) as sizeDelta_int256
from optimism.logs
where contract_address = 0xa1ace9ce6862e865937939005b1a6c5ac938a11f
and topic0 = 0xc9d5ada2ea384fe04826ecd1b258955ac73c3e2e20d755108eafde90bc5588d4
-- sample transaction hash
and tx_hash IN (0x3e3c558e7f723e3bb7de1d8f5f920ca206e3e878984296a2b8e6af2969003a19,
                0xccfd2033adfb1fdd14fdfc047fe554ba7549e396abc6c559e9528a4259295b89)
```

#### bytea2numeric()

**``bytea2numeric(varbinary)``** → bigint

This function has been deprecated. It is an alias for `varbinary_to_bigint`.

## Varbinary to text

#### from_utf8()

**``from_utf8(varbinary)``** → varchar

Converts a varbinary to a string using the UTF-8 encoding.

```sql
Select from_utf8(0x48656c6c6f20576f726c64)
-- returns "Hello World"
```

most commonly will have to be used like this:

```sql
Select from_utf8(varbinary_ltrim(0x0000000000000000006e66746e657264732e6169))
```

## Text to varbinary

#### from_hex()

**``from_hex(varchar)``** → varbinary

Converts a varbinary expression in datatype `string` to `varbinary` datatype

```sql
Select from_hex('0x6574686275696c646572')
-- returns VARBINARY 0x6574686275696c646572
```

!!!warning
       you **cannot** use ``cast(x as varbinary)`` in these cases as it will actually encode the string as varbinary which is different from converting the expression to `varbinary`. 

## Varbinary Manipulation Functions

#### varbinary_concat()

**``varbinary_concat(varbinary, varbinary)``** → varbinary  

Concatenates two varbinarys or strings.


```sql
SELECT varbinary_concat(0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2,
                        0xa0b86991c6218b36c1d19d4a2e9eb0ce3606eb48)
```

**`varbinary_concat(varchar, varchar)`** → varchar

Concatenates two varbinarys or strings.


```sql
-- concatenate varchar
-- using typeof to check the datatype
SELECT varbinary_concat('0xabcd', '0x00ab') as varbinary_varchar_concat,
       typeof(varbinary_concat('0xabcd', '0x00ab')) as varbinary_varchar_type

```

#### varbinary_length()

**``varbinary_length(varbinary)``** → bigint

Returns the length of a varbinary.


```sql
 -- this will return 20
SELECT varbinary_length(0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2)
```

**``varbinary_length(varchar)``** → bigint

Returns the length of a string.


```sql
 -- this will return 20
SELECT typeof('0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2') as data_type,
       varbinary_length('0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2') varchar_length
```

#### varbinary_ltrim()

**``varbinary_ltrim(varbinary)``** → varbinary

Removes zero bytes or spaces from the beginning of a varbinary


```sql
 -- this will remove the zeros at the front,
 -- returning 0xa2b80f9c09558945800ddf4f8786dcc8b1c44974
SELECT varbinary_ltrim(0x000000000000000000000000a2b80f9c09558945800ddf4f8786dcc8b1c44974)
```

**``varbinary_ltrim(varchar)``** → varchar

Removes spaces from the beginning of a string.


```sql
 -- this will remove the zeros at the front,
 -- returning 0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2
SELECT typeof('0x0000000000000000000000000000000000000000c02aaa39b223fe8d0a0e5c4f27ead9083c756cc2') as data_type,
       varbinary_ltrim('0x0000000000000000000000000000000000000000c02aaa39b223fe8d0a0e5c4f27ead9083c756cc2') varchar_ltrim
```
#### varbinary_rtrim()

**``varbinary_rtrim(varbinary) or varbinary_rtrim(varchar)``** → varbinary or varchar

Removes zero bytes or spaces from the end of a varbinary or string.


```sql
 -- this will remove the zeros at the end,
 -- returning 0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2
SELECT varbinary_ltrim(0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc20000000000000000000000000000000000000000)
```

#### varbinary_position()

**``varbinary_position(varbinary, varbinary)``** → bigint

Returns the index of the first occurrence of a given bytearray or string (or 0 if not found) within a varbinary or string.


```sql

-- get $ARKM claimers 
SELECT * FROM ethereum.transactions
WHERE block_time >= TIMESTAMP '2023-07-17' -- claim start date
AND varbinary_position(data,0x3d13f874) = 1 -- 0x3d13f874 is the methodID
AND success
LIMIT 100

```

**``varbinary_position(varchar, varchar)``** → bigint

Returns the index of the first occurrence of a given bytearray or string (or 0 if not found) within a varbinary or string.


```sql
-- search for '0x6cc2' and return its position
SELECT varbinary_position('0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2','0x6cc2') 
```

#### varbinary_replace()

**``varbinary_replace(varbinary, varbinary, varbinary)``** → varbinary

Greedily replaces occurrences of a pattern within a varbinary.


```sql

-- replacing the blackhole address (ETH)
-- to WETH address
SELECT varbinary_replace(0x0000000000000000000000000000000000000000,
                         0x0000000000000000000000000000000000000000,
                         0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2)  
```

**``varbinary_replace(varchar, varchar, varchar)``** → varchar

Greedily replaces occurrences of a pattern within a string.


```sql

SELECT varbinary_replace('0x0000000000000000000000000000000000000000a2b80f9c09558945800ddf4f8786dcc8b1c44974',
                         '0x0000000000000000000000000000000000000000',
                         '0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2')  
```

#### varbinary_reverse()

**``varbinary_reverse(varbinary)``** → varbinary

Reverses a given varbinary.


```sql

SELECT varbinary_reverse(0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2)
```

**``varbinary_reverse(varchar)``** → varchar

Reverses a given string.


```sql
-- '0xabcdef' as original
-- '0xefcdab' as reversed
SELECT '0xabcdef' as original,
       varbinary_reverse('0xabcdef') as reversed
```


#### varbinary_starts_with()

**``varbinary_starts_with(varbinary, varbinary)``** → boolean

Determines whether a varbinary starts with a prefix.


```sql

-- get $ARKM claimers 
-- varbinary_starts_with checks whether 
-- data starts with 0x3d13f874 (claim methodID)
SELECT * FROM ethereum.transactions
WHERE block_time >= TIMESTAMP '2023-07-17'
AND varbinary_starts_with(data,0x3d13f874) -- returns true if starts with 0x3d13f874
AND success
LIMIT 100

```

**``varbinary_starts_with(varchar, varchar)``** → boolean

Determines whether a string starts with a prefix.


```sql
-- returns true if starts with 0x3d13f874
SELECT varbinary_starts_with(0x3d13f874abcd,0x3d13f874) 

```

#### varbinary_substring()

**``varbinary_substring(varbinary, integer)``** → varbinary

Returns a suffix varbinary or string starting at a given index.


```sql
-- using varbinary_substring starting from the 21th index
-- this returns 0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2 
SELECT 0x0000000000000000000000000000000000000000c02aaa39b223fe8d0a0e5c4f27ead9083c756cc2 as original_bytearray,
       varbinary_substring(0x0000000000000000000000000000000000000000c02aaa39b223fe8d0a0e5c4f27ead9083c756cc2,21) as bytearraysubstring_data
```

**``varbinary_substring(varchar, integer)``** → varchar

Returns a suffix string starting at a given index.

Returns a sub varbinary or string of a given length starting at an index.


```sql
-- getting the sizeDelta using varbinary_substring
-- and converting to uint256 using varbinary_to_uint256
SELECT tx_hash,
       varbinary_substring(data,65,32) as sizeDelta,
       varbinary_to_uint256(varbinary_substring(data,65,32)) as sizeDelta_uint256
FROM optimism.logs
WHERE contract_address = 0xa1ace9ce6862e865937939005b1a6c5ac938a11f
AND topic0 = 0xc9d5ada2ea384fe04826ecd1b258955ac73c3e2e20d755108eafde90bc5588d4
-- some sample transaction hash
AND tx_hash IN (0x3e3c558e7f723e3bb7de1d8f5f920ca206e3e878984296a2b8e6af2969003a19, 
                0xccfd2033adfb1fdd14fdfc047fe554ba7549e396abc6c559e9528a4259295b89) 
```

**``varbinary_substring(varchar, integer, integer)``** → varchar

Returns a sub string of a given length starting at an index.


```sql
-- returns 	'0xabcd'
SELECT '0xabcdefabcdef' as varchar_data,
       varbinary_substring('0xabcdefabcdef',1,3) as varchar_substring
```

**``varbinary_substring(varbinary, integer, integer)``** → varbinary


```sql
-- returns  0xabcd
SELECT 0xabcdefabcdef as varbinary_data,
       varbinary_substring(0xabcdefabcdef,1,3) as varbinary_substring
```


