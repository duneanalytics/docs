---
title: Query Views
description: The "Query View" feature in DuneSQL allows you to use an existing query as a view in another query. This powerful functionality enables you to create reusable queries, build complex queries, and take advantage of existing queries as views.
---

## Overview

The "Query View" feature in DuneSQL allows you to use an existing query as a view in another query. This powerful functionality enables you to create reusable queries, build complex queries, and take advantage of existing queries as views. 

**You can also pass on parameters when querying a query view.**

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

### Adding parameters

The table below shows the syntax for passing parameters to different types. The parameters need to be named.

For varchar, uint256, int256 and datetime parameters, you should use single quotes wrapping the params on the base query. So '{{some_param}}' in the base query.

| **Parameter Type** | **Syntax** | **Example** |
| --- | --- | --- |
| Literal | `query(tableName='labels.all', whateverKey='lala')` | Original Query: select * from {{tableName}} <br> Macro: select * from "query_123(tableName='labels.all')" |
| Integer, Bigint | `query(integerKey='1')` | Original Query: select {{integerKey}} <br> Macro: select * from "query_123(integerKey='1')" |
| Decimal, Double | `query(decimalKey='1.2')` <br> `query(realKey='1.2F')` <br> `query(doubleKey='1.2E0')` | Original Query: select {{realKey}} <br> Macro: select * from "query_123(realKey='1.2F')" |
| Varchar | `query(varcharKey='\'ethereum\'')` | Original Query: select * from labels.all where name = {{varcharKey}} <br> Macro: select * from "query_123(varcharKey='\'DEX Trader\'')" |
| Char | `query(charKey='\'a\'')` | Original Query: select {{charKey}} <br> Macro: select * from "query_123(charKey='\'a\'')" |
| Varbinary | `query(varbinaryKey='0xabcd')` | Original Query: select * from labels.all where address = {{varbinaryKey}} <br> Macro: select * from "query_123(varbinaryKey='0xabcd')" |
| UINT256 | `query(uint256Key='UINT256 \'1\'')` | Original Query: select * from arbitrum.transactions where gas_price = {{uint256Key}} <br> Macro: select * from "query_123(uint256Key='uint256 \'1\'')" <br> Original Query: select * from arbitrum.transactions where gas_price = uint256 '{{uint256Key}}' <br> Macro: select * from "query_123(uint256Key='1')" |
| INT256 | `query(int256Key='INT256 \'-1\'')` | Original Query: select * from arbitrum.transactions where gas_price = {{int256Key}} <br> Macro: select * from "query_123(int256Key='int256 \'-1\'')" <br> Original Query: select * from arbitrum.transactions where gas_price = int256 '{{int256Key}}' <br> Macro: select * from "query_123(int256Key='1')" |
| Date, Time, Timestamp | `query(dateKey='2023-01-02')` <br> `query(dateKey='date \'2023-01-02\'')` <br> `query(dateKey='13:45:30 +05:00')` <br> `query(dateKey='time \'13:45:30 +05:00\'')` <br> `query(dateKey='2023-08-24 13:45:30 UTC')` <br> `query(dateKey='timestamp \'2023-08-24 13:45:30 UTC\'')` | Original Query: select * from ethereum.blocks where time > {{dateKey}} <br> Macro: select * from "query_123(dateKey='timestamp \'2023-08-24\'')" <br> Original Query: select * from ethereum.blocks where time > timestamp '{{dateKey}}' <br> Macro: select * from "query_123(dateKey='2023-08-24')" |
| Array | `query(arrayKey='array[1,2,3]')` <br> `query(arrayKey='array[uint256 \'1\', uint256 \'2\']')` <br> `query(arrayKey='array[\'these\', \'are\, \'varchar\]')` | Original Query: select * from dex_aggregator.trades where trace_address = {{arrayKey}} <br> Macro: select * from "query_123(arrayKey='array[1, 2]')" |
| Boolean | `query(booleanKey='true')` | Original Query: select * from bitcoin.inputs where is_coinbase = {{booleanKey}} <br> Macro: select * from "query_123(booleanKey='false')" |
| Row | `query(rowKey='row(1, uint256 \'1\', \'hi\')')` | Original Query: select {{rowKey}} <br> Macro: select * from "query_123(rowKey='row(false, 1, uint256 \'1\', \'hi\')')" |
| Map | `query(mapKey='map(array[\'key1\', \'key2\'], array[\'value1\', \'value2\'])')` | Original Query: select {{mapKey}} <br> Macro: select * from "query_123(mapKey='map(array[\'key1\', \'key2\'], array[\'value1\', \'value2\'])')" |


## Limitations

There are some important limitations and requirements to consider when using the "Query a Query" feature:

1. **Named output columns**: All output columns of the query being queried must be named. For example, you cannot query `select 1` or `select count(*) from ethereum.transactions`, but you can query `select 1 as v` and `select count(*) as total from ethereum.transactions`.
2. **Saved queries**: Only saved queries can be used with the "Query a Query" feature.
3. **Archived queries**: Archived queries cannot be queried.
4. **Dune SQL**: Only queries written in Dune SQL can be queried.

!!! Tip
    Querying private queries is a [premium feature](https://dune.com/pricing) only. You can't query private queries with a free or plus account. 

## Best Practices

When using the "Query View" feature, consider the following best practices:

1. **Naming conventions**: Ensure that your queries follow a consistent naming convention for output columns. This will make it easier to understand and reuse queries as views.
2. **Documentation**: Provide clear documentation and comments for your queries, especially when they are intended to be used as views in other queries.
3. **Modularity**: Break down complex queries into smaller, reusable components. This will make your queries more maintainable and easier to understand.
4. **Version control**: If you need to update a query that is being used as a view in other queries, consider creating a new version of the query instead of modifying the existing one. This will help prevent unexpected changes in dependent queries.
5. **Forking** If you use the query of another user as a view in your query, consider forking the query instead of querying it. That way, you will not be affected by changes made to the original query. On the other hand, you will also not be able to benefit from any improvements made to the original query.




