# 区块表

## Solana.blocks

该表包含Solana区块链中的区块数据。它可用于识别区块活动和交易随时间的变化。

Query examples can be found here: [Solana blocks over time](https://dune.xyz/queries/389979) and [Transactions per day](https://dune.xyz/queries/390045)
可在此处找到查询示例：[随时间变化的Solana区块数据](https://dune.xyz/queries/389979)和[每日交易数据](https://dune.xyz/queries/390045)

| 字段名称               | 字段类型 | 描述                                         |
| ------------------------- | ----------- | --------------------------------------------------- |
| hash                      | string      | 此区块的哈希值，base-58编码      |
| height                    | bigint      | 此区块之下的已存在的区块数量             |
| slot                      | bigint      | 此区块在账本中的槽索引               |
| time                      | timestamp   | 此区块的（估计）生成时间        |
| date                      | date        | 用于分区                                |
| parent\_slot              | bigint      | 此区块的父区块的槽索引               |
| previous\_block\_\_\_hash | string      | 此区块的父区块的哈希值，base-58编码    |
| total\_transactions       | bigint      | 此区块中的交易总数      |
| successful\_transactions  | bigint      | 此区块中成功交易的数量 |
| failed\_transactions      | bigint      | 此区块中失败的交易数量     |

##
