[View code on GitHub](https://dune.com/docs/query/DuneSQL-reference/SQL-statement-syntax/create-view.md)

# CREATE VIEW

The `CREATE VIEW` command is used to create a new view of a `SELECT` query. A view is a logical table that can be referenced by future queries. Views do not contain any data. Instead, the query stored by the view is executed every time the view is referenced by another query. 

The optional `OR REPLACE` clause causes the view to be replaced if it already exists rather than raising an error. 

The `SECURITY` clause specifies the security mode of the view. In the default `DEFINER` security mode, tables referenced in the view are accessed using the permissions of the view owner (the *creator* or *definer* of the view) rather than the user executing the query. This allows providing restricted access to the underlying tables, for which the user may not be allowed to access directly. In the `INVOKER` security mode, tables referenced in the view are accessed using the permissions of the user executing the query (the *invoker* of the view). A view created in this mode is simply a stored query. Regardless of the security mode, the `current_user` function will always return the user executing the query and thus may be used within views to filter out rows or otherwise restrict access.

The `COMMENT` clause is used to add a comment to the view. 

The `AS` keyword is used to specify the query that defines the view. 

The `EXAMPLES` section provides examples of how to create views. 

The `SEE ALSO` section provides links to related commands such as `DROP VIEW` and `SHOW CREATE VIEW`. 

Overall, this guide covers the `CREATE VIEW` command, which is used to create a new view of a `SELECT` query. It explains how to specify the security mode of the view, add a comment to the view, and provides examples of how to create views. This guide is relevant to the `API` section of the `dune docs` project, which involves creating and managing views for the application.
## Questions: 
 1. What is the purpose of the `CREATE VIEW` command in the context of a blockchain SQL database?
- Answer: A blockchain SQL analyst might want to know how the `CREATE VIEW` command can be used to create logical tables that can be referenced by future queries in order to summarize or filter blockchain data.

2. How does the `DEFINER` security mode work, and what implications does it have for blockchain data access?
- Answer: A blockchain SQL analyst might want to know how the `DEFINER` security mode allows tables referenced in the view to be accessed using the permissions of the view owner, which could be useful for providing restricted access to blockchain data.

3. Are there any limitations or best practices for using the `CREATE VIEW` command in the context of a blockchain SQL database?
- Answer: A blockchain SQL analyst might want to know if there are any limitations or best practices for using the `CREATE VIEW` command in order to optimize performance or avoid potential security risks when working with blockchain data.