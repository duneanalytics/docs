[View code on GitHub](https://dune.com/docs/query/DuneSQL-reference/SQL-statement-syntax/create-materialized-view.md)

# CREATE MATERIALIZED VIEW

## Synopsis

This section provides the syntax for creating a new materialized view. The `CREATE MATERIALIZED VIEW` statement is used to create and validate the definition of a new materialized view. The statement includes the `view_name` and a `select` query. The `refresh-materialized-view` statement is required after the creation to populate the materialized view with data. 

## Description

This section explains the concept of materialized views and how they differ from regular views. Materialized views are a physical manifestation of the query results at the time of refresh. The data is stored and can be referenced by future queries. Queries accessing materialized views are typically faster than retrieving data from a view created with the same query. Any computation, aggregation, and other operation to create the data is performed once during refresh of the materialized views, as compared to each time of accessing the view. Multiple reads of view data over time, or by multiple users, all trigger repeated processing. This is avoided for materialized views.

The section also explains the optional clauses that can be used with the `CREATE MATERIALIZED VIEW` statement. The `OR REPLACE` clause causes the materialized view to be replaced if it already exists rather than raising an error. The `IF NOT EXISTS` clause causes the materialized view only to be created or replaced if it does not exist yet. The `COMMENT` clause causes a `string` comment to be stored with the metadata about the materialized view. The comment is displayed with the `show-create-materialized-view` statement and is available in the table `system.metadata.materialized_view_properties`. The `WITH` clause is used to define properties for the materialized view creation. Separate multiple property/value pairs by commas. The connector uses the properties as input parameters for the materialized view refresh operation. The supported properties are different for each connector and detailed in the SQL support section of the specific connector's documentation.

## Examples

This section provides examples of how to create a materialized view using the `CREATE MATERIALIZED VIEW` statement. The examples include creating a simple materialized view over a table that only includes cancelled orders, creating or replacing a materialized view that summarizes orders across all orders from all customers, creating a materialized view for a catalog using the Iceberg connector, and setting multiple properties.

## See also

This section provides links to related statements that can be used with the `CREATE MATERIALIZED VIEW` statement. The related statements include `drop-materialized-view`, `show-create-materialized-view`, and `refresh-materialized-view`.
## Questions: 
 1. What is the purpose of a materialized view in the context of a blockchain SQL database?
- A blockchain SQL analyst might want to know how materialized views can be used to improve query performance and reduce repeated processing of data.

2. How does the `refresh-materialized-view` statement work and when should it be used?
- A blockchain SQL analyst might want to know more about the process of refreshing a materialized view and how it ensures that the view stays in sync with the source tables.

3. What are the supported properties for creating a materialized view using the Iceberg connector?
- A blockchain SQL analyst might want to know more about the specific properties that can be defined when creating a materialized view using the Iceberg connector, and how they can be used to optimize performance.