[View code on GitHub](https://dune.com/docs/query/DuneSQL-reference/SQL-statement-syntax/describe-input.md)

## `DESCRIBE INPUT`

The `DESCRIBE INPUT` statement is used to list the input parameters of a prepared statement along with the position and type of each parameter. This statement is useful when you need to know the types of the parameters in a prepared statement, especially when some of the parameter types cannot be determined.

The `DESCRIBE INPUT` statement takes the name of the prepared statement as its argument. The output of the statement is a table that shows the position and type of each parameter in the prepared statement. If a parameter type cannot be determined, it will appear as `unknown`.

### Examples

#### Example 1

In this example, we prepare a query with three parameters and then describe the input parameters of the prepared statement using `DESCRIBE INPUT`.

``` sql
PREPARE my_select1 FROM
SELECT ? FROM nation WHERE regionkey = ? AND name < ?;
```

``` sql
DESCRIBE INPUT my_select1;
```

The output of the `DESCRIBE INPUT` statement will be:

``` text
Position | Type
--------------------
       0 | unknown
       1 | bigint
       2 | varchar
(3 rows)
```

This output shows that the prepared statement `my_select1` has three input parameters. The first parameter has an unknown type, while the second parameter is of type `bigint` and the third parameter is of type `varchar`.

#### Example 2

In this example, we prepare a query with no parameters and then describe the input parameters of the prepared statement using `DESCRIBE INPUT`.

``` sql
PREPARE my_select2 FROM
SELECT * FROM nation;
```

``` sql
DESCRIBE INPUT my_select2;
```

The output of the `DESCRIBE INPUT` statement will be:

``` text
Position | Type
-----------------
(0 rows)
```

This output shows that the prepared statement `my_select2` has no input parameters.

### See also

- `PREPARE`: prepares a statement for execution.
## Questions: 
 1. What is the purpose of the `DESCRIBE INPUT` statement in the context of a blockchain SQL database?
- A blockchain SQL analyst might want to know how to use the `DESCRIBE INPUT` statement to list the input parameters of a prepared statement and their types, which can be useful for debugging and optimizing blockchain queries.

2. How does the `DESCRIBE INPUT` statement handle unknown parameter types?
- A blockchain SQL analyst might want to know how the `DESCRIBE INPUT` statement handles unknown parameter types, which are listed as `unknown` in the output.

3. Are there any other related SQL statements or functions that a blockchain SQL analyst should be aware of when working with prepared statements?
- A blockchain SQL analyst might want to know if there are any other related SQL statements or functions that work with prepared statements, such as the `prepare` statement mentioned in the "See also" section.