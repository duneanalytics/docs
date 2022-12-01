# 交易表

## optimism.transactions

交易是来自账户的加密签名指令。帐户通过发起交易来更新以太坊网络的状态。交易始终来自外部拥有的账户，智能合约无法发起交易。

交易需要广播到整个网络。任何节点都可以广播在EVM上即将执行交易的请求；广播发送后，矿工将执行交易并将结果状态更改传播到网络的其余部分。

点击[这里](https://ethereum.org/en/developers/docs/transactions)在以太坊官方文档中阅读更多信息。

| **字段名称**              | **数据类型** | **描述**                                                                                                                                                                                        |
| ---------------------------- | ------------ | ------------------------------------------------------------------------------------------------ |
| block\_time                  | timestamptz  | 包含此交易的区块被开采的时间                                                                                                                                       |
| nonce                        | numeric      | 发起交易的钱包的唯一值交易随机数                                                                                                                                                           |
| index                        | numeric      | 当前交易在区块中的索引位置                                                                                                                                                           |
| success                      | boolean      | 显示交易是否成功的真/假值                                                                                                                                             |
| from                         | string       | 发送者的地址                                                                                                                                                                                  |
| to                           | string       | 接收者的地址。当是合约创建交易时值为`NULL`                                                                                                                                 |
| value                        | numeric      | 在此交易中发送的以`wei`为单位的以太币数量。请注意，erc20代币不会出现在这里。                                                                                                       |
| block\_number                | int8         | 区块链的长度（以区块数为单位）                                                                                                                                                                 |
| block\_hash                  | string       | 当前区块的唯一标识符                                                                                                                                                                     |
| gas\_limit                   | numeric      | 以`wei`表示的燃料限制                                                                                                                                                                                   |
| gas\_price                   | numeric      | 以`wei`表示的燃料价格                                                                                                                                                                                   |
| gas\_used                    | numeric      | 以`wei`表示的当前交易消耗的燃料数量                                                                                                                                                             |
| data                         | string       | 可以是空值、十六进制编码的消息或智能合约调用指令                                                                                                                   |
| hash                         | string       | 交易的哈希值                                                                                                                                                                            |
| type                         | text         | 交易类型：`Legacy`，`AccessList`或`DynamicFee`                                                                                                                                    |
| access\_list                 | jsonb        | n/a               |
| max\_fee\_per\_gas           | numeric      | n/a                                                              |
| max\_priority\_fee\_per\_gas | numeric      | n/a            |
| priority\_fee\_per\_gas      | numeric      | n/a                                                                         |
| l1\_gas\_used                | numeric      | 将输入数据（calldata）发送到L1的成本                                               |
| l1\_gas\_price               | numeric      | L1上的燃料价格                                                                             |
| l1\_fee                      | numeric      | 以`wei`表示的L1上支付的燃料费                                                                     |
| l1\_fee\_scalar              | numeric      | 确保L1上的燃料成本得到覆盖并且有利可图的可变参数                    |
| l1\_block\_\number           | numeric      | 该批次交易在L1上结算的区块的编号                 |
| l1\_timestamp                | numeric      | 此交易在L1上批量结算的区块的时间戳                     |
| l1\_tx\_origin               | numeric      | ??                                                                                               |

\*\*\*\*[**请自行查看查询示例**](https://dune.xyz/queries/38964)\*\*\*\*
