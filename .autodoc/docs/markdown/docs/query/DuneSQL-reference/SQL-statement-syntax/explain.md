[View code on GitHub](https://dune.com/docs/query/DuneSQL-reference/SQL-statement-syntax/explain.md)

The app technical guide covers the usage of the `EXPLAIN` statement in various formats and types to analyze and validate SQL query execution plans. The guide provides a detailed explanation of the `EXPLAIN` statement syntax, options, and descriptions of different plan fragment types.

The guide is divided into the following sections:

1. **Synopsis**: This section provides the syntax for the `EXPLAIN` statement, including the available options for format and type.

2. **Description**: This section explains the purpose of the `EXPLAIN` statement and the different plan fragment types, such as `SINGLE`, `HASH`, `ROUND_ROBIN`, `BROADCAST`, and `SOURCE`.

3. **Examples**: This section contains various examples demonstrating the usage of the `EXPLAIN` statement with different types and formats. The examples include:
   - EXPLAIN (TYPE LOGICAL): Shows the logical execution plan in text format.
   - EXPLAIN (TYPE LOGICAL, FORMAT JSON): Shows the logical execution plan in JSON format.
   - EXPLAIN (TYPE DISTRIBUTED): Shows the distributed execution plan in text format.
   - EXPLAIN (TYPE DISTRIBUTED, FORMAT JSON): Shows the distributed execution plan in JSON format.
   - EXPLAIN (TYPE VALIDATE): Validates the supplied query statement for syntactical and semantic correctness.
   - EXPLAIN (TYPE IO): Shows the input and output details about the accessed objects in JSON format.

4. **See also**: This section provides a reference to the `explain-analyze` documentation for further reading.
## Questions: 
 1. **What are the different output formats supported by the EXPLAIN command?**

   The EXPLAIN command supports three output formats: TEXT, GRAPHVIZ, and JSON. These formats allow users to view the execution plan in different representations, making it easier to understand and analyze the plan.

2. **What are the different types of execution plans that can be generated using the EXPLAIN command?**

   The EXPLAIN command can generate four types of execution plans: LOGICAL, DISTRIBUTED, VALIDATE, and IO. The LOGICAL and DISTRIBUTED plans show the logical and distributed execution plans of a statement, respectively. The VALIDATE plan checks the statement for syntactical and semantic correctness, while the IO plan provides input and output details about the accessed objects in JSON format.

3. **How does the EXPLAIN command represent data distribution in the execution plan?**

   The EXPLAIN command represents data distribution in the execution plan using fragment types. The fragment types include SINGLE, HASH, ROUND_ROBIN, BROADCAST, and SOURCE. These types specify how the fragment is executed by Trino nodes and how the data is distributed between fragments.