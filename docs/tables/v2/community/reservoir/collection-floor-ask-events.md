# collection floor ask events

## **reservoir.collection\_floor\_ask\_events**

This table contains records with information about each collection floor ask changes.

Query examples can be found here: [TBD](TBD)

| **Column name** | **Type**  | **Description**                                                                                                 |
|-----------------|-----------|-----------------------------------------------------------------------------------------------------------------|
| id              | bigint    | Internal event id                                                                                               |
| kind            | string    | Event type (new-order, expiry, sale, cancel, balance-change, approval-change, bootstrap, revalidation, reprice) |
| collection\_id  | string    | Collection id                                                                                                   |
| contract        | string    | Contract address                                                                                                |
| token\_id       | string    | Id of the token in the collection                                                                               |
| order\_id       | string    | Associated ask id                                                                                               |
| maker           | string    | Associated ask maker wallet address                                                                             |
| price           | decimal   | Associated ask price (native currency)                                                                          |
| previous\_price | decimal   | previous floor ask price (native currency)                                                                      |
| valid\_until    | bigint    | Associated ask validity expiration                                                                              |
| source          | string    | Source of the order (e.g. opensea.io)                                                                           |
| tx\_hash        | string    | Associated transaction hash                                                                                     |
| tx\_timestamp   | bigint    | Associated transaction timestamp                                                                                |
| created\_at     | timestamp | Timestamp the event was recorded                                                                                |
