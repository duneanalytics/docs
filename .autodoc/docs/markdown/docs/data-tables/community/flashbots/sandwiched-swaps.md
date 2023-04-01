[View code on GitHub](https://dune.com/docs/data-tables/community/flashbots/sandwiched-swaps.md)

# Sandwiched Swaps

The Sandwiched Swaps section of the Dune Docs project focuses on the `flashbots.sandwiched_swaps` table, which contains additional data about one or more swaps that were sandwiched with a corresponding sandwich in the database. This section provides a detailed explanation of the columns in the table and their respective data types.

The `created_at` column contains the time of the record's creation, while the `block_number` column contains the block number of the transaction. The `sandwich_id` column contains the internal ID of the sandwiched swap, and the `trace_address` column contains the trace pattern related to the position of the swap in the chain of all swaps related to the arbitrage trade. Finally, the `transaction_hash` column contains the transaction hash, and the `timestamp` column contains the timestamp of the latest update of the file.

This section also provides query examples for the `flashbots.sandwiched_swaps` table, which can be used as a reference for developers working on the Dune Docs project. The query examples include the column name, data type, and description of each column in the table.

Overall, the Sandwiched Swaps section of the Dune Docs project provides a comprehensive guide to the `flashbots.sandwiched_swaps` table, including its purpose, columns, and query examples. This information is essential for developers working on the Dune Docs project to understand the structure and functionality of the table and to use it effectively in their work.
## Questions: 
 1. What is the purpose of the sandwiched_swaps table in the context of blockchain and SQL analysis?
- A blockchain SQL analyst might want to know how the sandwiched_swaps table fits into the overall data schema and how it can be used to analyze arbitrage trades involving swaps.

2. Are there any limitations or constraints on the data that can be queried from the sandwiched_swaps table?
- A blockchain SQL analyst might want to know if there are any restrictions on the types of queries that can be run on the sandwiched_swaps table, such as limitations on the time range or block numbers that can be queried.

3. How frequently is the sandwiched_swaps table updated and what triggers these updates?
- A blockchain SQL analyst might want to know how often the sandwiched_swaps table is updated and what events trigger these updates, such as new blocks being added to the blockchain or new transactions being processed.