[View code on GitHub](https://dune.com/docs/query/DuneSQL-reference/SQL-statement-syntax/describe-output.md)

# Dune Docs App Technical Guide

## Describe Output

The `DESCRIBE OUTPUT` statement is used to list the output columns of a prepared statement in the Dune Docs app. This includes the column name (or alias), catalog, schema, table, type, type size in bytes, and a boolean indicating if the column is aliased. 

The `DESCRIBE OUTPUT` statement is useful for debugging and understanding the structure of a prepared statement. It can be used to verify that the output columns of a prepared statement match the expected structure.

The `DESCRIBE OUTPUT` statement takes the following syntax:

``` text
DESCRIBE OUTPUT statement_name
```

Where `statement_name` is the name of the prepared statement to describe.

### Examples

The following examples demonstrate how to use the `DESCRIBE OUTPUT` statement in the Dune Docs app:

#### Example 1

Prepare and describe a query with four output columns:

``` sql
PREPARE my_select1 FROM
SELECT * FROM nation;

DESCRIBE OUTPUT my_select1;
```

This will output the following:

``` text
Column Name | Catalog | Schema | Table  |  Type   | Type Size | Aliased
-------------+---------+--------+--------+---------+-----------+---------
nationkey   | tpch    | sf1    | nation | bigint  |         8 | false
name        | tpch    | sf1    | nation | varchar |         0 | false
regionkey   | tpch    | sf1    | nation | bigint  |         8 | false
comment     | tpch    | sf1    | nation | varchar |         0 | false
(4 rows)
```

#### Example 2

Prepare and describe a query whose output columns are expressions:

``` sql
PREPARE my_select2 FROM
SELECT count(*) as my_count, 1+2 FROM nation;

DESCRIBE OUTPUT my_select2;
```

This will output the following:

``` text
Column Name | Catalog | Schema | Table |  Type  | Type Size | Aliased
-------------+---------+--------+-------+--------+-----------+---------
my_count    |         |        |       | bigint |         8 | true
_col1       |         |        |       | bigint |         8 | false
(2 rows)
```

#### Example 3

Prepare and describe a row count query:

``` sql
PREPARE my_create FROM
CREATE TABLE foo AS SELECT * FROM nation;

DESCRIBE OUTPUT my_create;
```

This will output the following:

``` text
Column Name | Catalog | Schema | Table |  Type  | Type Size | Aliased
-------------+---------+--------+-------+--------+-----------+---------
rows        |         |        |       | bigint |         8 | false
(1 row)
```

## See also

`prepare`{.interpreted-text role="doc"}

The `prepare` statement is used to prepare a SQL statement for execution in the Dune Docs app. It is often used in conjunction with the `DESCRIBE OUTPUT` statement to debug and understand the structure of prepared statements.
## Questions: 
 1. What is the purpose of the `DESCRIBE OUTPUT` statement in the context of a blockchain SQL analyst's work?
- A blockchain SQL analyst might want to know how to use the `DESCRIBE OUTPUT` statement to list the output columns of a prepared statement, including the column name (or alias), catalog, schema, table, type, type size in bytes, and a boolean indicating if the column is aliased.

2. How can a blockchain SQL analyst use the `DESCRIBE OUTPUT` statement to prepare and describe a query with expressions as output columns?
- A blockchain SQL analyst can use the `DESCRIBE OUTPUT` statement to prepare and describe a query with expressions as output columns by specifying the name of the prepared statement that contains the query.

3. What is the relationship between the `DESCRIBE OUTPUT` statement and the `prepare` statement in the context of a blockchain SQL analyst's work?
- The `DESCRIBE OUTPUT` statement is related to the `prepare` statement in that it is used to describe the output columns of a prepared statement that was created using the `prepare` statement.