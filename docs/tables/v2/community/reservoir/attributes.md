# 属性

## **reservoir.属性**

该表包含有关于每个属性的信息记录.

查询的示例可以在这里找到:

[https://dune.com/queries/1302927/2232298](https://dune.com/queries/1302927/2232298)

[https://dune.com/queries/1302966/2232361](https://dune.com/queries/1302966/2232361)

| **列名**    | **类型**  | **说明**                                            |
|--------------------|-----------|------------------------------------------------------------|
| id                 | 大数    | 内部属性ID                                     |
| attribute\_key\_id | 大数    | 内部属性键ID                                  |
| value              | 字符串    | 属性值                                            |
| token\_count       | 大数    | 具有属性的代币数量                   |
| on\_sale\_count    | 大数    | 正在出售的具有属性的代币数量 |
| floor\_sell\_value | 精确小数型   | 当前的出售底价                                    |
| sell\_updated\_at  | 时间戳 | 最后更新底价的时间戳                  |
| collection\_id     | 字符串    | 相关的集合ID                                   |
| kind               | 字符串    | 值类型 (字符串, 数字, 日期, 范围)                   |
| key                | 字符串    | 相关的键名称                                        |
| created\_at        | 时间戳 | 创建属性的时间戳                        |
| updated\_at        | 时间戳 | 更新属性的时间戳                        |
