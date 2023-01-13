# collection top bid events

## **reservoir.collection\_top\_bid\_events**

This table contains records with information about each collection top bid change.

Query examples can be found here: [TBD](TBD)

| **Column name** | **Type**  | **Description**                                                                                                 |
|-----------------|-----------|-----------------------------------------------------------------------------------------------------------------|
| id              | string    | Internal event id                                                                                               |
| kind            | string    | Event type (new-order, expiry, sale, cancel, balance-change, approval-change, bootstrap, revalidation, reprice) |
| collection\_id  | string    | Collection id                                                                                                   |
| contract        | string    | Contract address                                                                                                |
| token\_id       | string    | Id of the token in the collection                                                                               |
| order\_id       | string    | Associated bid id                                                                                               |
| maker           | string    | Associated bid maker wallet address                                                                             |
| price           | string    | Associated bid price (native currency)                                                                          |
| previous\_price | decimal   | previous top bid price (native currency)                                                                        |
| valid\_until    | bigint    | Associated bid validity expiration                                                                              |
| source          | string    | Source of the order (e.g. opensea.io)                                                                           |
| tx\_hash        | string    | Associated transaction hash                                                                                     |
| tx\_timestamp   | bigint    | Associated transaction timestamp                                                                                |
| created\_at     | timestamp | Timestamp the event was recorded                                                                                |
