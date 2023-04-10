---
title: Overview
description: Instead of working with the transactions, logs, and traces in their raw states, on Dune we decode smart contract activity into nice human-readable tables.
---

To make it easier to work with smart contracts, Dune also provides decoded data as individual, human readable tables. **This means you don't need to work with any of the raw bytearray/binary data from the blockchain!**

## EVM decoded tables

We support [decoded tables for Ethereum based chains (EVM)](evm/index.md) like Ethereum, Optimism, Arbitrum - basically all chains in Dune except Solana and Bitcoin. There are two types of EVM decoded tables, one that decodes functions and one that decodes event logs. 
<div class="cards grid" markdown>
- [Call Tables](evm/call-tables.md): These are decoded from traces, which contain every function call within a transaction (i.e. between contracts).
- [Event Log Tables](evm/event-logs.md): These are decoded from event logs, which are data points emitted during a function call.
</div>

## Solana decoded tables

We also support [decoded tables on Solana](solana/idl-tables.md). Right now the tables decode instruction calls from each transaction to programs that have a verified Anchor IDL or are System/Native programs.

<div class="cards grid" markdown>
- [IDL Tables](solana/idl-tables.md): These are decoded from `instruction_calls`, so all function calls at the first instruction level (not inner instructions) are decoded.
</div>