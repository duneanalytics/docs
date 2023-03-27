[View code on GitHub](https://dune.com/blob/master/data tables\community\reservoir\token-floor-ask-events.md)

# Token Floor Ask Events

This section of the app technical guide covers the `reservoir.token_floor_ask_events` table, which contains records with information about each NFT token floor ask change. The table includes columns such as `id`, `kind`, `contract`, `token_id`, `order_id`, `maker`, `price`, `previous_price`, `nonce`, `valid_from`, `valid_until`, `source`, `tx_hash`, `tx_timestamp`, and `created_at`.

The `id` column represents the internal token attribute id, while the `kind` column represents the event type, such as `new-order`, `expiry`, `sale`, `cancel`, `balance-change`, `approval-change`, `bootstrap`, `revalidation`, or `reprice`. The `contract` column contains the contract address, and the `token_id` column contains the id of the token in the collection. The `order_id` column represents the associated Ask id, and the `maker` column represents the associated Ask maker wallet address. The `price` column contains the associated ask price in native currency, while the `previous_price` column contains the previous ask price in native currency. The `nonce` column represents the order nonce of the maker, and the `valid_from` and `valid_until` columns represent the associated ask validity start and expiration, respectively. The `source` column contains the source of the order, such as `opensea.io`, while the `tx_hash` column contains the associated transaction hash, and the `tx_timestamp` column contains the associated transaction timestamp. Finally, the `created_at` column represents the timestamp the event was recorded.

This section also includes two query examples that can be found at the specified URLs. These queries can be used to retrieve information from the `reservoir.token_floor_ask_events` table.

Overall, this section of the app technical guide provides a detailed explanation of the `reservoir.token_floor_ask_events` table and its columns, as well as query examples that can be used to retrieve information from the table.
## Questions: 
 1. What is the purpose of this table in the context of a blockchain application?
- This table contains records of NFT token floor ask changes, which could be useful for analyzing market trends and pricing behavior.

2. Are there any limitations or constraints on the data stored in this table?
- The technical guide does not mention any specific limitations or constraints on the data stored in this table, but it may be important to check the underlying database schema for any such restrictions.

3. How frequently is this table updated and what triggers those updates?
- The technical guide does not provide information on the frequency or triggers for updates to this table, which could be important for understanding the timeliness and accuracy of the data.