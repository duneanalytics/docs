---
title: Dune Quickstart
description: Get started on Dune in five minutes!
---

### Why learn to use Dune?

get hired, don't deal with raw data, learn from hundreds of other analysts, don't build an infra pipeline

- call out key use cases here, aligned with product marketing materials
- mention if they want API then go to API quickstart instead
- call out what values/time Dune is saving for you quickly

### Analyze Web3 Data: DEX Volumes

In this short guide, we'll walk you through how to get the weekly USD volume traded by DEXs in the last six months on Ethereum. You'll learn how to write a basic SQL query and create a visualization in Dune. 

Click through the interactive walkthrough below to understand how to leverage the `dex.trades` table for this basic analysis.

<div style="position: relative; padding-bottom: calc(67.14527027027027% + 41px); height: 0;"><iframe src="https://demo.arcade.software/gNuUxSbr6NZi4aXBURWu?embed" frameborder="0" loading="lazy" webkitallowfullscreen mozallowfullscreen allowfullscreen style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;color-scheme: light;" title="Dashboards"></iframe></div>

Once we have this query, you can leverage it in future queries by tracking the query id (see the URL).

...insert Query-a-Query recording...

Now, `dex.trades` is a spellbook table, meaning that it's an abstracted table that's been put together by hundreds of star analysts in the community, supported by the Dune team. You can find spellbook table columns [defined here](https://spellbook-docs.dune.com/#!/model/model.spellbook.dex_trades). The lower level tables you'll often work with are `raw` and `decoded` tables. You'll find out how to work with these in the guides mentioned in the [advanced section](five_minutes.md).

### Learning SQL and Blockchain Basics

The query above might be confusing to you if you aren't familiar with SQL or Blockchain basics. Here are a few beginner resources to get you started:

- [Dune Official Getting Started Video Series](../app/guides/video-tutorial.md) to learn how the data flows and how to navigate the Dune app to create queries, visualizations, and dashboards. 

- [Weekly Web3 SQL problems](https://daodatadesign.notion.site/Web3-SQL-Weekly-0bababb5e59a412bb73594c512db8cc1) to learn wizard tips and tricks in byte-sized bits. Covers things like token balances, protocol integrations, product metrics, and much more.

- [All Ethereum and SQL Basics](https://web3datadegens.substack.com/p/a-basic-wizard-guide-to-dune-sql) to learn all the basic SQL concepts and Ethereum tables you'll need in your analysis.

Join the community and learn together [in Discord](https://discord.com/invite/ErrzwBz) by participating in the `#🐥︱beginners` and `#🙋︱query-questions` channels

And when you feel ready to do advanced analysis, check out the [next guide](../docs/five_minutes.md)

You should also read about Dune SQL specific concepts like custom types and functions, and different kinds of tables in our database.

### Still stuck, or want to hire someone else to help?

There are quite a few people in the crypto industry who either specialize in building on Dune or have the necessary skills to quickly get up to speed on the particulars.

To reach out to this pool of freelancers, you can [fill out this questionnaire](http://bounties.dune.com) and hopefully freelancers will get back to you in little to no time. If that yields no results, posting the bounty on relevant social channels and spreading it in your networks may help.
