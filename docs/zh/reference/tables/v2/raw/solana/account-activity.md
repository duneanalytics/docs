# 账户活动表

## Solana.account\_activity

此表包含来自交易表中的关注帐户使用情况的信息。每行包含有关交易中一个帐户使用情况的所有信息。

| 字段名称                | 字段类型 | 描述                                                      |
| -------------------------- | ----------- | ---------------------------------------------------------------- |
| block\_slot                | bigint      | 交易所在区块的槽位                   |
| block\_hash                | string      | 交易所在区块的哈希值                    |
| block\_time                | timestamp   | 此帐户使用发生的时间戳                   |
| block\_date                | date        | 此帐户使用发生的日期                             |
| address                    | string      | 账户地址，也称为公钥       |
| tx\_index                  | int         | 交易在区块中的索引                       |
| tx\_id                     | string      | 引发此帐户使用的交易的ID   |
| tx\_success                | boolean     | 此交易是否成功并已提交                      |
| signed                     | boolean     | 此帐户是否签署了当前交易                             |
| writeable                  | boolean     | 此帐户是否在当前交易中被授予写入权限   |
| pre\_balance               | bigint      | 此账户在交易处理前的余额 |
| pre\_token\_\_\_balance    | decimal     | 交易处理前的代币余额           |
| post\_balance              | bigint      | 交易处理后该账户的余额  |
| post\_token\_\_\_balance   | decimal     | 交易处理后的代币余额            |
| balance\_change            | bigint      | 作为交易的一部分发生的余额变化      |
| token\_balance\_\_\_change | decimal     | 作为交易的一部分发生的代币余额变化      |
