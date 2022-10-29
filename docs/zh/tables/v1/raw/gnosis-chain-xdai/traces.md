# Traces

## gnosis.traces

Traces是交易中可以改变以太坊虚拟机状态的最小原子操作，这些操作的信息会被记录下来，并且可以存储为EVM执行跟踪，或者简称 _跟踪（trace）_，在Etherscan上称为”内部交易“。

更多内容请阅读[这里](https://medium.com/chainalysis/ethereum-traces-not-transactions-3f0533d26aa).

| **列名** | **数据类型** | **说明**                                                                                                                                                                                                                                |
| --------------- | ------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| block\_time     | timestamptz  | 区块被开采的时间                                                                                                                                                                                                              |
| tx\_success     | boolean      | 显示交易是否成功的真/假值                                                                                                                                                                                 |
| success         | boolean      | 显示跟踪操作是否成功的真/假值                                                                                                                                                                                    |
| block\_hash     | bytea        | 该区块的唯一标识符                                                                                                                                                                                                             |
| block\_number   | int8         | 区块链的长度（以块为单位）                                                                                                                                                                                                         |
| tx\_hash        | bytea        | 事件的交易哈希                                                                                                                                                                                                              |
| from            | bytea        | 发送者的地址                                                                                                                                                                                                                          |
| to              | bytea        | 接收者的地址。当是合约创建交易时为NULL                                                                                                                                                                       |
| value           | numeric      | 在此交易中发送的以 wei 为单位的以太币数量。                                                                                                                                                                                         |
| gas             | numeric      | gas 限制                                                                                                                                                                                                             |
| gas\_used       | numeric      | 以 wei 为单位的交易消耗的 gas                                                                                                                                                                                                     |
| tx\_index       | numeric      | 交易索引                                                                                                                                                                                                    |
| trace\_address  | array        | 调用图森林中的跟踪地址。例如，[0, 2, 1] 是 [0, 2, 1, 0] 的父级。                                                                                                                                            |
| sub\_traces     | numeric      | 子跟踪(trace)的数量                                                                                                                                                                                                                  |
| type            | text         | 描述在此trace中执行的操作类型，可以是 `reward`, `create`, `call` or `suicide`。                                                                                                                                              |
| address         | bytea        | 当类型type是`suicide` or `create`被调用的合约                                                                                                                                                                           |
| code            | bytea        | 部署新合约的子节代码数据，只包括type是`create`的数据。                                                                                                                                                               |
| call\_type      | bytea        | <p>可以是 <code>staticcall</code>, <code>delegatecall</code> or <code>call</code>.<br>更多信息请参考 <a href="https://medium.com/coinmonks/delegatecall-calling-another-contract-function-in-solidity-b579f804178c">这里</a>. </p> |
| input           | bytea        | 对另一个智能合约的调用的字节码                                                                                                                                                                                |
| output          | bytea        | 被调用的智能合约的字节码                                                                                                                                                                              |
| refund\_address | bytea        | 包括类型`type` 是 `suicide`的数据，用于指定将以太坊余额发送到哪里                                                                                                                                          |




### traces中的gas使用

* 一个trace中的`gas_used`包括该trace和它所有的子trace所消耗的gas。
* 最初调用的`gas_used`不包括首先进行调用的费用。
  * 你需要把21000个gas单位+发送0的费用+非零字节的费用加到顶部trace的`gas_used`值中，以得出"真正的"`gas_used`值。
  * 关于这个问题的更多阅读请参考这个[stackexchange条目](https://ethereum.stackexchange.com/questions/31443/what-do-the-response-values-of-a-parity-trace-transaction-call-actually-repres)
  * 在dune中做的一个查询。[https://dune.com/queries/895857](https://dune.com/queries/895857)
