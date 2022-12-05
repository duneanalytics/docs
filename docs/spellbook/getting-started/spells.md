---
title: Spells
---

Everything in a `.sql` file should solely consist of a `select` statement.

You don’t need to specify `create view` or `create table`. [Materialization strategies](https://docs.getdbt.com/docs/building-a-dbt-project/building-models/materializations) are handled by JINJA blocks or by the YAML schema file for the model.

Models will (by default) be views but we can override that to make them tables or incrementally loaded tables.

The basic trade-off is that a view is fast to create and doesn’t require additional storage but is slower to query. A table is much slower to create and does require additional storage but is faster to query. Generally, we’ll try to stick to views but upgrade to tables or incrementally loaded tables if performance is an issue.

To learn more about all the features in DBT, take a look at their [documentation](https://docs.getdbt.com/docs/introduction). We've written a few [example](../examples/index.md) guides for building Spells for ERC20.

## Anatomy of a spell

Spells are dbt models and as such are ultimately `select` queries. Each Spell's SQL file has to contain a select statement and follow a few additional rules:

Querying data from other parts of Dune is must be done using [Jinja syntax](https://docs.getdbt.com/docs/build/jinja-macros):

- **sources** are decoded and raw tables on Dune, they should be addressed with `{{ source('ethereum', 'transactions' }}` and, in case of decoded tables, should be referenced on the `sources.yml` file (see details [here](#_ht3y58fudwir))
- **refs** are all the other Spells created in spellbook, should be addressed with the `ref` function e.g. `{{ ref('uniswap_ethreum_trades') }}`

At the top of each Spell's SQL file you'll find a config block. Its contents will vary depending on the type of materialization but at the very least:

- The config block should assign an alias to the view.
- If the view should be available on the Dune Data Explorer, a post\_hook must be added.

- There will be additional requirements depending on the type of materialization you use (see details for [incremental](#_526g7qsxh9q)[table](#_526g7qsxh9q) and [table](#_9gqiuknnb44))

### Metadata Files

The power of dbt lies in automatically performing many of the tasks our Wizard ancestors had to code by hand in ETL software.

To use this power, though, dbt needs to know (or be able to infer) details about our Spells that is not contained in the SQL itself. That's where the yml metadata files come in.

dbt starts working based on the parent config file `dbt_project.yml`. Any new Spell we add has to be reflected in [project.yml](https://github.com/duneanalytics/spellbook/blob/main/dbt_project.yml) under `models \> spellbook`.

In every Spell you will find two very important .yml files:

- \*\_sources.yml contains metadata about the sources required by the Spell. This includes any Raw or Decoded Table that you call using `source()` Jinja function.
- \*\_schema.yml contains metadata about the models included in the Spell. As long as the schema file is referenced by dbt\_project.yml, you can consolidate multiple models into a single schema file.

The content of these files is usually fairly simple, although the options are endless. If you want to understand what to use for your case, it may be best to refer to examples of similar Spells. Explore all our existing Spells in the [Spellbook Model docs](https://spellbook-docs.dune.com/#!/overview).

## Checking your spell

Copy your Spell from the target folder and try running it on dune.com in a new query window.

We are working diligently on a secure sandbox where you can freely run your Spells directly from DBT. But in the meantime, the best way to check your work locally is to “compile” your spells.

After you’re [instatited DBT](https://github.com/duneanalytics/spellbook/blob/master/README.md) with \`dbt init\`, run \`dbt compile\`. This will create a new folder called “target”. Inside the target folder will be all of the Spells compiled into plain SQL. Then you can copy your Spell and run it directly on dune.com.

![type:video](https://www.youtube.com/embed/9sut8560oUE)
