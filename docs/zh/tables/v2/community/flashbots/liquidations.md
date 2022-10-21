# 清算
## **flashbots.清算**

清算是另一种MEV策略。本表包含与已执行的清算有关的细节。

查询示例可以在这找到: [Liquidations by Protocol](https://dune.com/queries/625715/1166880)

| **列名称**          | **类型**  | **描述**                                                                                                     |
| ------------------------ | --------- | ------------------------------------------------------------------------------------------------------------------- |
| created\_at              | 字符串    | 记录的时间                                                                                        |
| transaction\_hash        | 字符串    | 交易哈希                                                                                                    |
| trace\_address           | 字符串    |该交易与所有MEV交易链中的相关记录|
| debt\_token\_address     | 字符串    |债务的代币地址                                                                        |
| received\_amount         | bigint    | 从清算中收到的金额                                                                                |
| protocol                 | 字符串    | 协议名称                                                                                                   |
| liquidated\_user         | 字符串    | 被清算地址                                                                                     |
| liquidator\_user         | 字符串    | 发起清算的地址                                                                                      |
| received\_token\_address | 字符串    | 收到的资产的地址                                                                                       |
| block\_number            | 大数    | 区块号                                                                                                        |
| debt\_purchase\_amount   | 大数    | 购买的债务金额                                                                                            |
| timestamp                | 时间戳 | 文件最后更新的时间戳                                                                          |
