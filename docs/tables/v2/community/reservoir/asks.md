# asks

## **reservoir.asks**

This table contains records with information about each listing.

Query examples can be found here: [TBD](TBD)

| **Column name**     | **Type**  | **Description**                              |
|---------------------|-----------|----------------------------------------------|
| id                  | string    | Internal order id                            |
| kind                | string    | Protocol name (e.g. seaport)                 |
| status              | string    | Order status (active, inactive)              |
| contract            | string    | Contract address                             |
| token\_id           | string    | Id of the token in the collection            |
| maker               | string    | Maker wallet address                         |
| taker               | string    | Taker wallet address                         |
| price               | bigint    | The current price (native currency)          |
| start\_price        | bigint    | Start Listing price (for dutch auctions)     |
| end\_price          | bigint    | End Listing price (for dutch auctions)       |
| currency\_address   | string    | Currency address                             |
| currency\_symbol    | string    | Currency symbol                              |
| currency\_price     | bigint    | Currency price                               |
| dynamic             | boolean   | Is dutch auction?                            |
| quantity            | bigint    | Amount of tokens that is listed              |
| quantity\_filled    | bigint    | Amount of tokens that was filled             |
| quantity\_remaining | bigint    | Amount of tokens remaining                   |
| valid\_from         | bigint    | Listing start time                           |
| valid\_until        | bigint    | Listing end time                             |
| nonce               | string    | The order nonce of the maker                 |
| source              | string    | Source of the listing (e.g. opensea.io)      |
| fee\_bps            | string    | Listing fee                                  |
| expiration          | bigint    | Associated transaction hash                  |
| raw\_data           | string    | Raw order data (format will vary per source) |
| created\_at         | timestamp | Timestamp the listing was created            |
| updated\_at         | timestamp | Timestamp the listing was updated            |
