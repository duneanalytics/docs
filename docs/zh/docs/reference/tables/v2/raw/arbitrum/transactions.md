# 交易表

## arbitrum.transactions

交易是来自账户的加密签名指令。帐户通过发起交易来更新以太坊网络的状态。交易始终来自外部拥有的账户，智能合约无法发起交易。

交易需要广播到整个网络。任何节点都可以广播在EVM上即将执行交易的请求；广播发送后，矿工将执行交易并将结果状态更改传播到网络的其余部分。

点击[这里](https://ethereum.org/en/developers/docs/transactions)在以太坊官方文档中阅读更多信息。

| **字段名称**              | **数据类型** | **描述**                                                                                  |
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
| gas\_price                   | numeric      | 本次交易愿意支付的最高燃料价格，单位为`wei`                                  |
| effective\_gas\_price        | numeric      | 本次交易实际支付的燃料价格，单位为`wei`                                                       |
| gas\_limit                   | numeric      | 以ArbGas表示的燃料限制                                                                          |
| gas\_used                    | numeric      | 以ArbGas表示的本次交易实际消耗的燃料数量                                                    |
| gas\_used\_for\_l1           | numeric      | 以ArbGas表示的本次交易中L1资源消耗的燃料数量                         |
| data                         | string       | 可以是空值、十六进制编码的消息或智能合约调用指令             |
| hash                         | string       | 交易的哈希值                                                                      |
| type                         | text         | 不适用于Arbitrum                                                                      |
| access\_list                 | jsonb        | 不适用于Arbitrum                                                                      |
| max\_fee\_per\_gas           | numeric      | 不适用于Arbitrum                                                                      |
| max\_priority\_fee\_per\_gas | numeric      | 不适用于Arbitrum                                                                      |
| priority\_fee\_per\_gas      | numeric      | 不适用于Arbitrum                                                                      |
