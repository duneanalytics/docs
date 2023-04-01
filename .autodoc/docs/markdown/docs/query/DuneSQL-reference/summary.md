[View code on GitHub](https://dune.com/docs/query/DuneSQL-reference)

The `docs/query/DuneSQL-reference` folder contains a technical guide focused on DuneSQL, a custom-built query engine optimized for blockchain data. This guide is essential for developers and analysts working on the app feature that involves writing SQL queries and understanding the data types supported by DuneSQL.

The `index.md` file provides an overview of DuneSQL, its capabilities, and how it differs from TrinoSQL. It covers the wide array of functions and operators that DuneSQL provides, such as arithmetic, string manipulation, date and time calculations, and more. It also explains that DuneSQL follows the standard SQL syntax and is ANSI-compliant, allowing users to leverage their existing SQL knowledge while working with blockchain data.

For example, a developer working on a feature that requires querying blockchain data can refer to the `index.md` file to understand the basic syntax and capabilities of DuneSQL:

```
SELECT COUNT(*) FROM transactions WHERE block_number > 1000000;
```

The `SQL-language` subfolder contains a comprehensive guide on various aspects of DuneSQL. The `datatypes.md` file provides an in-depth explanation of the various data types used in DuneSQL, such as Boolean, Integer, Floating-point, Fixed-precision, String, Date and time, Structural, Network address, UUID, HyperLogLog, SetDigest, Quantile digest, and T-Digest. This guide is useful for developers who need to understand the properties and functions of each data type when designing database schemas or writing SQL queries.

For example, a developer working on a feature that requires querying blockchain data can refer to the `datatypes.md` file to understand the appropriate data types to use in their queries:

```
SELECT COUNT(*) FROM transactions WHERE to_address = '0x987654321fedcba';
```

The `reserved.md` file lists all the reserved keywords in Trino, along with their status in the SQL standard. This section is crucial for developers to avoid syntax errors when writing SQL queries by quoting reserved keywords.

The `sql-support.md` file offers a detailed guide on using SQL statements in the app, including examples of SELECT, INSERT, UPDATE, and DELETE statements. It also covers the use of parameters in SQL statements for more dynamic and flexible queries and provides tips on handling errors that may occur.

Overall, the guide in this folder is an essential resource for developers and analysts working on the app feature that involves writing SQL queries and understanding the data types supported by DuneSQL. It provides clear explanations, examples, and tips to ensure smooth and efficient querying of blockchain data.
