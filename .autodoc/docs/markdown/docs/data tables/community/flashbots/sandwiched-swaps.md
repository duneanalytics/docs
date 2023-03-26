[View code on GitHub](https://dune.com/blob/master/data tables\community\flashbots\sandwiched-swaps.md)

# Sandwiched Swaps

This section of the app technical guide covers the `flashbots.sandwiched_swaps` table, which contains additional data about one or more swaps that were sandwiched with a corresponding sandwich in the database. The table includes columns such as `created_at`, `block_number`, `sandwich_id`, `trace_address`, `transaction_hash`, and `timestamp`.

The `created_at` column indicates the time of the record's creation, while the `block_number` column shows the block number of the swap. The `sandwich_id` column contains the internal ID of the sandwiched swap, and the `trace_address` column shows the trace pattern related to the position of the swap in the chain of all swaps related to the arbitrage trade. The `transaction_hash` column contains the transaction hash, and the `timestamp` column shows the timestamp of the latest update of the file.

Query examples for this table can be found in the file located at `dune docs/app/query/sandwiched_swaps.sql`. These examples demonstrate how to retrieve data from the `flashbots.sandwiched_swaps` table using SQL queries.

Overall, this section of the app technical guide provides information on how to work with the `flashbots.sandwiched_swaps` table in the Dune Docs app. It covers the purpose of the table and the columns it contains, as well as providing examples of how to query the table.
## Questions: 
 1. What is the purpose of the sandwiched_swaps table in the context of blockchain and SQL analysis?
- A blockchain SQL analyst might want to know how the sandwiched_swaps table fits into the overall data analysis process and what insights it can provide about swaps and arbitrage trades.

2. Are there any limitations or potential issues with the data in the sandwiched_swaps table?
- A blockchain SQL analyst might want to know if there are any data quality issues or limitations that could affect the accuracy of their analysis.

3. How frequently is the sandwiched_swaps table updated and what is the source of the data?
- A blockchain SQL analyst might want to know how often they can expect new data to be added to the table and where that data is coming from in order to better understand the timeliness and reliability of the information.