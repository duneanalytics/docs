---
title: Dune V2
description: Dune Engine V2 is an update to our Query engine that brings a new level of performance, scalability and functionality to the core tools that enable Wizards to query, extract, and visualize blockchain data.
---

**Dune Engine V2** is an update to our Query engine that brings a new level of performance, scalability and functionality to the core tools that enable Wizards to query, extract, and visualize blockchain data.

It leverages **[Apache Spark SQL](https://spark.apache.org/docs/latest/sql-programming-guide.html)** to  increase performance for complex Queries, handle data scale, and enable cross-chain Queries all within the [Query Editing UI](../../getting-started/queries/index.md) you're used to.

All of the data sources contained in this section are available for querying with the new Query engine today. We currently have the following data available in V2:

- [**Raw tables**](../tables/raw/index.md)
- [**Decoded projects**](../tables/decoded/index.md)
- [**Spells**](../tables/spells/index.md)
- [**Community Tables**](../tables/community/index.md)

## New Query engine

Dune V2 changes our entire database architecture. We are transitioning away from a PostgresQL database to an Instance of Apache Spark hosted on Databricks. The difference between the two systems can be summarized as follows:

* Instead of PostgresQL, we will now use Spark SQL. The change in SQL keywords is minimal but might be relevant for some of your querying habits.
* Spark is a column oriented database in contrast to PostgresQL’s row oriented approach.
* traditional indexes are replaced by column chunk level `min/max` values

**You can read more about the changes here:**

<div class="cards grid" markdown>
- [Query Engine](query-engine.md)
</div>

**Or start getting your wand dirty by following along here:**

<div class="cards grid" markdown>
- [@springzhang](https://dune.com/springzhang/)'s [Tips and Tricks for Dune V2 Queries and Visualizations](https://dune.com/springzhang/tips-and-tricks-for-query-and-visualization-in-v2-engine)
</div>
 

## Spellbook

Abstractions have been upgraded to Spells stored in the [Spellbook](../../spellbook/index.md) in Dune V2.

They run on [data build tool (dbt)](https://docs.getdbt.com/docs/introduction). dbt enables analytics engineers to transform data in their warehouses by simply writing select statements. dbt handles turning these select statements into [tables](https://docs.getdbt.com/terms/table) and [views](https://docs.getdbt.com/terms/view).

This will makes the data abstractions built as Spells more robust, scalable and easier to work with.

<div class="cards grid" markdown>
- [Spells](../../spellbook/index.md)
</div>

## Feedback

One final note, as the Query engine is still in in **beta** you may run into bugs or have feedback on how it can be improved, feel free to share it with us on in our [#general-feedback Discord channel](https://discord.com/channels/757637422384283659/1012706316755664926) or on our [Canny board](https://dune.canny.io).
