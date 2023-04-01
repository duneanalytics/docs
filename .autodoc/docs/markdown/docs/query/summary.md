[View code on GitHub](https://dune.com/docs/query)

The `docs/query` folder contains a technical guide focused on DuneSQL, a custom-built query engine optimized for blockchain data analysis. This guide is essential for developers and analysts working on app features that involve writing SQL queries and understanding the data types supported by DuneSQL.

For example, a developer working on a feature that requires querying blockchain data can refer to the `dunesql-changes.md` file to understand the migration changes that occurred on March 2nd, 2023, and how to adjust their queries accordingly. The guide provides examples of queries that need to be adjusted and common errors that users may encounter.

The `index.md` file provides an overview of DuneSQL, its features, and how it differs from TrinoSQL. It covers the wide array of functions and operators that DuneSQL provides, such as arithmetic, string manipulation, date and time calculations, and more. It also explains that DuneSQL follows the standard SQL syntax and is ANSI-compliant, allowing users to leverage their existing SQL knowledge while working with blockchain data.

The `query-a-query.md` file explains how to query a query in DuneSQL, allowing users to create reusable queries, build up complex queries, and reuse queries as views. This feature is useful for creating more complex queries and reusing queries as views. An example query is provided in the guide for reference.

The `storage.md` file provides an overview of the differences and thinking behind the V2 database structure, focusing on the differences between row-oriented and column-oriented databases and how they affect query speed. The guide provides examples of Dune V2 queries and how they work, as well as tips for optimizing query performance.

The `syntax-differences.md` file provides a comprehensive guide for migrating queries from Postgres and Spark SQL to Dune SQL. It is a valuable resource for developers who are new to Dune SQL and need to migrate their queries from other databases.

The `DuneSQL-reference` subfolder contains a comprehensive guide on various aspects of DuneSQL, such as data types, reserved keywords, and SQL statement support. This guide is useful for developers who need to understand the properties and functions of each data type when designing database schemas or writing SQL queries.

Overall, the guide in this folder is an essential resource for developers and analysts working on app features that involve writing SQL queries and understanding the data types supported by DuneSQL. It provides clear explanations, examples, and tips to ensure smooth and efficient querying of blockchain data.
