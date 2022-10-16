# Transactions

## bnb.transactions

Transactions are cryptographically signed instructions from accounts. An account will initiate a transaction to update the state of the Ethereum network. Transactions will always originate from externally owned accounts, a smart contract can not initiate a transaction.

Transactions need to be broadcast to the whole network. Any node can broadcast a request for a transaction to be executed on the EVM; after this happens, a miner will execute the transaction and propagate the resulting state change to the rest of the network.

Read more in the official Ethereum documentation [here](https://ethereum.org/en/developers/docs/transactions).

| **Column Name**              | **datatype** | **Description**                                                                                                                                                                                        |
| ---------------------------- | ------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| block\_time                  | timestamptz  | the time when the block was mined that includes this transaction                                                                                                                                       |
| nonce                        | numeric      | the transaction nonce, unique to that wallet                                                                                                                                                           |
| index                        | numeric      | the transactions index position in the block                                                                                                                                                           |
| success                      | boolean      | a true/false value that shows if the transaction succeeded                                                                                                                                             |
| from                         | bytea        | address of the sender                                                                                                                                                                                  |
| to                           | bytea        | address of the receiver. Null when its a contract creation transaction                                                                                                                                 |
| value                        | numeric      | the amount of bnb sent in this transaction in jager. note that erc20 tokens do not show up here.                                                                                                       |
| block\_number                | int8         | the length of the blockchain in blocks                                                                                                                                                                 |
| block\_hash                  | bytea        | a unique identifier for that block                                                                                                                                                                     |
| gas\_limit                   | numeric      | the gas limit in jager                                                                                                                                                                                   |
| gas\_price                   | numeric      | the gas price in jager                                                                                                                                                                                   |
| gas\_used                    | numeric      | the gas consumed by the transaction in jager                                                                                                                                                             |
| data                         | bytea        | can either be empty, a hex encoded message or instructions for a smart contract call                                                                                                                   |
| hash                         | bytea        | the hash of the transaction                                                                                                                                                                            |
| type                         | text         | always legacy since no eip1559 on BNB chain                                                                                                                                                            |
| access\_list                 | jsonb        | n/a                                                                                                                                                                                                    |
| max\_fee\_per\_gas           | numeric      | n/a                                                                                                                                                                                                    |
| max\_priority\_fee\_per\_gas | numeric      | n/a                                                                                                                                                                                                    |
| priority\_fee\_per\_gas      | numeric      | n/a                                                                                                                                                                                                    |

\*\*\*\*[**Take a look for yourself**](https://dune.com/queries/38964)\*\*\*\*
