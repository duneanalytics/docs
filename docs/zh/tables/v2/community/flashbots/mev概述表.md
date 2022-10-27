# mev概述表

## **flashbots.mev\_summary**

本表包含所有交易分类的摘要。

查询示例可以在这里找到： [Miner Revenue from Liquidations and Arbitrages](https://dune.com/queries/625974/1167301)

| **列名称**                      | **类型**  | **描述**                                        |
| ------------------------------------ | --------- | ------------------------------------------------------ |
| block\_timestamp                     | timestamp | 区块时间戳                                        |
| block\_number                        | bigint    | 区块号                                           |
| base\_fee\_per\_gas                  | bigint    | 单位gas费用                                       |
| coinbase\_transfer                   | bigint    | 直接给到矿工的矿工费                     |
| error                                | string    | 错误                                       |
| gas\_price                           | bigint    | gas费                                       |
| gas\_price\_with\_coinbase\_transfer | bigint    | 总消耗的gas+直接给到矿工的矿工费 |
| gas\_used                            | bigint    | gas消耗量                                     |
| gross\_profit\_usd                   |  double    | 从交易中获取的总收益（美金）               |
| miner\_address                       | string    | 矿工地址                                   |
| miner\_payment\_usd                  |  double    | 矿工收益（美金）                   |
| protocol                             | string    | 主要交互的协议                               |
| protocols                            | string    | 交易中涉及到的协议          |
| transaction\_hash                    | string    | 交易哈希                                |
| type                                 | string    | MEV类型（比如套利）                       |
| timestamp                            | timestamp | 文件最后更新的时间戳             |
