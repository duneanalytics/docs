# asks

## **reservoir.asks**

该表包含有关于每个列表信息的记录.

查询的示例可以在这里找到:

[https://dune.com/queries/1302885/2232229](https://dune.com/queries/1302885/2232229)

[https://dune.com/queries/1302904/2232257](https://dune.com/queries/1302904/2232257)

| **列名**     | **类型**  | **说明**                              |
|---------------------|-----------|----------------------------------------------|
| id                  | 字符串    | 内部订单ID                            |
| kind                | 字符串    | 协议名称 (e.g. seaport)                 |
| status              | 字符串    | 订单状态 (活跃的, 不活跃的)              |
| contract            | 字符串    | 合约地址                             |
| token\_id           | 字符串    | 集合中的代币ID            |
| maker               | 字符串    | 制作者的钱包地址                         |
| taker               | 字符串    | 接受者的钱包地址                        |
| price               | 精确小数   | 当前的价格 (本地货币)          |
| start\_price        | 长整型数字    | 列表的初始价格 (用于荷兰拍卖)     |
| end\_price          | 长整型数字    | 列表的结束价格 (用于荷兰拍卖)       |
| currency\_address   | 字符串    | 货币地址                             |
| currency\_symbol    | 字符串    | 货币代码                              |
| currency\_price     | 精确小数   | 货币价格                               |
| dynamic             | 布尔型   | 是荷兰拍卖                            |
| quantity            | 长整型数字    | 列表的代币数量              |
| quantity\_filled    | 长整型数字    | 填补的代币数量             |
| quantity\_remaining | 长整型数字    | 剩余的代币数量                   |
| valid\_from         | 长整型数字    | 列表开始时间                          |
| valid\_until        | 长整型数字    | 列表结束时间                             |
| nonce               | 字符串    | 制作者的目前订单                 |
| source              | 字符串    | 列表的来源 (e.g. opensea.io)      |
| fee\_bps            | 长整型数字    | 列表费用                                  |
| expiration          | 长整型数字    | 相关的交易哈希值                  |
| raw\_data           | 字符串    | 原始订单数据（每个来源的格式会有所不同） |
| created\_at         | 时间戳 | 创建列表的时间戳            |
| updated\_at         | 时间戳 | 更新列表的时间戳            |
