# bid events

## **reservoir.bid\_events**

This table contains records with information about each bid change.

Query examples can be found here: [TBD](TBD)

| **Column name**     | **Type**  | **Description**                                                                                                 |
| ------------------- | --------- | --------------------------------------------------------------------------------------------------------------- |
| id                  | string    | Internal event id                                                                                               |
| kind                | string    | Event type (new-order, expiry, sale, cancel, balance-change, approval-change, bootstrap, revalidation, reprice) |
| status              | string    | Event status (active, expired)                                                                                  |
| contract            | string    | Contract address                                                                                                |
| token\_set\_id      | string    | Id of the token set                                                                                             |
| order\_id           | string    | Associated bid id                                                                                               |
| maker               | string    | Associated bid maker wallet address                                                                             |
| price               | string    | Associated bid price (native currency)                                                                          |
| value               | string    | Associated bid value (native currency)                                                                          |
| quantity\_remaining | bigint    | Associated bid tokens remaining                                                                                 |
| valid\_from         | bigint    | Associated bid validity start                                                                                   |
| valid\_until        | bigint    | Associated bid validity expiration                                                                              |
| source              | string    | Source of the order (e.g. opensea.io)                                                                           |
| tx\_hash            | string    | Associated transaction hash                                                                                     |
| tx\_timestamp       | bigint    | Associated transaction timestamp                                                                                |
| created\_at         | timestamp | Timestamp the event was recorded                                                                                |
