# 事件日志表

## polygon.logs

该表存储所有由智能合约产生的日志。它对查询尚未解析的合约很有用，包括那些因为代码未公开的智能合约。

日志是一种优雅的方式，可以用极少量的手续费，在EVM区块链上存储极少量的数据。具体来说，事件日志对于让其他人知道发生了什么事是很有用的，而不需要他们单独查询合约。


更多信息请阅读 [这篇文档](https://medium.com/mycrypto/understanding-event-logs-on-the-ethereum-blockchain-f4ae7ba50378).



**Note: 我们的topic索引会便宜, 所以 `topic0` 会显示成 `topic1`, `topic1` 显示成 `topic2` ，以此类推。**

| **列名**   | **数据类型** | **说明**                                                                                              |
| ----------------- | ------------ | ------------------------------------------------------------------------------------------------------------ |
| block\_hash       | bytea        | 该区块的唯一标识符                                                                           |
| block\_number     | int8         | 区块链的高度（以块为单位）                                                                       |
| block\_time       | timestamptz  | 区块被开采的时间                                                     |
| contract\_address | bytea        | 发出日志的合约地址                                                             |
| topic1            | bytea        | 对事件声明函数用keccak256函数运算后的哈希值                                                       |
| topic2            | bytea        | 事件的索引主题2                                                                                 |
| topic3            | bytea        | 事件的索引主题3                                                                                 |
| topic4            | bytea        | 事件的索引主题4                                                                                 |
| data              | bytea        | 事件中未索引的数据值                                                   |
| tx\_hash          | bytea        | 事件的交易哈希                                               |
| index             | numeric      | 这个log在区块中的索引位置 (按日志执行的顺序累计)                       |
| tx\_index         | numeric      | 改transaction交易在区块中的索引位置（ 按交易执行的顺序累计) |

