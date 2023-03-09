---
title: Dune Quickstart
description: Get started on Dune in five minutes!
---

### Why Learn to Use Dune?

You're probably here because you've realized that:

1. While blockchain data is open and transparent, **it isn't easy to understand, ingest, and aggregate.** Each chain has different nuances, decoding contract functions and events is not as straightforward as it seems.

2. Either your own protocol or someone else's protocol was not built with a data engineer/analyst in mind. **You've reached the limits of how you can keep up with just contract read functions and most recent events.**

3. You want to do heavy cross context analysis, combining tokens, wallets, and protocols across chains. This requires an end-to-end data warehouse that can scale on demand - and a full team to maintain it. **That's hundreds of terabytes of data to store, and exponential amounts of compute ($$$$).**

4. You're an analyst that wants to **showcase your work to tens of thousands of users**, and earn stars to climb the Wizard Leaderboard to find freelance or full-time roles.

You're in luck! Dune and the community of thousands of wizards are here to bring you powerful analysis of all onchain data. If you just go and search for anything Web3 related, I'm sure **you'll find [at least one dashboard on that topic](https://dune.com/browse/dashboards?q=dex&order=favorites&time_range=all)**. This goes for every chain we have, including EVMs like **Ethereum, Polygon, Goerli, and Optimism** and non-EVM chains like **Solana and Bitcoin.**

You can quickly explore [NFT marketplaces](https://dune.com/hildobby/NFTs), [DEX metrics](https://dune.com/hagaetc/dex-metrics), [Bridges](https://dune.com/eliasimos/Bridge-Away-(from-Ethereum)), [DAO Accounting (Maker)](https://dune.com/SebVentures/maker---accounting_1), [Base Chain Metrics](https://dune.com/optimismfnd/Optimism), and much more!

Enough chatting, let's show you some magic. ✨

### Analyze Web3 Data: DEX Volumes

In this short section, we'll walk you through how to get the weekly USD volume traded by DEXs in the last six months on Ethereum. Click through the interactive walkthrough below to understand how we use the `dex.trades` table to:

- Find and preview data for tables we're interested in

- Write and run a basic query on the Dune SQL engine

- Create and format a stacked bar chart visualization

<div style="position: relative; padding-bottom: calc(67.14527027027027% + 41px); height: 0;"><iframe src="https://demo.arcade.software/gNuUxSbr6NZi4aXBURWu?embed" frameborder="0" loading="lazy" webkitallowfullscreen mozallowfullscreen allowfullscreen style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;color-scheme: light;" title="Dashboards"></iframe></div>

Now, `dex.trades` is a spellbook table, meaning that it's an abstracted table that's been put together by hundreds of star analysts in the community, supported by the Dune team. You can find any spellbook table's column descriptions [defined here](https://spellbook-docs.dune.com/#!/model/model.spellbook.dex_trades). The lower level tables you'll often work with are `raw` and `decoded` tables. Raw tables are defined [here](data%20tables/raw/index.md), but for decoded tables you'll need to find the protocol's documentation such as [this one for Uniswap V3](https:/.uniswap.org/contracts/v3/reference/core/UniswapV3Factory). You'll find out how to work with these in the guides mentioned in the [advanced section](analytics_guidelines.md).

Once we have this query running, anyone can leverage it in future queries by tracking the query id (link to our query-a-query guide later).

### Learning SQL and Blockchain Basics

The query above might be confusing to you if you aren't familiar with SQL or Blockchain basics. Here are a few beginner resources and guides ~~to~~ get you started:

- [Dune Official Getting Started Video Series](https://www.youtube.com/watch?v=S-cctFmR828&list=PLK3b5d4iK10ext4v-GBySekaA8-GP8quD&index=1) to learn how the data flows and how to navigate the Dune app to create queries, visualizations, and dashboards. 

- [Weekly Web3 SQL problems](https://daodatadesign.notion.site/Web3-SQL-Weekly-0bababb5e59a412bb73594c512db8cc1) to learn wizard tips and tricks in byte-sized bits. Covers things like token balances, protocol integrations, product metrics, and much more.

- [All Ethereum and SQL Basics](https://web3datadegens.substack.com/p/a-basic-wizard-guide-to-dune-sql) to learn all the basic SQL concepts and Ethereum tables you'll need in your analysis.

Join the community and learn together [in Discord](https://discord.com/invite/ErrzwBz) by participating in the `#🐥︱beginners` and `#🙋︱query-questions` channels

And when you feel ready to do advanced analysis, check out the [next guide](analytics_guidelines.md)

You should also read about Dune SQL specific concepts like custom types and functions, and different kinds of tables in our database.

### Still stuck, or want to hire someone else to help?

There are quite a few people in the crypto industry who either specialize in building on Dune or have the necessary skills to quickly get up to speed on the particulars.

To reach out to this pool of expert freelancers, you can [fill out this questionnaire](http://bounties.dune.com) and wait for freelancers to get back to you in little to no time. If that yields no results, posting the bounty on relevant social channels and spreading it in your networks may help.