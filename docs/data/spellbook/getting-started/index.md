---
title: Spellbook Getting Started
---

**Spellbook is essentially a DBT project that runs on Dune's data platform.**

At a high level, you need to setup our DBT project locally, develop a Spell in Jinja-templated SQL, and get it to run on our data platform.

To start with, clone the Spellbook GitHub repository and setup your local dev env as per the README:

<div class="cards grid" markdown>
- [Spellbook on GitHub](https://github.com/duneanalytics/spellbook)
</div>

Decide what problem you're trying to solve. Think about the [data model](data-modelling.md).

Write your spell. At minimum, you'll need to:

- Reference your [data sources](data-sources.md), with tests and freshness checks
- Define a unit [test](tests.md) for your spell
- [Write your spell](spells.md) as a SQL select statement with Jinja templating
- Write a schema in a separate YAML file

To learn more about all the features in DBT, take a look at their [documentation](https://docs.getdbt.com/docs/introduction). We've written a few [example](../examples/index.md) guides for building Spells for ERC20.

!!! tip
    As you go along, you can use `dbt compile` to generate a SQL statement, and validate it on dune.com in the Query editor.

Once you're happy with your spell, you can [submit it to Dune](submissions.md):

- Fork the Spellbook repository and open a pull request
- Tag duneanalytics/data-experience and write a short description of your spell
- Your PR will trigger your Spell to be created in the staging database and run tests
- If everything looks good, Dune will merge your changes and deploy them to production

After that, your Spell will be visible on dune.com under "Spells". LFG!


## How To Guides

Our How to Cast a Spell step-by-step guide is the best place to start:

<div class="cards grid" markdown>
- [How to Cast a Spell](../how-to-guides/how-to-cast-a-spell/index.md)
</div>

But be sure to check out the other [How To Guides](../how-to-guides/) for a variety of step-by-step tutorials to make you a better Spell caster!