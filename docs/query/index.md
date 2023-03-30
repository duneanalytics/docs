---
title: DuneSQL
description: Dune utilizes a fork of TrinoSQL to power DuneSQL. DuneSQL is a custom built query engine that is optimized for blockchain data.   
---

## DuneSQL: Query Engine for Blockchain Data

DuneSQL is a custom-built query engine designed for efficient analysis of blockchain data. Based on the open-source TrinoSQL engine, it incorporates additional optimizations to handle blockchain-specific requirements.

### DuneSQL Features

DuneSQL offers several useful features for working with blockchain data:

1. **[Blockchain varbinary data types](DuneSQL-reference/SQL-language/datatypes.md#varbinary)**: Designed for storing addresses, hashes, and other encoded data.
2. **[Native support for uint256 and int256 data types](DuneSQL-reference/SQL-language/datatypes.md#UINT256)**: Ideal for handling large numbers commonly found in blockchain data, with built-in functions for ease of use.
3. **[Columnar storage format](storage.md)** Optimized for fast reads, this format organizes data in columns rather than rows, enabling quick access to single columns for aggregation or filtering.
4. **[Querying a query](query-a-query.md)**: DuneSQL allows you to query a query, which is great for creating reusable queries, building up complex queries, and reusing queries as views.

### Using DuneSQL

DuneSQL is our query engine for blockchain data. It is a fork of TrinoSQL, which is an open-source, distributed SQL query engine for running interactive analytic queries against data sources of all sizes ranging from gigabytes to petabytes.

We have created extensive documentation for DuneSQL, which you can find in the [DuneSQL Reference](DuneSQL-reference/index.md) section of our documentation. Here you will be able to find:

- [SQL statement reference](DuneSQL-reference/SQL-statement-syntax/index.md)
- [SQL language reference](DuneSQL-reference/SQL-language/index.md)
- [Functions and operators](DuneSQL-reference/Functions-and-operators/index.md)

docs/query/DuneSQL-reference/SQL-language/index.md

### [Understanding DuneSQL Storage](storage.md)

An efficient query-writing process requires knowledge of how data is stored in DuneSQL. For details on the database layout and querying techniques, consult the [Storage section](storage.md) of our documentation.

### Resources and Support

For assistance with DuneSQL, consider the following resources:

- Google search for TrinoSQL-related queries
- Talk to your favorite AI assistant about TrinoSQL-related questions
- [the official Trino docs - Functions and Operators](https://trino.io/docs/current/functions.html)

Join our #dune-sql Discord channel to connect with our team and the community for help and support.

### Feedback and Suggestions

We appreciate your feedback and suggestions for improvement. Please email us at dunesql-feedback@dune.com with any concerns or ideas for optimization.

