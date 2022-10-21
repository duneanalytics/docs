# mev\_概述

## **flashbots.mev\_概述**

本表包含所有交易分类的摘要

查询示例可以在这里找到： [Miner Revenue from Liquidations and Arbitrages](https://dune.com/queries/625974/1167301)

| **列名称**                      | **类型**  | **描述**                                        |
| ------------------------------------ | --------- | ------------------------------------------------------ |
| block\_timestamp                     | 时间戳 | 区块时间戳                                        |
| block\_number                        | 大数    | 区块号                                           |
| base\_fee\_per\_gas                  | 大数    | 单位gas费用                                       |
| coinbase\_transfer                   | 大数    | 直接给到矿工的矿工费                     |
| error                                | 字符串    | 错误                                       |
| gas\_price                           | 大数    | gas费                                       |
| gas\_price\_with\_coinbase\_transfer | 大数    | 总消耗的gas+直接给到矿工的矿工费 |
| gas\_used                            | 大数    | gas消耗量                                     |
| gross\_profit\_usd                   |  双精度浮点数    | 从交易中获取的总收益（美金）               |
| miner\_address                       | 字符串    | 矿工地址                                   |
| miner\_payment\_usd                  |  双精度浮点数    | 矿工收益（美金）                   |
| protocol                             | 字符串    | 主要交互的协议                               |
| protocols                            | 字符串    | 交易中涉及到的协议          |
| transaction\_hash                    | 字符串    | 交易哈希                                |
| type                                 | 字符串    | MEV类型（ 比如套利）                       |
| timestamp                            | 时间戳 | 文件最后更新的时间戳             |
