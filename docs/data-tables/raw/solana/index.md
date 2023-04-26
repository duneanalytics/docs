---
title: Solana Overview
description: As a non-EVM chain, Solana Raw data looks quite different from other chains. Learn more about Solana's data in these pages.
---

**Raw tables provide you raw, unfiltered and unedited data.**

Raw data tables are very useful to get transactions, pre and post balances, and instructions data. As a non-EVM chain, Solana Raw data looks quite different from other chains (largely due to it's account structure). You can learn to get started with Solana analysis [in this guide](https://web3datadegens.substack.com/p/starter-guide-to-solana-data-analysis).

However, queries that have been written using raw data tables are notoriously hard to understand and audit due to the nature of the the encoded data commonly found in these tables. Furthermore, the raw data tables have a very large number of rows and hence can be slow to query. Most of the time you are better off working with [decoded data](../../decoded/solana/idl-tables.md).

## Data Available

<div class="grid cards" markdown>
-   **Account Activity**
    ---
    This table contains information from the transactions table focused on account usage.
    [:octicons-arrow-right-24: Account Activity](account-activity.md)
-   **Blocks**
    ---
    Blocks are the base unit that all transactions fit into.
    [:octicons-arrow-right-24: Blocks](blocks.md)
-   **Rewards**
    ---
    This table contains data about rewards paid out on Solana.
    [:octicons-arrow-right-24: Rewards](rewards.md)
-   **Transactions**
    ---
    Transactions are cryptographically signed instructions from accounts.
    [:octicons-arrow-right-24: Transactions](transactions.md)
-   **Instruction Calls**
    ---
    Transactions are unnested here such that each instruction gets its own row.
    [:octicons-arrow-right-24: Instruction Calls](instruction-calls.md)
-   **Vote Transactions**
    ---
    This table contains the full set of vote transactions that are submitted by validators to vote on a block.
    [:octicons-arrow-right-24: Vote Transactions](vote-transactions.md)
</div>

