[View code on GitHub](https://dune.com/docs/data-tables/community/reservoir/token-floor-ask-events.md)

# Token Floor Ask Events

This section of the app technical guide covers the `reservoir.token_floor_ask_events` table, which contains records with information about each NFT token floor ask change. The table includes various columns such as `id`, `kind`, `contract`, `token_id`, `order_id`, `maker`, `price`, `previous_price`, `nonce`, `valid_from`, `valid_until`, `source`, `tx_hash`, `tx_timestamp`, and `created_at`.

The `kind` column specifies the type of event, which can be one of the following: `new-order`, `expiry`, `sale`, `cancel`, `balance-change`, `approval-change`, `bootstrap`, `revalidation`, or `reprice`. The `contract` column specifies the address of the contract associated with the event, while the `token_id` column specifies the ID of the token in the collection. The `order_id` column specifies the associated ask ID, and the `maker` column specifies the wallet address of the ask maker.

The `price` column specifies the associated ask price in native currency, while the `previous_price` column specifies the previous ask price in native currency. The `nonce` column specifies the order nonce of the maker, and the `valid_from` and `valid_until` columns specify the validity start and expiration of the ask. The `source` column specifies the source of the order, such as `opensea.io`. The `tx_hash` column specifies the associated transaction hash, and the `tx_timestamp` column specifies the associated transaction timestamp. Finally, the `created_at` column specifies the timestamp the event was recorded.

This section also includes two query examples that can be found at the specified URLs. These queries can be used to retrieve information from the `reservoir.token_floor_ask_events` table.
## Questions: 
 1. What is the purpose of this table in the context of the dune docs project?
- As a technical guide documentation expert, it is not clear from this table alone what the overall purpose of the dune docs project is, so a blockchain SQL analyst might have this question.

2. What is the meaning of the "kind" column and what are the possible values?
- The "kind" column is described as an event type, but it is not clear what each possible value represents, so a blockchain SQL analyst might have this question.

3. Are there any other tables or data sources that are related to this one and can be used to gain a more complete understanding of NFT token floor asks?
- This table provides information about NFT token floor ask changes, but it is possible that there are other tables or data sources that are related to this one and can provide additional context or insights, so a blockchain SQL analyst might have this question.