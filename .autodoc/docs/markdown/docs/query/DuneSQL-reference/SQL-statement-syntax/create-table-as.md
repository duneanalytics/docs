[View code on GitHub](https://dune.com/docs/query/DuneSQL-reference/SQL-statement-syntax/create-table-as.md)

# CREATE TABLE AS

## Synopsis

The `CREATE TABLE AS` statement is used to create a new table that contains the result of a `SELECT` query. This statement can be used to create a new table with or without data. 

## Description

This section of the app technical guide provides a detailed explanation of the `CREATE TABLE AS` statement. It explains how to create a new table with the results of a `SELECT` query and how to set properties on the newly created table. 

The guide explains that the `CREATE TABLE AS` statement can be used to create a new table with the results of a `SELECT` query. It also explains that the `CREATE TABLE` statement can be used to create an empty table. The guide also explains that the `IF NOT EXISTS` clause can be used to suppress the error if the table already exists. 

The guide also explains that the `WITH` clause can be used to set properties on the newly created table. It provides an example of how to list all available table properties using a query. 

## Examples

This section of the app technical guide provides examples of how to use the `CREATE TABLE AS` statement. It provides examples of how to create a new table with the results of a `SELECT` query and how to set properties on the newly created table. 

The examples show how to create a new table with the results of a `SELECT` query and how to specify column names for the new table. The examples also show how to create a new table that summarizes data from an existing table. 

The examples also show how to create a new table if it does not already exist and how to create an empty table with the same schema as an existing table. 

## See also

This section of the app technical guide provides links to related statements that are used in conjunction with the `CREATE TABLE AS` statement. It provides links to the `CREATE TABLE` statement and the `SELECT` statement.
## Questions: 
 1. What is the purpose of the `WITH` clause in the `CREATE TABLE AS` statement?
   
   The `WITH` clause in the `CREATE TABLE AS` statement is used to set properties on the newly created table. 

2. How can a blockchain SQL analyst list all available table properties?
   
   A blockchain SQL analyst can list all available table properties by running the following query: `SELECT * FROM system.metadata.table_properties`.

3. Can the `CREATE TABLE AS` statement be used to create an empty table?
   
   No, the `CREATE TABLE AS` statement is used to create a new table containing the result of a `SELECT` query. To create an empty table, the `CREATE TABLE` statement should be used.