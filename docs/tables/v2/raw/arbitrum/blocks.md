# Blocks

## arbitrum.blocks

Blocks are the building blocks of blockchains and rollups. A block contains transactions which will alter the state of an EVM system incrementally. Transaction within a block can only be executed one after the other, not in parallel.

| **Column Name**     | **datatype** | **Description**                           |
| ------------------- | ------------ | ----------------------------------------- |
| time                | timestamptz  | the time when the block was mined.        |
| number              | numeric      | the length of the blockchain in blocks    |
| hash                | string       | a unique identifier for that block        |
| parent hash         | string       | the unique identifier for the prior block |
| gas\_limit          | numeric      | the ArbGas limit of the current block     |
| gas\_used           | numeric      | the ArbGas used in this block             |
| miner               | string       | not applicable                            |
| difficulty          | numeric      | not applicable                            |
| total\_difficulty   | numeric      | not applicable                            |
| nonce               | string       | not applicable                            |
| size                | numeric      | not applicable                            |
| base\_fee\_per\_gas | numeric      | not applicable                            |
