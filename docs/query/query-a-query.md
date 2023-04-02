---
title: Query a Query
description: The "Query a Query" feature in DuneSQL allows you to use an existing query as a view in another query. This powerful functionality enables you to create reusable queries, build complex queries, and take advantage of existing queries as views.
---

## Overview

The "Query a Query" feature in DuneSQL allows you to use an existing query as a view in another query. This powerful functionality enables you to create reusable queries, build complex queries, and take advantage of existing queries as views.
Currently the "Query a Query" feature is only available for public queries written in Dune SQL.  

!!!note 
    All upstream queries are executed as functional SQL views, which means that they need to be executed every time they are queried. This means there currently is no performance benefit to using the "Query a Query" feature.
## Using Query a Query

To use the "Query a Query" feature, you will need the queryId of the query you want to use as a view. The queryId can be found in the URL of a query. For example, if the URL of a query is [https://dune.com/queries/1746191](https://dune.com/queries/1746191), the queryId would be `1746191`.

Once you have the queryId, you can use it in your new query using the following syntax:

```sql
select * from query_<queryId>
```

For example, if you want to use the query with queryId 1746191 as a view in your new query, you would write:

```sql
select * from query_1746191
```

## Limitations

There are some important limitations and requirements to consider when using the "Query a Query" feature:

1. **Named output columns**: All output columns of the query being queried must be named. For example, you cannot query `select 1` or `select count(*) from ethereum.transactions`, but you can query `select 1 as v` and `select count(*) as total from ethereum.transactions`.
2. **Parameterized queries**: Parameterized queries are not supported for the "Query a Query" feature.
3. **Public queries**: Only public queries can be queried. Support for querying private queries will be added in the future.
4. **Saved queries**: Only saved queries can be used with the "Query a Query" feature.
5. **Dune SQL**: Only queries written in Dune SQL can be queried.

## Best Practices

When using the "Query a Query" feature, consider the following best practices:

1. **Naming conventions**: Ensure that your queries follow a consistent naming convention for output columns. This will make it easier to understand and reuse queries as views.
2. **Documentation**: Provide clear documentation and comments for your queries, especially when they are intended to be used as views in other queries.
3. **Modularity**: Break down complex queries into smaller, reusable components. This will make your queries more maintainable and easier to understand.
4. **Version control**: If you need to update a query that is being used as a view in other queries, consider creating a new version of the query instead of modifying the existing one. This will help prevent unexpected changes in dependent queries.
5. **Forking** If you use the query of another user as a view in your query, consider forking the query instead of querying it. That way, you will not be affected by changes made to the original query. On the other hand, you will also not be able to benefit from any improvements made to the original query.

## Conclusion

The "Query a Query" feature in DuneSQL is a powerful way to create reusable queries, build complex queries, and reuse queries as views. By understanding its limitations and following best practices, you can take full advantage of this functionality to improve your query development process.


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


