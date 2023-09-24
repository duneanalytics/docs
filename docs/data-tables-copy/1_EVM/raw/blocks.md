---
title: Blocks
description: Blocks are the building blocks of blockchains and rollups.
---

Blocks are the building blocks of blockchains and rollups. A block contains transactions which will alter the state of an EVM system incrementally. Transaction within a block can only be executed one after the other, not in parallel.

These tables are useful for identifying block activity and transaction changes over time.

## Column Data

| Column name           |   Data type    |    Description                                     |
| --------------------- | :------------: | ------------------------------------------------- |
| `time`                | _timestamptz_  | The time when the block was mined                 |
| `number`              | _numeric_      | The length of the blockchain in blocks            |
| `hash`                | _bytea_        | A unique identifier for that block                |
| `parent hash`         | _bytea_        | The unique identifier for the prior block         |
| `gas_limit`           | _numeric_      | The gas limit of the current block                |
| `gas_used`            | _numeric_      | The gas used in this block                        |
| `miner`               | _bytea_        | The address of the miner                          |
| `difficulty`          | _numeric_      | The effort required to mine the block             |
| `total_difficulty`    | _numeric_      | Total difficulty of the chain until this block    |
| `nonce`               | _bytea_        | The block nonce is used to demonstrate the proof of work during mining |
| `size`                | _numeric_      | This block's size in bytes (limited by gas limit) |
| `base_fee_per_gas`    | _numeric_      | This block's base fee (introduced by [EIP1559](https://eips.ethereum.org/EIPS/eip-1559)) |

## Example

![type:video](https://dune.com/embeds/3045123/5064331)



