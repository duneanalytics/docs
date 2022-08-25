# mev\_summary

## **flashbots.mev\_summary**

This table contains summary of all the classified transactions

Query examples can be found here: [Miner Revenue from Liquidations and Arbitrages](https://dune.com/queries/625974/1167301)

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
