[View code on GitHub](https://dune.com/docs/query/DuneSQL-reference/SQL-statement-syntax/show-create-materialized-view.md)

The `SHOW CREATE MATERIALIZED VIEW` section of the app technical guide covers the SQL command used to display the SQL statement that creates a specified materialized view in the app. The `view_name` parameter specifies the name of the materialized view for which the SQL statement is to be displayed. This command is useful for developers who want to view the SQL statement used to create a materialized view for debugging or optimization purposes.

The `See also` section provides links to related commands that are used to create, drop, and refresh materialized views. The `create-materialized-view` command is used to create a new materialized view, while the `drop-materialized-view` command is used to delete an existing materialized view. The `refresh-materialized-view` command is used to update the data in a materialized view with the latest data from the underlying tables.

An example of how this command can be used is as follows:

``` text
SHOW CREATE MATERIALIZED VIEW sales_by_region;
```

This command would display the SQL statement used to create the `sales_by_region` materialized view in the app. Developers can use this information to optimize the performance of the materialized view or to troubleshoot any issues that may arise. Overall, this section of the app technical guide provides developers with a useful tool for working with materialized views in the app.
## Questions: 
 1. What is the purpose of the `SHOW CREATE MATERIALIZED VIEW` command in the context of a blockchain SQL database?
- The blockchain SQL analyst might want to know how this command can be used to retrieve the SQL statement that creates a specific materialized view in the database.

2. How does the `create-materialized-view` command mentioned in the `See also` section relate to the `SHOW CREATE MATERIALIZED VIEW` command?
- The analyst might want to know how the `create-materialized-view` command can be used to create a new materialized view, and how it differs from the `SHOW CREATE MATERIALIZED VIEW` command which is used to retrieve the SQL statement that creates an existing materialized view.

3. Can the `SHOW CREATE MATERIALIZED VIEW` command be used to modify or update an existing materialized view?
- The analyst might want to know if this command can be used to make changes to an existing materialized view, or if it is only used to retrieve the SQL statement that creates the view.