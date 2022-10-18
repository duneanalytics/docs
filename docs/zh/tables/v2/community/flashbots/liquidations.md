# liquidations

## **flashbots.liquidations**

Liquidation is another MEV strategy. This table contains details related to executed liquidations.

Query examples can be found here: [Liquidations by Protocol](https://dune.com/queries/625715/1166880)

| **Column name**          | **Type**  | **Description**                                                                                                     |
| ------------------------ | --------- | ------------------------------------------------------------------------------------------------------------------- |
| created\_at              | string    | Time of the records creation                                                                                        |
| transaction\_hash        | string    | Transaction hash                                                                                                    |
| trace\_address           | string    | Trace pattern related to the position of the transaction in the chain of all transactions related to the MEV trade. |
| debt\_token\_address     | string    | Underlying token address of the debt to pay                                                                         |
| received\_amount         | bigint    | Amount received from the liquidation                                                                                |
| protocol                 | string    | Protocol name                                                                                                       |
| liquidated\_user         | string    | Address of the liquidated user                                                                                      |
| liquidator\_user         | string    | Address of the liquidator user                                                                                      |
| received\_token\_address | string    | Address of the received asset                                                                                       |
| block\_number            | bigint    | Block number                                                                                                        |
| debt\_purchase\_amount   | bigint    | Amount of purchased debt                                                                                            |
| timestamp                | timestamp | Timestamp of the latest update of the file                                                                          |
