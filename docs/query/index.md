---
title: Query
description: Dune utilizes a fork of TrinoSQL to power DuneSQL. DuneSQL is a custom built query engine that is optimized for blockchain data.   
---

**Querying for blockchain data on Dune is powered by DuneSQL, a custom-built query engine designed for efficient analysis of blockchain data.**

## DuneSQL Features

DuneSQL offers several useful features for working with blockchain data:

1. **[Blockchain varbinary data types](DuneSQL-reference/datatypes.md#varbinary)**: Designed for storing addresses, hashes, and other encoded data.
2. **[Native support for uint256 and int256 data types](DuneSQL-reference/datatypes.md#UINT256)**: Ideal for handling large numbers commonly found in blockchain data, with built-in functions for ease of use.
3. **[Columnar storage format](storage.md)** Optimized for fast reads, this format organizes data in columns rather than rows, enabling quick access to single columns for aggregation or filtering.
4. **[Querying a query](query-a-query.md)**: DuneSQL allows you to query a query, which is great for creating reusable queries, building up complex queries, and reusing queries as views.

!!! warning "Sunsetting Old Query Engines"
    We are sunsetting our old query engines, SparkSQL and PostgreSQL. Please find all information in the [Migrating to DuneSQL](../migrations/index.md) section of our documentation.


## Using DuneSQL

DuneSQL is our query engine for blockchain data. It is a fork of TrinoSQL, which is an open-source, distributed SQL query engine for running interactive analytic queries against data sources of all sizes ranging from gigabytes to petabytes.

We have created extensive documentation for DuneSQL, which you can find in the [DuneSQL Reference](DuneSQL-reference/index.md) section of our documentation. Here you will be able to find:

<div class="cards grid" markdown>

-   #### Functions and operators

    ---

    A reference guide to DuneSQL functions and operators.
  
    [→ Functions and operators](DuneSQL-reference/Functions-and-operators/index.md)

-   #### Data types

    ---

    A reference guide to DuneSQL data types.
  
    [→ Data types](DuneSQL-reference/datatypes.md)

-   #### Reserved keywords

    ---

    A list of reserved keywords in DuneSQL.
  
    [→ Reserved keywords](DuneSQL-reference/reserved-keywords.md)

</div>


## Writing efficient queries

An efficient query-writing process requires knowledge of how DuneSQL and data storage works.

<div class="cards grid" markdown>

- [→ Writing efficient queries](writing-efficient-queries.md)

</div>

## Querying a query

DuneSQL allows you to query a query, which is great for creating reusable queries, building up complex queries, and reusing queries as views.

<div class="cards grid" markdown>

- [→ Querying a query](query-a-query.md)

</div>

### Resources and Support

For assistance with DuneSQL, consider the following resources:

- Google search for TrinoSQL-related queries
- Talk to your favorite AI assistant about TrinoSQL-related questions
- [the official Trino docs - Functions and Operators](https://trino.io/docs/current/functions.html)

Join our #dune-sql [Discord channel](https://discord.gg/dunecom) to connect with our team and the community for help and support.

### Feedback and Suggestions

We appreciate your feedback and suggestions for improvement. Please email us at dunesql-feedback@dune.com with any concerns or ideas for optimization.

