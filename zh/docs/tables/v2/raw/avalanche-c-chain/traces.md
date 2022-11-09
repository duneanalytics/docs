# 内部合约调用表

## avalanche\_c.traces

交易（Transactions）可以触发修改以太坊虚拟机内部状态的更小的原子操作。有关这些操作执行的信息会被记录下来，并且可以存储为EVM执行内部合约，或者只是一个_内部合约_。在Etherscan中，这些被称为“内部交易”。

点击[这里](https://medium.com/chainalysis/ethereum-traces-not-transactions-3f0533d26aa)阅读更多信息。

| **字段名称** | **数据类型** | **描述**                                                                                                                                                                                                                               |
| --------------- | ------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| block\_time     | timestamptz  | 包含此内部合约调用的区块被开采的时间                                                                                                                                                                                                             |
| tx\_success     | boolean      | 指示交易是否成功的真/假值                                                                                                                                                                                |
| success         | boolean      | 指示当前内部合约调用操作是否成功的真/假值                                                                                                                                                                                   |
| block\_hash     | string       | 当前区块的唯一标识符                                                                                                                                                                                                            |
| block\_number   | int8         | 区块链的长度（以区块数为单位）                                                                                                                                                                                                        |
| tx\_hash        | string       | 发出此内部合约调用的交易的哈希值                                                                                                                                                                                                            |
| from            | string       | 发送者的地址                                                                                                                                                                                                                         |
| to              | string       | 接收者的地址。当它是一个合约创建交易时，其值为`Null`                                                                                                                                                                     |
| value           | numeric      | 本次交易中发送的avx数量，以`nanoavax`表示                                                                                                                                                                                       |
| gas             | numeric      | 随消息调用发送的燃料数量                                                                                                                                                                                                            |
| gas\_used       | numeric      | 消息调用消耗的燃料数量，以`nanoavax`表示                                                                                                                                                                                                   |
| tx\_index       | numeric      | 归属的交易在区块中的索引位置                                                                                                                                                                                                   |
| trace\_address  | array        | 当前内部合约调用在调用图森林中的地址。例如，[0, 2, 1] 是 [0, 2, 1, 0] 的父级                                                                                                                                           |
| sub\_traces     | numeric      | 子级内部合约调用的数量                                                                                                                                                                                                                 |
| type            | text         | 可以是`reward`，`create`，`call`或者`suicide`。描述在此内部合约调用中使用的操作类型。                                                                                                                                             |
| address         | string       | 当类型是`suicide`或者`create`时保存调用的合约地址                                                                                                                                                                            |
| code            | string       | 部署新合约的字节码，仅在调用类型为`create`时包含数据。                                                                                                                                                              |
| call\_type      | string       | <p>可以是<code>staticcall</code>，<code>delegatecall</code>或者<code>call</code>。<br>更多信息请参考<a href="https://medium.com/coinmonks/delegatecall-calling-another-contract-function-in-solidity-b579f804178c">这里</a>。</p> |
| input           | string       | 调用另一个智能合约的字节码                                                                                                                                                                               |
| output          | string       | 被调用智能合约发送回来的字节码响应                                                                                                                                                                             |
| refund\_address | string       | 仅在`type`是`suicide`时包含数据。指定将未支出的以太币余额发送到哪里。                                                                                                                                            |

### 内部合约调用消耗的燃料

avax\_c.traces表中的`gas_used`字段有点难以理解，所以这里有一些提示：

* 内部合约调用的`gas_used`将始终包括合约调用本身以及其所有子级合约调用所消耗的燃料。
* 初始调用的`gas_used`将不包含发起调用时已发生的燃料消耗。
* 您需要将“21000个燃料单位 + 发送零子节及发送非零字节的燃料成本”添加到顶部内部合约调用的`gas_used`值上，以得到“真实”的`gas_used`值。
* 有关此内容的更多信息，请参阅此[stackexchange条目](https://ethereum.stackexchange.com/questions/31443/what-do-the-response-values-of-a-parity-trace-transaction-call-actually-repres)
* 在Dune中执行此操作的查询示例：[https://dune.com/queries/895857](https://dune.com/queries/895857)
