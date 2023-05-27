---
title: Spellbook Tables
description: With the help of the community we construct customs tables which cover the entirety of a type of activity on the blockchain called Spells.
---

**Spellbook Tables are the easiest way to query blockchain data on Dune**

<div class="cards grid" markdown>

-   #### Github Repo

    The Spellbook GitHub repository can be found here.
  
    [:octicons-arrow-right-24: Spellbook Github Repo](https://github.com/duneanalytics/spellbook)

-   #### Model Docs

    Visit the Spellbook Model Docs to see a complete list of Spellbook Spell tables.
  
    [:octicons-arrow-right-24: Spellbook Model Docs](https://dune.com/spellbook)

</div>

## Abstraction and Aggregation Tables for Blockchain Data

Spellbook is an open-source [dbt repository](https://docs.getdbt.com/docs/introduction) for creating and maintaining high-level blockchain data tables using SQL and [Jinja templating](https://realpython.com/primer-on-jinja-templating/).

**Spells are custom tables that are built and maintained by Dune and our community.**

It enables the community to build toward a standardized way to transform data into meaningful abstraction layers. With web3 data, we have a foundational layer of [Raw Data](../raw/index.md) - blockchain transactions, traces, and logs. Spellbook lets us create abstracted data sets, like [dex.trades](https://dune.com/spellbook#!/model/model.spellbook.dex_trades) and [nft.trades](https://dune.com/spellbook#!/model/model.spellbook.nft_trades), which aggregate and organize raw data from multiple sources to make it much easier to query.

dbt natively understands the dependencies between all models. In our old abstractions logic we were managing dependencies manually, which made deploying and maintaining them a mess. With dependency management, we can guarantee that all models are deployed in the correct order.

![Dependency graph created by dbt showing erc20 daily balances dependency tree](images/dbt-erc20-dependency-graph.jpg)

We hope you are as excited as we are about this tool. You can add a view, seed file (excel/csv), or materialized table (incremental or not) by [contributing to spellbook](contributing/index.md).

## Contributing to Spellbook

If you'd like to contribute to Dune spells, take a look at [Spellbook](contributing/index.md).

These enable you to effortlessly aggregate lots of data with as little friction as possible.

To view available Spells, take a look at our [Spellbook model documentation](https://dune.com/spellbook) and learn how to contribute new Spells [here](contributing/index.md)

Our Spells are managed via the public [Spellbook GitHub repository](https://github.com/duneanalytics/spellbook/). We welcome pull requests!

!!! note "Spellbook Model Creation Runs on Spark SQL"
       Spellbook Spells are available on Dune V2, queryable from both Spark SQL and Dune SQL [V2 Query Engines](/query/index.md). For now, Spells will continue to be written in Spark SQL and querying them with Dune SQL will require small syntax changes. While the changes needed to make Spells Dune SQL native are small, we want to make sure Dune SQL is rock solid before we implement them!

## Why Spellbook?

To better understand why we use Spellbook, let’s see it in action.

Once upon a time, crypto Twitter was alight with talk of a new NFT project called Renga.

What’s the project about? Is it something worth buying as an investment?

If we want to do some on-chain analysis, we could start by going to OpenSea and finding the Renga collection ([here](https://opensea.io/collection/renga)).

![renga collection opensea](../spellbook/contributing/images/RENGA-Collection-OpenSea.png)

[By viewing an item from this collection](https://opensea.io/assets/ethereum/0x394e3d3044fc89fcdd966d3cb35ac0b32b0cda91/6294), we can get the collection’s contract address as well as the unique ID from its OpenSea URL.

![get renga contract address from url](../spellbook/contributing/images/get-renga-contract-address-from-url.png)

We can also scroll down and click on a transaction to [view it on the blockchain explorer](https://etherscan.io/tx/0x96f158d75379057d95c1c562b9908603e543feee25a71ac420e21ecf0a0c643c) and get more data like:

* The transaction block and hash
* The To/From addresses for the transfer
* How much ETH was transferred

At a base level, blockchain data is packaged in blocks, which is one form of data we call “Raw” in Dune.

So from our research, we could build a Query that pulls the data from the block in which this transaction happened.

```sql

SELECT *

FROM ethereum.blocks

WHERE number = 15661624 --the block number we found in etherscan

```

That returns:

![type:video](https://dune.com/embeds/1645898/2727844/09c37981-3b21-4bfd-85da-c029755af873)

A lot is going on in this block so this isn’t very targeted. Also, the data here isn’t very understandable.

We could also search for this specific transaction to get closer to our target:

```sql

SELECT *

FROM ethereum.transactions

--the transaction hash we found in etherscan

WHERE where block_number = 15661624 AND hash = '0x96f158d75379057d95c1c562b9908603e543feee25a71ac420e21ecf0a0c643c'

```

Which gets us:

![type:video](https://dune.com/embeds/1645938/2727926/8a442735-79c7-4903-a525-303c8163d7fd)

Some more interesting info here like `gas_price` and `gas_used` but the juicy stuff is in the `data` column - but to understand that we’d need to reference the contract’s [Application Binary Interface](https://www.quicknode.com/guides/smart-contract-development/what-is-an-abi) ABI.

Thankfully, Dune has [Decoded Data](../decoded/index.md), which contains contract data that’s been automatically decoded from the transaction’s raw data using the ABI - the machines save us time.

With Decoded Data, we can make a Query like this:

```sql

SELECT *

    , concat('0x',substr(get_json_object(offer[0], "$.token"),3,40)) as token_contract_address

    , get_json_object(consideration[0], "$.identifier") as token_id

FROM seaport_ethereum.Seaport_evt_OrderFulfilled

WHERE evt_tx_hash = lower("0x96f158d75379057d95c1c562b9908603e543feee25a71ac420e21ecf0a0c643c") --sample tx

```

Which would return data like this:

![type:video](https://dune.com/embeds/1345665/2296143/757ed708-17da-4c81-9633-ac19a9d3f3d3)

What’s happening here:

* We dug through Dune to find the `seaport_ethereum` contract set and the `Seaport_evt_OrderFulfilled` table which contains the data for our specific transaction. (which takes a lot of time in and of itself).
* To get closer to something we really want, token contract address and token ID, we had to:
    * Know to look for the offer column and get the first position in that array
    * Make it a JSON object, knowing token contracts are 20 bytes which means 40 characters.
    * And do a similar amount of manual abstraction for the token ID

Yet now we still don’t have something interesting like how much money was this NFT sold for.

If we want to get there, someone has to do this abstraction work.

But what if, once that work was done the first time, the rest of the community could skip all that noise to get straight to the juicy insights?

With the [nft.trades](https://dune.com/spellbook#!/model/model.spellbook.nft_trades) Spell, we can do this:

```sql

SELECT

    seller

    , buyer

    , amount_original

    , currency_symbol

    , *

FROM nft.trades

WHERE tx_hash = lower("0x96f158d75379057d95c1c562b9908603e543feee25a71ac420e21ecf0a0c643c") --sample tx

```

Which returns this:

![type:video](https://dune.com/embeds/1345985/2296638/51cc251d-c1ec-4f71-a269-2b194b25bdac)

And right away, with a couple of lines of SQL we can see:

* The seller and buyer wallet addresses
* The amount that was paid in what cryptocurrency
* Which blockchain it was on

And more!

This illustrates how on a micro level, for one transaction, a ton of work was saved thanks to the Spell adding done by Wizards who came before us.

This of course also scales to the macro.

If we wanted to do a cross-chain NFT marketplace analysis, we might aim to build something like this dashboard:

<div class="cards grid" markdown>
- [Cross Chain NFT Marketplace Metrics by @agaperste](https://dune.com/agaperste/cross-chain-nft-marketplace-metrics)
</div>

With the nft.trades spell, we can see industry-wide stats like:

* Total volume by # of txs and $USD
* 24-hr volume
* 24-hour and 7-day growth
* Market share by marketplace
* Volume by marketplace
* Transaction count by marketplace

And we can query, visualize, and make a dashboard out of that data all in a couple of hours instead of dozens.

And once a new NFT marketplace is launched, anyone in the community who knows how to add a Spell can do the data engineering for that marketplace, submit a Pull Request to Spellbook, and have the entire community benefit from their work.

For the first time in history, we have access to an open dataset thanks to blockchains.

Thanks to Spellbook, we can all build on top of that open data to make it more transparent, accessible, and meaningful together!


