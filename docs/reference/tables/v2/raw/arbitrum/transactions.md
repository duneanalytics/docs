# Transactions

## arbitrum.transactions

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
| to                           | string       | address of the receiver. Null when it's a contract creation transaction                          |
| value                        | numeric      | the amount of ether sent in this transaction in wei. Note that erc20 tokens do not show up here. |
| block\_number                | int8         | the length of the blockchain in blocks                                                           |
| block\_hash                  | string       | a unique identifier for that block                                                               |
| gas\_price                   | numeric      | the maximum gas price this transaction is willing to pay in wei                                  |
| effective\_gas\_price        | numeric      | the gas price this transaction paid in wei                                                       |
| gas\_limit                   | numeric      | the gas limit in ArbGas                                                                          |
| gas\_used                    | numeric      | the gas consumed by the transaction in ArbGas                                                    |
| gas\_used\_for\_l1           | numeric      | the gas consumed by the L1 resources used for this transaction in ArbGas                         |
| data                         | string       | can either be empty, a hex encoded message or instructions for a smart contract call             |
| hash                         | string       | the hash of the transaction                                                                      |
| type                         | text         | not applicable for Arbitrum                                                                      |
| access\_list                 | jsonb        | not applicable for Arbitrum                                                                      |
| max\_fee\_per\_gas           | numeric      | not applicable for Arbitrum                                                                      |
| max\_priority\_fee\_per\_gas | numeric      | not applicable for Arbitrum                                                                      |
| priority\_fee\_per\_gas      | numeric      | not applicable for Arbitrum                                                                      |
