# token floor ask events

## **reservoir.token\_floor\_ask\_events**

This table contains records with information about each NFT token floor ask changes.

Query examples can be found here: [TBD](TBD)

| **Column name** | **Type**  | **Description**                                                                                                 |
|-----------------|-----------|-----------------------------------------------------------------------------------------------------------------|
| id              | bigint    | Internal token attribute id                                                                                     |
| kind            | string    | Event type (new-order, expiry, sale, cancel, balance-change, approval-change, bootstrap, revalidation, reprice) |
| contract        | string    | Contract address                                                                                                |
| token\_id       | string    | Id of the token in the collection                                                                               |
| order\_id       | string    | Associated Ask id                                                                                               |
| maker           | string    | Associated Ask maker wallet address                                                                             |
| price           | bigint    | Associated ask price (native currency)                                                                          |
| previous\_price | bigint    | Associated ask price (native currency)                                                                          |
| nonce           | string    | The order nonce of the maker                                                                                    |
| valid\_from     | bigint    | Associated ask validity start                                                                                   |
| valid\_until    | bigint    | Associated ask validity expiration                                                                              |
| source          | string    | Source of the order (e.g. opensea.io)                                                                           |
| tx\_hash        | string    | Associated transaction hash                                                                                     |
| tx\_timestamp   | bigint    | Associated transaction timestamp                                                                                |   
| created\_at     | timestamp | Timestamp the event was recorded                                                                                |
