# 代币

## **reservoir.代币**

该表包含有关于每个NFT代币的信息记录.

查询的示例可以在这里找到:

[https://dune.com/queries/1303052/2232521](https://dune.com/queries/1303052/2232521)

[https://dune.com/queries/1303064/2232571](https://dune.com/queries/1303064/2232571)

| **列名**         | **类型**  | **说明**                    |
|-------------------------|-----------|------------------------------------|
| id                      | 字符串    | 内部代币ID                  |
| contract                | 字符串    | 合约地址                   |
| token\_id               | 字符串    | 集合中的代币地址  |
| name                    | 字符串    | NFT名称                           |
| description             | 字符串    | NFT说明                    |                                                                                         |
| collection\_id          | 字符串    | 相关的集合ID           |
| owner                   | 字符串    | 拥有者的钱包地址               |
| floor\_ask\_id          | 字符串    | 底部请求ID                       |
| floor\_ask\_value       | 大数    | 底部请求值                   |
| floor\_ask\_maker       | 字符串    | 底部请求制作者的钱包地址     |
| floor\_ask\_valid\_from | 大数    | 底部请求列表的开始时间       |
| floor\_ask\_valid\_to   | 大数    | 底部请求列表的结束时间         |
| floor\_ask\_source      | 字符串    | 底部请求来源(e.g. opensea.io) |
| last\_sale\_value       | 大数    | 相关的交易时间戳   |   
| last\_sale\_timestamp   | 大数    | 相关的交易时间戳   |   
| created\_at             | 时间戳 | 创建代币的时间戳    |
| updated\_at             | 时间戳 | 更新代币的时间戳   |                                                                          |
