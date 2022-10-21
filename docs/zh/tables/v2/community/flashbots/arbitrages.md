# 套利

## **flashbots.套利**

此表包含有关于每个套利交易的额外信息的记录。

查询示例可以在这里找到: [Total Arb Protocols](https://dune.com/queries/626076/1167481)

| **列名称**        | **类型**  | **描述**                               |
| ---------------------- | --------- | --------------------------------------------- |
| block\_number          | 大数    | 区块号                                  |
| account\_address       | 字符串    | 寻找人的地址                       |
| created\_at            | 字符串    | 记录的时间                   |
| end\_amount            | 大数    | 套利后可获数量          |
| error                  | 字符串    | 套利后可获数量         |
| id                     | 字符串   | 套利的内部Id                 |
| profit\_amount         | 大数    | 套利后可获收益        |
| profit\_token\_address | 字符串    | 获利资产地址                  |
| protocols              | 字符串    |交易中设计的协议列表 |
| start\_amount          | 大数    | 套利前可获数量       |
| transaction\_hash      | 字符串   | 交易哈希                       |
| timestamp              | 时间戳 | 文件最后更新的时间戳    |
