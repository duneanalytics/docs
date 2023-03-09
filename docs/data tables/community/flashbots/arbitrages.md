# arbitrages

## **flashbots.arbitrages**

This table contains records with additional information about each arbitrage trade.

Query examples can be found here: [Total Arb Protocols](https://dune.com/queries/626076/1167481)

| **Column name**        | **Type**  | **Description**                               |
| ---------------------- | --------- | --------------------------------------------- |
| block\_number          | bigint    | Block number                                  |
| account\_address       | string    | Address of the searcher                       |
| created\_at            | string    | Time of the record creation                   |
| end\_amount            | bigint    | Available amount after the arbitrage          |
| error                  | string    | Available amount after the arbitrage          |
| id                     | string    | Internal id of the arbitrage                  |
| profit\_amount         | bigint    | Profit amount after the arbitrage             |
| profit\_token\_address | string    | Address of the profit asset                   |
| protocols              | string    | List of protocols involved in the transaction |
| start\_amount          | bigint    | Available amount before the arbitrage         |
| transaction\_hash      | string    | Hash of the transaction                       |
| timestamp              | timestamp | Timestamp of the latest update of the file    |
