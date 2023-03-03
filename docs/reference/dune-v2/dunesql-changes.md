---
title: DuneSQL changes
description: Documentation regarding the changes to DuneSQL on March 2nd, 2023
---

!!! Warning
    We are still experiencing issues with datatypes in some tables in DuneSQL. We are working on fixing them and will update this page once they are resolved.
    Currently affected tables are:  
    - ``prices.usd``  
    - some Spellbook tables    
    - ``flashbots.*``  
    - ``reservoir.*``  
    - ``snapshot.*`` 

    You can temporarily cast the columns which are incorrectly still `varchar` to `varbinary` with  `from_hex(substring( x from 3))` 
    

## DuneSQL Alpha Deprecation and Data Type Changes
DuneSQL officially exited its alpha stage on March 2nd, 2023.

#### What changed?
DuneSQL now uses the same data types as the underlying EVM blockchain. This means that we now store addresses, transactions hashes and other encoded data(transaction data,trace instructions, log topics & data) as `varbinary` datatype.      

Additionally, we now support `uint256` and `int256` allowing full wei-level precision calculations.  

Furthermore, we have corrected an ancient mistake in our database -  we now store logs with the correct topic indexing. This means that columns in `<blockchain>.logs` table are now indexed from 0 instead of 1. `Topic1` changed to `Topic0`, `Topic2` changed to `Topic1`, etc.
#### What does this mean for me?

First of all, switching to the `varbinary` datatype should significantly(≈30%) improve the speed of your queries!

Secondly, we can get rid of all string casts and conversions, which should make your queries more readable and easier to maintain. All addresses, hashes, and other encoded data are now stored as `varbinary` and can be used directly in your queries. No more `lower()` casting or string encasing. You can simply query for `0x1234...` instead of `'0x1234...'` or `lower('0x1234...')`.  

Thirdly, with the introduction of `uint256` and `int256` we can now perform full wei-level precision calculations. This means that you can now query for the exact amount of tokens transferred in a transaction, instead of the rounded value.  

Finally, we have corrected the indexing of logs topics. This means that Dune now matches the indexing of logs topics with the rest of the blockchain ecosystem.

#### What do I need to do?

We have appended a comment `-- dunesql_alpha_deprecated` to any query which had incompatible functions. This comment allows the query to be ran against the old data types until March 23, 2023. We urge you to remove the comment and convert your query to use compatible functions before the deprecation date.

More specifically, you will need to:

1. Remove the `-- dunesql_alpha_deprecated` comment from your query
2. Adjust all occurences of `0x`strings to fit the new data types. For example, `'0x1234...'` should be changed to `0x1234...` and all `lower()` casts should be removed.  
If you used any other operator on string columns, you will need to adjust them to the new approaches of working with `varbinary` columns. They are documented in the [DuneSQL documentation](https://dune.com/docs/reference/dune-v2/query-engine/#byte-array-functions-in-dune-sql). 
3. If you used any `varchar -> double`, `varchar -> decimals` or `varchar -> bigint` casts, you can now remove them. This is not strictly necessary, but it will make your query more readable and easier to maintain.
4. If your query used any columns from logs tables, you will need to adjust the indexing of topics. `Topic1` changed to `Topic0`, `Topic2` changed to `Topic1`, etc.
5. If you used the [query a query function](https://dune.com/docs/reference/dune-v2/query-engine/#query-a-query), you will need to remove all `--dunesql_alpha_deprecated` comments from all involved queries.

#### What if I don't do anything?

If you don't remove the `-- dunesql_alpha_deprecated` comment from your query, it will continue to run against the old data types until March 23, 2023. After that date, your query will no longer run and you will need to update it to use compatible functions.

#### Common Errors and Fixes
| Error | Example | Solution |
|---|---|---|
| Needing to cast varchar to varbinary | `Cannot apply operator: varbinary = varchar(X)` or `Cannot apply operator: varchar = varbinary at` | `from_hex(substring( x from 3)` |
| Casting to uint256 | `Cannot apply operator: UINT256 = varchar(7) at`  | `cast(xxx as uint256)` |
| Use bytearray_subtring |`Unexpected parameters (varbinary, integer, integer) for function substring. Expected: substring(varchar(x), bigint), substring(varchar(x), bigint, bigint), substring(char(x), bigint), substring(char(x), bigint, bigint) at`  | `substring(data, 3, 16)` would be `bytearray_substring(data, 1, 8)` |
| Use `bytearray_substring` and `bytearray_starts_with` instead of LIKE expression | `Left side of LIKE expression must evaluate to a varchar (actual: varbinary) at` | `bytearray_starts_with(varbinary, expression)` |
 
#### Changes


| Description | Previous behavior | New behavior | Breaking query/anti-pattern | Fixed query |
|---|---|---|---|---|
| 0x-literals change type to varbinary | 0x-literals had type varchar. I.e., 0xabCD = ‘0xabcd’, and typeof(0xabcd) = ‘varchar’ | 0x-literals have type varbinary. I.e. 0xabCD = X’abcd’, and typeof(0xabcd) = ‘varbinary’ | select * from ethereum.logs where tx_hash = ‘0xabcdef’ | select * from ethereum.logs where tx_hash = 0xabcdef |
| Byte array type columns of base tables and decoded tables now have varbinary type. Example byte array columns are hash, to, from, block_hash, tx_hash, evt_tx_hash, contract_address, call_tx_hash, data, topic0, topic1. This changes the way byte arrays are indexed, as you now index by bytes, instead of by hexadecimal digits. | Byte array type columns had type varchar and were represented as 0x-prefixed hex strings. Byte arrays are indexed by hexadecimal digits instead of by the natural byte position, after accounting for the 0x-prefix. | Byte array type columns have type varbinary. Bytes are indexed with their natural position. | select substring(data, 3, 16) from ethereum.transactions limit 10 -- start at characther 3 to skip 0x-prefix, and read 16 hex characters to get 8 bytes | select bytearray_substring(data, 1, 8) from ethereum.transactions limit 10 -- read 8 bytes |
| Numeric columns with potentially larger numbers are stored as UINT256 or INT256. | Numeric columns with potentially large  numbers were stored as strings. They would need to be cast to bigint or double before they could be used for arithmetic. | Numeric columns are stored as UINT256 or INT256. They show up as UINT256 or INT256 in the data explorer instead of VARCHAR. | select sum(cast(amount as double)) from aave_ethereum.AToken_call_transfer where call_success = true | select sum(amount) from aave_ethereum.AToken_call_transfer where call_success = true -- no longer required to cast to double |
| The logs.topicX columns are renamed to be topic0, topic1, topic2, topic3 | The topic columns of logs tables were named topic1, topic2, topic3, topic4. | The topic columns of logs tables are renamed to topic0, topic1, topic2, topic3. | select topic1, topic2, topic3, topic4 from ethereum.logs limit 10 | select topic0, topic1, topic2, topic3 from ethereum.logs limit 10 |
| Decoded tables no longer automatically coerce breaking type changes on contract updates. It is very rare for contract updates to do breaking type changes. | We would automatically convert values with different data types to the same, either implicitly using Spark, or with a couple of explicit rules. | We no longer automatically coerce breaking type changes of contract updates. These need to be handled manually. |  |  |