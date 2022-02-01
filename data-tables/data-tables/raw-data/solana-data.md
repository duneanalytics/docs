---
description: >-
  Our database automatically pulls in raw data from the Solana Blockchain and
  parses them into different tables depending on which aspect that table is
  focused on.
---

# Solana Data

All of the tables below are built in an updated version of the Dune platform that will require a slight change to how wizards write queries in the platform. The new data platform leverages spark to increase query speed, data scale, and to support multi-chain queries. &#x20;

A reference document to use as you start to query the Solana tables is available here:&#x20;

[https://spark.apache.org/docs/latest/sql-ref-ansi-compliance.html](https://spark.apache.org/docs/latest/sql-ref-ansi-compliance.html)

## Solana.blocks

This table contains the block data within Solana’s blockchain. A query example can be found here: [**Solana blocks over time**](https://dune.xyz/queries/389979)****

| Column Name             | Column Type | Description                                      |
| ----------------------- | ----------- | ------------------------------------------------ |
| hash                    | string      | string The hash of this block, base-58 encoded   |
| height                  | bigint      | The number of blocks beneath this block          |
| slot                    | bigint      | This block’s slot index in the ledger            |
| time                    | timestamp   | The (estimated) time this block was produced     |
| date                    | date        | Used to partition by                             |
| parent\_slot            | bigint      | The slot index of this block's parent            |
| previous\_block_\__hash | string      | The hash of this block's parent, base-58 encoded |

## Solana.transactions

This table contains the transaction data within Solana’s blockchain. A query example can be found here: [Transactions per day (2022)](https://dune.xyz/queries/390045)

| Column Name                    | Column Type    | Description                                                                                                                                                                                                                           |
| ------------------------------ | -------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| block\_slot                    | bigint         | This block’s slot index in the ledger                                                                                                                                                                                                 |
| block\_time                    | timestamp      | The (estimated) time this block was produced                                                                                                                                                                                          |
| block\_date                    | date           | Event date                                                                                                                                                                                                                            |
| index                          | bigint         | Index into the block’s transactions                                                                                                                                                                                                   |
| fee                            | bigint         | Fee this transaction was charged, as paid by first account                                                                                                                                                                            |
| block\_hash                    | string         | The hash of this block, base-58 encoded                                                                                                                                                                                               |
| error\_index                   | bigint         | The index of the instruction that failed. Null if success is true.                                                                                                                                                                    |
| required\_signatures           | bigint         | The total number of signatures required to make the transaction valid.                                                                                                                                                                |
| readonly\_signed_\__accounts   | bigint         | The last readonly\_signed\_accounts of the signed keys are read-only accounts.                                                                                                                                                        |
| readonly\_unsigned_\__accounts | bigint         | The last readonly\_unsigned\_accounts of the unsigned keys are read-only accounts.                                                                                                                                                    |
| id                             | string         | The first signature in the transaction                                                                                                                                                                                                |
| success                        | boolean        | The transaction was valid and thus committed.                                                                                                                                                                                         |
| error\_message                 | string         | The error message of the instruction that failed                                                                                                                                                                                      |
| recent\_block_\__hash          | string         | The hash of a recent block in the ledger, used to prevent transaction duplication and to give transactions lifetimes                                                                                                                  |
| instructions                   | array\<object> | Instructions to execute (in order)                                                                                                                                                                                                    |
| accountKeys                    | array\<string> | List of base-58 encoded public keys used by the transaction, including by the instructions and for signatures                                                                                                                         |
| innerInstructions              | array\<object> | Instructions invoked by the instructions in the instructions array                                                                                                                                                                    |
| log\_messages                  | array\<string> | The log messages emitted by the transaction                                                                                                                                                                                           |
| preBalances                    | array\<number> | Array of account balances from before the transaction was processed                                                                                                                                                                   |
| postBalances                   | array\<number> | Array of account balances from after the transaction was processed                                                                                                                                                                    |
| preTokenBalance                | array\<object> | List of [token balances](https://docs.solana.com/developing/clients/jsonrpc-api#token-balances-structure) from before the transaction was processed or omitted if token balance recording was not yet enabled during this transaction |
| postTokenBalance               | array\<object> | List of [token balances](https://docs.solana.com/developing/clients/jsonrpc-api#token-balances-structure) from after the transaction was processed or omitted if token balance recording was not yet enabled during this transaction  |
| signatures                     | array\<string> | A list of base-58 encoded signatures applied to the transaction                                                                                                                                                                       |

## Solana.rewards

This table contains data about rewards paid out on Solana. One block may contain zero or more rewards, and each row corresponds to one reward.

| Column Name   | Column Type | Description                                                                                       |
| ------------- | ----------- | ------------------------------------------------------------------------------------------------- |
| block\_slot   | bigint      | This block’s slot index in the ledger                                                             |
| block\_hash   | string      | The hash of this block, base-58 encoded                                                           |
| block\_time   | timestamp   | The (estimated) time this block was produced                                                      |
| block\_date   | date        | Event date                                                                                        |
| commission    | string      | Vote account commission when the reward was credited, only present for voting and staking rewards |
| lamports      | bigint      | Number of reward lamports credited or debited by the account                                      |
| pre\_balance  | bigint      | Account balance in lamports before the reward was applied                                         |
| post\_balance | bigint      | Account balance in lamports after the reward was applied                                          |
| recipient     | string      | The public key, as base-58 encoded string, of the account that received the reward                |
| reward\_type  | string      | Type of reward: "fee", "rent", "voting", "staking"                                                |

