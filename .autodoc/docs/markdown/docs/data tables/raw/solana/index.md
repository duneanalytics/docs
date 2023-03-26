[View code on GitHub](https://dune.com/blob/master/data tables\raw\solana\index.md)

# Solana Technical Guide

This technical guide provides information on Solana's raw data and how it differs from other chains. It also provides details on the data available in the app and the changelog of the app.

## Data Available

This section provides a list of the data available in the app. It includes the following:

- Account Activity: This table contains information from the transactions table focused on account usage.
- Blocks: Blocks are the building blocks of blockchains and rollups.
- Rewards: This table contains data about rewards paid out on Solana.
- Transactions: Transactions are cryptographically signed instructions from accounts.
- Vote Transactions: This table contains the full set of vote transactions that are submitted by validators to vote on a block.

## Changelog

This section provides a list of changes made to the app. It includes the following:

### 2022-03-25

The `solana.account_activity` table has been updated to a new version. The new version of the table contains additional information around token activity. The following columns were added to the table:

- `pre_token_balances`: The token balance before the transaction was processed.
- `post_token_balances`: The token balance after the transaction was processed.
- `token_balance_changes`: The balance change that occurred as part of the transaction.

### 2022-03-18

The `solana.account_activity` table has been released. It contains all of the information about an account’s usage in a transaction. The table is optimized to run with ‘WHERE address = …’ queries.

### 2022-03-01

The `solana.transactions` table has been upgraded to a new version. The new version of the table uses cleaner array structs to make it easier to extract useful information. The vote transactions have also been split into their own table `solana.vote_transactions`, so queries using `solana.transactions` will have better performance. 

This section also provides information on what the changes mean for existing queries using `solana.transactions`. It includes the following:

- You won't need to check if a transaction is a vote transaction.
- The `error_index` and `error_message` columns have been removed and merged into the `error` column.
- Structs containing indexes to `account_keys` now include the account address directly.
- The `pre_token_balances` and `post_token_balances` columns have changed.
- The `instructions` column has changed.
- The `inner_instructions` column is removed, and inner instructions have been moved into the `instructions` column.

Overall, this technical guide provides a comprehensive overview of Solana's raw data and the data available in the app. It also provides information on the changes made to the app and what they mean for existing queries.
## Questions: 
 1. What is Solana and how does it differ from other chains?
- Solana is a non-EVM chain and its raw data looks different from other chains.

2. What data is available in this app and what information does it provide?
- The app provides information on account activity, blocks, rewards, transactions, and vote transactions.

3. What changes were made to the `solana.transactions` table and how might it affect existing queries?
- The `solana.transactions` table has been upgraded to a new version, with cleaner array structs and better performance for queries. However, some existing queries may break due to changes in column names and structures.