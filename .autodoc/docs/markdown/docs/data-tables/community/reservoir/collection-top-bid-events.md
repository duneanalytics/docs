[View code on GitHub](https://dune.com/docs/data-tables/community/reservoir/collection-top-bid-events.md)

# Collection Top Bid Events

The `collection_top_bid_events` table is a part of the Dune Docs project and contains records with information about each collection top bid change. This table is located in the `data-tables` folder of the project.

The table has several columns, including `id`, `kind`, `collection_id`, `contract`, `token_id`, `order_id`, `maker`, `price`, `previous_price`, `valid_until`, `source`, `tx_hash`, `tx_timestamp`, and `created_at`. Each column has a specific data type and description.

The `id` column is an internal event ID, while the `kind` column specifies the type of event, such as `new-order`, `expiry`, `sale`, `cancel`, `balance-change`, `approval-change`, `bootstrap`, `revalidation`, or `reprice`. The `collection_id` column contains the ID of the collection, and the `contract` column contains the contract address. The `token_id` column contains the ID of the token in the collection, and the `order_id` column contains the associated bid ID. The `maker` column contains the associated bid maker wallet address, and the `price` column contains the associated bid price in native currency.

The `previous_price` column contains the previous top bid price in native currency, and the `valid_until` column contains the associated bid validity expiration. The `source` column specifies the source of the order, such as `opensea.io`, and the `tx_hash` column contains the associated transaction hash. The `tx_timestamp` column contains the associated transaction timestamp, and the `created_at` column contains the timestamp the event was recorded.

The `collection_top_bid_events` table can be queried using SQL. Query examples can be found in the project, but the link is currently TBD. This table is useful for tracking changes in top bids for collections and analyzing bidding behavior.
## Questions: 
 1. What is the purpose of the `reservoir.collection_top_bid_events` table in the context of the dune docs project?
- The `reservoir.collection_top_bid_events` table contains records with information about each collection top bid change in the dune docs project.

2. What are the different event types that can be found in the `kind` column of the `reservoir.collection_top_bid_events` table?
- The `kind` column in the `reservoir.collection_top_bid_events` table contains different event types such as new-order, expiry, sale, cancel, balance-change, approval-change, bootstrap, revalidation, and reprice.

3. How are the bid prices represented in the `price` and `previous_price` columns of the `reservoir.collection_top_bid_events` table?
- The `price` and `previous_price` columns in the `reservoir.collection_top_bid_events` table represent the associated bid price and previous top bid price in native currency, respectively.