# token attributes

## **reservoir.token\_attributes**

This table contains records with information about each NFT token attribute.

Query examples can be found here: [TBD](TBD)

| **Column name** | **Type**  | **Description**                           |
|-----------------|-----------|-------------------------------------------|
| id              | bigint    | Internal token attribute id               |
| contract        | string    | Contract address                          |
| token\_id       | string    | Id of the token in the collection         |
| attribute\_id   | bigint    | Internal attribute id                     |
| collection\_id  | string    | Internal collection id                    |
| key             | string    | Attribute name                            |
| value           | string    | Attribute value                           |
| created\_at     | timestamp | Timestamp the token attribute was created |
| updated\_at     | timestamp | Timestamp the token attribute was updated |                                                               |
