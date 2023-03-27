[View code on GitHub](https://dune.com/blob/master/data tables\community\flashbots\sandwiches.md)

# Sandwiches Table

The `sandwiches` table is a part of the Dune Docs project and contains detailed information about executed sandwiches. The table has ten columns, each with a specific purpose. 

- `created_at`: This column stores the time of the record's creation.
- `block_number`: This column stores the block number.
- `backrun_swap_trace_address`: This column stores the address of the swap in the backrun transaction.
- `backrun_swap_transaction_hash`: This column stores the transaction hash of the backrun transaction of the specified sandwich.
- `frontrun_swap_trace_address`: This column stores the address of the swap in the frontrun transaction.
- `frontrun_swap_transaction_hash`: This column stores the transaction hash of the frontrun transaction of the specified sandwich.
- `id`: This column stores the internal ID of the sandwich.
- `profit_amount`: This column stores the profit amount after the arbitrage.
- `profit_token_address`: This column stores the address of the profit asset.
- `sandwicher_address`: This column stores the address of the sandwicher.
- `timestamp`: This column stores the timestamp of the latest update of the file.

This table is useful for analyzing the performance of executed sandwiches and identifying any issues that may arise during the execution process. For example, if a sandwicher consistently experiences low profits, they may need to adjust their strategy or look for new opportunities. 

Here is an example of how to query the `sandwiches` table:

```
SELECT *
FROM sandwiches
WHERE sandwicher_address = '0x123abc'
```

This query will return all sandwiches executed by the sandwicher with the address `0x123abc`.
## Questions: 
 1. What is the purpose of the "sandwiches" table in the Dune Docs app?
- The "sandwiches" table contains detailed information about executed sandwiches, including block number, transaction hashes, profit amount, and addresses of the sandwicher and profit asset.

2. How is the data in the "sandwiches" table updated?
- The "timestamp" column indicates the latest update of the file, but it is unclear how the data in the table is updated or if it is updated automatically.

3. Is there any connection between the Dune Docs app and blockchain technology?
- The table includes columns for block number and transaction hashes, suggesting that the app may be connected to a blockchain network. However, without further information it is unclear what type of blockchain or how it is being used.