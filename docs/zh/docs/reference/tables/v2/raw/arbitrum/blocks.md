# 区块表

## arbitrum.blocks

区块是区块链和汇总（rollups）的构建组件。一个区块包含将逐渐改变EVM系统状态的多个交易。区块内的交易只能一个接一个地执行，不能并行执行。

| **Column Name**     | **datatype** | **Description**                           |
| ------------------- | ------------ | ----------------------------------------- |
| time                | timestamptz  | 当前区块被开采的时间        |
| number              | numeric      | 区块链的长度（以区块数为单位）    |
| hash                | string       | 当前区块的唯一标识符        |
| parent hash         | string       | 前一个区块的唯一标识符 |
| gas\_limit          | numeric      | 当前区块的ArbGas燃料限制     |
| gas\_used           | numeric      | 当前区块消耗的ArbGas燃料数量             |
| miner               | string       | 不适用                            |
| difficulty          | numeric      | 不适用                            |
| total\_difficulty   | numeric      | 不适用                            |
| nonce               | string       | 不适用                            |
| size                | numeric      | 不适用                            |
| base\_fee\_per\_gas | numeric      | 不适用                            |
