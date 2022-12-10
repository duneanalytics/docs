# 投票交易表

## Solana.vote\_transactions

此表包含验证者提交的用于对区块进行投票的全部投票交易。它可以与上面的非投票交易表结合起来，以获得所有交易的完整细分。它与主交易表具有相同的架构。

此处提供了一个示例查询：[Solana过去30天的交易](https://dune.xyz/queries/389976/743760)

| 字段名称                     | 字段类型                   | 描述                                                                                                                                                                                                                           |
| -------------------------------- | ----------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| block\_slot                      | bigint                        | 此区块在账本中的槽索引                                                                                                                                                                                                |
| block\_time                      | timestamp                     | 此区块的（估计）生成时间                                                                                                                                                                                          |
| block\_date                      | date                          | 事件日期                                                                                                                                                                                                                            |
| index                            | bigint                        | 此交易在区块中的索引位置                                                                                                                                                                                                   |
| fee                              | bigint                        | 此交易支付的费用，由第一个帐户支付                                                                                                                                                                            |
| block\_hash                      | string                        | 此区块的哈希值，base-58编码                                                                                                                                                                                               |
| error                            | STRUCT error                  | 如果 success = true 则为 NULL值.                                                                                                                                                                                                              |
| required\_signatures             | bigint                        | 使当前交易有效所需的签名数量                                                                                                                                                                |
| readonly\_signed\_\_\_accounts   | bigint                        | 只读的签名账户数量                                                                                                                                                        |
| readonly\_unsigned\_\_\_accounts | bigint                        | 只读的非签名账户数量                                                                                                                                                    |
| id                               | string                        | 交易的第一个签名（也就是交易的哈希值）                                                                                                                                                                                               |
| success                          | boolean                       | 交易有效且已被提交                                                                                                                                                                                         |
| recent\_block\_\_\_hash          | string                        | 账本中最近区块的哈希值，用于防止交易重复并赋予交易生命周期                                                                                                                  |
| instructions                     | array\<STRUCT instructions>   | 执行的指令数组（按顺序）                                                                                                                                                                                                    |
| accountKeys                      | array\<string>                | 交易中使用的帐户地址                                                                                                                                                                                             |
| log\_messages                    | array\<string>                | 此交易发出的日志消息                                                                                                                                                                                           |
| pre\_balances                    | array\<bigint>                | 处理交易之前的账户余额数组。第i个余额值就是account\_keys数组中第i个账户的余额                                                                                              |
| post\_balances                   | array\<bigint>                | 处理交易之后的账户余额数组。第i个余额值就是account\_keys数组中第i个账户的余额                                                                                               |
| pre\_token\_balance              | array\<STRUCT token\_balance> | 交易处理前的[代币余额](https://docs.solana.com/developing/clients/jsonrpc-api#token-balances-structure)列表，如果在此交易期间尚未启用代币余额记录，则省略     |
| post\_token\_balance             | array\<STRUCT token\_balance> | 交易处理后的[代币余额](https://docs.solana.com/developing/clients/jsonrpc-api#token-balances-structure)列表，如果在此交易期间尚未启用代币余额记录，则省略     |
| signatures                       | array\<string>                | 应用于交易的base-58编码签名列表。长度总是等于numRequiredSignatures值                                                                                                                               |
| signer                           | string                        | 发起交易并支付交易费用的 account\_keys 数组的初始值     
