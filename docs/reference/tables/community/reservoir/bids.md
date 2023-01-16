# bids

## **reservoir.bids**

This table contains records with information about each bid.

Query examples can be found here: [TBD](TBD)

| **Column name**     | **Type**  | **Description**                              |
| ------------------- | --------- | -------------------------------------------- |
| id                  | string    | Internal order id                            |
| kind                | string    | Protocol name (e.g. seaport)                 |
| status              | string    | Order status (active, inactive)              |
| contract            | string    | Contract address                             |
| token\_set\_id      | string    | Id of the token set                          |
| maker               | string    | Maker wallet address                         |
| taker               | string    | Taker wallet address                         |
| price               | string    | The current price (native currency)          |
| value               | string    | The current value (native currency)          |
| currency\_address   | string    | Currency address                             |
| currency\_symbol    | string    | Currency symbol                              |
| currency\_price     | string    | Currency price                               |
| quantity            | bigint    | Amount of tokens that is listed              |
| quantity\_filled    | bigint    | Amount of tokens that was filled             |
| quantity\_remaining | bigint    | Amount of tokens remaining                   |
| valid\_from         | bigint    | Listing start time                           |
| valid\_until        | bigint    | Listing end time                             |
| nonce               | bigint    | The order nonce of the maker                 |
| source              | string    | Source of the listing (e.g. opensea.io)      |
| fee\_bps            | bigint    | Listing fee                                  |
| expiration          | bigint    | Associated transaction hash                  |
| raw\_data           | string    | Raw order data (format will vary per source) |
| created\_at         | timestamp | Timestamp the listing was created            |
| updated\_at         | timestamp | Timestamp the listing was updated            |
