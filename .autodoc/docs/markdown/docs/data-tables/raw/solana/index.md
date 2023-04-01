[View code on GitHub](https://dune.com/docs/data-tables/raw/solana/index.md)

# Solana Technical Guide

This technical guide provides information on Solana's raw data and how it differs from other chains. The guide is divided into two main sections: Data Available and Changelog.

## Data Available

This section provides a list of tables available in Solana's data. The tables are:

- Account Activity: This table contains information from the transactions table focused on account usage.
- Blocks: Blocks are the building blocks of blockchains and rollups.
- Rewards: This table contains data about rewards paid out on Solana.
- Transactions: Transactions are cryptographically signed instructions from accounts.
- Vote Transactions: This table contains the full set of vote transactions that are submitted by validators to vote on a block.

## Changelog

This section provides a list of changes made to Solana's data. The changes are:

### 2022-03-25

The `solana.account_activity` table has been updated to a new version. The new version of the table contains additional information around token activity. The following columns were added to the table:

- `pre_token_balances`: The token balance before the transaction was processed.
- `post_token_balances`: The token balance after the transaction was processed.
- `token_balance_changes`: The balance change that occurred as part of the transaction.

### 2022-03-18

The `solana.account_activity` table was released. The table contains all of the information about an account’s usage in a transaction. The table is optimized to run with ‘WHERE address = …’ queries.

### 2022-03-01

The `solana.transactions` table has been upgraded to a new version. The new version of the table uses cleaner array structs to make it easier to extract useful information. The vote transactions have also been split into their own table `solana.vote_transactions`, so queries using `solana.transactions` will have better performance. Unfortunately, the table change also means that some existing queries will now break and need to be changed.

The changes made to the `solana.transactions` table are:

- You won't need to check if a transaction is a vote transaction, which has typically been done with `WHERE ARRAY_CONTAINS(account_keys, "Vote111111111111111111111111111111111111111") = false`.
- The `error_index` and `error_message` columns have been removed, and have been merged into the `error` column (which is a struct). So now instead of `WHERE error_index is not null`, a query should do `WHERE error is not null`.
- Structs containing indexes to `account_keys` now include the account address directly, so there is no need to use the `account_keys` column to look up the account addresses.
- The `pre_token_balances` and `post_token_balances` columns have changed. The token balance is now included in the field `amount`. And as mentioned above, the struct in the array now has a field `account`, which is the account of the token balance.
- The `instructions` column has changed. As mentioned above, the struct in the array now has a field `executing_account`, which is the account executing the instruction.
- The `inner_instructions` column is removed, and inner instructions have been moved into the `instructions` column.

In summary, this technical guide provides information on Solana's raw data and the available tables. It also highlights the changes made to the `solana.account_activity` and `solana.transactions` tables. The guide is useful for developers who want to work with Solana's data and need to understand the changes made to the tables.
## Questions: 
 1. What is Solana and how does it differ from other chains?
- Solana is a non-EVM chain and its raw data looks different from other chains. 

2. What data is available in Solana and what information does each table contain?
- Solana has several tables available, including account activity, blocks, rewards, transactions, and vote transactions. Each table contains specific data related to its name.

3. What changes were made to the Solana tables in the latest update and how might this affect existing queries?
- The latest update added new columns to the `solana.account_activity` table and split vote transactions into their own table. Existing queries may need to be updated to reflect changes in column names and structures.