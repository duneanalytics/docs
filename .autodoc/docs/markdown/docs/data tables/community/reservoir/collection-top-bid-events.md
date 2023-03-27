[View code on GitHub](https://dune.com/blob/master/data tables\community\reservoir\collection-top-bid-events.md)

# Collection Top Bid Events

This section of the app technical guide covers the `reservoir.collection_top_bid_events` table. This table contains records with information about each collection top bid change. The table has several columns, including `id`, `kind`, `collection_id`, `contract`, `token_id`, `order_id`, `maker`, `price`, `previous_price`, `valid_until`, `source`, `tx_hash`, `tx_timestamp`, and `created_at`. 

The `id` column contains the internal event ID, while the `kind` column specifies the type of event, such as `new-order`, `expiry`, `sale`, `cancel`, `balance-change`, `approval-change`, `bootstrap`, `revalidation`, or `reprice`. The `collection_id` column contains the ID of the collection, and the `contract` column contains the contract address. The `token_id` column contains the ID of the token in the collection, and the `order_id` column contains the associated bid ID. The `maker` column contains the associated bid maker wallet address, and the `price` column contains the associated bid price in native currency. The `previous_price` column contains the previous top bid price in native currency, and the `valid_until` column contains the associated bid validity expiration. The `source` column contains the source of the order, such as `opensea.io`. The `tx_hash` column contains the associated transaction hash, and the `tx_timestamp` column contains the associated transaction timestamp. Finally, the `created_at` column contains the timestamp the event was recorded.

This section also provides a link to query examples, which are currently TBD. 

Overall, this section of the app technical guide provides a detailed overview of the `reservoir.collection_top_bid_events` table and its various columns. It is useful for developers who need to work with this table and understand the information it contains.
## Questions: 
 1. What is the purpose of the "reservoir.collection_top_bid_events" table in the context of blockchain and SQL? 
- The table contains records with information about each collection top bid change, which could be useful for analyzing bidding behavior and trends within a collection.

2. Are there any limitations or constraints on the data types used in the table columns? 
- The table lists the data types for each column, but it does not specify any limitations or constraints on those data types. A blockchain SQL analyst may need to investigate further to determine if there are any restrictions on the data that can be stored in the table.

3. Is there any additional documentation or context available for the "kind" column, which lists different event types? 
- The table provides a list of possible values for the "kind" column, but it does not explain what each of those event types represents. A blockchain SQL analyst may need to consult other documentation or resources to gain a better understanding of the different event types and their significance.