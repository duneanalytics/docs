# Blocks

## polygon.blocks

Blocks are the building blocks of blockchains and rollups. A block contains transactions which will alter the state of an EVM system incrementally. Transaction within a block can only be executed one after the other, not in parallel.

| **Column Name**     | **datatype** | **Description**                                                                          |
| ------------------- | ------------ | ---------------------------------------------------------------------------------------- |
| time                | timestamptz  | the time when the block was mined.                                                       |
| number              | numeric      | the length of the blockchain in blocks                                                   |
| hash                | bytea        | a unique identifier for that block                                                       |
| parent hash         | bytea        | the unique identifier for the prior block                                                |
| gas\_limit          | numeric      | the gas limit of the current block                                                       |
| gas\_used           | numeric      | the gas used in this block                                                               |
| miner               | bytea        | the address of the miner                                                                 |
| difficulty          | numeric      | the effort required to mine the block                                                    |
| total\_difficulty   | numeric      | total difficulty of the chain until this block                                           |
| nonce               | bytea        | the block nonce is used to demonstrate the proof of work during mining                   |
| size                | numeric      | this block's size in bytes (limited by gas limit)                                        |
| base\_fee\_per\_gas | numeric      | this block's base fee (introduced by [EIP1559](https://eips.ethereum.org/EIPS/eip-1559)) |

