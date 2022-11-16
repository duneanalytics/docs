# sales

## **reservoir.sales**

This table contains records with information about each sale.

Query examples can be found here:

[https://dune.com/queries/1302771/2232036](https://dune.com/queries/1302771/2232036)

[https://dune.com/queries/1302775/2232040](https://dune.com/queries/1302775/2232040)

| **Column name**      | **Type**  | **Description**                                   |
|----------------------|-----------|---------------------------------------------------|
| id                   | string    | Internal sale id                                  |
| contract             | string    | Contract address                                  |
| token\_id            | string    | Id of the token in the collection                 |
| order\_id            | string    | Associated order id                               |
| order\_kind          | string    | Protocol name (e.g. seaport)                      |
| order\_side          | string    | Order type (ask / bid)                            |
| order\_source        | string    | Source of the listing (e.g. opensea.io)           |
| from                 | string    | Maker wallet address                              |
| to                   | string    | Taker wallet address                              |
| price                | decimal   | Sale price (native currency)                      |
| usd\_price           | string    | Sale price in USD                                 |
| currency\_address    | string    | The currency address used for this sale           |
| currency\_symbol     | string    | The currency symbol used for this sale            |
| currency\_price      | decimal   | Sale price                                        |
| amount               | string    | Amount of tokens sold                             |
| fill\_source         | string    | Where the order was filled                        |
| aggregator\_source   | string    | aggregator source (e.g. reservoir)                |
| wash\_trading\_score | int       | Internal wash trading score (based on past sales) |
| is\_primary          | boolean   | Is paid mint?                                     |
| tx\_hash             | string    | Associated transaction hash                       |
| tx\_log\_index       | int       | Associated transaction log index                  |
| tx\_batch\_index     | int       | Associated transaction batch index                |
| tx\_timestamp        | bigint    | Associated transaction timestamp                  |
| created\_at          | timestamp | Timestamp the sale was recorded                   |
| updated\_at          | timestamp | Timestamp the sale was updated                    |                                                               |
