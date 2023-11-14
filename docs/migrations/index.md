---
title: Overview
description: This Page describes the old query engines that will soon be depreceated. SparkSQL and PostgresSQL will be replaced by DuneSQL.   
---

## Dune's Query Engines

Dune formerly supported three different query engines:  

- DuneSQL  
- SparkSQL (shut down) 
- PostgreSQL (shut down) 

The SparkSQL and PostgreSQL query engines were deprecated and are replaced by DuneSQL. You can read more about the decisions to sunset the old query engines in the [announcement post](https://dune.com/blog/introducing-dune-sql).

**You should use the [migration tool](migration-tool.md) to try and translate your queries. If you run into issues, please let us know by [creating an issue](https://github.com/duneanalytics/harmonizer/issues).**

## Sunsetting Schedule

We are progressively disabling the ability to create new queries on the old query engines. You can read up on the stages of that in the table below. 
The final date of the sunsetting was **30/07/2023**. The old query engines will no longer receive new data and there is no more executions.


### SparkSQL

| Date          | 11/4/2023            | 30/05/2023              | 15/07/2023                     | 30/07/2023     |
|---------------|----------------------|-------------------------|--------------------------------|----------------|
|**SparkSQL**   | Sunsetting Kickoff   | no action taken         | Query creation, edits disabled | End of Service |

### PostgreSQL

| Date          | 11/4/2023            | 30/05/2023              | 15/07/2023     | 30/07/2023          |
|---------------|----------------------|-------------------------|----------------|---------------------|
|**PostgreSQL** | Sunsetting Kickoff   | Query creation disabled | edits disabled | End of Service      |

## What this means for you

You will need to migrate your queries from SparkSQL or PostgreSQL to DuneSQL. If you don't migrate your queries, you queries will cease to update on **30/07/2023** and you will no longer be able to edit or execute them without migrating them to DuneSQL. 

### Migrating your queries

If you are using SparkSQL or PostgreSQL, you will need to migrate your queries to DuneSQL by **30/07/2023**.  

To migrate your queries from SparkSQL or PostgreSQL to DuneSQL, you can use the [DuneSQL migration tool](migration-tool.md).  
This tool will automatically convert your queries to DuneSQL.
You can read about the Syntax differences between the engines in the respective sections of SparkSQL and PostgreSQL.

<div class="cards grid" markdown>

- [→ SparkSQL](SparkSQL.md)
- [→ PostgreSQL](PostgreSQL.md)

</div>


### What happens to non-migrated queries?
After **30/07/2023**, queries running on either SparkSQL or PostgreSQL will no longer be updated. You will still be able to access the data from your queries, but there won't be any new data added to your query results and they will stop executing. Query code will still be available to you, but you will not be able to edit it.

## FAQ

### general

??? question "What is DuneSQL?"

    DuneSQL is a powerful distributed SQL query engine, based on Trino, that is designed to address the limitations of the old query engines and provide a more modern and flexible solution.

??? question "Why another query engine?"

    DuneSQL was created to address the limitations of the old query engines, such as performance and scalability issues, as well as to provide a more modern and flexible solution. DuneSQL gives Dune full control over storage, execution, and query planning, which allows us to provide a faster, more reliable, and more scalable service.

??? question "What are the main differences between DuneSQL and the old query engines?"

    Some of the main differences between DuneSQL and the old query engines are:

    - DuneSQL is designed for scalability, whereas the old query engines have struggled with scaling issues in the past.
    - with DuneSQL, we control the entire stack, from the database to the query engine, which allows us to provide a more stable and reliable service.
    - DuneSQL has a simplified syntax that makes it easier to write and read queries.

??? question "Why a fork of Trino?"

    DuneSQL is a fork of Trino (formerly known as PrestoSQL) that has been customized to meet the specific needs of Dune. Trino is a powerful distributed SQL query engine that is widely used in the industry, and by forking it, Dune was able to leverage its proven technology while also adding its own unique features and improvements.

??? question "What happens to the existing queries that I have already migrated?"

    If you have already migrated your queries to DuneSQL, they will continue to work as before and you won't need to take any additional action.

??? question "Will Postgres and SparkSQL still be around for a while?"

    PostgreSQL and SparkSQL are being deprecated and will be replaced by DuneSQL. After **30/07/2023**, queries running on either SparkSQL or PostgreSQL will no longer be updated. You will still be able to access the last execution result from your queries, but there won't be any new data added to your query results and they will stop executing. The Query code will still be available to you, but you will not be able to edit it.

??? question "What happens with Spellbook? Can I still contribute?"

    Spellbook is still a valuable tool for Dune and will continue to be used. You can still contribute to Spellbook by submitting pull requests on the project's GitHub repository. We are working on migrating Spellbook to DuneSQL. The Spellbook code will be migrated to DuneSQL by the Dune Team. The migration to DuneSQL has started and there now is 2 spellbook repos.
 

### Timeline

??? question "When do Spark Queries stop working?"

    SparkSQL queries will stop being updated on **30/07/2023**. This means they will no longer receive new data and will stop executing.

??? question "When do Postgres Queries stop working?"

    PostgreSQL queries will stop being updated on **30/07/2023**. This means they will no longer receive new data and will stop executing.

### Migration

??? question "How can I migrate existing Queries?"

    To migrate your queries from SparkSQL or PostgreSQL to DuneSQL, you can use the [DuneSQL migration tool](migration-tool.md). This tool will automatically convert your queries to DuneSQL.
    Additionally, you can read about the Syntax differences between the engines in the respective sections of (SparkSQL)[sparksql.md] and (PostgreSQL)[postgresql.md].

??? question "Can I get help to migrate existing queries?"

    Please [create an issue in the translator github](https://github.com/duneanalytics/harmonizer/issues) for priority support. Otherwise, you can direct your general questions in the #DuneSQL Channel in the [Dune Discord](https://discord.gg/dunecom).

