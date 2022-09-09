# Transactions

## polygon.transactions

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
| value                        | numeric      | the amount of ether sent in this transaction in wei. note that erc20 tokens do not show up here.                                                                                                       |
| block\_number                | int8         | the length of the blockchain in blocks                                                                                                                                                                 |
| block\_hash                  | bytea        | a unique identifier for that block                                                                                                                                                                     |
| gas\_limit                   | numeric      | the gas limit in wei                                                                                                                                                                                   |
| gas\_price                   | numeric      | the gas price in wei                                                                                                                                                                                   |
| gas\_used                    | numeric      | the gas consumed by the transaction in wei                                                                                                                                                             |
| data                         | bytea        | can either be empty, a hex encoded message or instructions for a smart contract call                                                                                                                   |
| hash                         | bytea        | the hash of the transaction                                                                                                                                                                            |
| type                         | text         | the type of the transaction: `Legacy`, `AccessList`, or`DynamicFee`                                                                                                                                    |
| access\_list                 | jsonb        | a list of addresses and storage keys the transactions intends to access. See [EIP2930](https://eips.ethereum.org/EIPS/eip-2930). Applicable if the transaction is of type `AccessList` or `DynamicFee` |
| max\_fee\_per\_gas           | numeric      | the maximum fee per gas the transaction sender is willing to pay total (introduced by [EIP1559](https://eips.ethereum.org/EIPS/eip-1559))                                                              |
| max\_priority\_fee\_per\_gas | numeric      | maximum fee per gas the transaction sender is willing to give to miners to incentivize them to include their transaction (introduced by [EIP1559](https://eips.ethereum.org/EIPS/eip-1559))            |
| priority\_fee\_per\_gas      | numeric      | the priority fee paid out to the miner for this transaction (introduced by [EIP1559](https://eips.ethereum.org/EIPS/eip-1559))                                                                         |

\*\*\*\*[**Take a look for yourself**](https://dune.com/queries/38964)\*\*\*\*
