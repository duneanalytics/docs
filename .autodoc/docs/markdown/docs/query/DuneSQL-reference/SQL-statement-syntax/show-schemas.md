[View code on GitHub](https://dune.com/docs/query/DuneSQL-reference/SQL-statement-syntax/show-schemas.md)

The "Show Schemas" section of the app technical guide covers the syntax and usage of the `SHOW SCHEMAS` command in the Dune Docs project. This command is used to list the schemas in a specified catalog or in the current catalog. The command takes two optional parameters: `FROM catalog` specifies the catalog to list the schemas from, and `LIKE pattern` allows for filtering the results to a desired subset based on a pattern.

The guide provides an example of using the `LIKE` clause to find schemas that have `3` as the third character in their name. The response to this query would be a list of all schemas in the specified catalog (or current catalog if none is specified) that match the given pattern.

Overall, this section of the guide is useful for developers who need to work with database schemas in the Dune Docs project. It provides clear instructions on how to use the `SHOW SCHEMAS` command and includes an example to help illustrate its usage.
## Questions: 
 1. What database management system does this app technical guide apply to?
- The app technical guide does not specify which database management system it applies to.

2. Can this command be used to show schemas in a blockchain database?
- It is unclear from the app technical guide whether this command can be used to show schemas in a blockchain database.

3. Are there any limitations or restrictions on the use of the `LIKE` clause?
- The app technical guide does not provide information on any limitations or restrictions on the use of the `LIKE` clause.