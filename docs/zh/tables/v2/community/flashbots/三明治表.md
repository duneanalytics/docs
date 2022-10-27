# 三明治表

## **sandwiches**

这个表中包含已执行的三明治中的细节信息。

| **列名称**                   | **数据类型**  | **描述n**                                                 |
| --------------------------------- | --------- | --------------------------------------------------------------- |
| created\_at                       | datetime  | 记录的时间                                    |
| block\_number                     | bigint    | 区块号                                                    |
| backrun\_swap\_trace\_address     | string    | 三明治中反向交易的地址                  |
| backrun\_swap\_transaction\_hash  | string    | 具体的一个三明治中反向交易的交易哈希  |
| frontrun\_swap\_trace\_address    | string    | 三明治中前向交易的地址                 |
| frontrun\_swap\_transaction\_hash | string    | 具体的一个三明治中前向交易的交易哈希 |
| id                                | string    | 三明治中的内部Id                                    |
| profit\_amount                    | bigint    | 套利后的利润                               |
| profit\_token\_address            | string    | 利润资产的地址                                     |
| sandwicher\_address               | string    | 发起三明治的地址                                       |
| timestamp                         | timestamp | 文件最后更新的时间戳                     |

## \*\*\*\*
