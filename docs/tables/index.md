---
title: Tables
---

**Dune enables you to query data on our supported chains at different levels of abstraction.**

To start with, you have access to the raw tables for each supported blockchain, with tables like `blocks` and `transactions`. This is the most flexible option.

To make it easier to work with smart contracts, Dune also provides decoded data as individual, human readable tables. We use the ABI for smart contracts and the interface standard for standardized token smart contracts (ERC20, ERC721 etc.). We've indexed over 280k contracts as of writing, and you can [submit new contracts](../features/adding-new-contracts.md).

On top of that, we're building a set of abstractions for common use cases (e.g. NFTs or DEX) and third party datasets.

Here is an overview what is available:

- [Raw data](raw.md): unedited, raw and encoded blockchain data
- [Decoded data](decoded.md): (**most popular**) view the decoded calls and events made to smart contracts
- [Abstractions, or Spells](abstractions.md): custom tables that are maintained by Dune and our community
- [Community](community.md): partnering with select organizations for off-chain data
- [Prices](prices.md): prices from third party data providers
- [User generated](user-generated.md): construct your own view, function or table inside of our database

The details of the data model depends on the blockchain and engine. We've compiled detailed references for tables on our [Dune V1 Engine](v1/raw/index.md) (PostgreSQL) and [Dune V2 Engine](v2/raw/index.md) (Databricks SQL).