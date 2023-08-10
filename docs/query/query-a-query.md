---
title: Query Views
description: The "Query View" feature in DuneSQL allows you to use an existing query as a view in another query. This powerful functionality enables you to create reusable queries, build complex queries, and take advantage of existing queries as views.
---

## Overview

The "Query View" feature in DuneSQL allows you to use an existing query as a view in another query. This powerful functionality enables you to create reusable queries, build complex queries, and take advantage of existing queries as views. 

!!! info
    All upstream queries are executed as functional SQL views, which means that they will be executed every time they are queried. This means there currently is no performance benefit to using the "Query a Query" feature.
## Using Query View

To use the "Query View" feature, you will need the queryID of the query you want to use as a view. The queryID can be found in the URL of a query. For example, if the URL of a query is [https://dune.com/queries/1746191](https://dune.com/queries/1746191), the queryID would be `1746191`.

Once you have the queryID, you can use it in your new query using the following syntax:

```sql
select * from query_<queryID>
```

For example, if you want to use the query with queryID 1746191 as a view in your new query, you would write: 

```sql
select * from query_1746191 
```

## Limitations

There are some important limitations and requirements to consider when using the "Query a Query" feature:

1. **Named output columns**: All output columns of the query being queried must be named. For example, you cannot query `select 1` or `select count(*) from ethereum.transactions`, but you can query `select 1 as v` and `select count(*) as total from ethereum.transactions`.
2. **Parameterized queries**: Parameterized queries are not supported for the "Query a Query" feature.
3. **Saved queries**: Only saved queries can be used with the "Query a Query" feature.
4. **Archived queries**: Archived queries cannot be queried.
5. **Dune SQL**: Only queries written in Dune SQL can be queried.

!!! Tip
    Querying private queries is a [premium feature](https://dune.com/pricing) only. You can't query private queries with a free or plus account. 

## Best Practices

When using the "Query View" feature, consider the following best practices:

1. **Naming conventions**: Ensure that your queries follow a consistent naming convention for output columns. This will make it easier to understand and reuse queries as views.
2. **Documentation**: Provide clear documentation and comments for your queries, especially when they are intended to be used as views in other queries.
3. **Modularity**: Break down complex queries into smaller, reusable components. This will make your queries more maintainable and easier to understand.
4. **Version control**: If you need to update a query that is being used as a view in other queries, consider creating a new version of the query instead of modifying the existing one. This will help prevent unexpected changes in dependent queries.
5. **Forking** If you use the query of another user as a view in your query, consider forking the query instead of querying it. That way, you will not be affected by changes made to the original query. On the other hand, you will also not be able to benefit from any improvements made to the original query.




