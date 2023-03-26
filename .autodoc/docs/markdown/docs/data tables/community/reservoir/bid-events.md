[View code on GitHub](https://dune.com/blob/master/data tables\community\reservoir\bid-events.md)

# Bid Events

This section of the app technical guide covers the `reservoir.bid_events` table, which contains records with information about each bid change. The table includes various columns such as `id`, `kind`, `status`, `contract`, `token_set_id`, `order_id`, `maker`, `price`, `value`, `quantity_remaining`, `valid_from`, `valid_until`, `source`, `tx_hash`, `tx_timestamp`, and `created_at`. 

The `id` column represents the internal event ID, while the `kind` column represents the type of event, such as `new-order`, `expiry`, `sale`, `cancel`, `balance-change`, `approval-change`, `bootstrap`, `revalidation`, and `reprice`. The `status` column represents the status of the event, which can be either `active` or `expired`. The `contract` column represents the contract address, while the `token_set_id` column represents the ID of the token set. The `order_id` column represents the associated bid ID, while the `maker` column represents the associated bid maker wallet address. The `price` column represents the associated bid price in native currency, while the `value` column represents the associated bid value in native currency. The `quantity_remaining` column represents the associated bid tokens remaining, while the `valid_from` column represents the associated bid validity start. The `valid_until` column represents the associated bid validity expiration, while the `source` column represents the source of the order, such as `opensea.io`. The `tx_hash` column represents the associated transaction hash, while the `tx_timestamp` column represents the associated transaction timestamp. Finally, the `created_at` column represents the timestamp the event was recorded.

This section also includes a link to query examples, which are currently TBD. The query examples will likely demonstrate how to retrieve specific information from the `reservoir.bid_events` table, such as bids of a certain type or bids associated with a specific contract or token set. Overall, this section of the app technical guide provides a detailed overview of the `reservoir.bid_events` table and its various columns, which will be useful for developers working on the bidding functionality of the Dune Docs app.
## Questions: 
 1. What is the purpose of the dune docs project and how does it relate to blockchain technology?
- The app technical guide provided does not give any information about the purpose of the dune docs project or its relation to blockchain technology.

2. How is the data in the bid events table being stored and accessed?
- The app technical guide does not provide information on how the data in the bid events table is being stored and accessed.

3. Are there any security measures in place to protect the bid events data?
- The app technical guide does not mention any security measures in place to protect the bid events data.