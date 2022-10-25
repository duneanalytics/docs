# 奖励表

## Solana.rewards

此表包含有关在Solana上支付的奖励的数据。一个区块可能包含零个或多个奖励，每一行对应一个奖励。

可以在此处找到示例查询：[Solana每日奖励费用](https://dune.xyz/queries/391421/747012)。

| 字段名称   | 字段类型 | 描述                                                                                       |
| ------------- | ----------- | ------------------------------------------------------------------------------------------------- |
| block\_slot   | bigint      | 此区块在账本中的槽索引                                                             |
| block\_hash   | string      | 此区块的哈希值，base-58编码                                                          |
| block\_time   | timestamp   | 此区块的（估计）生成时间                                                      |
| block\_date   | date        | 事件日期                                                                                        |
| commission    | string      | 奖励入账时的投票账户佣金，仅用于投票和质押奖励             |
| lamports      | bigint      | 账户贷记或借记的奖励lamports数量                                      |
| pre\_balance  | bigint      | 应用奖励前的账户余额（以`lamports`表示）                                         |
| post\_balance | bigint      | 应用奖励后的账户余额（以`lamports`表示）                                          |
| recipient     | string      | 收到奖励的账户的公钥，以base-58编码的字符串                |
| reward\_type  | string      | 奖励类型：“fee”，“rent”，“voting”，“staking”                                                |
