---
title: Transactions
description: Transactions are cryptographically signed instructions from accounts.
---

Transactions are cryptographically signed instructions from accounts. An account will initiate a transaction to update the state of the Ethereum network. Transactions will always originate from externally owned accounts, a smart contract can not initiate a transaction.

Transactions need to be broadcast to the whole network. Any node can broadcast a request for a transaction to be executed on the EVM; after this happens, a miner will execute the transaction and propagate the resulting state change to the rest of the network.

Read more in the official Ethereum documentation [here](https://ethereum.org/en/developers/docs/transactions).

## Tables

=== "V2 Engine (Spark SQL)"

    |   Chain           |   Table               | Notes |
    | ----------------  | --------------------- | ----- |
    | Ethereum Mainnet  | `ethereum.transactions`     |  |
    | Gnosis Chain      | `gnosis.transactions`       |  |
    | Polygon           | `polygon.transactions`      |  |
    | Optimism          | `optimism.transactions`     | No EIP1559 so does not contain  `access_list`, `max_fee_per_gas`,`max_priority_fee_per_gas`, `priority_fee_per_gas` and `type` is always `Legacy` |
    | Optimism (legacy) | `optimism_legacy_ovm1.transactions` | No EIP1559 so does not contain  `access_list`, `max_fee_per_gas`,`max_priority_fee_per_gas`, `priority_fee_per_gas` and `type` is always `Legacy` |
    | BNB Chain         | `bnb.transactions`          | No EIP1559 so does not contain  `access_list`, `max_fee_per_gas`,`max_priority_fee_per_gas`, `priority_fee_per_gas` and `type` is always `Legacy` |
    | Arbitrum          | `arbitrum.transactions`     | No EIP1559 so does not contain  `access_list`, `max_fee_per_gas`,`max_priority_fee_per_gas`, `priority_fee_per_gas` and `type` is always `Legacy`. Gas is measured in `ArbGas` instead of `wei` |
    | Avalanche C-Chain  | `avalanche_c.transactions` | Does not contain. Gas is measured in `nanoavax` instead of `wei` |

=== "V1 Engine (PosgreSQL)"

    |   Chain              |   Table                 |   Notes   |
    | -------------------  | ----------------------- | --------- |
    | Ethereum Mainnet     | `ethereum.transactions` |           |
    | Gnosis Chain (xDai)  | `xdai.transactions`     |           |
    | Polygon              | `polygon.transactions`  |           |
    | Optimism (OVM 1 & 2) | `optimism.transactions` | No EIP1559 so does not contain  `access_list`, `max_fee_per_gas`,`max_priority_fee_per_gas`, `priority_fee_per_gas` and `type` is always `Legacy` |
    | BNB Chain (BSC)      | `bsc.transactions`      | No EIP1559 so does not contain  `access_list`, `max_fee_per_gas`,`max_priority_fee_per_gas`, `priority_fee_per_gas` and `type` is always `Legacy` |

## Column Data

### Example

![type:video](https://dune.com/embeds/1582277/2634087/017d7f95-4cef-46f6-8637-7077ce9f5536)

### Description

|  Column  **            |  Data type   |  Description                                                   |
| -------------------------- | :-----------: | ---------------------------------------------------------------- |
| `block_time`               | _timestamptz_ | The time when the block was mined that includes this transaction |
| `block_number`             | _int8_        | The length of the blockchain in blocks                     |
| `value`                      | _numeric_     | The amount of `[chain_gas_token]` sent in this transaction in `wei`. Note that ERC20 tokens do not show up here |
| `gas_limit`                | _numeric_     | The gas limit in `wei` (ArbGas for Arbitrum) |
| `gas_price`                | _numeric_     | The gas price in `wei`                                    |
| `gas_used`                 | _numeric_     | The gas consumed by the transaction in `wei`              |
| `max_fee_per_gas`          | _numeric_     | The maximum fee per gas the transaction sender is willing to pay total (introduced by [EIP1559](https://eips.ethereum.org/EIPS/eip-1559)) |
| `max_priority_fee_per_gas` | _numeric_     | Maximum fee per gas the transaction sender is willing to give to miners to incentivize them to include their transaction (introduced by [EIP1559](https://eips.ethereum.org/EIPS/eip-1559)) |
| `priority_fee_per_gas`     | _numeric_     | The priority fee paid out to the miner for this transaction (introduced by [EIP1559](https://eips.ethereum.org/EIPS/eip-1559)) |
| `nonce`                    | _numeric_     | The transaction nonce, unique to that wallet               |
| `index`                    | _numeric_     | The transactions index position in the block               |
| `success`                  | _boolean_     | A true/false value that shows if the transaction succeeded |
| `from`                     | _bytea_       | Address of the sender                                      |
| `to`                       | _bytea_       | Address of the receiver. `null` when its a contract creation transaction |
| `block_hash`               | _bytea_       | A unique identifier for that block                         |
| `data`                     | _bytea_       | Can either be empty, a hex encoded message or instructions for a smart contract call |
| `hash`                     | _bytea_       | The hash of the transaction                                |
| `type`                     | _text_        | The type of the transaction: `Legacy`, `AccessList`, or `DynamicFee` |
| `access_list`              | _jsonb_       | A list of addresses and storage keys the transaction intends to access. See [EIP2930](https://eips.ethereum.org/EIPS/eip-2930). Applicable if the transaction is of type `AccessList` or `DynamicFee` |
| `effective_gas_price` | _numeric_      | [Arbitrum and Avalanche C-Chain only] The gas price this transaction paid in `wei` (Arbitrum) or `nanoavax` (Avalanche) |
| `gas_used_for_l1` | _numeric_ | [Arbitrum only] The gas consumed by the L1 resources used for this transaction in ArbGas |
| `l1_gas_used` | _numeric_ | [Optimism only] The costs to send the input `calldata` to L1 |
| `l1_gas_price` | _numeric_ | [Optimism only] The gas price on L1 |
| `l1_fee` | _numeric_ | [Optimism only] The amount in wei paid on L1  |
| `l1_fee_scalar` | _numeric_ | [Optimism only] Variable parameter that makes sure that gas costs on L1 get covered + profits |
| `l1_block_number` | _numeric_ | [Optimism only] The block_number of the block in which this transaction got batch settled on L1 |
| `l1_timestamp` | _numeric_ | [Optimism only] The timestamp of the block in which this transaction got batch settled on L1 |
| `l1_tx_origin` | _numeric_ | [Optimism only] ?? |