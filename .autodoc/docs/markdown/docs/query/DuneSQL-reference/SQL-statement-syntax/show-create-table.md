[View code on GitHub](https://dune.com/docs/query/DuneSQL-reference/SQL-statement-syntax/show-create-table.md)

## `SHOW CREATE TABLE`

The `SHOW CREATE TABLE` command is used to display the SQL statement that was used to create a specified table. This command is useful when you need to recreate a table or when you want to see the exact structure of a table. 

### Synopsis

``` text
SHOW CREATE TABLE table_name
```

### Description

The `SHOW CREATE TABLE` command is used to display the SQL statement that was used to create a specified table. This command is useful when you need to recreate a table or when you want to see the exact structure of a table. 

### Examples

The following example shows how to use the `SHOW CREATE TABLE` command to display the SQL statement that was used to create the `orders` table:

``` text
SHOW CREATE TABLE sf1.orders;
```

This will output the following SQL statement:

``` text
CREATE TABLE tpch.sf1.orders (
orderkey bigint,
orderstatus varchar,
totalprice double,
orderdate varchar
)
WITH (
format = 'ORC',
partitioned_by = ARRAY['orderdate']
)
```

### See also

`create-table`{.interpreted-text role="doc"}

This command is useful in the `data-tables` section of the project, where tables are created and managed. It allows users to view the exact SQL statement used to create a table, which can be useful for debugging or recreating tables.
## Questions: 
 1. What is the purpose of the `SHOW CREATE TABLE` command in the context of a blockchain SQL analyst? 
   - A blockchain SQL analyst might want to know how to create tables in a database to store blockchain data, and this command can show them the SQL statement needed to do so.
   
2. Can this command be used with all SQL databases commonly used in blockchain analysis, or are there limitations? 
   - A blockchain SQL analyst might want to know if this command is compatible with the specific SQL database they are using for blockchain analysis, as some databases may have different syntax or limitations.
   
3. Are there any security concerns or best practices to keep in mind when using this command to view SQL statements? 
   - A blockchain SQL analyst might want to know if there are any potential security risks or best practices to follow when using this command to view SQL statements, especially if they are working with sensitive blockchain data.