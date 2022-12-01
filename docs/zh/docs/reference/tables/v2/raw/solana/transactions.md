# 交易表

## Solana.transactions

此表包含Solana区块链中的交易数据。此表中提供了与帐户、协议和计划活动相关的大多数相关数据。

查询示例可以在这里找到：[过去7天热门程序的NFT交易](https://dune.xyz/queries/390720/745376)和[drift-protocol概述](https://dune.xyz/bigz/drift-\(solana\))

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
| signer                           | string                        | 发起交易并支付交易费用的 account\_keys 数组的初始值                                                                                                                            |

### 结构定义

在其中的几个列中使用了STRUCT数据类型，它允许表示嵌套的分层数据并具有键值对。它类似于python中的字典，可用于将字段组合在一起以使它们更易于访问。

一个如何关于从结构字段提取数据的示例：[Solana去中心化交易所的指令数](https://dune.xyz/queries/416358/794290)

**token\_balance**

| 字段名称   | 字段类型 | 描述                                                                                                                                                                  |
| ------- | --------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| account | string    | 代币余额归属的帐户地址                                                                                                       |
| mint    | string    | 代币铸造合约的公钥。这是一个存储有关代币元数据的帐户：供应量、小数位数以及控制铸造的各种权限。         |
| amount  | Decimal   | 源自代币余额的原始金额 (ui\_token\_amount.amount) 和小数位数 (ui\_token\_amount.decimals)                                               |

***

**instructions**

| 字段名称               | 字段类型                          | 描述                                                    |
| ------------------- | ---------------------------------- | -------------------------------------------------------------- |
| account\_arguments  | array\<string>                     | 要传递给程序的帐户的有序列表                |
| data                | string                             | 以base-58编码的程序输入数据                         |
| executing\_account  | string                             | 执行此指令的程序的帐户地址 |
| inner\_instructions | array\<STRUCT inner\_instructions> | 该指令调用的内部指令                  |

***

**inner\_instructions**

| 字段名称              | 字段类型      | 描述                                                    |
| ------------------ | -------------- | -------------------------------------------------------------- |
| account\_arguments | array\<string> | 要传递给程序的帐户的有序列表                |
| data               | string         | 以base-58编码的程序输入数据                         |
| executing\_account | string         | 执行此指令的程序的帐户地址        |

***

**error**

| 字段名称                  | 字段类型 | 描述                        |
| ---------------------- | --------- | ---------------------------------- |
| **instruction\_index** | int       | 失败的指令号码 |
| message                | string    | 错误信息                  |

##
