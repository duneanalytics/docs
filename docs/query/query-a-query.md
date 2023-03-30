---
title: Query a Query
description: In DuneSQL you can query a query, which is great for creating reusable queries, building up complex queries, and reusing queries as views.
---

## Query queries as views in Dune SQL

All non-paramterized queries written using Dune SQL can be queried as views in other queries using the identifier `query_<queryId>`. For instance:
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


