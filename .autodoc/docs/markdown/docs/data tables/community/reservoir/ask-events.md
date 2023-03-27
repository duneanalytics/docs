[View code on GitHub](https://dune.com/blob/master/data tables\community\reservoir\ask-events.md)

# Ask Events

This section of the app technical guide covers the `reservoir.ask_events` table, which contains records with information about each ask change. The table includes columns such as `id`, `kind`, `contract`, `token_id`, `order_id`, `maker`, `price`, `quantity_remaining`, `valid_from`, `valid_until`, `source`, `tx_hash`, `tx_timestamp`, and `created_at`. 

The `id` column is an internal event ID, while the `kind` column specifies the type of event (e.g. new-order, expiry, sale, cancel, balance-change, approval-change, bootstrap, revalidation, reprice). The `contract` column contains the contract address, and the `token_id` column contains the ID of the token in the collection. The `order_id` column is the associated ask ID, and the `maker` column contains the associated ask maker wallet address. The `price` column contains the associated ask price in native currency, and the `quantity_remaining` column contains the associated ask tokens remaining. The `valid_from` and `valid_until` columns contain the associated ask validity start and expiration, respectively. The `source` column specifies the source of the order (e.g. opensea.io), while the `tx_hash` and `tx_timestamp` columns contain the associated transaction hash and timestamp, respectively. Finally, the `created_at` column contains the timestamp the event was recorded.

This section also includes links to query examples for the `reservoir.ask_events` table, which can be found at [https://dune.com/queries/1302858/2232178](https://dune.com/queries/1302858/2232178) and [https://dune.com/queries/1302863/2232189](https://dune.com/queries/1302863/2232189).

Overall, this section of the app technical guide provides a detailed overview of the `reservoir.ask_events` table and its various columns, as well as links to query examples for further exploration. It is relevant to the data tables section of the project app.
## Questions: 
 1. What is the purpose of the `reservoir.ask_events` table in the context of blockchain and SQL analysis?
- The `reservoir.ask_events` table contains records with information about each ask change, which could be useful for analyzing the behavior of buyers and sellers in a blockchain marketplace.

2. Are there any limitations or constraints on the data that can be queried from this table?
- The app technical guide does not provide information on any limitations or constraints on the data that can be queried from this table.

3. Are there any other tables or data sources that are related to the `reservoir.ask_events` table and could be used for more comprehensive analysis?
- The app technical guide does not provide information on any other related tables or data sources, but a blockchain SQL analyst may want to explore other tables or data sources to gain a more comprehensive understanding of the marketplace behavior.