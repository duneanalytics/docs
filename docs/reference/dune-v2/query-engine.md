---
title: V2 Query Engines
description: Dune V2 uses Spark and Dune SQL query engines. Learn how they work here!
hide:
  - toc
---

With Dune V2 we’re moving away from a [PostgreSQL](https://www.postgresql.org/) query engine to:

1. Spark SQL - [Apache Spark](https://www.databricks.com/glossary/what-is-apache-spark) hosted on [Databricks](https://docs.databricks.com/getting-started/introduction/index.html).
2. Dune SQL - A self hosted instance of [Trino](https://trino.io/)(**currently in alpha**). 

As Dune usage has increased, our data access pattern has become quite clear: Dune writes data Once and wizard query it millions of times.

In order to scale Dune to meet the demand for query execution, we need to decouple data storage from the computation of queries - something that can’t be done in PostgreSQL.

As we experimented with solutions internally, we built a new system around the [Delta framework](https://delta.io/) and used Spark for parallel processing of that data.

During experimentation, we began ingesting Solana data. Since solana.transactions is about 100x the size of ethereum.transactions, it was both a primary reason we needed to upgrade our systems (there’s no way Postgres could handle this) and the perfect test candidate.

We saw some great wins in how quickly and flexibly we could write and store data but when it came time to start sharing access to Solana data we faced a dilemma.

As we were focused on optimizing the ingesting and storing of this data, we did not spend a lot of time upgrading our infrastructure for querying that data.

When we asked ourselves whether we should spend months figuring out how to improve our querying infrastructure or get Solana data in the hands of our community ASAP, we chose the latter - which meant shipping Dune V2 in beta with Spark SQL as our query engine.

Now that we have a massive amount of usage data (compared to our internal testing), cracks have appeared that weren’t evident to us pre-launch.

As things stand:

* A range of queries that performed super well on v1, now take minutes on V2 (looking at you WHERE tx_hash = y). Part of this is clearly the tradeoff we’ve made in laying out our data in columnar form, as opposed to in rows, but that doesn’t fully explain the latency.
* V2 (Beta) lacks support for user defined functions, views, tables, and it’s not easy for Dune to enable that functionality in a way that’s safe and helpful to users in Spark.
* Because the Spark clusters are outsourced, we have trouble scaling them, and tuning them. It’s also not possible for us to improve performance or fix bugs without waiting for months for someone to [merge them](https://github.com/delta-io/delta/pull/1210).
* We oftentimes find ourselves without visibility into the health of the query engine, which has lead to us being unable to resolve confusion for ourselves or the community when some queries have failed.

As a result of these challenges, we’ve been internally researching how to fundamentally improve our V2 query experience and after a few breakthroughs, we’ve developed what Dune SQL, powered by a self-hosted instance of [Trino](https://trino.io/). 

And as a step toward resolving some of the communication errors we made with the initial Spark SQL launch, we’re emphasizing that **Dune SQL is currently in alpha**.

This means:

* While we strongly believe Dune SQL/Trino is the long term solution for creating the best blockchain data querying experience in the world, it isn’t there yet - with your help we’ll break lots of things and use what we learn to continuously build a better system.
* While we have a timeline for [Sunsetting Dune V1 (PostgreSQL)](../v1-sunsetting.md), we do not have one for fully transitioning from Spark to Dune SQL and will work with the community to decide when and how that transition will take place to move forward with [Speed](https://www.notion.so/Values-and-working-at-Dune-7efdcec2298a4913aaef8067b25820df#ffc480bf5c5e4e38a1c53d2fb9926e3e) and transparency.

## Joining the SQL revolution

We’re excited to have you join the SQL revolution with us as we make Dune SQL the absolute best blockchain querying experience around.

To help out as an alpha tester, you’ll first need to create a separate account at [https://dev.dune.com/](https://dev.dune.com/).

There you’ll find Dune SQL as an option in the Query Explorer, and right off the bat you should see some improvements over Spark SQL ([incomplete & cryptic error messages](https://dev.dune.com/queries/59553) or [0x strings](https://dev.dune.com/queries/59390), we’re looking at you).

## Syntax and operator differences

The syntax and keyword operator differences between Postgres, Spark, and Dune SQL are quite minimal, however there are a few to be aware of.

!!! warning
    **Dune SQL is still in alpha!** If you find any other changes in Spark or Dune SQL that are important to note, please feel free to [submit a PR to this docs page on GitHub](https://github.com/duneanalytics/docs/edit/master/docs/reference/dune-v2/query-engine.md) or let us know in #dune-sql.

### Syntax Comparison

| <div style="width:290px">**Description**</div> | **V1 - PostgreSQL** | **V2 - Spark SQL** | **V2 - Dune SQL** |
| --- | --- | --- | --- |
| **`bytea2numeric` does not exist in Spark.** | `bytea2numeric` (bytea) | `bytea2numeric_v2` (string) | `bytea2numeric` (string) |
| **0 vs 1 array based indexing** | 1 indexed | 0 indexed | 1 indexed |
| **Implicit type conversions between character and numeric types** | Available | Available | [Not available](https://trino.io/docs/current/functions/conversion.html) |
| **Addresses** | `\x2A7D...`(bytea)<br><br>Works in Postgres | `0x2a7d...` (string)<br><br>Has to be lowercase in Spark.<br><br>Can be done via `lower('0x2A7D...')` | `0x2a7d...` (Byte array) <br><br> No escape quotes should be used, and the literal does __not__ need to be lowercased. |
| **Selecting keyword columns is different** | `from` | `'from'` | `from` |
| **Alias naming is different** | as `daily active users` | as `'daily active user'` | as `daily active users` |
| **Exponentiation notation** | `x/10^y` or `x * 1e123` | `x*power(10,y)` or `x*1e123` | `x*power(10,y)` or `x * 1e123` |
| **Interval argument has different syntax** | `Interval '1day'` | `Interval '1 day'` | `Interval '1' day` |
| **Generate_series () is now sequence ()** | `generate_series('2022-05-15', CURRENT_DATE, '1 day')` | `explode(sequence(to_date('2022-01-01'), to_date('2022-02-01'), interval 1 day))` | `values(sequence(cast('2022-01-01' as date) - interval '7' day,cast('2022-02-01' as date),interval '1' day))`<br><br>Has a 10000 values limit. |
| **Handling decimals for prices.usd** | Don’t use `prices.usd decimals` | Replaced by `prices.tokens decimals` | Replaced by `tokens_[blockchain].erc20.decimals` |
| **Define NULL array** |` NULL::integer[]` | `CAST(NULL AS ARRAY&lt;int&gt;))` | `CAST(NULL AS ARRAY&lt;int&gt;))` |
| **encoding strings to hex** | `encode(string, 'hex')` | `hex(string)` | `hex(string)`<br><br>*available soon |
| **Get json object differences** | `(takerOutputUpdate->'deltaWei'->'value') decode(substring((addressSet->'baseAsset')::TEXT, 4,40), 'hex')` | `get_json_object(get_json_object(takerOutputUpdate,'\(.deltaWei'),'\).value')'0x'` | `json_query(json_query(takerOutputUpdate, 'lax $.deltaWei' omit quotes), 'lax $.value')` |
| **Group by an alias** | `SELECT date_trunc('hour',evt_block_time) as col1, COUNT(*) FROM erc721_ethereum evt_Transfer GROUP BY col1` | Same as PostgreSQL | `GROUP BY date_trunc('hour',evt_block_time)`Or: `GROUP BY 1, 2` |
| **Explicit date/time casting** | `'2021-08-08 17:00'::timestamp` | `cast('2021-08-08 17:00' as timestamp)` | `cast('2021-08-08 17:00' as timestamp)`<br><br>Or, `timestamp '2021-08-08 17:00'`<br><br>There are [many helper functions for casting to date/time types](https://trino.io/docs/current/functions/datetime.html?highlight=date), such as `date(‘2022-01-01’)` |
| **Checking if an item exists in an array** | `value = ANY (array)` | array_contains(array, value)` | `contains(array,value)` |
| **Explode** | `SELECT unnest(array) FROM table` | `SELECT explode(array) FROM table` | `SELECT vals.val FROM table1, unnest(arrayFromTable1) as vals(val)`<br><br>you have to use `unnest` with a `cross join`, as described in this [blog post](https://theleftjoin.com/how-to-explode-arrays-with-presto/). |
| **Median** | `PERCENTILE_CONT(0.5) WITHIN GROUP(ORDER BY x)` | `PERCENTILE_CONT(0.5) WITHIN GROUP(ORDER BY x)` | `approx_percentile(x, 0.5)` |
| **Using “is True/False”** | `X is true` | `X is true` | `X = true` |

### Double quotes are not recommended

Using double quotes is not recommended in DuneV2, even when the engine runs your query without returning an error.

This is because the parser sometimes treats words in double quotes as a string and sometimes it treats them as an object like a column name.

For example, referencing a column name in the `WHERE` clause using double quotes works as expected. However, the same query inside a CTE treats the column name as a string, [as can be seen here](https://dune.com/queries/1199604).

## Query queries as views in Dune SQL

All queries written using Dune SQL can be queried as views in other queries using the identifier `query_<queryId>`. For instance:
```
select * from query_1234
```
[Here is an example query](https://dune.com/queries/1746224) which queries [this query](https://dune.com/queries/1746191).
The `queryId` is part of the URL of a query.

**Note**:

- All output columns of the query being queried must be named. That is, you cannot query `select 1` or `select count(*) from ethereum.transactions`, but you can query `select 1 as v` and `select count(*) as total from ethereum.transactions`.
- Parametrized queries are not supported.
- Only public queries can be queried. Support for querying private queries will be added in the future.
- Only saved queries can be queried.
- Only queries written in Dune SQL can be queried.

## Other questions and feedback

As ever, Google is a great friend in answering your SQL questions.

With Dune V2, instead of googling “PGSQL median”, you should now google “Spark SQL median” (for Spark SQL) or “Trino SQL median” (for Dune SQL). 

Both also have well documented index of built in functions on their website:

* [Spark - Spark SQL Language Reference](https://spark.apache.org/docs/latest/sql-programming-guide.html)
* [Trino - Functions and Operators](https://trino.io/docs/current/functions.html)

Our [#dune-sql Discord channel](https://discord.com/channels/757637422384283659/1051871389432422491) is the best place to get help from our team and Wizard community when Google fails you.

As you come across issues or identify areas of improvement, please send us an email at [dunesql-feedback@dune.com](mailto:dunesql-feedback@dune.com) and we’ll work with you to update and optimize!
