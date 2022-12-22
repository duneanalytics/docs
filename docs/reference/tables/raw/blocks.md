---
title: Blocks
description: Blocks are the building blocks of blockchains and rollups.
---

Blocks are the building blocks of blockchains and rollups. A block contains transactions which will alter the state of an EVM system incrementally. Transaction within a block can only be executed one after the other, not in parallel.

These tables are useful for identifying block activity and transaction changes over time.

## Tables

=== "V2 Engine (Spark SQL)"

    | Chain             | Table                | Notes                                                 |
    | ----------------  | -------------------- | ----------------------------------------------------- |
    | Ethereum Mainnet  | `ethereum.blocks`    |                                                       |
    | Gnosis Chain      | `gnosis.blocks`      | Does not contain `nonce`                              |
    | Polygon           | `polygon.blocks`     |                                                       |
    | Optimism          | `optimism.blocks`    | Does not contain `miner` `nonce` `base_fee_per_gas`   |
    | Optimism (legacy) | `optimism_legacy_ovm1.blocks` | Does not contain `miner` `nonce` `base_fee_per_gas` |
    | BNB Chain         | `bnb.blocks`         | Does not contain `base_fee_per_gas`                   |
    | Arbitrum          | `arbitrum.blocks`    | Does not contain `miner` `difficulty` `total_difficulty` `nonce` `size` `base_fee_per_gas` |
    | Avalanche C-Chain  | `avalanche_c.blocks` | Does not contain `miner` `difficulty`                 |
    

=== "V1 Engine (PosgreSQL)"

    | Chain                | Table             | Notes                                               |
    | -------------------  | ----------------- | --------------------------------------------------- |
    | Ethereum Mainnet     | `ethereum.blocks` |                                                     |
    | Gnosis Chain (xDai)  | `xdai.blocks`     | Does not contain `nonce`                            |
    | Polygon              | `polygon.blocks`  |                                                     |
    | Optimism (OVM 1 & 2) | `optimism.blocks` | Does not contain `miner` `nonce` `base_fee_per_gas` |
    | BNB Chain (BSC)      | `bsc.blocks`      | Does not contain `base_fee_per_gas`                 |

## Column Data

### Example

![type:video](https://dune.com/embeds/1513349/2544895/3a7395c7-0555-4cc4-a563-78c24a9bacbd)

### Description

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