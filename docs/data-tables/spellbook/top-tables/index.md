---
title: Top Spellbook Tables
description: Some top spells to get you started
---

This section contains some of the most useful spells (abstracted tables) on Dune. You'll likely use these in many of your queries, from beginner to advanced.

<div class="cards grid" markdown>
- [dex.trades](dex.trades.md): The standardization and aggregation of all Decentralized Exchanges (DEX) across EVM chains.
- [nft.trades](nft.trades.md): The standardization and aggregation of all NFT marketplaces across chains (EVM + Solana)
- [labels](labels.md): Labels contain identifiers such as CEX wallets, ENS names, Top 1% NFT Traders, and many more for each address.
- [tokens](tokens.md): The tokens and transfers tables will be essential to calculating decimals, finding symbols, and tracking balances for ERC20s and NFTs
- [prices](prices.md): The `prices_usd` tables will help you assign values to volume, TVL, and many more token metrics.
</div>

## Spell Categories

In general, there are two types of spell categories. 
### Sector Spells

Sector Spells are tables like dex.trades, erc20.stablecoins, lending.borrow, tokens.erc20, etc.

These Spells take in data from multiple contracts and projects, standardize the data across them and therefore make it very easy to query for this data and compare the metrics of different projects with each other.

Most of the [sector Dashboards](../../app/dashboards/sector-dashboards.md) dashboards depend on sector spells. This introduces an interesting dynamic in which projects can easily get their data into these dashboards by making a pull request to our public [github repo](https://github.com/duneanalytics/spellbook/index.md).

Team Dune and the community are always improving on these sector spells, all new additions to existing ones are always welcome.

### Project Spells

Projects (Opensea, Uniswap, Aave, etc) can assemble their data into one neat table that has all the data they need in one place. To do this, you can construct views or tables in our spells.

The main advantage here over just constructing a view is that you are able to deal with bigger amounts of data in our Spells since we can run them automatically in the background every few hours.