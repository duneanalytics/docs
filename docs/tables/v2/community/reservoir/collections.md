# 集合

## **reservoir.集合**

该表包含有关于每个NFT集合的信息记录.

查询的示例可以在这里找到:

[https://dune.com/queries/1302781/2232054](https://dune.com/queries/1302781/2232054)

[https://dune.com/queries/1302788/2232065](https://dune.com/queries/1302788/2232065)

| **列名**            | **类型**  | **说明**                             |
|----------------------------|-----------|---------------------------------------------|
| id                         | 字符串    | 内部集合ID                      |
| slug                       | 字符串    | 集合标题                             |
| name                       | 字符串    | 集合名称                             |
| description                | 字符串    | 集合说明                      |
| token\_count               | 大数    | 集合中的代币ID           |
| contract                   | 字符串    | 合约地址                            |
| day1\_rank                 | 大数    | 前1日的排名                 |
| day7\_rank                 | 大数    | 前7日的排名              |
| day30\_rank                | 大数    | 前30日的排名             |
| all\_time\_rank            | 大数    | 所有时间的排名                            |
| day1\_volume               | 精确小数型   | 前1日的交易量            |
| day7\_volume               | 精确小数型   | 前7日的交易量         |
| day30\_volume              | 精确小数型   | 前30日的交易量        |
| all\_time\_volume          | 精确小数型   | 所有时间的交易量                       |
| day1\_volume\_change       | 双精度浮点型    | 前1日的交易量变化     |
| day7\_volume\_change       | 双精度浮点型    | 前7日的交易量变化  |
| day30\_volume\_change      | 双精度浮点型    | 前30日的交易量变化 |
| floor\ask\_value           | 精确小数型   | 当前的出售底价 (本地货币)  |
| day1\_floor\_sale\_value   | 精确小数型   | 前1日的出售底价        |
| day7\_floor\_sale\_value   | 精确小数型   | 前7日的出售底价                 |
| day30\_floor\_sale\_value  | 精确小数型   | 前30日的出售底价                |
| day1\_floor\_sale\_change  | 双精度浮点型    | 前1日的出售底价变化   |
| day7\_floor\_sale\_change  | 双精度浮点型    | 前7日的出售底价变化     |
| day30\_floor\_sale\_change | 双精度浮点型    | 前30日的出售底价变化    |
| created\_at                | 时间戳 | 创建集合的时间戳        |
| updated\_at                | 时间戳 | 更新集合的时间戳        |                                                               |
