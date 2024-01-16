---
title: Query Views
description: The "Query View" feature in DuneSQL allows you to use an existing query as a view in another query. This powerful functionality enables you to create reusable queries, build complex queries, and take advantage of existing queries as views.
---

## Overview

The "Query View" feature in DuneSQL allows you to use an existing query as a view in another query. This powerful functionality enables you to create reusable queries, build complex queries, and take advantage of existing queries as views. 

**You can also pass on parameters when querying a query view.**

!!! info
    All upstream queries are executed as functional SQL views, which means that they will be executed every time they are queried. This means there currently is no performance benefit to using the "Query a Query" feature. If you are looking for a performance benefit, consider using [materialized views](materialized-views.md) instead.

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

### Adding Parameters When Using Query Views

You can also pass on parameters when querying a query view. This allows you to use the same query view with different parameters in different queries.

To pass on parameters when querying a query view, you need to use the following syntax:

```sql

Select * from "query_<queryID>(<parameter1>='<value1>', <parameter2>='<value2>', ...)"
```

For example, if you want to use the query with queryID 3256410 as a view in your new query and pass on the parameter `blockchain` with the value `ethereum`, the setup would look like this: 

```sql
--query_3256410, our query to be invoked
Select 
    project,
    block_date,
    sum(amount_usd) as amount_usd
from dex.trades
where blockchain = '{{blockchain}}'
and block_time > now() - interval '7' day 
```
[link to query](https://dune.com/queries/3256410)

```sql
--query_3256401, our query that invokes the query_3256410
Select 
    project,
    block_date,
    amount_usd 
from "query_3256410(blockchain='ethereum')"
```
[link to query](https://dune.com/queries/3256401)

Parameters in the query view are passed on as strings and therefore always need to be wrapped in single quotes. Since we sometimes want to pass a `string` including the single quotes, we need to escape the single quotes in the query view. We can do that by adding a backslash in front of the single quote. Escaping single quotes means that the single quote will be treated as a literal character and not as a string delimiter.

**For example:**

```sql
--query to be invoked
Select 
    project,
    block_date,
    sum(amount_usd) as volume_in_usd
from dex.trades
where blockchain = {{blockchain}}
-- we want to pass a string including the single quotes to this query
```

```sql
--query that invokes the query above
Select 
    project,
    block_date,
    volume_in_usd
from "query_3256410(blockchain='\'ethereum\'')"
--note the escaped single quotes
--this will pass the parameter blockchain with the value 'ethereum'
``` 

The backslash is not needed when passing on a parameter that doesn't need to be wrapped in single quotes on the receiving side, like `integers` or `booleans`.
You can choose to handle this on the query view side or on the query that invokes the query view side. If you wrap your parameter in single quotes on the receiving side, you don't need to escape the single quotes on the query view side. 

**For example:**

```sql
--query_3256410, our query to be invoked
Select 
    project,
    block_date,
    sum(amount_usd) as amount_usd
from dex.trades
where blockchain = '{{blockchain}}'
and block_time > now() - interval '7' day 
--note the single quotes around the parameter blockchain
```

```sql
Select 
    project,
    block_date,
    amount_usd 
from "query_3256410(blockchain='ethereum')"
--since we wrap the parameter blockchain in single quotes on the receiving side, we don't need to escape the single quotes on the query view side
```

The table below shows how different parameter types are passed on when using the "Query view" feature:


| **Parameter Type** | **Syntax** | **Example** |
| --- | --- | --- |
| Literal | `query(tableName='labels.all', whateverKey='lala')` | **Original Query**: select * from {{tableName}} <br> **Macro**: select * from "query_123(tableName='labels.all')" |
| Integer, Bigint | `query(integerKey='1')` | **Original Query**: select {{integerKey}} <br> **Macro**: select * from "query_123(integerKey='1')" |
| Decimal, Double | `query(decimalKey='1.2')` <br> `query(realKey='1.2F')` <br> `query(doubleKey='1.2E0')` | **Original Query**: select {{realKey}} <br> **Macro**: select * from "query_123(realKey='1.2F')" |
| Varchar | `query(varcharKey='\'ethereum\'')` | **Original Query**: select * from labels.all where name = {{varcharKey}} <br> **Macro**: select * from "query_123(varcharKey='\'DEX Trader\'')" |
| Char | `query(charKey='\'a\'')` | **Original Query**: select {{charKey}} <br> **Macro**: select * from "query_123(charKey='\'a\'')" |
| Varbinary | `query(varbinaryKey='0xabcd')` | **Original Query**: select * from labels.all where address = {{varbinaryKey}} <br> **Macro**: select * from "query_123(varbinaryKey='0xabcd')" |
| UINT256 | `query(uint256Key='UINT256 \'1\'')` | **Original Query**: select * from arbitrum.transactions where gas_price = {{uint256Key}} <br> **Macro**: select * from "query_123(uint256Key='uint256 \'1\'')" <br> **Original Query**: select * from arbitrum.transactions where gas_price = uint256 '{{uint256Key}}' <br> **Macro**: select * from "query_123(uint256Key='1')" |
| INT256 | `query(int256Key='INT256 \'-1\'')` | **Original Query**: select * from arbitrum.transactions where gas_price = {{int256Key}} <br> **Macro**: select * from "query_123(int256Key='int256 \'-1\'')" <br> **Original Query**: select * from arbitrum.transactions where gas_price = int256 '{{int256Key}}' <br> **Macro**: select * from "query_123(int256Key='1')" |
| Date, Time, Timestamp | `query(dateKey='2023-01-02')` <br> `query(dateKey='date \'2023-01-02\'')` <br> `query(dateKey='13:45:30 +05:00')` <br> `query(dateKey='time \'13:45:30 +05:00\'')` <br> `query(dateKey='2023-08-24 13:45:30 UTC')` <br> `query(dateKey='timestamp \'2023-08-24 13:45:30 UTC\'')` | **Original Query**: select * from ethereum.blocks where time > {{dateKey}} <br> **Macro**: select * from "query_123(dateKey='timestamp \'2023-08-24\'')" <br> **Original Query**: select * from ethereum.blocks where time > timestamp '{{dateKey}}' <br> **Macro**: select * from "query_123(dateKey='2023-08-24')" |
| Array | `query(arrayKey='array[1,2,3]')` <br> `query(arrayKey='array[uint256 \'1\', uint256 \'2\']')` <br> `query(arrayKey='array[\'these\', \'are\, \'varchar\]')` | **Original Query**: select * from dex_aggregator.trades where trace_address = {{arrayKey}} <br> **Macro**: select * from "query_123(arrayKey='array[1, 2]')" |
| Boolean | `query(booleanKey='true')` | **Original Query**: select * from bitcoin.inputs where is_coinbase = {{booleanKey}} <br> **Macro**: select * from "query_123(booleanKey='false')" |
| Row | `query(rowKey='row(1, uint256 \'1\', \'hi\')')` | **Original Query**: select {{rowKey}} <br> **Macro**: select * from "query_123(rowKey='row(false, 1, uint256 \'1\', \'hi\')')" |
| Map | `query(mapKey='map(array[\'key1\', \'key2\'], array[\'value1\', \'value2\'])')` | **Original Query**: select {{mapKey}} <br> **Macro**: select * from "query_123(mapKey='map(array[\'key1\', \'key2\'], array[\'value1\', \'value2\'])')" |


## Limitations

There are some important limitations and requirements to consider when using the "Query a Query" feature:

1. **Named output columns**: All output columns of the query being queried must be named. For example, you cannot query `select 1` or `select count(*) from ethereum.transactions`, but you can query `select 1 as v` and `select count(*) as total from ethereum.transactions`.
2. **Saved queries**: Only saved queries can be used with the "Query a Query" feature.
3. **Archived queries**: Archived queries cannot be queried.
4. **Dune SQL**: Only queries written in Dune SQL can be queried.
5. **Mixed cases on parameters:** If you pass parameters when querying a query, the parameter key and its values should be lower case (i.e.: `select "query_123(Key=\'VaLue\')"` will not work).
6. **List parameters:** the query you're querying cannot have parameters that use list options from the results of a separate query.

!!! Tip
    Querying private queries is a [premium feature](https://dune.com/pricing) only. You can't query private queries with a free or plus account. 

## Best Practices

When using the "Query View" feature, consider the following best practices:

1. **Naming conventions**: Ensure that your queries follow a consistent naming convention for output columns. This will make it easier to understand and reuse queries as views.
2. **Documentation**: Provide clear documentation and comments for your queries, especially when they are intended to be used as views in other queries.
3. **Modularity**: Break down complex queries into smaller, reusable components. This will make your queries more maintainable and easier to understand.
4. **Version control**: If you need to update a query that is being used as a view in other queries, consider creating a new version of the query instead of modifying the existing one. This will help prevent unexpected changes in dependent queries.
5. **Forking** If you use the query of another user as a view in your query, consider forking the query instead of querying it. That way, you will not be affected by changes made to the **Original Query**. On the other hand, you will also not be able to benefit from any improvements made to the **Original Query**.




