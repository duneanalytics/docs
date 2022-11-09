---
title: Spells
---

Everything in a `.sql` file should solely consist of a `select` statement.

You don’t need to specify `create view` or `create table`. [Materialization strategies](https://docs.getdbt.com/docs/building-a-dbt-project/building-models/materializations) are handled by JINJA blocks or by the YAML schema file for the model.

Models will (by default) be views but we can override that to make them tables or incrementally loaded tables.

The basic trade-off is that a view is fast to create and doesn’t require additional storage but is slower to query. A table is much slower to create and does require additional storage but is faster to query. Generally, we’ll try to stick to views but upgrade to tables or incrementally loaded tables if performance is an issue.

To learn more about all the features in DBT, take a look at their [documentation](https://docs.getdbt.com/docs/introduction). We've written a few [example](../examples/index.md) guides for building spells for ERC20.

## Checking your spell

Copy your spell from the target folder and try running it on dune.com in a new query window.

We are working diligently on a secure sandbox where you can freely run your spells directly from DBT. But in the meantime, the best way to check your work locally is to “compile” your spells.

After you’re [instatited DBT](https://github.com/duneanalytics/spellbook/blob/master/README.md) with \`dbt init\`, run \`dbt compile\`. This will create a new folder called “target”. Inside the target folder will be all of the spells compiled into plain SQL. Then you can copy your spell and run it directly on dune.com.

![type:video](https://www.youtube.com/embed/9sut8560oUE)
