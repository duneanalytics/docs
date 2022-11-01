---
title: Query Quick Start
description: Here's a short five-step guide to getting familiar with a protocol and figuring out how to query around it using Dune.
---

Here's a short five-step guide to getting familiar with a protocol and figuring out how to query around it using Dune.

Thanks to [@ilemi](https://dune.com/ilemi) for putting this together!

[Learn more about how Queries work here](../queries/index.md).

## 1. Find the main point of entry

Using the [Dune Data Explorer](../queries/data-explorer.md) and the protocol app page/docs and try to figure out what the main user entry point function is.

Sometimes this is straightforward, but different contract patterns on more complex protocols will make this confusing. 

For most of decentralized finance (DeFi), the primary entry point for users is just some variation of `Deposit`.

If the contract isn't [Decoded](../decoding-contracts.md) yet, you can start with some raw queries for finding the most common function and event signatures here: [Dune Utility Queries](../../reference/wizard-tools/utility-queries.md)
    
If you're having trouble figuring out the tables, [see our Table docs here](../../reference/tables).    
    
## 2. Explore the contract flow

Typically a function call is not as simple as an ETH/token transfer that only involves one contract.

Once you figure out the entry point, run a basic LIMIT query on it and look at some example transactions in [the relevant blockchain explorer](../../reference/wizard-tools/blockchain-explorers.md) for data hints (i.e. what protocols did the tx interact with besides the main one).
    
```sql
SELECT * FROM protocol_name."Contractname_evt_EventEmitted"
LIMIT 10
```
   
Look at `evt_tx_hash` and plop it into the blockchain explorer to start getting a sense of what contracts and interactions are involved.
  
## 3. Decide what question you want to answer

If you already have a question in mind, then skip this step. If you don't have a question yet, think through the flow chart of contract interactions.

Here are some starter questions to help you find something interesting to look into: 

1. What other protocols did the entry function touch?
2. If there is yield/interest being generated, where and when did the tokens get swapped? 
3. How many tokens went in and how many were burned/minted by the end? 
4. Is it possible that anything from the last three questions would lead to some sort of imbalance or accumulation? i.e. a DEX pool ending in low liquidity, or depositing so much into one pool that the yield/interest rate falls from supply imbalance. Or if this involves NFTs, what were the effects on future bid/sale behavior (or were there behaviors in bid/sale that led up to this transaction)?

## 4. Build your Query

Now that you have settled on a question, the real fun begins. 🧙

You'll quickly notice that the function call data and event log data don't always have all the parameters you're looking for.

The usual culprits that are missing are the transaction signer (found in `ethereum."transactions"` ) and the ETH value transferred (found in `ethereum."traces"`).

Typically you'll have to work with the base tables (transactions, traces, logs) and possibly tables from other protocols (like DEX/exchange protocols) to complete the data you need for your query.

Figuring out which tables to pull what data from takes a while to learn, and the best way to get started is usually to search for existing dashboards or queries that have attempted something similar.

Dune has been around long enough that most query patterns aren't too hard to find somewhere else. ✨

## 5. Make your Visualization

Lastly, you should visualize the query in a chart by clicking "New visualization" next to "Query Results".  
    
    ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/8dbf893c-33f5-47cb-8d4f-41ff4b2df8d6/Untitled.png)
    
If you're showing token amounts, you likely have to [fix for decimals](https://dune.xyz/queries/85746) or multiply by token price (in `prices.usd` or `dex.trades`) to get to a USD value which is more interpretable.