# 套利表

## **flashbots.arbitrages**

此表包含有关于每个套利交易的额外信息的记录。

查询示例可以在这里找到: [Total Arb Protocols](https://dune.com/queries/626076/1167481)

| **列名称**        | **类型**  | **描述**                               |
| ---------------------- | --------- | --------------------------------------------- |
| block\_number          | bigint    | 区块号                                  |
| account\_address       | string    | 寻找人（searcher）的地址                       |
| created\_at            | string    | 记录的时间                   |
| end\_amount            | bigint    | 套利后可获数量          |
| error                  | string    | 套利后可获数量         |
| id                     | string   | 套利的内部Id                 |
| profit\_amount         | bigint    | 套利后可获收益        |
| profit\_token\_address | string    | 获利资产地址                  |
| protocols              | string    |交易中设计的协议列表 |
| start\_amount          | bigint    | 套利前可获数量       |
| transaction\_hash      | string   | 交易哈希                       |
| timestamp              | timestamp | 文件最后更新的时间戳    |
