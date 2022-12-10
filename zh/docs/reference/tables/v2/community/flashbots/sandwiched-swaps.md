# 三明治交易表
## **flashbots.sandwiched_swaps**

三明治交易表包含了关于一个或多个与数据表中与三明治交易相关的数据。
查询示例可以在这里找到：

| **列名称**   | **类型**  | **类型**                                                                                             |
| ----------------- | --------- | ----------------------------------------------------------------------------------------------------------- |
| created\_at       | string    | 记录的时间                                                                               |
| block\_number     | bigint    | 区块号                                                                                               |
| sandwich\_id      | string    | 三明治交易内部的Id                                                                          |
| trace\_address    | string   | 与套利交易相关的所有交易的记录 |
| transaction\_hash | string    | 交易哈希                                                                                            |
| timestamp         | timestamp | 文件最后更新的时间戳                                                                  |
