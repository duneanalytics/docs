---
title: Raw Tables Overview
---

**Raw tables provide you raw, unfiltered and unedited data.**

This allows you to query for any transaction, block, event log or trace across the blockchains Dune supports.  Raw data tables are very useful to get meta information about the blockchain, a transaction, traces or certain events.

However, queries that have been written using raw data tables are notoriously hard to understand and audit due to the nature of the the encoded data commonly found in these tables. Furthermore, the raw data tables have a very large number of rows and hence can be slow to query. Most of the time you are better off [submitting contracts for decoding](../../app/decoding-contracts.md) and working with [decoded data](../decoded/index.md).

## EVM Raw Table Data

Ethereum Virtual Machine (EVM) powers all chains in Dune except Solana and Bitcoin - meaning they share the base structure for underlying data. For a full written guide on getting started, [check out this one](https://web3datadegens.substack.com/p/a-basic-wizard-guide-to-dune-sql).

<div class="cards grid" markdown>
- [Blocks](evm/blocks.md): Blocks are the base unit that all transactions fit into.
- [Event Logs](evm/event-logs.md): These are data points emitted during a function call.
- [Traces](evm/traces.md): Traces contain data from every function call within a transaction (i.e. between contracts) and based calls like deploying a contract.
- [Transactions](evm/transactions.md): Transactions are cryptographically signed instructions from accounts.
</div>

## Bitcoin Raw Table Data

Bitcoin data follows a UTXO model. For a full written guide on getting started, [check out this one](https://web3datadegens.substack.com/p/how-to-analyze-bitcoin-data-with).

<div class="cards grid" markdown>
- [Blocks](bitcoin/blocks.md): Blocks are the base unit that all transactions fit into.
- [Transactions](bitcoin/transactions.md): Transactions contain all spent inputs and created outputs from a UTXO transaction.
- [Outputs](bitcoin/outputs.md): Just the outputs, unnested.
- [Inputs](bitcoin/inputs.md): Just the inputs, unnested.
</div>

## Solana Raw Table Data

Solana data follows an instruction/program based model. You initiate a set of instruction calls (instead of just a single call), and those will set off a bunch of inner instruction calls during execution.. For a full written guide on getting started, [check out this one](https://web3datadegens.substack.com/p/how-to-analyze-bitcoin-data-with).

<div class="cards grid" markdown>
- [Account Activity](solana/account-activity.md): This table contains information from the transactions table focused on account usage.
- [Blocks](solana/blocks.md): Blocks are the base unit that all transactions fit into.
- [Rewards](solana/rewards.md): This table contains data about rewards paid out on Solana.
- [Transactions](solana/transactions.md): Transactions are cryptographically signed instructions from accounts.
- [Instruction Calls](solana/instruction-calls.md): Transactions are unnested here such that each instruction gets it's own row.
- [Vote Transactions](solana/vote-transactions.md): This table contains the full set of vote transactions that are submitted by validators to vote on a block.
</div>