# 区块表

## bnb.blocks

区块是区块链和汇总（rollups）的构建组件。一个区块包含将逐渐改变EVM系统状态的多个交易。区块内的交易只能一个接一个地执行，不能并行执行。

| **字段名称**     | **数据类型** | **描述**                                                                          |
| ------------------- | ------------ | ---------------------------------------------------------------------- |
| time                | timestamptz  | 当前区块被开采的时间                                                     |
| number              | numeric      | 区块链的长度（以区块数为单位）                                                  |
| hash                | string       | 当前区块的唯一标识符                                                      |
| parent hash         | string       | 前一个区块的唯一标识符                                               |
| gas\_limit          | numeric      | 当前区块的燃料限制                                                      |
| gas\_used           | numeric      | 当前区块消耗的燃料数量                                                              |
| miner               | string       | 矿工的地址                                                                 |
| difficulty          | numeric      | 难度值，即开采当前区块所需的努力                                                   |
| total\_difficulty   | numeric      | 区块链到当前区块为止的总难度值                                          |
| nonce               | string       | 区块随机数，用于展示挖矿过程中的工作量证明                  |
| size                | numeric      | 区块的大小（以字节为单位），受本区块燃料限制的约束                                       |
| base\_fee\_per\_gas | numeric      | N/A                                                                    |
