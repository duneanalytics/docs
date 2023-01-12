---
title: Dune V2
description: Dune Engine V2 is an update to our Query Engine and Database that brings a new level of performance, scalability and functionality to the core tools that enable Wizards to query, extract, and visualize blockchain data.
---

Dune V2 brings a new level of performance, scalability and functionality to the core tools that let Wizards query, extract, and visualize the vast amounts of blockchain data available.

Dune V2 is an update to our database and query engine that includes:

1. A scalable column oriented database (in contrast to PostgreSQL’s row oriented approach)
2. Dune’s new query engines, Dune SQL and [Spark SQL](https://spark.apache.org/docs/latest/sql-programming-guide.html).

For more on the why behind Dune V2, be sure to [read the post from our CTO](https://dune.com/blog/introducing-dune-sql)!

## New Database

DuneV2 changes our entire database architecture. We are transitioning away from a PostgreSQL database to a scalable columnar database.The difference between the two systems can be summarized as follows:

* V2 uses a columnar storage format in contrast to PostgreSQL’s row oriented approach.
* Traditional indexes are replaced by [block range indexes](https://en.wikipedia.org/wiki/Block_Range_Index), which are chunk level min/max values

Read more about how the Dune V2 database works here:

<div class="cards grid" markdown>
- [V2 Database](database.md)
</div>

## New Query Engines

DuneV2 leverages two different query engines as we transition away from a PostgreSQL database to a data lake house.

* Spark SQL, powered by [Spark SQL](https://spark.apache.org/docs/latest/sql-programming-guide.html)
* Dune SQL, powered by [Trino](https://trino.io/)

Spark SQL was our initial choice for a V2 Query engine, but after gathering data and feedback from our Beta release we realized it won’t allow us to continue to have the best blockchain data querying experience as we scale.

We believe the solution is Dune SQL powered by Trino, and we’re excited to have it live in *alpha*.

Once we’ve work with the community to revise and refine Dune SQL into a polished release state, we’ll phase out Spark SQL as we have Postgres.

You can read more about how the new query engines work here:

<div class="cards grid" markdown>
- [V2 Query Engines](query-engine.md)
</div>

## Spells

Abstractions in DuneV2 run on [dbt](https://docs.getdbt.com/docs/introduction) (data build tool). dbt enables analytics engineers to transform data in their warehouses by simply writing select statements, then dbt handles turning these select statements into [tables](https://docs.getdbt.com/terms/table) and [views](https://docs.getdbt.com/terms/view).

Spells currently run on Spark SQL in Dune v2 but can also be queried on Dune SQL. Certain Spells will need some slight modifications to be used as queries on Dune SQL. Our team will help you with this during the submission process!

Learn more about Spells here:

<div class="cards grid" markdown>
- [Spells in Dune V2](../../spellbook/index.md)
</div>

## Other questions and feedback

As ever, Google is a great friend in answering your SQL questions.

With Dune V2, instead of googling “PGSQL median”, you should now google “Spark SQL median” (for Spark SQL) or “Trino SQL median” (for Dune SQL). 

Both also have well documented index of built in functions on their website:

* [Spark - Spark SQL Language Reference](https://spark.apache.org/docs/latest/sql-programming-guide.html)
* [Trino - Functions and Operators](https://trino.io/docs/current/functions.html)

Our [#dune-sql Discord channel](https://discord.com/channels/757637422384283659/1051871389432422491) is the best place to get help from our team and Wizard community when Google fails you.

As you come across issues or identify areas of improvement, please send us an email at [dunesql-feedback@dune.com](mailto:dunesql-feedback@dune.com) and we’ll work with you to update and optimize!
