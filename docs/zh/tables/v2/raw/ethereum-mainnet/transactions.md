# 交易表

## ethereum.transactions

交易是来自账户的加密签名指令。帐户通过发起交易来更新以太坊网络的状态。交易始终来自外部拥有的账户，智能合约无法发起交易。

交易需要广播到整个网络。任何节点都可以广播在EVM上即将执行交易的请求；广播发送后，矿工将执行交易并将结果状态更改传播到网络的其余部分。

点击[这里](https://ethereum.org/en/developers/docs/transactions)在以太坊官方文档中阅读更多信息。

| **字段名称**              | **数据类型** | **描述**                                                                                                                                                                                        |
| ---------------------------- | ------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| block\_time                  | timestamptz  | 包含此交易的区块被开采的时间                                                                                                                                       |
| nonce                        | numeric      | 发起交易的钱包独有的交易随机数                                                                                                                                                           |
| index                        | numeric      | 当前交易中区块中的索引位置                                                                                                                                                           |
| success                      | boolean      | 显示交易是否成功的真/假值                                                                                                                                             |
| from                         | string       | 发送者的地址                                                                                                                                                                                  |
| to                           | string       | 接收者的地址。当是合约创建交易时值为NULL                                                                                                                                 |
| value                        | numeric      | 在此交易中发送的以`wei`为单位的以太币数量。请注意，erc20 代币不会出现在这里。                                                                                                       |
| block\_number                | int8         | 区块链的长度（以区块数为单位）                                                                                                                                                                 |
| block\_hash                  | string       | 当前区块的唯一标识符                                                                                                                                                                     |
| gas\_limit                   | numeric      | 以`wei`表示的燃料限制                                                                                                                                                                                   |
| gas\_price                   | numeric      | 以`wei`表示的燃料价格                                                                                                                                                                                   |
| gas\_used                    | numeric      | 以`wei`表示的当前交易消耗的燃料数量                                                                                                                                                             |
| data                         | string       | 可以是空的、十六进制编码的消息或智能合约调用指令                                                                                                                   |
| hash                         | string       | 交易的哈希值                                                                                                                                                                            |
| type                         | text         | 交易类型：`Legacy`，`AccessList`或`DynamicFee`                                                                                                                                    |
| access\_list                 | jsonb        | 交易准备访问的地址和存储密钥的列表。参见[EIP2930](https://eips.ethereum.org/EIPS/eip-2930)。适用于交易类型为`AccessList`或`DynamicFee`的情况 |
| max\_fee\_per\_gas           | numeric      | 交易发送者愿意支付的每单位燃料的最高费用总额（由[EIP1559](https://eips.ethereum.org/EIPS/eip-1559)引入）                                                              |
| max\_priority\_fee\_per\_gas | numeric      | 交易发送者愿意向矿工支付的每单位燃料的最高费用，以激励他们包含他们的交易（由[EIP1559](https://eips.ethereum.org/EIPS/eip-1559)引入）            |
| priority\_fee\_per\_gas      | numeric      | 本次交易支付给矿工的优先费用（由[EIP1559](https://eips.ethereum.org/EIPS/eip-1559) 引入）                                                                         |
