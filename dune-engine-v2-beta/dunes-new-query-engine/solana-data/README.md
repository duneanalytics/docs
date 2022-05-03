---
description: >-
  Our database automatically pulls in raw data from the Solana Blockchain and
  parses them into different tables depending on which aspect that table is
  focused on.
---

# Solana Data

All of the tables below are built in an updated version of the Dune platform that will require a slight change to how wizards write queries in the platform. The new data platform leverages spark to increase query speed, data scale, and to support multi-chain queries. &#x20;

A reference document to use as you start to query the Solana tables is available here:&#x20;

{% embed url="https://spark.apache.org/docs/latest/sql-ref-ansi-compliance.html" %}

## Solana.blocks

This table contains the block data within Solana’s blockchain. It can be used to identify block activity and transaction changes over time.

&#x20;Query examples can be found here: [Solana blocks over time](https://dune.xyz/queries/389979) and [Transactions per day](https://dune.xyz/queries/390045)

| Column Name              | Column Type | Description                                         |
| ------------------------ | ----------- | --------------------------------------------------- |
| hash                     | string      | string The hash of this block, base-58 encoded      |
| height                   | bigint      | The number of blocks beneath this block             |
| slot                     | bigint      | This block’s slot index in the ledger               |
| time                     | timestamp   | The (estimated) time this block was produced        |
| date                     | date        | Used to partition by                                |
| parent\_slot             | bigint      | The slot index of this block's parent               |
| previous\_block_\__hash  | string      | The hash of this block's parent, base-58 encoded    |
| total\_transactions      | bigint      | The total number of transactions in this block      |
| successful\_transactions | bigint      | The number of successful transactions in this block |
| failed\_transactions     | bigint      | The number of failed transactions in this block     |

## Solana.transactions

This table contains the transaction data within Solana’s blockchain. Most of the relevant data related to account, protocol, and program activity is available in this table.

Query examples can be found here: [NFT transactions of popular programs past 7 days](https://dune.xyz/queries/390720/745376) and [drift-protocol overview ](https://dune.xyz/bigz/drift-\(solana\))

| Column Name                    | Column Type                   | Description                                                                                                                                                                                                                           |
| ------------------------------ | ----------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| block\_slot                    | bigint                        | This block’s slot index in the ledger                                                                                                                                                                                                 |
| block\_time                    | timestamp                     | The (estimated) time this block was produced                                                                                                                                                                                          |
| block\_date                    | date                          | Event date                                                                                                                                                                                                                            |
| index                          | bigint                        | Index into the block’s transactions                                                                                                                                                                                                   |
| fee                            | bigint                        | Fee this transaction was charged, as paid by first account                                                                                                                                                                            |
| block\_hash                    | string                        | The hash of this block, base-58 encoded                                                                                                                                                                                               |
| error                          | STRUCT error                  | NULL if success is true.                                                                                                                                                                                                              |
| required\_signatures           | bigint                        | The total number of signatures required to make the transaction valid.                                                                                                                                                                |
| readonly\_signed_\__accounts   | bigint                        | The last readonly\_signed\_accounts of the signed keys are read-only accounts.                                                                                                                                                        |
| readonly\_unsigned_\__accounts | bigint                        | The last readonly\_unsigned\_accounts of the unsigned keys are read-only accounts.                                                                                                                                                    |
| id                             | string                        | The first signature in the transaction                                                                                                                                                                                                |
| success                        | boolean                       | The transaction was valid and thus committed.                                                                                                                                                                                         |
| recent\_block_\__hash          | string                        | The hash of a recent block in the ledger, used to prevent transaction duplication and to give transactions lifetimes                                                                                                                  |
| instructions                   | array\<STRUCT instructions>   | Instructions to execute (in order)                                                                                                                                                                                                    |
| accountKeys                    | array\<string>                | The account keys used in the transaction                                                                                                                                                                                              |
| log\_messages                  | array\<string>                | The log messages emitted by the transaction                                                                                                                                                                                           |
| pre\_balances                  | array\<bigint>                | Array of account balances before the transaction was processed. The i-th balance is the balance of the i-th account key in account\_keys                                                                                              |
| post\_balances                 | array\<bigint>                | Array of account balances after the transaction was processed. The i-th balance is the balance of the i-th account key in account\_keys                                                                                               |
| pre\_token\_balance            | array\<STRUCT token\_balance> | List of [token balances](https://docs.solana.com/developing/clients/jsonrpc-api#token-balances-structure) from before the transaction was processed or omitted if token balance recording was not yet enabled during this transaction |
| post\_token\_balance           | array\<STRUCT token\_balance> | List of [token balances](https://docs.solana.com/developing/clients/jsonrpc-api#token-balances-structure) from after the transaction was processed or omitted if token balance recording was not yet enabled during this transaction  |
| signatures                     | array\<string>                | A list of base-58 encoded signatures applied to the transaction. Always of length numRequiredSignatures                                                                                                                               |
| signer                         | string                        | The initial value from the account\_keys array that initiates the transaction and pays the transaction fee                                                                                                                            |

### Struct definitions

Within several of these columns is a data type of STRUCT which allows for representing nested hierarchical data and has key-value pairs. It's similar to a dictionary in python and can be used to group fields together to make them more accessible.&#x20;

An example of how these can be used to extract data: [# of Solana instructions by day for DEXes](https://dune.xyz/queries/416358/794290)

**token\_balance**

| Field   | Data type | Description                                                                                                                                                                  |
| ------- | --------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| account | string    | The account key of the account that the token balance is provided for.                                                                                                       |
| mint    | string    | Public key of the token’s mint. This is an account that stores metadata about the token: The supply, number of decimals, and various authorities with control over the mint. |
| amount  | Decimal   | Derived from the token balance's raw amount (ui\_token\_amount.amount) and the number of decimals (ui\_token\_amount.decimals)                                               |

****

**instructions**

| Field               | Data type                          | Description                                                    |
| ------------------- | ---------------------------------- | -------------------------------------------------------------- |
| account\_arguments  | array\<string>                     | Ordered list of accounts to pass to the program                |
| data                | string                             | Program input data in a base-58 string                         |
| executing\_account  | string                             | The account key of the program that executed this instruction. |
| inner\_instructions | array\<STRUCT inner\_instructions> | The instructions invoked by this instruction.                  |

****

**inner\_instructions**

| Field              | Data type      | Description                                                    |
| ------------------ | -------------- | -------------------------------------------------------------- |
| account\_arguments | array\<string> | Ordered list of accounts to pass to the program                |
| data               | string         | Program input data in a base-58 string                         |
| executing\_account | string         | The account key of the program that executed this instruction. |

****

**error**

| Field                  | Data type | Description                        |
| ---------------------- | --------- | ---------------------------------- |
| **instruction\_index** | int       | The instruction number that failed |
| message                | string    | The error message                  |

## Solana.vote\_transactions

This table contains the full set of vote transactions that are submitted by validators to vote on a block. It can be joined with the non-vote transactions table above to get a full breakdown of all transactions. It has the same schema as the main transactions table.

An example query that demonstrates that is available here: [Solana transactions past 30 days](https://dune.xyz/queries/389976/743760)

## Solana.rewards

This table contains data about rewards paid out on Solana. One block may contain zero or more rewards, and each row corresponds to one reward.&#x20;

An example query can be found here: [Solana rewards fee per day](https://dune.xyz/queries/391421/747012)

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

## Solana.account\_activity

This table contains information from the transactions table focused on account usage. Each row contains all information about an account's usage in a transaction.

An example query can be found here:&#x20;

| Column Name              | Column Type | Description                                                      |
| ------------------------ | ----------- | ---------------------------------------------------------------- |
| block\_slot              | bigint      | The slot of the block this transaction was in.                   |
| block\_hash              | string      | The hash of the block this transaction was in                    |
| block\_time              | timestamp   | The timestamp that this account usage occurred                   |
| block\_date              | date        | The date this account usage occurred                             |
| address                  | string      | The address of the account, also referred to as public key       |
| tx\_index                | int         | The index of this transaction in the block                       |
| tx\_id                   | string      | The ID of the transaction in which this account usage occurred   |
| tx\_success              | boolean     | The transaction succeeded and was committed                      |
| signed                   | boolean     | This account signed this transaction                             |
| writeable                | boolean     | This account was granted read-write access in this transaction   |
| pre\_balance             | bigint      | The balance of this account before the transaction was processed |
| pre\_token_\__balance    | decimal     | The token balance before the transaction was processed           |
| post\_balance            | bigint      | The balance of this account after the transaction was processed  |
| post\_token_\__balance   | decimal     | he token balance after the transaction was processed             |
| balance\_change          | bigint      | The balance change that occurred as part of the transaction      |
| token\_balance_\__change | decimal     | The balance change that occurred as part of the transaction      |

