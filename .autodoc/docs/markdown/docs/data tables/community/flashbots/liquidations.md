[View code on GitHub](https://dune.com/blob/master/data tables\community\flashbots\liquidations.md)

# Liquidations

This section of the app technical guide covers the `flashbots.liquidations` table, which contains details related to executed liquidations. Liquidation is a Miner Extractable Value (MEV) strategy. MEV refers to the value that miners can extract from the blockchain by reordering, censoring, or including transactions in blocks. 

The table contains the following columns:

- `created_at`: Time of the record's creation.
- `transaction_hash`: Transaction hash.
- `trace_address`: Trace pattern related to the position of the transaction in the chain of all transactions related to the MEV trade.
- `debt_token_address`: Underlying token address of the debt to pay.
- `received_amount`: Amount received from the liquidation.
- `protocol`: Protocol name.
- `liquidated_user`: Address of the liquidated user.
- `liquidator_user`: Address of the liquidator user.
- `received_token_address`: Address of the received asset.
- `block_number`: Block number.
- `debt_purchase_amount`: Amount of purchased debt.
- `timestamp`: Timestamp of the latest update of the file.

The guide provides a query example for the `flashbots.liquidations` table. The query is called "Liquidations by Protocol" and can be found at [https://dune.com/queries/625715/1166880](https://dune.com/queries/625715/1166880). 

This section of the app technical guide is relevant to the `app` folder of the project, as it provides information on the `flashbots.liquidations` table, which is likely used in the app's interface to display liquidation data to users.
## Questions: 
 1. What is the purpose of the liquidations table in the context of blockchain and how is it related to MEV (Miner Extractable Value)? 
- The liquidations table contains details related to executed liquidations, which is another MEV strategy. It shows the underlying token address of the debt to pay, amount received from the liquidation, and other relevant information.

2. Are there any specific protocols or blockchain networks that this app technical guide is designed for? 
- The app technical guide does not specify any particular protocols or blockchain networks. However, it does provide a query example for liquidations by protocol using Dune Analytics.

3. How frequently is the liquidations table updated and what triggers the updates? 
- The app technical guide states that the timestamp column shows the latest update of the file, but it does not provide information on how frequently the table is updated or what triggers the updates.