[View code on GitHub](https://dune.com/docs/query/DuneSQL-reference/SQL-statement-syntax/alter-materialized-view.md)

# ALTER MATERIALIZED VIEW

## Synopsis

This section provides a brief overview of the `ALTER MATERIALIZED VIEW` command. The command is used to rename an existing materialized view. The syntax for the command is as follows:

``` text
ALTER MATERIALIZED VIEW [ IF EXISTS ] name RENAME TO new_name
ALTER MATERIALIZED VIEW name SET PROPERTIES property_name = expression [, ...]
```

## Description

This section provides a detailed explanation of the `ALTER MATERIALIZED VIEW` command. The command is used to change the name of an existing materialized view. The optional `IF EXISTS` clause suppresses the error if the materialized view does not exist. However, the error is not suppressed if the materialized view does not exist, but a table or view with the given name exists.

### SET PROPERTIES

This section explains the `SET PROPERTIES` statement that can be used with the `ALTER MATERIALIZED VIEW` command. The `ALTER MATERIALIZED VIEW SET PROPERTIES` statement followed by some number of `property_name` and `expression` pairs applies the specified properties and values to a materialized view. Omitting an already-set property from this statement leaves that property unchanged in the materialized view. A property in a `SET PROPERTIES` statement can be set to `DEFAULT`, which reverts its value back to the default in that materialized view. However, support for `ALTER MATERIALIZED VIEW SET PROPERTIES` varies between connectors. Refer to the connector documentation for more details.

## Examples

This section provides examples of how to use the `ALTER MATERIALIZED VIEW` command. The examples include:

- Renaming a materialized view `people` to `users` in the current schema
- Renaming a materialized view `people` to `users`, if materialized view `people` exists in the current catalog and schema
- Setting view properties (`x = y`) in materialized view `people`
- Setting multiple view properties (`foo = 123` and `foo bar = 456`) in materialized view `people`
- Setting view property `x` to its default value in materialized view `people`

## See also

This section provides links to related commands that can be used with the `ALTER MATERIALIZED VIEW` command. The related commands include:

- `create-materialized-view`
- `refresh-materialized-view`
- `drop-materialized-view`
## Questions: 
 1. What is the purpose of the `ALTER MATERIALIZED VIEW` statement in this app? 
- The `ALTER MATERIALIZED VIEW` statement is used to change the name of an existing materialized view.

2. How does the `SET PROPERTIES` statement work in this app? 
- The `SET PROPERTIES` statement followed by some number of `property_name` and `expression` pairs applies the specified properties and values to a materialized view. Ommitting an already-set property from this statement leaves that property unchanged in the materialized view.

3. Is support for `ALTER MATERIALIZED VIEW SET PROPERTIES` consistent across all connectors? 
- No, support for `ALTER MATERIALIZED VIEW SET PROPERTIES` varies between connectors. It is recommended to refer to the connector documentation for more details.