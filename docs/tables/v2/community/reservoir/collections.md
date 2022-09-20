# collections

## **reservoir.collections**

This table contains records with information about each NFT collection.

Query examples can be found here: [TBD](TBD)

| **Column name**            | **Type**  | **Description**                             |
|----------------------------|-----------|---------------------------------------------|
| id                         | string    | Internal collection id                      |
| slug                       | string    | Collection slug                             |
| name                       | string    | Collection name                             |
| description                | string    | Collection description                      |
| token\_count               | bigint    | Id of the token in the collection           |
| contract                   | string    | Contract address                            |
| day1\_rank                 | string    | Ranking in the previous day                 |
| day7\_rank                 | bigint    | Ranking in the previous 7 days              |
| day30\_rank                | bigint    | Ranking in the previous 30 days             |
| all\_time\_rank            | bigint    | All time ranking                            |
| day1\_volume               | bigint    | Trade volume in the previous day            |
| day7\_volume               | bigint    | Trade volume in the previous 7 days         |
| day30\_volume              | bigint    | Trade volume in the previous 30 days        |
| all\_time\_volume          | bigint    | All time trade volume                       |
| day1\_volume\_change       | bigint    | Trade volume change in the previous day     |
| day7\_volume\_change       | bigint    | Trade volume change in the previous 7 days  |
| day30\_volume\_change      | bigint    | Trade volume change in the previous 30 days |
| floor\_sale\_value         | bigint    | Current floor sale price (native currency)  |
| day1\_floor\_sale\_value   | bigint    | Floor sale price in the previous day        |
| day7\_floor\_sale\_value   | bigint    | Floor sale price 7 days ago                 |
| day30\_floor\_sale\_value  | bigint    | Floor sale price 30 days ago                |
| day1\_floor\_sale\_change  | bigint    | Floor sale price change from previous day   |
| day7\_floor\_sale\_change  | bigint    | Floor sale price change from 7 days ago     |
| day30\_floor\_sale\_change | bigint    | Floor sale price change from 30 days ago    |
| created\_at                | timestamp | Timestamp the collection was created        |
| updated\_at                | timestamp | Timestamp the collection was updated        |                                                               |
