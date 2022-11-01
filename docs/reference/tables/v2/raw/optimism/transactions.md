# Transactions

## optimism.transactions

Transactions are cryptographically signed instructions from accounts. An account will initiate a transaction to update the state of the Ethereum network. Transactions will always originate from externally owned accounts, a smart contract can not initiate a transaction.

Transactions need to be broadcast to the whole network. Any node can broadcast a request for a transaction to be executed on the EVM; after this happens, a miner will execute the transaction and propagate the resulting state change to the rest of the network.

Read more in the official Ethereum documentation [here](https://ethereum.org/en/developers/docs/transactions).

| **Column Name**              | **datatype** | **Description**                                                                                  |
| ---------------------------- | ------------ | ------------------------------------------------------------------------------------------------ |
| block\_time                  | timestamptz  | the time when the block was mined that includes this transaction                                 |
| nonce                        | numeric      | the transaction nonce, unique to that wallet                                                     |
| index                        | numeric      | the transactions index position in the block                                                     |
| success                      | boolean      | a true/false value that shows if the transaction succeeded                                       |
| from                         | string       | address of the sender                                                                            |
| to                           | string       | address of the receiver. Null when its a contract creation transaction                           |
| value                        | numeric      | the amount of ether sent in this transaction in wei. note that erc20 tokens do not show up here. |
| block\_number                | int8         | the length of the blockchain in blocks                                                           |
| block\_hash                  | string       | a unique identifier for that block                                                               |
| gas\_limit                   | numeric      | the gas limit in wei                                                                             |
| gas\_price                   | numeric      | the gas price in wei                                                                             |
| gas\_used                    | numeric      | the gas consumed by the transaction in wei                                                       |
| data                         | string       | can either be empty, a hex encoded message or instructions for a smart contract call             |
| hash                         | string       | the hash of the transaction                                                                      |
| type                         | text         | the type of the transaction: `Legacy`, `AccessList`, or`DynamicFee`                              |
| access\_list                 | jsonb        | n/a                                                                                              |
| max\_fee\_per\_gas           | numeric      | n/a                                                                                              |
| max\_priority\_fee\_per\_gas | numeric      | n/a                                                                                              |
| priority\_fee\_per\_gas      | numeric      | n/a                                                                                              |
| l1\_gas\_used                | numeric      | the costs to send the input data (calldata) to L1                                                |
| l1\_gas\_price               | numeric      | the gas price on L1                                                                              |
| l1\_fee                      | numeric      | the amount in wei paid on l1                                                                     |
| l1\_fee\_scalar              | numeric      | variable parameter that makes sure that gas costs on l1 get covered + profits                    |
| l1\_block\_\number           | numeric      | the block\_number of the block in which this transaction got batch settled on L1                 |
| l1\_timestamp                | numeric      | the timestamp of the block in which this transaction got batch settled on L1                     |
| l1\_tx\_origin               | numeric      | ??                                                                                               |

\*\*\*\*[**Take a look for yourself**](https://dune.xyz/queries/38964)\*\*\*\*
