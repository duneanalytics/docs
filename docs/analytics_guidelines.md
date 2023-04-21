---
title: Web3 Analytics Resources
description: End to End tutorials on how to analyze specific protocols
---

*This section will contain links to many community contributed guides and dashboards.*

Analyzing protocols in web3 is both really easy and really hard. It's really easy because everything is transparent and standardized - a deployed contract has a set of functions and events that are pretty much immutable. However, it's an ever expanding data battlefield as new protocols, tokens, and wallets join the fray and add to the chaos. 

To build your reputation as an expert wizard, you must stay centered on what you want to analyze and what metrics you want to present.

### Finding What To Analyze

Once you've learned [basic SQL and blockchain concepts](https://web3datadegens.substack.com/p/a-basic-wizard-guide-to-dune-sql), you're ready to start doing your own end-to-end analysis. It's easy to get lost in an ever-expanding web of tables and analysis - so here are some top tips on scoping your work. 

When looking into a protocol, you'll need to understand the contract architecture and context. That starts with functions, events, and wallets overviews. There is a [quickstart dashboard](https://dune.com/duniversity/contract-quickstart) built just for this, you can see a walkthrough analyzing Opensea [here](https://web3datadegens.substack.com/p/how-to-start-analyzing-any-web3-protocol). 

Remember that no protocol lives in isolation - there is always some mix of onchain events happening. That could be some new airdrop, a new upstream/downstream protocol integration, large whales making moves, governance changes in protocol parameters, and more. Once you have a solid understanding of protocol history in usage, user, and integration trends, you're ready to start building some metrics.

### Metrics Driven Analysis

There are two great end-to-end video series guides for metrics analysis we've created:

- [Uniswap in 12 Days](https://www.youtube.com/watch?v=FtnGiI9MGgA&list=PLK3b5d4iK10cIrN8c_au9RrC0_eBCOyR2&index=1&t=149s) (includes metrics like price impact, TVL, MEV volume, liquidity stability)

- [Gnosis Safe Point-in-Time](https://www.youtube.com/watch?v=8atzYkpez5I) (includes metrics like signers, diversification, valuations)

Protocol metrics are usually dependent on different token and wallet segments. For example, Uniswap allows you to create pairs of two tokens at a time to add liquidity and swap through. However, the USDC-WETH pair will have a very different behaviors from SHIB-WETH. 

To understand token trends and contexts, check out this [ERC20 dashboard](https://dune.com/ilemi/Token-Overview-Metrics) and this [NFT dashboard](https://dune.com/rantum/NFT-Collection-Dashboard). 

To understand wallet/user segments, you'll need to leverage [labels](data-tables/spellbook/top-tables/labels.md) to enhance your analysis.

Once you have metrics and also understand the underlying tokens and users, it will start to become clear what that real narrative is. Try and pull together a few insights, and then create a really compelling dashboard and story around them. Don't try too hard to capture everything at once - it will become overwhelming for both you those you share it with. 

### Share your work with the Community

When you're done, be sure to share your work [in the Discord](https://discord.com/invite/ErrzwBz) `#📺︱show-your-work` channel and on Twitter tagging [@duneanalytics](https://twitter.com/DuneAnalytics). We'll be sure to give great analysts a boost! Web3 is all about connecting with communities - your queries and dashboards will do nothing if you don't share it around.

## OurNetwork Course

!!! note
    This course is based on Dune's V1 engine. The domain logic still applies, but the SQL syntax has now switched from [postgreSQL to Dune SQL](query/syntax-differences.md).

In collaboration with the Dune Team and Community, our friends at OurNetwork created a course with an ambitious goal: teach 30 people web3 data analytics in 30 days.

Hosted by some of our community's top Wizards, you can now access the presentations for free! More details and all of the course materials can be found here:

<div class="cards grid" markdown>
- [OurNetwork Course](https://ournetwork.mirror.xyz/gP16wLY-9BA1E_ZuOSv1EUAgYGfK9mELNza8cfgMWPQ)
</div>

Videos are also available on YouTube:

![type:video](https://www.youtube.com/embed/yDSmTUrpdoQ)
