---
description: >-
  Flashbots is a research and development organization formed with the goal is
  to make sure MEV incentives do not become opaque and undemocratic.
---

# Flashbots

## **flashbots.mev\_summary**

This table contains summary of all the classified transactions

&#x20;Query examples can be found here:&#x20;

| **Column name**                      | **Type**  | **Description**                                        |
| ------------------------------------ | --------- | ------------------------------------------------------ |
| block\_timestamp                     | timestamp | Block timestamp                                        |
| block\_number                        | bigint    | Block number                                           |
| base\_fee\_per\_gas                  | bigint    | Base fee per gas                                       |
| coinbase\_transfer                   | bigint    | Direct transfer to miner’s address                     |
| error                                | string    | Error if exists                                        |
| gas\_price                           | bigint    | Price of the gas                                       |
| gas\_price\_with\_coinbase\_transfer | bigint    | Amount of gas spent + direct transfer to miner address |
| gas\_used                            | bigint    | Amount of gas used                                     |
| gross\_profit\_usd                   | double    | Total profit from the transaction in usd               |
| miner\_address                       | string    | Address of the miner                                   |
| miner\_payment\_usd                  | double    | Payment received by the miner in usd                   |
| protocol                             | string    | Main interacted protocol                               |
| protocols                            | string    | List of protocols involved in the transaction          |
| transaction\_hash                    | string    | Hash of the transaction                                |
| type                                 | string    | Type of the MEV (e.g. arbitrage)                       |
| timestamp                            | timestamp | Timestamp of the latest update of the file             |

## **flashbots.arbitrages**

This table contains records with additional information about each arbitrage trade.

&#x20;Query examples can be found here:&#x20;

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

## **flashbots.liquidations**

Liquidation is another MEV strategy. This table contains details related to executed liquidations.

&#x20;Query examples can be found here:&#x20;

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

## **flashbots.sandwiched\_swaps**

One common way to extract MEV is to execute automated swaps to capture arbitrage opportunities across different platforms. This table contains records of swaps executed within specified arbitrage trades.

&#x20;Query examples can be found here:&#x20;

| **Column name**   | **Type**  | **Description**                                                                                             |
| ----------------- | --------- | ----------------------------------------------------------------------------------------------------------- |
| created\_at       | string    | Time of the records creation                                                                                |
| block\_number     | bigint    | Block number                                                                                                |
| sandwich\_id      | string    | Internal id of the sandwiched swap                                                                          |
| trace\_address    | string    | Trace pattern related to the position of the swap in the chain of all swaps related to the arbitrage trade. |
| transaction\_hash | string    | Transaction hash                                                                                            |
| timestamp         | timestamp | Timestamp of the latest update of the file                                                                  |

## **flashbots.sandwiches**

This table contains detailed information about executed sandwiches

&#x20;Query examples can be found here:&#x20;

| **Column name**                   | **Type**  | **Description**                            |
| --------------------------------- | --------- | ------------------------------------------ |
| created\_at                       | datetime  | Time of the records creation               |
| block\_number                     | bigint    | Block number                               |
| backrun\_swap\_trace\_address     | string    |                                            |
| backrun\_swap\_transaction\_hash  | string    |                                            |
| frontrun\_swap\_trace\_address    | string    |                                            |
| frontrun\_swap\_transaction\_hash | string    |                                            |
| id                                | string    | Internal id of the sandwich                |
| profit\_amount                    | bigint    | Profit amount after the arbitrage          |
| profit\_token\_address            | string    | Address of the profit asset                |
| sandwicher\_address               | string    | Address of the sandwicher                  |
| timestamp                         | timestamp | Timestamp of the latest update of the file |

## **flashbots.blocks**

This table contains block numbers and corresponding block\_timestamps

&#x20;Query examples can be found here:&#x20;

| **Column name**  | **Type**  | **Description** |
| ---------------- | --------- | --------------- |
| block\_number    | bigint    | Block number    |
| block\_timestamp | timestamp | Block timestamp |

