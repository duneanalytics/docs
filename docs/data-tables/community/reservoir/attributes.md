# Attributes

## **reservoir.attributes**

This table contains records with information about each attribute.

Query examples can be found here:

[https://dune.com/queries/1302927/2232298](https://dune.com/queries/1302927/2232298)

[https://dune.com/queries/1302966/2232361](https://dune.com/queries/1302966/2232361)

| **Column name**    | **Type**  | **Description**                                            |
|--------------------|-----------|------------------------------------------------------------|
| id                 | bigint    | Internal attribute id                                      |
| attribute\_key\_id | bigint    | Internal attribute key id                                  |
| value              | string    | Attribute value                                            |
| token\_count       | bigint    | Amount of tokens that have the attribute                   |
| on\_sale\_count    | bigint    | Amount of tokens that have the attribute which are on sale |
| floor\_sell\_value | decimal   | Current floor ask price                                    |
| sell\_updated\_at  | timestamp | Timestamp the floor sale was last updated                  |
| collection\_id     | string    | Associated collection id                                   |
| kind               | string    | Value type (string, number, date, range)                   |
| key                | string    | Associated key name                                        |
| created\_at        | timestamp | Timestamp the attribute was created                        |
| updated\_at        | timestamp | Timestamp the attribute was updated                        |
