# 区块表

## gnosis.blocks

区块是区块链和汇总（rollups）的构建组件。一个区块包含将逐渐改变EVM系统状态的多个交易。区块内的交易只能一个接一个地执行，不能并行执行。

| **字段名称**     | **数据类型** | **描述**                                                                          |
| ------------------- | ------------ | ---------------------------------------------------------------------------------------- |
| time                | timestamptz  | 当前区块被开采的时间                                                     |
| number              | numeric      | 区块链的长度（以区块数为单位）                                                  |
| hash                | bytea       | 当前区块的唯一标识符                                                      |
| parent hash         | bytea       | 前一个区块的唯一标识符                                               |
| gas\_limit          | numeric      | 当前区块的燃料限制                                                      |
| gas\_used           | numeric      | 当前区块消耗的燃料数量                                                              |
| miner               | bytea       | 矿工的地址                                                                 |
| difficulty          | numeric      | 难度值，即开采当前区块所需的努力                                                   |
| total\_difficulty   | numeric      | 区块链到当前区块为止的总难度值                                          |
| nonce               | bytea       | n/a                 |
| size                | numeric      | 区块的大小（以字节为单位），受本区块燃料限制的约束                                       |
| base\_fee\_per\_gas | numeric      | 当前区块的基本燃料费用（由[EIP1559](https://eips.ethereum.org/EIPS/eip-1559)）引入 |
