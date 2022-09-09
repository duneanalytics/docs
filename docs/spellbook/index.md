---
title: Spellbook
---

**Spellbook is a data transformation layer for Dune, built by the community.**

Spells are recipes to build high level tables that support common use cases, like NFT trades. You write them in SQL, wrapped in a Python templating language called Jinja2.

Spellbook automates the build, maintenance and data quality of these tables. Anyone in our community can contribute to our spells, whether that is adding a new exchange or writing an entirely new spell.

!!! note
    Spellbook is available on our Dune V2 Engine. For abstractions on Dune V1 Engine, see [abstractions](../tables/v1/abstractions/index.md).

## New level unlocked.

We’ve updated our database and now it’s time to update our contribution tools.

On January 31, 2020, we launched the abstractions repo as a place for wizards to create views and later tables. Since then, we’ve had over three hundred contributors and nearly 1k commits.

![Mats inaugural comment](images/mats-inaugural-comment.jpg)

Abstractions are some of the most queried tables on Dune. That makes creating them one of the highest leverage things a wizard can do. We want to make that experience better by launching the **Spellbook**, a retooling of our existing [abstractions](https://github.com/duneanalytics/spellbook/index.md) repo + a first-in-class open-source analytics engineering tool called dbt.

[dbt-core](https://docs.getdbt.com/docs/introduction) (data build tool) is an open-source framework that injects more classical software engineering practices into writing SQL by mixing SQL with JINJA templating.

![Succinct description of why we are appropriately hyped on dbt ](images/short-dbt-description.jpg)

Abstractions, henceforth **models** in dbt-speak or **spells** in dune-speak, can be materialized into views and tables, but there are many possible refinements, including incrementally-loaded tables, date-partitioned tables, and more. These can all be compiled into SQL and run on dune.com. No more contributing code that you can’t test without our help.

dbt allows us to write and manage unit tests to spot and prevent any issues in our abstractions.

Data integrity tests can easily be added with a single line in a YAML file. Models can be checked for unique primary keys, non-null values, accepted values, and relational integrity with minimal effort.

dbt natively understands the dependencies between all models. In our old abstractions logic we were managing dependencies manually, which made deploying and maintaining them a mess. With dependency management, we can guarantee that all models are deployed in the correct order.

![Dependency graph created by dbt showing erc20 daily balances dependency tree](images/dbt-erc20-dependency-graph.jpg)

We hope you are as excited as we are about this new tool. Spellbook is now live in prod and we welcome new contributors.
