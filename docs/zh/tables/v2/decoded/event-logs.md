# 事件日志

### 事件日志

当某些预先定义的操作完成时，智能合约会产生**事件日志**。这些日志的产出结构是由智能合约的开发者预先定义的，日志的内容是在交易过程中动态生成的。

日志对于监控、警报和日常跟踪智能合约内部发生的事情很有用。 作为数据分析师，日志是您最好的朋友，因为它们为您提供了用于事后分析的可靠的数据。如果您想查看某一个智能合约可以产生哪些日志，您只需在智能合约的源代码中搜索关键字 `emit` 即可。

我们会将智能合约所有事件的日志解码为根据此方式命名的表：`projectname_blockchain.contractName_evt_eventName`。

让我们停留在 [uniswap v3 factory](https://etherscan.io/address/0x1f98431c8ad98523631ae4a59f267346ea31f984#code) 的上下文中，看看在创建新池子的时候所产生的事件。该事件被称为“PoolCreated”，每次有人通过调用“createPool”函数成功部署新的 Uniswap V3 池子的时候都会触发该事件。该事件将很容易地为我们提供池子中的代币循序、该池的费率等级和tick spacing等信息。在 Etherscan 中，您可以通过打开[日志选项卡](https://etherscan.io/tx/0xdeb368592f3de0f2840754bce61d2c3f29cdb3407c63c699052e68a854c71eaa#eventlog)简单地找到事件的日志。 在 Dune 中，这种特定事件将存储在表 [`uniswap_v3_ethereum.Factory_evt_PoolCreated`](https://dune.com/queries/757381) 中。


**多个实例**

如果有多个合约实例，我们将在一张表中收集此智能合约所有实例的所有事件日志。 例如，所有 uniswap v3 池子的 `swap` 事件（以太坊上的）都存储在表 \`\` [`uniswap_v3_ethereum.Pair_evt_Swap`](https://dune.com/queries/742037)中。`contract_address` 列表明了是哪个智能合约发出了此事件。

**延伸阅读:**

[了解以太坊上的事件日志](https://medium.com/mycrypto/understanding-event-logs-on-the-ethereum-blockchain-f4ae7ba50378)

[关于以太坊上的事件和日志你想知道的一切](https://medium.com/linum-labs/everything-you-ever-wanted-to-know-about-events-and-logs-on-ethereum -fec84ea7d0a5)
