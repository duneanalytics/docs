# 请求事件表

## **reservoir.ask\_events**

该表包含每个关于请求变更的信息记录。

查询的示例可以在这里找到：

[https://dune.com/queries/1302858/2232178](https://dune.com/queries/1302858/2232178)

[https://dune.com/queries/1302863/2232189](https://dune.com/queries/1302863/2232189)

| **列名称**     | **类型**   | **说明**                                                                                                 |
|---------------------|------------|-----------------------------------------------------------------------------------------------------------------|
| id                  | bigint    | 内部事件ID                                                                                               |
| kind                | string     | 事件类型（新订单、到期、出售、取消、余额变化、批准变化、引导、重新验证、重新定价） |
| contract            | string     | 合约地址                                                                                                |
| token\_id           | string     | 合集（collection）中的代币ID                                                                             |
| order\_id           | string     | 相关请求的ID                                                                                             |
| maker               | string     | 相关请求的卖方钱包地址                                                                            |
| price               | decimal    | 相关请求的价格 (原生货币)                                                                          |
| quantity\_remaining | bigint     | 相关请求的剩余代币                                                                                 |
| valid\_from         | bigint     | 相关请求的有效期限开始                                                                                   |
| valid\_until        | bigint     | 相关请求的有效期限结束                                                                              |
| source              | string     | 订单来源 (比如OpenSea)                                                                           |
| tx\_hash            | string     | 相关的交易哈希值                                                                                     |
| tx\_timestamp       | bigint     | 相关的交易时间戳                                                                               |
| created\_at         | timestamp  | 事件记录的时间戳                                                                                |
