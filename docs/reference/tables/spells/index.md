---
title: Spells
description: With the help of the community we construct customs tables which cover the entirety of a type of activity on the blockchain called Spells.
---

**Spells are custom tables that are built and maintained by Dune and our community.**

!!! note
       Spellbook Spells are available on Dune V2, queryable from both Spark SQL and Dune SQL [V2 Query Engines](../../dune-v2/query-engine.md). For now, Spells will continue to be written in Spark SQL and querying them with Dune SQL will require small syntax changes. While the changes needed to make Spells Dune SQL native are small, we want to make sure Dune SQL is rock solid before we implement them! [Learn more about casting a Spell here](../../../spellbook/index.md).

To learn more about what Spells are see [Spellbook](../../../spellbook/index.md).

To see a complete list of Spellbook Spell tables, visit the [Spellbook Model Docs](../../../spellbook/spellbook-model-docs.md).

You can generally divide them into 2 distinct categories:

## Sector Spells

Sector Spells are tables like dex.trades, erc20.stablecoins, lending.borrow etc.

These Spells take in data from multiple contracts and projects, standardize the data across them and therefore make it very easy to query for this data and compare the metrics of different projects with each other.

Most of the [sector Dashboards](../../../getting-started/use-cases/sector-dashboards.md) dashboards depend on sector spells. This introduces an interesting dynamic in which projects can easily get their data into these dashboards by making a pull request to our public [github repo](https://github.com/duneanalytics/spellbook/index.md).

Team Dune and the community are always improving on these sector spells, all new additions to existing ones are always welcome.

## Project Spells

Projects can assemble their data into one neat table that has all the data they need in one place. To do this, you can construct views or tables in our spells.

The main advantage here over just constructing a view is that you are able to deal with bigger amounts of data in our Spells since we can run them automatically in the background every few hours.

## Contributing to Spellbook

If you'd like to contribute to Dune spells, take a look at [Spellbook](../../../spellbook/index.md).

These enable you to effortlessly aggregate lots of data with as little friction as possible.

To view available Spells, take a look at our [Spellbook model documentation](https://dune.com/spellbook) and learn how to contribute new Spells [here](../../../spellbook/index.md)

Our Spells are managed via the public [Spellbook GitHub repository](https://github.com/duneanalytics/spellbook/index.md). We welcome pull requests!

## Abstractions (Dune V1 PostgreSQL)

For our **V1 Engine** (PostgreSQL), abstractions are snippets of SQL executed the data platform. You can check for existing abstractions on [GitHub](https://github.com/duneanalytics/dune-v1-abstractions).

You can check for existing abstractions in our [public github repository](https://github.com/duneanalytics/spellbook/index.md), under `deprecated-dune-v1-abstractions`.

Our abstractions for v1 are no longer open for contributions.

