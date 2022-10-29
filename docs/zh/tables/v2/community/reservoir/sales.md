# 销售表

## **reservoir.sales**

该表包含有关于每笔销售的信息记录。

查询的示例可以在这里找到：

[https://dune.com/queries/1302771/2232036](https://dune.com/queries/1302771/2232036)

[https://dune.com/queries/1302775/2232040](https://dune.com/queries/1302775/2232040)

| **列名称**      | **类型**  | **说明**                                   |
|----------------------|-----------|---------------------------------------------------|
| id                   | string    | 内部销售ID                                  |
| contract             | string    | 合约地址                                  |
| token\_id            | string    | 合集中的代币ID                 |
| order\_id            | string    | 相关订单ID                               |
| order\_kind          | string    | 协议名称 (例如Seaport)                      |
| order\_side          | string    | 订单类型 (请求 / 拍卖)                            |
| order\_source        | string    | 挂单来源 (例如OpenSea)           |
| from                 | string    | 卖方的钱包地址                              |
| to                   | string    | 买方的钱包地址                              |
| price                | decimal   | 出售价格 (原生货币)                      |
| usd\_price           | string    | 出售价格(美元)                                 |
| currency\_address    | string    | 本次销售使用的货币的合约地址           |
| currency\_symbol     | string    | 本次出售使用的货币代号            |
| currency\_price      | decimal   | 出售价格                                        |
| amount               | string    | 出售的货币数量                             |
| fill\_source         | string    | 订单执行的地方                       |
| aggregator\_source   | string    | 合集来源 (例如reservoir)                |
| wash\_trading\_score | int      | 含水交易（wash trading）评分 (基于过去的销售) |
| is\_primary          | boolean   | 是否是花费铸造（paid mint）                                     |
| tx\_hash             | string    | 相关的交易哈希值                       |
| tx\_log\_index       | int       | 相关的交易日志索引                  |
| tx\_batch\_index     | int       | 相关的交易批次索引                |
| tx\_timestamp        | bigint    | 相关的交易时间戳                  |
| created\_at          | timestamp | 记录出售的时间戳                   |
| updated\_at          | timestamp | 更新出售的时间戳                    |                                                               |
