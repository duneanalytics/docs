[View code on GitHub](https://dune.com/docs/data-tables/community/flashbots/sandwiches.md)

# Sandwiches Table

The `sandwiches` table is a part of the Dune Docs project and contains detailed information about executed sandwiches. The table consists of the following columns:

- `created_at`: This column contains the time of the record's creation.
- `block_number`: This column contains the block number.
- `backrun_swap_trace_address`: This column contains the address of the swap in the backrun transaction.
- `backrun_swap_transaction_hash`: This column contains the transaction hash of the backrun transaction of the specified sandwich.
- `frontrun_swap_trace_address`: This column contains the address of the swap in the frontrun transaction.
- `frontrun_swap_transaction_hash`: This column contains the transaction hash of the frontrun transaction of the specified sandwich.
- `id`: This column contains the internal id of the sandwich.
- `profit_amount`: This column contains the profit amount after the arbitrage.
- `profit_token_address`: This column contains the address of the profit asset.
- `sandwicher_address`: This column contains the address of the sandwicher.
- `timestamp`: This column contains the timestamp of the latest update of the file.

The `sandwiches` table is used to keep track of executed sandwiches and their details. For example, it can be used to analyze the performance of the sandwicher and the profitability of the arbitrage. 

Here is an example of how the `sandwiches` table can be queried:

```
SELECT *
FROM sandwiches
WHERE sandwicher_address = '0x1234567890abcdef'
```

This query will return all the sandwiches executed by the sandwicher with the address `0x1234567890abcdef`.
## Questions: 
 1. What is the purpose of the "sandwiches" table in the Dune Docs app?
- The "sandwiches" table contains detailed information about executed sandwiches, including the time of record creation, block number, swap addresses and transaction hashes, profit amount and token address, sandwicher address, and timestamp of the latest update of the file.

2. How is the data in the "sandwiches" table stored and accessed?
- The data in the "sandwiches" table is stored in columns with corresponding data types and descriptions, and can be accessed through SQL queries.

3. Are there any limitations or potential issues with using SQL to analyze the data in the "sandwiches" table?
- It is unclear from the provided technical guide whether there are any limitations or potential issues with using SQL to analyze the data in the "sandwiches" table. A blockchain SQL analyst may need to consult additional documentation or perform further testing to determine any such limitations or issues.