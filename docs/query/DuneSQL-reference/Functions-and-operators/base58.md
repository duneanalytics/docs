---
title: Base58 functions
---

Base58 is a binary-to-text encoding scheme that is commonly used in Bitcoin and Solana. It uses an alphabet of 58 characters, which is the same as the Base64 encoding scheme, but omits the characters `0`, `O`, `I`, and `l` to avoid confusion between similar-looking letters and numbers.

You can use the `from_base58` function to convert a Base58-encoded string to a `VARBINARY` value. For example, the following query converts the Base58-encoded string `3DZBMRwnSU8f` to a `VARBINARY` value:

```sql
SELECT 
    from_base58('3DZBMRwnSU8f')
-- results in VARBINARY 0x030094357700000000
```

Now that we are able to convert Base58-encoded strings to `VARBINARY` values, we can use the `bytearray_to_bigint` function to convert the `VARBINARY` value to a `BIGINT` value. However, we need to consider more things:

1. The decoded `VARBINARY` value does not only contain the data we want to convert to a `BIGINT` value. It also contains a discriminator that indicates which function of a solana program was called. We need to remove this discriminator before we can convert the `VARBINARY` value to a `BIGINT` value. We do this by using the `bytearray_substring` function.

2. Solana uses little-endian byte order, so we need to reverse the byte order before we can convert the `VARBINARY` value to a `BIGINT` value. We do this by using the `bytearray_reverse` function.

```sql
SELECT 
    bytearray_to_bigint(bytearray_reverse(bytearray_substring(from_base58('3DZBMRwnSU8f'), 2, 8))) as token_sold_amount
-- results in BIGINT 2000000000
```

In a real-world scenario, here is how you would use these functions to decode a Base58-encoded string that represents a token amount in a Solana swap transaction:

```sql
SELECT
sp.call_inner_instructions[1].data
,from_base58(sp.call_inner_instructions[1].data) as first_step
,bytearray_substring(from_base58(sp.call_inner_instructions[1].data), 2, 8) as second_step
,bytearray_reverse(bytearray_substring(from_base58(sp.call_inner_instructions[1].data), 2, 8)) as third_step
,bytearray_to_bigint(bytearray_reverse(bytearray_substring(from_base58(sp.call_inner_instructions[1].data), 2, 8))) as decoded_amount
FROM whirlpool_solana.whirlpool_call_swap sp
WHERE sp.account_whirlpool = '7qbRF6YsyGuLUVs6Y1q64bdVrfe4ZcUUz1JRdoVNUJnm'
AND call_tx_id = '44kmeC1edSfp21K5kKNVViJvLHG8XQqqu3KbHsrYcYZGmopWwBgP48c9u1DRBMGtQcbvyxd2TT8syY7ZvwpHqkhF'
and call_block_slot = 187701147
```

[→ Query in Dune](https://dune.com/queries/2846422)

!!! info
    This specific query decodes the token amount that was sold in a Solana swap transaction. While probably applicable for lots of other solana programs, it is not guaranteed to work for all solana programs. You might need to adjust the query to your specific use case, depending on the solana program you are querying.


 
## Functions

#### from_base58()
**`from_base58(varchar)`** → `varbinary`

Converts a Base58-encoded string to a `VARBINARY` value.

```sql
SELECT 
    from_base58('3DZBMRwnSU8f')
-- results in VARBINARY 0x030094357700000000
```

#### to_base58()
**`to_base58(varbinary)`** → `varchar`

Converts a `VARBINARY` value to a Base58-encoded string.

```sql 
SELECT 
    to_base58(0x030094357700000000)
-- results in base58 encoded varchar 3DZBMRwnSU8f
```