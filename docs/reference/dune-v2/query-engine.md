---
title: V2 Query Engines
description: Dune V2 uses Spark and Dune SQL query engines. Learn how they work here!
--- 

With Dune V2 we’re moving away from a [PostgreSQL](https://www.postgresql.org/) query engine to:

1. Spark SQL - [Apache Spark](https://www.databricks.com/glossary/what-is-apache-spark) hosted on [Databricks](https://docs.databricks.com/getting-started/introduction/index.html).
2. Dune SQL - A self hosted instance of [Trino](https://trino.io/)(**currently in alpha**). 

## Syntax and operator differences

The syntax and keyword operator differences between Postgres, Spark, and Dune SQL are quite minimal, however there are a few to be aware of.

!!! warning
    **Dune SQL is still in alpha!** If you find any other changes in Spark or Dune SQL that are important to note, please feel free to [submit a PR to this docs page on GitHub](https://github.com/duneanalytics/docs/edit/master/docs/reference/dune-v2/query-engine.md) or let us know in #dune-sql.


| **Description** | **V1 - PostgreSQL** | **V2 - Dune SQL** | **V2 - Spark SQL** |
| --- | --- | --- | --- |
| **bytea2numeric does not exist in Spark.** | bytea2numeric(bytea) | bytea2numeric(string) | bytea2numeric_v2(string) |
| **0 vs 1 array based indexing** | 1 indexed | 1 indexed | 0 indexed |
| **Implicit type conversions between character and numeric types** | Available | [Not available](https://trino.io/docs/current/functions/conversion.html) | Available |
| **bytea vs string for address, tx hash, etc…** | \\x2a7d..<br><br>(bytea) | <depending on [bytearray outcome](https://docs.google.com/document/d/1X47-aJs6Yw0h-HZD9O2q1Hs6H1yGZZfOM2E47sPh05M/edit#heading=h.wz929gyolmil)> | 0x2a7d...<br><br>(string) |
| **Addresses (strings) are lower case in dune v2** | \\x2A7D...(bytea)<br><br>Works in Postgres | <depending on [bytearray outcome](https://docs.google.com/document/d/1X47-aJs6Yw0h-HZD9O2q1Hs6H1yGZZfOM2E47sPh05M/edit#heading=h.wz929gyolmil)> | 0x2a7d... (string)<br><br>Has to be lowercase in Spark.<br><br>Can be done via lower('0x2A7D...'). |
| **Selecting keyword columns is different** | "from" | "from" | \`from\` |
| **Alias naming is different** | as "daily active users" | as "daily active users" | as \`daily active user\` |
| **Exponentiation notation** | x/10^y or x * 1e123 | x\*power(10,y), or x \* 1e123 | x\*power(10,y) or x\*1e123 |
| **Interval argument has different syntax** | Interval '1day' | Interval '1' day | Interval '1 day' |
| **Generate_series () is now sequence ()** | generate\_series('2022-05-15', CURRENT\_DATE, '1 day') | values(sequence(cast('2022-01-01' as date) - interval '7' day,cast('2022-02-01' as date),interval '1' day))<br><br>Has a 10000 values limit. | explode(sequence(to\_date('2022-01-01'), to\_date('2022-02-01'), interval 1 day)) |
| **Decimals are no longer in prices.usd** | Don’t use<br><br>prices.usd decimals | Replace by<br><br>tokens_blockchain.erc20.decimals | Replace by prices.tokens decimals |
| **Define NULL array** | NULL::integer\[\] | CAST(NULL AS ARRAY&lt;int&gt;)) | CAST(NULL AS ARRAY&lt;int&gt;)) |
| **encoding strings to hex** | encode(string, 'hex') | hex(string)<br><br>*available soon | hex(string) |
| **Get json object**<br><br>**differences** | ("takerOutputUpdate"-><br><br>'deltaWei'->'value')<br><br>decode(substring(("addressSet"->'baseAsset')::TEXT, 4,40), 'hex') | json\_query(json\_query(takerOutputUpdate, 'lax $.deltaWei' omit quotes), 'lax $.value') | get\_json\_object(get\_json\_object(takerOutputUpdate,'\\(.deltaWei'),'\\).value')<br><br>'0x' |
| **Group by an alias** | SELECT<br><br>date\_trunc('hour',evt\_block_time) as col1, COUNT(*)<br><br>FROM erc721\_ethereum.evt\_Transfer<br><br>GROUP BY col1 | GROUP BY date\_trunc('hour',evt\_block_time)<br><br>….Or:<br><br>GROUP BY 1, 2 | Same as Postgres |
| **Explicit date/time casting** | '2021-08-08 17:00'::timestamp | cast('2021-08-08 17:00' as timestamp)<br><br>Or, timestamp '2021-08-08 17:00'<br><br>There are [many helper functions for casting to date/time types](https://trino.io/docs/current/functions/datetime.html?highlight=date), such as date(‘2022-01-01’) | cast('2021-08-08 17:00' as timestamp) |
| **Checking if an item exists in an arrary** | value = ANY (array) | contains(array,value) | array_contains(array, value) |
| **Explode** | SELECT unnest(array) FROM table | SELECT vals.val FROM table1, unnest(arrayFromTable1) as vals(val)<br><br>you have to use \`unnest\` with a \`cross join\`, as described in this [blog post](https://theleftjoin.com/how-to-explode-arrays-with-presto/). | SELECT explode(array) FROM table |
| **Median** | PERCENTILE_CONT(0.5) WITHIN GROUP(ORDER BY x) | approx_percentile(x, 0.5) | PERCENTILE_CONT(0.5) WITHIN GROUP(ORDER BY x) |
| **Using “is True/False”** | X is true | X = true | X is true |

## Other questions and feedback

As ever, Google is a great friend in answering your SQL questions.

With Dune V2, instead of googling “PGSQL median”, you should now google “Spark SQL median” (for Spark SQL) or “Trino SQL median” (for Dune SQL). 

Both also have well documented index of built in functions on their website:

* [Spark - Spark SQL Language Reference](https://spark.apache.org/docs/latest/sql-programming-guide.html)
* [Trino - Functions and Operators](https://trino.io/docs/current/functions.html)

Our #dune-sql Discord channel is the best place to get help from our team and Wizard community when Google fails you.

As you come across issues or identify areas of improvement, please send us an email at [dunesql-feedback@dune.com](mailto:dunesql-feedback@dune.com) and we’ll work with you to update and optimize!
