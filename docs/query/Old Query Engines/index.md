---
title: Old Query Engines
description: This Page describes the old query engines that will soon be depreceated. SparkSQL and PostgresSQL will be replaced by DuneSQL.   
---

## Overview

Dune Analytics supports three different query engines: SparkSQL, PostgreSQL, and DuneSQL. The SparkSQL and PostgreSQL query engines are being deprecated and will be replaced by DuneSQL. This page describes the old query engines and how to migrate your queries to DuneSQL.

## Sunsetting Schedule

The following table shows the schedule for the sunsetting of the old query engines.

| Query Engine | Introduced | Deprecated | Removed    |
|--------------|------------|------------|------------|
| SparkSQL     | 2022-05-01 | 2023-07-31 | 2024-07-31 |
| PostgreSQL   | 2019-11-01 | 2023-07-31 | 2024-07-31 |
| DuneSQL      | 2023-01-01 | ∞          | ∞          |

## SparkSQL

SparkSQL is a query engine that is based on Apache Spark. It is used to query the data that is stored in our databases. This engine was introduced on 2022-05-01. Unfortunately SparkSQL is not a good fit for our use case and therefore we are deprecating it.

SparkSQL is still in production and will be supported until 2023-07-31. After that date, SparkSQL will be removed from production and all queries will be migrated to DuneSQL.

You can read more about SparkSQL in the [SparkSQL documentation](https://spark.apache.org/docs/latest/sql-ref.html).

## PostgreSQL

Our PostgresSQL database and query engine are the oldest parts of Dune Analytics. They were introduced on 2019-11-01. PostgresSQL does not scale well and therefore we are deprecating it. 

PostgresSQL is still in production and will be supported until 2023-07-31. After that date, PostgresSQL will be removed from production and all queries will be migrated to DuneSQL.

You can read more about PostgreSQL in the [PostgreSQL documentation](https://www.postgresql.org/docs/).

## Migrating Queries

To migrate your queries from SparkSQL or PostgreSQL to DuneSQL, you can use the [DuneSQL migration tool](https://dune.com/migrate). This tool will automatically convert your queries to DuneSQL. The Tool is based on GPT4 and still under active development, we will share updates as we make progress.



