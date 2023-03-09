---
title: Web3 Analytics Guidelines
description: End to End tutorials on how to analyze specfic protocols
---

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

To understand wallet/user segments, you'll need to leverage [labels](data%20tables/spellbook/top%20tables/labels.md) to enhance your analysis.

Once you have metrics and also understand the underlying tokens and users, it will start to become clear what that real narrative is. Try and pull together a few insights, and then create a really compelling dashboard and story around them. Don't try too hard to capture everything at once - it will become overwhelming for both you those you share it with. 

### Share your work with the Community

When you're done, be sure to share your work [in the Discord](https://discord.com/invite/ErrzwBz) `#📺︱show-your-work` channel and on Twitter tagging [@duneanalytics](https://twitter.com/DuneAnalytics). We'll be sure to give great analysts a boost! Web3 is all about connecting with communities - your queries and dashboards will do nothing if you don't share it around.

### More Community Guides

Don't forget to start with the Dune official guides [here](https://dune.com/docs/#learning-sql-and-blockchain-basics)

!!! suggestion
    If you've created a guide and want to feature it here, be sure to dm us on Twitter at @duneanalytics!


=== "Spark SQL"
    
    **[0xPhilan](https://dune.com/phillan) [:material-twitter:](https://twitter.com/0xPhillan)**

    * [Dune Analytics: A Guide for Complete Beginners](https://mirror.xyz/phillan.eth/17VAXsMPpwJg4OQNBHKTYAQTWfJMwFuXZQDAxPStf0o)

    **[James Bachini](https://dune.com/jamesbachini) [:material-twitter:](https://twitter.com/james_bachini)**

    * [Dune Analytics Tutorial | How To Create A Dune Analytics Dashboard](https://jamesbachini.com/dune-analytics-tutorial/)

    **[Kirubakumaresh](https://twitter.com/kirubakumaresh)**

    * [Build Ethereum Metrics Dashboard](https://www.twigblock.com/projects/eth-intro-dune/t/eit-overview)

    **[Jamesin Seidel](https://twitter.com/seidtweets)**

    * [Blockchain Analytics 101 — Dune Queries for On-Chain NFT Analysis](https://medium.com/@jseid212/blockchian-analytics-101-queries-for-on-chain-nft-analysis-fe08cbfa9ec2)

    **[@1chioku](https://dune.com/1chioku)**

    * [Journey to the Centre of Arakis](https://1chioku.substack.com/p/preface)

    **[cryptofreedman](https://dune.com/cryptofreedman) [:material-twitter:](https://twitter.com/cryptofreedman)**

    * [How to Learn SQL and Create a Dune Dashboard in 3 Hours](https://cryptofreedman.substack.com/p/how-to-learn-sql-and-create-a-dune)
    * [Beginners Guide to Blockchain Data on Dune](https://cryptofreedman.substack.com/p/beginners-guide-to-blockchain-data)

=== "PostgreSQL"

    **[Andrew Hong](https://dune.com/ilemi) [:material-twitter:](https://twitter.com/andrewhong5297) [:material-youtube:](https://www.youtube.com/channel/UCYG9WSr8G4khYLaxP9tLCkQ)**

    * [Your guide to basic SQL while learning Ethereum at the same time](https://towardsdatascience.com/your-guide-to-basic-sql-while-learning-ethereum-at-the-same-time-9eac17a05929) (Part 1)
    * [Your guide to intermediate SQL while learning Ethereum at the same time](https://towardsdatascience.com/your-guide-to-intermediate-sql-while-learning-ethereum-at-the-same-time-7b25119ef1e2?source=user\_profile---------6----------------------------) (Part 2)
    * [Learning SQL and Ethereum](https://towardsdatascience.com/learning-sql-and-ethereum-part-3-5422f080ad36) (Part 3)
    * [SQL on Ethereum: How to Work With All the Data from a Transaction](https://ath.mirror.xyz/mbR1n\_CvflL1KIKCTG42bnM4HpfGBqDPNndH8mu2eJw)

    **[Alex Manuskin](https://dune.com/ksunama) [:material-twitter:](https://twitter.com/amanusk\_)**

    * [How to get started with querying on Dune Analytics](https://dune.com/blog/get-started-guide)

    **[Paul Pivat](https://dune.com/paulapivat) [:material-twitter:](https://twitter.com/paulapivat)**

    * [Learn foundational Ethereum topics with SQL](https://ethereum.org/en/developers/tutorials/learn-foundational-ethereum-topics-with-sql)

    **[Alex Kroeger](https://dune.com/kroeger0x) [:material-twitter:](https://twitter.com/alex\_kroeger)**

    * [How to use Dune Analytics like a degen](https://mirror.xyz/0x7B542178633f16940a131F8F6d670ffdbBe6b2Ab/0C3EQBtFqAK4k2TAGPZhg0JMY-upfTAxuTD-o91vBPc)

    **[Chuxin](https://dune.com/chuxin) [:material-twitter:](https://twitter.com/chuxin\_h)**

    * [Select \* from web3](https://www.chuxinhuang.com/blog/select-from-web3)

    **Gracelily [:material-twitter:](https://twitter.com/\_grace\_lily)**

    * [PostgreSQL Query Optimization Tricks - How to Make Queries Faster in Dune Analytics](https://gracelily.medium.com/postgresql-query-optimization-tricks-6d5b7358d7fa)

    **Twigblock**

    * [Build an Ethereum Metrics Dashboard](https://www.twigblock.com/projects/eth-intro-dune/t/eit-overview)
    * [Learn to Analyze Ethereum Gas Prices](https://www.twigblock.com/projects/eth-gas-analysis/t/eg-overview)



## OurNetwork Course

!!! note
    This course is based on Dune's V1 engine. Much of the content is still applicable, but the SQL dialect and some table names have changed in Dune V2.

In collaboration with the Dune Team and Community, our friends at OurNetwork created a course with an ambitious goal: teach 30 people web3 data analytics in 30 days.

Hosted by some of our community's top Wizards, you can now access the presentations for free!

As it covers all of the important topics you'll need to know to effectively analyze blockchain data and become a full-fledged Dune Wizard, it's one of the best places to start your Dune Journey.

More details and all of the course materials can be found here:

<div class="cards grid" markdown>
- [OurNetwork Course](https://ournetwork.mirror.xyz/gP16wLY-9BA1E_ZuOSv1EUAgYGfK9mELNza8cfgMWPQ)
</div>

Please consider buying an edition of the Mirror post to support the teachers of this course.

Videos are also available on YouTube:

![type:video](https://www.youtube.com/embed/yDSmTUrpdoQ)
