# Instruction Calls

!!! example "Warning"
    These tables are still in alpha state, as we are still ironing out some kinks in decoding. If you discover any issues, please let us know by [dming on Twitter](https://twitter.com/andrewhong5297). There may still be some changes to the table schemas as we add more decoding features.

This is an unnested table of [`solana.transactions`](transactions.md). There can be multiple instructions in a transaction, so having an exploded view here will make it a little easier to work with the data. **This table mainly exists as the base for [Solana decoded tables](../../decoded/solana/idl-tables.md) though, which you should be using instead.**

Here is the schema:

| Column Name               | Data Type     | Description                                         |
| ------------------- | --------------- | ------------------------------------ |
| block_slot | bigint | This block’s slot index in the ledger |
| block_date | date | Event date |
| block_time | timestamp(3) with time zone | Event time |
| block_hash | varchar | The hash of this block, base-58 encoded
| index | integer | the order of the instruction in the original instructions of the transaction |
| tx_index | integer | Index into the block’s transactions |
| executing_account | varchar | The account key of the program that executed this instruction |
| data | varbinary | Program input data in a base-58 string |
| account_arguments | array(varchar) | Ordered list of accounts to pass to the program |
| inner_instructions | array(row(data varchar, executing_account varchar, account_arguments array(varchar))) | see breakout below |
| tx_signer | varchar | The address that initiates the transaction and pays the transaction fee |
| tx_id | varchar | the first signature in the transaction |
| tx_success | boolean |The transaction was valid and thus committed. |
| log_messages | array<string> | The log messages emitted by the transaction |

**inner\_instructions**

| Field              | Data type      | Description                                                    |
| ------------------ | -------------- | -------------------------------------------------------------- |
| account\_arguments | array&lt;string&gt; | Ordered list of accounts to pass to the program                |
| data               | string         | Program input data in a base-58 string                         |
| executing\_account | string         | The account key of the program that executed this instruction. |
