---
title: Event Logs
description: Smart Contracts emit event logs to record predefined actions that have been executed.
---

## Introduction

Smart Contracts generate **event logs** to document predefined actions once they are executed. These logs possess a structure predetermined by the contract's developer, while the content is dynamically generated during transactions.

Utilizing logs is pivotal for monitoring, alerting, and generally tracking the activities within a smart contract. As a data analyst, logs serve as a reliable tool, offering data that is curated for post-transaction analysis. To ascertain which logs a smart contract _can_ generate, simply search for the `emit` keyword in the contract's source code.

We facilitate the decoding of all event logs for smart contracts, organizing them into tables with names corresponding to this schema: `[projectname_blockchain].[contractName]_evt_[eventName]`.

Taking the [uniswap v3 factory](https://etherscan.io/address/0x1f98431c8ad98523631ae4a59f267346ea31f984#code) as an example, let us explore the `PoolCreated` event, which is triggered whenever a new Uniswap V3 pool is successfully deployed through the `createPool` function. This event offers insights into various aspects, such as the tokens involved in the pool, the pool's fee tier, and tick spacing. On Etherscan, you can view the transaction's event logs under the [logs tab](https://etherscan.io/tx/0xdeb368592f3de0f2840754bce61d2c3f29cdb3407c63c699052e68a854c71eaa#eventlog). On Dune, this specific event is stored in the `uniswap_v3_ethereum.Factory_evt_PoolCreated` table.   

![type:video](https://dune.com/embeds/3033062/5041840)

## Addressing Multiple Instances

In situations where a contract has multiple instances, we consolidate all event logs from every instance into a unified table. For instance, all the `swap` events from Uniswap v3 pools (on Ethereum) are catalogued in the `uniswap_v3_ethereum.Pair_evt_Swap` table.

![type:video](https://dune.com/embeds/3033067/5041845)

The `contract_address` column denotes the specific instance of that smart contract that generated the event.

## Additional Resources

<div class="cards grid" markdown>
- [Understanding event logs on the Ethereum blockchain](https://medium.com/mycrypto/understanding-event-logs-on-the-ethereum-blockchain-f4ae7ba50378)
- [Everything You Ever Wanted to Know About Events and Logs on Ethereum](https://medium.com/linum-labs/everything-you-ever-wanted-to-know-about-events-and-logs-on-ethereum-fec84ea7d0a5)
</div>
