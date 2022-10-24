# 出售

## **reservoir.出售**

该表包含有关于每笔出售的信息记录

查询的示例可以在这里找到:

[https://dune.com/queries/1302771/2232036](https://dune.com/queries/1302771/2232036)

[https://dune.com/queries/1302775/2232040](https://dune.com/queries/1302775/2232040)

| **列名**      | **类型**  | **说明**                                   |
|----------------------|-----------|---------------------------------------------------|
| id                   | 字符串    | 内部出售ID                                  |
| contract             | 字符串    | 合约地址                                  |
| token\_id            | 字符串    | 集合中的代币ID                 |
| order\_id            | 字符串    | 相关订单ID                               |
| order\_kind          | 字符串    | 协议名称 (e.g. seaport)                      |
| order\_side          | 字符串    | 订单类型 (请求 / 拍卖)                            |
| order\_source        | 字符串    | 列表来源 (e.g. opensea.io)           |
| from                 | 字符串    | 制作者的钱包地址                              |
| to                   | 字符串    | 接受者的钱包地址                              |
| price                | 精确小数型   | 出售价格 (本地货币)                      |
| usd\_price           | 字符串    | 出售价格(美元)                                 |
| currency\_address    | 字符串    | 本次出售使用的货币地址           |
| currency\_symbol     | 字符串    | 本次出售使用的货币代码            |
| currency\_price      | 精确小数型   | 出售价格                                        |
| amount               | 字符串    | 出售的货币数量                             |
| fill\_source         | 字符串    | 订单执行的地方                       |
| aggregator\_source   | 字符串    | 集合来源 (e.g. reservoir)                |
| wash\_trading\_score | 整数型      | 内部洗涤交易评分 (基于过去的出售) |
| is\_primary          | 布尔型   | 交易铸造了吗？                                     |
| tx\_hash             | 字符串    | 相关的交易哈希值                       |
| tx\_log\_index       | 整数型       | 相关的交易日志索引                  |
| tx\_batch\_index     | 整数型       | 相关的交易批次索引                |
| tx\_timestamp        | 大数    | 相关的交易时间戳                  |
| created\_at          | 时间戳 | 记录出售的时间戳                   |
| updated\_at          | 时间戳 | 更新出售的时间戳                    |                                                               |
