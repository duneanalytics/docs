---
title: Web3 Data & Analytics Learning Resources
description: Navigate the Ever-Expanding World of Web3 Data with Ease, from Beginners to Experts
---

After you've gone through the [quickstart guide](../quickstart.md), you'll be ready to really start learning how to navigate the Web3 data analytics space.

Analyzing protocols in web3 is both really easy and really hard. It's really easy because everything is transparent and standardized - a deployed contract has a set of functions and events that are pretty much immutable. However, it's an ever expanding data arena as new protocols, tokens, and wallets join the fray. 

To build your reputation as an expert wizard, you must stay centered on what you want to analyze and what metrics you want to present.

## Dune Tutorials

### Dune 101
Speed up your learning curve and become a Dune creator. Dive into our [how-to tutorials](./how-tos/index.md).

### How-To Guides
Eager for focused insights? Explore our curated guides:

- [How to create Sankey diagram with Dune's data](create-sankey-diagram.md) 
- [How to conduct social network analysis for Farcaster with Dune API and Python](conduct-network-analysis.md)

### Metrics-Driven Analysis

- Video Series: Delve deep with our end-to-end video series guides:

    - [Uniswap in 12 Days](https://www.youtube.com/watch?v=FtnGiI9MGgA&list=PLK3b5d4iK10cIrN8c_au9RrC0_eBCOyR2&index=1&t=149s) (includes metrics like price impact, TVL, MEV volume, liquidity stability)
    - [Gnosis Safe Point-in-Time](https://www.youtube.com/watch?v=8atzYkpez5I) (includes metrics like signers, diversification, valuations)

- Dashboards for Insights:
    
    - To understand token trends and contexts, check out this [ERC20 dashboard](https://dune.com/ilemi/Token-Overview-Metrics) and this [NFT dashboard](https://dune.com/rantum/NFT-Collection-Dashboard). 

    - To understand wallet/user segments, you'll need to leverage [labels](../data-tables/spellbook/top-tables/labels.md) to enhance your analysis.

Once you have metrics and also understand the underlying tokens and users, it will start to become clear what that real narrative is. Try and pull together a few insights, and then create a really compelling dashboard and story around them. Don't try too hard to capture everything at once - it will become overwhelming for both you those you share it with. 


## Analysis Tips
- Start with a solid foundation. Master [basic SQL and blockchain concepts](https://web3datadegens.substack.com/p/a-basic-wizard-guide-to-dune-sql).

- Scope Your Work:
When looking into a protocol, you'll need to understand the contract architecture and context. That starts with functions, events, and wallets overviews. There is a [quickstart dashboard](https://dune.com/ilemi/contract-quickstart) built just for this, you can see a walkthrough analyzing Opensea [here](https://web3datadegens.substack.com/p/how-to-start-analyzing-any-web3-protocol). 

Remember that no protocol lives in isolation - there is always some mix of onchain events happening. That could be some new airdrop, a new upstream/downstream protocol integration, large whales making moves, governance changes in protocol parameters, and more. Once you have a solid understanding of protocol history in usage, user, and integration trends, you're ready to start building some metrics.

## Engage with the Community

When you're done, be sure to share your work [in the Discord](https://discord.com/invite/ErrzwBz) `#📺︱show-your-work` channel and on Twitter tagging [@duneanalytics](https://twitter.com/DuneAnalytics). We'll be sure to give great analysts a boost! Web3 is all about connecting with communities - your queries and dashboards will do nothing if you don't share it around.

## Special Course: OurNetwork

!!! note
    This course is based on Dune's V1 engine. The domain logic still applies, but the SQL syntax has now switched from [postgreSQL to Dune SQL](../query/syntax-differences.md).

In collaboration with the Dune Team and Community, our friends at OurNetwork created a course with an ambitious goal: teach 30 people web3 data analytics in 30 days.

Hosted by some of our community's top Wizards, you can now access the presentations for free! More details and all of the course materials can be found here:

<div class="cards grid" markdown>
- [OurNetwork Course](https://ournetwork.mirror.xyz/gP16wLY-9BA1E_ZuOSv1EUAgYGfK9mELNza8cfgMWPQ)
</div>

Videos are also available on YouTube:

![type:video](https://www.youtube.com/embed/yDSmTUrpdoQ)
