[View code on GitHub](https://dune.com/blob/master/data tables\raw\solana\vote-transactions.md)

# Vote Transactions

This section of the app technical guide covers the `Solana.vote_transactions` table, which contains the full set of vote transactions that are submitted by validators to vote on a block. This table can be joined with the non-vote transactions table to get a full breakdown of all transactions. The schema of this table is the same as the main transactions table.

The guide provides a detailed description of each column in the `Solana.vote_transactions` table, including the column name, column type, and description. Some of the key columns include:

- `block_slot`: This column contains the block's slot index in the ledger.
- `block_time`: This column contains the estimated time the block was produced.
- `fee`: This column contains the fee charged for the transaction.
- `success`: This column indicates whether the transaction was valid and committed.
- `instructions`: This column contains the instructions to execute in order.
- `signatures`: This column contains a list of base-58 encoded signatures applied to the transaction.

The guide also provides an example query that demonstrates how to use the `Solana.vote_transactions` table. The query shows how to retrieve Solana transactions from the past 30 days using Dune Analytics.

Overall, this section of the app technical guide provides a comprehensive overview of the `Solana.vote_transactions` table and its columns. It is a useful resource for developers who are working with Solana transactions and need to understand the data contained in this table.
## Questions: 
 1. What is the purpose of the dune docs app and how does it relate to blockchain technology?
- The app technical guide provided does not give information on the overall purpose of the dune docs app, so a blockchain SQL analyst may want to know more about how the app relates to blockchain technology and what specific features it offers for blockchain analysis.

2. How does the Solana.vote_transactions table differ from other transaction tables in the app?
- The app technical guide provides information on the Solana.vote_transactions table, but it does not explain how it differs from other transaction tables in the app. A blockchain SQL analyst may want to know this information in order to better understand how to use the table for analysis.

3. Are there any limitations or known issues with the app's data collection or analysis capabilities?
- The app technical guide does not provide any information on limitations or known issues with the app's data collection or analysis capabilities. A blockchain SQL analyst may want to know this information in order to assess the reliability and accuracy of the data provided by the app.