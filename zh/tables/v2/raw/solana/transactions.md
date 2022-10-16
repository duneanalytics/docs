# Transactions

## Solana.transactions

This table contains the transaction data within Solana’s blockchain. Most of the relevant data related to account, protocol, and program activity is available in this table.

Query examples can be found here: [NFT transactions of popular programs past 7 days](https://dune.xyz/queries/390720/745376) and [drift-protocol overview](https://dune.xyz/bigz/drift-\(solana\))

| Column Name                      | Column Type                   | Description                                                                                                                                                                                                                           |
| -------------------------------- | ----------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| block\_slot                      | bigint                        | This block’s slot index in the ledger                                                                                                                                                                                                 |
| block\_time                      | timestamp                     | The (estimated) time this block was produced                                                                                                                                                                                          |
| block\_date                      | date                          | Event date                                                                                                                                                                                                                            |
| index                            | bigint                        | Index into the block’s transactions                                                                                                                                                                                                   |
| fee                              | bigint                        | Fee this transaction was charged, as paid by first account                                                                                                                                                                            |
| block\_hash                      | string                        | The hash of this block, base-58 encoded                                                                                                                                                                                               |
| error                            | STRUCT error                  | NULL if success is true.                                                                                                                                                                                                              |
| required\_signatures             | bigint                        | The total number of signatures required to make the transaction valid.                                                                                                                                                                |
| readonly\_signed\_\_\_accounts   | bigint                        | The last readonly\_signed\_accounts of the signed keys are read-only accounts.                                                                                                                                                        |
| readonly\_unsigned\_\_\_accounts | bigint                        | The last readonly\_unsigned\_accounts of the unsigned keys are read-only accounts.                                                                                                                                                    |
| id                               | string                        | The first signature in the transaction                                                                                                                                                                                                |
| success                          | boolean                       | The transaction was valid and thus committed.                                                                                                                                                                                         |
| recent\_block\_\_\_hash          | string                        | The hash of a recent block in the ledger, used to prevent transaction duplication and to give transactions lifetimes                                                                                                                  |
| instructions                     | array\<STRUCT instructions>   | Instructions to execute (in order)                                                                                                                                                                                                    |
| accountKeys                      | array\<string>                | The account keys used in the transaction                                                                                                                                                                                              |
| log\_messages                    | array\<string>                | The log messages emitted by the transaction                                                                                                                                                                                           |
| pre\_balances                    | array\<bigint>                | Array of account balances before the transaction was processed. The i-th balance is the balance of the i-th account key in account\_keys                                                                                              |
| post\_balances                   | array\<bigint>                | Array of account balances after the transaction was processed. The i-th balance is the balance of the i-th account key in account\_keys                                                                                               |
| pre\_token\_balance              | array\<STRUCT token\_balance> | List of [token balances](https://docs.solana.com/developing/clients/jsonrpc-api#token-balances-structure) from before the transaction was processed or omitted if token balance recording was not yet enabled during this transaction |
| post\_token\_balance             | array\<STRUCT token\_balance> | List of [token balances](https://docs.solana.com/developing/clients/jsonrpc-api#token-balances-structure) from after the transaction was processed or omitted if token balance recording was not yet enabled during this transaction  |
| signatures                       | array\<string>                | A list of base-58 encoded signatures applied to the transaction. Always of length numRequiredSignatures                                                                                                                               |
| signer                           | string                        | The initial value from the account\_keys array that initiates the transaction and pays the transaction fee                                                                                                                            |

### Struct definitions

Within several of these columns is a data type of STRUCT which allows for representing nested hierarchical data and has key-value pairs. It's similar to a dictionary in python and can be used to group fields together to make them more accessible.

An example of how these can be used to extract data: [# of Solana instructions by day for DEXes](https://dune.xyz/queries/416358/794290)

**token\_balance**

| Field   | Data type | Description                                                                                                                                                                  |
| ------- | --------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| account | string    | The account key of the account that the token balance is provided for.                                                                                                       |
| mint    | string    | Public key of the token’s mint. This is an account that stores metadata about the token: The supply, number of decimals, and various authorities with control over the mint. |
| amount  | Decimal   | Derived from the token balance's raw amount (ui\_token\_amount.amount) and the number of decimals (ui\_token\_amount.decimals)                                               |

***

**instructions**

| Field               | Data type                          | Description                                                    |
| ------------------- | ---------------------------------- | -------------------------------------------------------------- |
| account\_arguments  | array\<string>                     | Ordered list of accounts to pass to the program                |
| data                | string                             | Program input data in a base-58 string                         |
| executing\_account  | string                             | The account key of the program that executed this instruction. |
| inner\_instructions | array\<STRUCT inner\_instructions> | The instructions invoked by this instruction.                  |

***

**inner\_instructions**

| Field              | Data type      | Description                                                    |
| ------------------ | -------------- | -------------------------------------------------------------- |
| account\_arguments | array\<string> | Ordered list of accounts to pass to the program                |
| data               | string         | Program input data in a base-58 string                         |
| executing\_account | string         | The account key of the program that executed this instruction. |

***

**error**

| Field                  | Data type | Description                        |
| ---------------------- | --------- | ---------------------------------- |
| **instruction\_index** | int       | The instruction number that failed |
| message                | string    | The error message                  |

##
