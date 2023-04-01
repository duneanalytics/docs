[View code on GitHub](https://dune.com/docs/data-tables/spellbook/top tables/dex.trades.md)

# Dex.Trades App Technical Guide

The Dex.Trades app is a decentralized exchange aggregator that collects data from multiple DEX platforms into one simple table. This guide provides an overview of the app and its features.

## Overview

Decentralized exchanges are the backbone of the DeFi industry, allowing users to swap any native (ETH) or ERC-20 token for any ERC-20 token through smart contracts. However, with so many decentralized exchanges available, it can be challenging to work with the smart contract data for all of them. Dex.Trades solves this problem by standardizing and normalizing trading data across virtually all relevant decentralized exchanges.

## Column Data

The Dex.Trades table contains the following columns:

- `block_time`: The timestamp of the block that included this transaction.
- `token_a_symbol`: The symbol of one of the two tokens that got traded.
- `token_b_symbol`: The symbol of one of the two tokens that got traded.
- `token_a_amount`: The amount of token A that got traded.
- `token_b_amount`: The amount of token B that got traded.
- `project`: The DEX on which this trade was executed.
- `version`: Which version of the DEX got used?
- `blockchain`: Which blockchain did this occur on?
- `taker`: Which contract called the DEX contract?
- `maker`: In some special cases, there actually is a counterparty to transactions, and this party will get displayed here if applicable.
- `token_a_amount_raw`: The raw amount of token A that got traded.
- `token_b_amount_raw`: The raw amount of token B that got traded.
- `usd_amount`: The USD value of this trade.
- `token_a_address`: The ERC-20 token contract address of token A.
- `token_b_address`: The ERC-20 token contract address of token B.
- `exchange_contract_address`: The address of the decentralized exchange contract that made this trade possible.
- `tx_hash`: The hash of the transaction that contained this trade.
- `tx_from`: Which address initiated this transaction?
- `tx_to`: What was the first smart contract that got called during this tx?
- `trace_address`: Which position in the graph tree does the execution of the trade have?
- `evt_index`: This logs index position in the block (cumulative amount of logs ordered by execution).
- `trade_id`: Just for database magic.

## Conclusion

The Dex.Trades app is an essential tool for anyone looking to work with decentralized exchanges. By aggregating data across multiple DEX platforms into one simple table, Dex.Trades makes it easy to query for trading data for your favorite tokens without having to deal with all of the different DEX smart contracts yourself. The scripts that generate the table can be found in the public Github repo.
## Questions: 
 1. What is the purpose of dex.trades and how does it work?
- Answer: dex.trades is a table that standardizes and normalizes trading data across multiple decentralized exchanges, making it easier to query for trading data for different tokens without having to deal with different DEX smart contracts. It works by aggregating data from various DEX platforms into one simple table.

2. What specific data is included in the dex.trades table?
- Answer: The dex.trades table includes data such as the timestamp of the block that included the transaction, the symbols and amounts of the tokens traded, the DEX on which the trade was executed, the blockchain on which it occurred, the contract addresses involved, and the USD value of the trade.

3. Where can the scripts that generate the dex.trades table be found?
- Answer: The scripts that generate the dex.trades table can be found in the public github repo at https://github.com/duneanalytics/spellbook/tree/master/ethereum/dex.