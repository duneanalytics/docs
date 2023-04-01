[View code on GitHub](https://dune.com/docs/query/DuneSQL-reference/SQL-statement-syntax/use.md)

# Dune Docs App Technical Guide: USE

## Synopsis

The `USE` command is used to update the session to use a specific catalog and schema. The syntax for using this command is as follows:

``` text
USE catalog.schema
USE schema
```

## Description

The `USE` command is used to specify the catalog and schema that should be used for subsequent queries in the session. If a catalog is not specified, the schema is resolved relative to the current catalog. This command is useful when working with multiple catalogs and schemas, as it allows you to easily switch between them without having to fully qualify table names in subsequent queries.

## Examples

Here are some examples of how to use the `USE` command:

``` sql
USE hive.finance;
```

This command sets the current catalog to `hive` and the current schema to `finance`.

``` sql
USE information_schema;
```

This command sets the current schema to `information_schema`, relative to the current catalog.

Overall, the `USE` command is a useful tool for managing catalogs and schemas in a session, and can help simplify subsequent queries by allowing you to work with unqualified table names.
## Questions: 
 1. What is the purpose of the "USE" command in this app and how does it relate to blockchain technology?
   - The "USE" command updates the session to use a specified catalog and schema. A blockchain SQL analyst might want to know how this command can be used to interact with blockchain data stored in a SQL database.

2. Can multiple catalogs and schemas be used simultaneously with this app?
   - The app technical guide does not provide information on whether multiple catalogs and schemas can be used simultaneously. A blockchain SQL analyst might want to know if this is possible and how it can be achieved.

3. Are there any security considerations to keep in mind when using the "USE" command?
   - The app technical guide does not mention any security considerations related to using the "USE" command. A blockchain SQL analyst might want to know if there are any potential security risks associated with using this command and how to mitigate them.