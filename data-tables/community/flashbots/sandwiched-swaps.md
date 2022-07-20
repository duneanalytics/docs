# sandwiched swaps

## **flashbots.sandwiched\_swaps**

The sandwiched\_swaps table contains additional data about one or more swaps that were sandwiched with a corresponding sandwich in the database.

Query examples can be found here:

| **Column name**   | **Type**  | **Description**                                                                                             |
| ----------------- | --------- | ----------------------------------------------------------------------------------------------------------- |
| created\_at       | string    | Time of the records creation                                                                                |
| block\_number     | bigint    | Block number                                                                                                |
| sandwich\_id      | string    | Internal id of the sandwiched swap                                                                          |
| trace\_address    | string    | Trace pattern related to the position of the swap in the chain of all swaps related to the arbitrage trade. |
| transaction\_hash | string    | Transaction hash                                                                                            |
| timestamp         | timestamp | Timestamp of the latest update of the file                                                                  |
