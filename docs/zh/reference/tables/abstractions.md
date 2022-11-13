---
title: Abstractions
description: >-
  We construct customs tables which cover the entirety of a type of activity on
  the blockchain and thereby enable you to effortlessly aggregate lots of data
  with as little friction as possible.
---

**Abstractions are custom tables that are built and maintained by Dune and our community.**

Our abstractions layer is managed in this public [GitHub repository](https://github.com/duneanalytics/spellbook/index.md). We welcome pull requests.

For our **V1 Engine** (PostgreSQL), abstractions are snippets of SQL executed the data platform. You can check for existing abstractions on [GitHub](https://github.com/duneanalytics/spellbook/tree/main/deprecated-dune-v1-abstractions), and view [documentation](v1/abstractions/index.md) on our most popular abstractions.

For our **V2 Engine** (Databricks SQL), abstractions are now upgraded to **spells** and live in [Spellbook](../spellbook/index.md). Spellbook is built with DBT, an open-source framework that injects more classical software engineering practices into writing SQL by mixing SQL with JINJA templating.

To view available spells, take a look at our Spellbook [documentation](https://spellbook-docs.dune.com) and learn how to contribute new spells [here](../spellbook/index.md).
