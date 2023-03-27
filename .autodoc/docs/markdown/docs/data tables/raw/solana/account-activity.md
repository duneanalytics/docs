[View code on GitHub](https://dune.com/blob/master/data tables\raw\solana\account-activity.md)

# Account Activity

This technical guide covers the `Solana.account_activity` table, which contains information from the transactions table focused on account usage. Each row contains all information about an account's usage in a transaction. The purpose of this guide is to provide a detailed description of the columns in the `Solana.account_activity` table and their corresponding data types.

The table contains the following columns:

- `block_slot`: a `bigint` representing the slot of the block this transaction was in.
- `block_hash`: a `string` representing the hash of the block this transaction was in.
- `block_time`: a `timestamp` representing the timestamp that this account usage occurred.
- `block_date`: a `date` representing the date this account usage occurred.
- `address`: a `string` representing the address of the account, also referred to as public key.
- `tx_index`: an `int` representing the index of this transaction in the block.
- `tx_id`: a `string` representing the ID of the transaction in which this account usage occurred.
- `tx_success`: a `boolean` representing whether the transaction succeeded and was committed.
- `signed`: a `boolean` representing whether this account signed this transaction.
- `writeable`: a `boolean` representing whether this account was granted read-write access in this transaction.
- `pre_balance`: a `bigint` representing the balance of this account before the transaction was processed.
- `pre_token_balance`: a `decimal` representing the token balance before the transaction was processed.
- `post_balance`: a `bigint` representing the balance of this account after the transaction was processed.
- `post_token_balance`: a `decimal` representing the token balance after the transaction was processed.
- `balance_change`: a `bigint` representing the balance change that occurred as part of the transaction.
- `token_balance_change`: a `decimal` representing the balance change that occurred as part of the transaction.
- `token_mint_address`: a `string` representing the address the associated token address is minting from (i.e. the actual token address).
- `token_owner_address`: a `string` representing the address that owns this token address.

This guide provides a clear understanding of the `Solana.account_activity` table and its columns. For example, if a developer wants to retrieve information about an account's usage in a transaction, they can use this table to get all the necessary information.
## Questions: 
 1. What blockchain platform is this app technical guide for?
- The app technical guide is for the Solana blockchain platform.

2. What specific account information is included in the table?
- The table contains information about an account's usage in a transaction, including its address, pre- and post-transaction balances, and token balances.

3. What is the purpose of the token\_mint\_address and token\_owner\_address columns?
- The token\_mint\_address column indicates the address from which the associated token is being minted, while the token\_owner\_address column indicates the address that owns the token address.