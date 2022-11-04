# 代币属性表

## **reservoir.token\_attributes**

该表包含有关于每个NFT代币属性的信息记录。

查询的示例可以在这里找到：

[https://dune.com/queries/1302940/2232326](https://dune.com/queries/1302940/2232326)

| **列名称** | **类型**  | **说明**                           |
|-----------------|-----------|-------------------------------------------|
| id              | bigint    | 内部代币属性ID              |
| contract        | string    | 合约地址                          |
| token\_id       | string    | 合集中的代币ID         |
| attribute\_id   | bigint    | 内部属性ID                   |
| collection\_id  | string    | 内部合集ID                   |
| key             | string    | 属性键名                            |
| value           | string    | 属性值                           |
| created\_at     | timestamp | 创建代币属性的时间戳 |
| updated\_at     | timestamp | 更新代币属性的时间戳 |                                                               |
