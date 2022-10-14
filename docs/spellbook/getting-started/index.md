---
title: Spellbook Getting Started
---

**Spellbook is essentially a DBT project that runs on Dune's data platform.**

At a high level, you need to setup our DBT project locally, develop a spell in Jinja-templated SQL, and get it to run on our data platform.

To start with, clone the [Spellbook](https://github.com/duneanalytics/spellbook/) repository and setup your local dev env as per the README.

Decide what problem you're trying to solve. Think about the [data model](data-modelling.md).

Write your spell. At minimum, you'll need to:

- Reference your [data sources](data-sources.md), with tests and freshness checks
- Define a unit [test](tests.md) for your spell
- [Write your spell](spells.md) as a SQL select statement with Jinja templating
- Write a schema in a separate YAML file

To learn more about all the features in DBT, take a look at their [documentation](https://docs.getdbt.com/docs/introduction). We've written a few [example](../examples/index.md) guides for building spells for ERC20.

!!! tip
    As you go along, you can use `dbt compile` to generate a SQL statement, and validate it on dune.com in the Query editor.

Once you're happy with your spell, you can [submit it to Dune](submissions.md):

- Fork the Spellbook repository and open a pull request
- Tag duneanalytics/data-experience and write a short description of your spell
- Your PR will trigger your spell to be created in the staging database and run tests
- If everything looks good, Dune will merge your changes and deploy them to production

After that, your spell will be visible on dune.com under "Spells". LFG!


## How To Guides

Check out our [How To Guides](../how-to-guides/) section for a variety of step-by-step tutorials to help you start casting Spells in no time!
