[View code on GitHub](https://dune.com/docs/query/query-a-query.md)

# Query a Query

This section of the DuneSQL app technical guide explains how to query a query in DuneSQL. This feature allows users to create reusable queries, build up complex queries, and reuse queries as views.

## Query queries as views in Dune SQL

In DuneSQL, all non-parameterized queries can be queried as views in other queries using the identifier `query_<queryId>`. For example, to query a query with ID 1234, the syntax would be:
```
select * from query_1234
```
The `queryId` is part of the URL of a query.

It is important to note that:
- All output columns of the query being queried must be named. This means that queries like `select 1` or `select count(*) from ethereum.transactions` cannot be queried, but queries like `select 1 as v` and `select count(*) as total from ethereum.transactions` can be queried.
- Parametrized queries are not supported.
- Only public queries can be queried. Support for querying private queries will be added in the future.
- Only saved queries can be queried.
- Only queries written in Dune SQL can be queried.

The ability to query a query is useful for creating more complex queries and reusing queries as views. An example query is provided in the guide for reference.

Overall, this section of the app technical guide provides a clear explanation of how to query a query in DuneSQL and the limitations of this feature. It is a useful reference for users who want to create more complex queries and reuse queries as views.
## Questions: 
 1. What is DuneSQL and how does it relate to blockchain technology?
- This app technical guide does not provide information on how DuneSQL relates to blockchain technology, so a blockchain SQL analyst might want to know more about the context and use cases of this tool.

2. Can parameterized queries be queried as views in DuneSQL?
- No, according to the app technical guide, only non-parameterized queries can be queried as views in DuneSQL.

3. Is it possible to query private queries in DuneSQL?
- No, the app technical guide states that only public queries can be queried as views in DuneSQL, and support for querying private queries will be added in the future.