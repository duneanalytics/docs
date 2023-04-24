# Ask Events

## **reservoir.ask\_events**

This table contains records with information about each ask change.

Query examples can be found here:

[https://dune.com/queries/1302858/2232178](https://dune.com/queries/1302858/2232178)

[https://dune.com/queries/1302863/2232189](https://dune.com/queries/1302863/2232189)

| **Column name**     | **Type**   | **Description**                                                                                                 |
|---------------------|------------|-----------------------------------------------------------------------------------------------------------------|
| id                  | bigint     | Internal event id                                                                                               |
| kind                | string     | Event type (new-order, expiry, sale, cancel, balance-change, approval-change, bootstrap, revalidation, reprice) |
| contract            | string     | Contract address                                                                                                |
| token\_id           | string     | Id of the token in the collection                                                                               |
| order\_id           | string     | Associated ask id                                                                                               |
| maker               | string     | Associated ask maker wallet address                                                                             |
| price               | decimal    | Associated ask price (native currency)                                                                          |
| quantity\_remaining | bigint     | Associated ask tokens remaining                                                                                 |
| valid\_from         | bigint     | Associated ask validity start                                                                                   |
| valid\_until        | bigint     | Associated ask validity expiration                                                                              |
| source              | string     | Source of the order (e.g. opensea.io)                                                                           |
| tx\_hash            | string     | Associated transaction hash                                                                                     |
| tx\_timestamp       | bigint     | Associated transaction timestamp                                                                                |
| created\_at         | timestamp  | Timestamp the event was recorded                                                                                |
