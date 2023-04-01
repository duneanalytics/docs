[View code on GitHub](https://dune.com/docs/data-tables/community/reservoir/bid-events.md)

# Bid Events

The `bid_events` table is a part of the Dune Docs project and contains records with information about each bid change. This table is located in the `data-tables` folder of the project.

The table has several columns that provide information about the bid event, including the event ID, event type, event status, contract address, token set ID, associated bid ID, bid maker wallet address, bid price, bid value, bid tokens remaining, bid validity start and expiration, source of the order, associated transaction hash, and timestamp the event was recorded.

The purpose of this table is to provide a record of all bid changes that occur within the system. This information can be used to track the progress of bids, monitor the performance of the system, and identify any issues that may arise.

Query examples for this table are not yet available, but they will be added to the project in the future.

Overall, the `bid_events` table is an important component of the Dune Docs project, providing valuable information about the bidding process within the system.
## Questions: 
 1. What is the purpose of the `reservoir.bid_events` table in the context of the Dune Docs project?
- The `reservoir.bid_events` table contains records with information about each bid change in the project.

2. What are the different types of events that can be found in the `kind` column of the `reservoir.bid_events` table?
- The different types of events that can be found in the `kind` column of the `reservoir.bid_events` table include new-order, expiry, sale, cancel, balance-change, approval-change, bootstrap, revalidation, and reprice.

3. How is the value of a bid represented in the `reservoir.bid_events` table?
- The value of a bid is represented in the `reservoir.bid_events` table as the associated bid value in native currency.