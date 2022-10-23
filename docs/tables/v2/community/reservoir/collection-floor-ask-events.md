# collection floor ask events

## **reservoir.collection\_floor\_ask\_events**

该表包含有关于每个底部请求改变集合的信息记录.

查询的示例可以在这里找到:

[https://dune.com/queries/1302799/2232083](https://dune.com/queries/1302799/2232083)

[https://dune.com/queries/1302841/2232151](https://dune.com/queries/1302841/2232151)

| **列名** | **类型**  | **说明**                                                                                                 |
|-----------------|-----------|-----------------------------------------------------------------------------------------------------------------|
| id              | 长整型数字    | 内部事件ID                                                                                              |
| kind            | 字符串    | 事件类型（新订单、到期、出售、取消、余额变化、批准变化、引导、重新验证、重新定价） |
| collection\_id  | 字符串    | 集合ID                                                                                                   |
| contract        | 字符串    | 合约地址                                                                                                |
| token\_id       | 字符串    | 集合中的代币ID                                                                              |
| order\_id       | 字符串    | 相关的请求ID                                                                                              |
| maker           | 字符串    | 相关的制作者钱包地址                                                                            |
| price           | 精确小数型   | 相关的请求价格 (本地货币)                                                                         |
| previous\_price | 精确小数型   | 前一天的请求底价 (本地货币)                                                                      |
| valid\_until    | 长整型数字    | 相关的有效请求到期                                                                              |
| source          | 字符串    | 订单来源 (e.g. opensea.io)                                                                           |
| tx\_hash        | 字符串    | 相关的交易哈希值                                                                                     |
| tx\_timestamp   | 长整型数字    | 相关的交易时间戳                                                                                |
| created\_at     | 时间戳 | 记录事件的时间戳                                                                                |
