# 区块表

## bnb.blocks


区块是区块链的基本单元，一个区块包含的交易记录会增量的改变EVM的状态，一个块中的交易只能一个接一个地执行，不能并行执行。

| **列名**     | **数据类型** | **说明**                                                                          |
| ------------------- | ------------ | ---------------------------------------------------------------------------------------- |
| time                | timestamptz  | 区块被矿工验证的时间.                                                       |
| number              | numeric      | 区块的高度                                                   |
| hash                | bytea        | 区块的唯一id                                                       |
| parent hash         | bytea        | 前一个区块的唯一id                                                |
| gas\_limit          | numeric      | 当前区块的gas限制                                                       |
| gas\_used           | numeric      | 当前区块中使用的gas                     |
| miner               | bytea        | 矿工的地址                                                                 |
| difficulty          | numeric      | 开采区块所需的难度值                                                    |
| total\_difficulty   | numeric      | 直到这个区块的总难度值                                           |
| nonce               | bytea        | 区块随机数，用于展示挖矿过程中的工作量证明                   |
| size                | numeric      | 此块的大小（以字节为单位）（受限于 gas limit）                                        |
| base\_fee\_per\_gas | numeric      | n/a |

