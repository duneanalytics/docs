# tokens

## **reservoir.tokens**

This table contains records with information about each NFT token.

Query examples can be found here:

[https://dune.com/queries/1303052/2232521](https://dune.com/queries/1303052/2232521)

[https://dune.com/queries/1303064/2232571](https://dune.com/queries/1303064/2232571)

| **Column name**         | **Type**  | **Description**                    |
|-------------------------|-----------|------------------------------------|
| id                      | string    | Internal token id                  |
| contract                | string    | Contract address                   |
| token\_id               | string    | Id of the token in the collection  |
| name                    | string    | NFT name                           |
| description             | string    | NFT description                    |                                                                                         |
| collection\_id          | string    | Associated Collection id           |
| owner                   | string    | Owner wallet address               |
| floor\_ask\_id          | string    | Floor ask id                       |
| floor\_ask\_value       | bigint    | Floor ask value                    |
| floor\_ask\_maker       | string    | Floor ask maker wallet address     |
| floor\_ask\_valid\_from | bigint    | Floor ask Listing start time       |
| floor\_ask\_valid\_to   | bigint    | Floor ask Listing end time         |
| floor\_ask\_source      | string    | Floor ask source (e.g. opensea.io) |
| last\_sale\_value       | bigint    | Associated transaction timestamp   |   
| last\_sale\_timestamp   | bigint    | Associated transaction timestamp   |   
| created\_at             | timestamp | Timestamp the token was created    |
| updated\_at             | timestamp | Timestamp the token was updated    |                                                                          |
