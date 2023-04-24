---
title: Spells
description: With the help of the community we construct customs tables which cover the entirety of a type of activity on the blockchain called Spells.
---

**Spells are custom tables that are built and maintained by Dune and our community.**

!!! note
       Spellbook Spells are available on Dune V2, queryable from both Spark SQL and Dune SQL [V2 Query Engines](/query/index.md). For now, Spells will continue to be written in Spark SQL and querying them with Dune SQL will require small syntax changes. While the changes needed to make Spells Dune SQL native are small, we want to make sure Dune SQL is rock solid before we implement them!

**The spellbook github repo can be found at [Spellbook](https://github.com/duneanalytics/spellbook).**

**To see a complete list of Spellbook Spell tables, visit the [Spellbook Model Docs](https://spellbook-docs.dune.com/#!/overview).**
## New level unlocked

We’ve updated our database and now it’s time to update our contribution tools.

On January 31, 2020, we launched the abstractions repo as a place for wizards to create views and later tables. Since then, we’ve had over three hundred contributors and nearly 1k commits.

![Mats inaugural comment](images/mats-inaugural-comment.jpg)

Abstractions are some of the most queried tables on Dune. That makes creating them one of the highest leverage things a wizard can do. We want to make that experience better by launching the **Spellbook**, a retooling of our existing [abstractions](https://github.com/duneanalytics/dune-v1-abstractions) repo + a first-in-class open-source analytics engineering tool called dbt.

[dbt-core](https://docs.getdbt.com/docs/introduction) (data build tool) is an open-source framework that injects more classical software engineering practices into writing SQL by mixing SQL with JINJA templating.

![Succinct description of why we are appropriately hyped on dbt ](images/short-dbt-description.jpg)

Abstractions, henceforth **models** in dbt-speak or **spells** in dune-speak, can be materialized into views and tables, but there are many possible refinements, including incrementally-loaded tables, date-partitioned tables, and more. These can all be compiled into SQL and run on dune.com. No more contributing code that you can’t test without our help.

dbt allows us to write and manage unit tests to spot and prevent any issues in our abstractions.

Data integrity tests can easily be added with a single line in a YAML file. Models can be checked for unique primary keys, non-null values, accepted values, and relational integrity with minimal effort.

dbt natively understands the dependencies between all models. In our old abstractions logic we were managing dependencies manually, which made deploying and maintaining them a mess. With dependency management, we can guarantee that all models are deployed in the correct order.

![Dependency graph created by dbt showing erc20 daily balances dependency tree](images/dbt-erc20-dependency-graph.jpg)

We hope you are as excited as we are about this new tool. Spellbook is now live in prod and we welcome new contributors.

## Sector Spells

Sector Spells are tables like dex.trades, erc20.stablecoins, lending.borrow etc.

These Spells take in data from multiple contracts and projects, standardize the data across them and therefore make it very easy to query for this data and compare the metrics of different projects with each other.

Most of the sector Dashboards dashboards depend on sector spells. This introduces an interesting dynamic in which projects can easily get their data into these dashboards by making a pull request to our public [github repo](https://github.com/duneanalytics/spellbook/index.md).

Team Dune and the community are always improving on these sector spells, all new additions to existing ones are always welcome.

## Project Spells

Projects can assemble their data into one neat table that has all the data they need in one place. To do this, you can construct views or tables in our spells.

The main advantage here over just constructing a view is that you are able to deal with bigger amounts of data in our Spells since we can run them automatically in the background every few hours.

## Contributing to Spellbook

If you'd like to contribute to Dune spells, take a look at [Spellbook](contributing/index.md).

These enable you to effortlessly aggregate lots of data with as little friction as possible.

To view available Spells, take a look at our [Spellbook model documentation](https://dune.com/spellbook) and learn how to contribute new Spells [here](contributing/index.md)

Our Spells are managed via the public [Spellbook GitHub repository](https://github.com/duneanalytics/spellbook/index.md). We welcome pull requests!

## Abstractions (Dune V1)

!!! warning
       Our abstractions for v1 are no longer open for contributions, and will be [sunsetted with the v1 engine](../../reference/v1-sunsetting.md) soon.

For our **V1 Engine** (PostgreSQL), abstractions are snippets of SQL executed the data platform. You can check for existing abstractions on [GitHub](https://github.com/duneanalytics/dune-v1-abstractions).

You can check for existing abstractions in our [public github repository](https://github.com/duneanalytics/spellbook/index.md), under `deprecated-dune-v1-abstractions`.
