---
title: 查询入门
description: Here's a short five-step guide to getting familiar with a protocol and figuring out how to query around it using Dune.
---

这里有一个简短的五步指南，以熟悉一个协议并弄清楚如何使用 Dune 进行查询。

感谢 [@ilemi](https://dune.com/ilemi) 整理此版内容！

[在此了解更多关于查询的内容](../queries/index.md)。

## 1. 找到主要切入点

使用 [Dune 数据浏览器](../queries/data-explorer.md)和协议应用界面/文档，并试着找出主要的用户入口点功能是什么。

有时这很直接，但在更复杂的协议上，不同的合约模式会让人感到困惑。

对于大多数去中心化金融（DeFi）来说，用户的主要入口只是 `Deposit`（存款）的一些变化。

如果合约还没有[解析](../decoding-contracts.md)，您可以从一些原始查询开始，在这里找到最常见的函数和事件签名：[Dune Utility Queries](../../reference/wizard-tools/utility-queries.md)。

如果您在理解数据表方面有困难，[请见我们的数据表文档](../../reference/tables)。  
    
## 2. 探索合约流程

通常情况下，一个函数调用并不像 ETH/代币 转移那样简单，只涉及一个合约。

一旦您弄清楚了入口点，对它运行一个基础的 LIMIT 查询，并在[相关区块链浏览器](../../reference/wizard-tools/blockchain-explorers.md)中查看一些示例交易以获得一些数据提示（即除了主协议之外，tx 还与哪些协议互动）。
    
```sql
SELECT * FROM protocol_name."Contractname_evt_EventEmitted"
LIMIT 10
```
查看 `evt_tx_hash` 并把它放到区块链浏览器中，开始了解所涉及的合约和交互。
  
## 3. 决定您要回答什么问题

如果您心里已经有了问题，那就跳过这一步。如果您还没有问题，就通过合约互动的流程图来思考。

这里有一些启发问题，可以帮助您找到有趣的东西来研究：

1. 入口功能还触及哪些协议？
2. 如果有收益率/利息产生，代币是在什么地方和什么时候交易的？
3. 有多少代币进入，到最后有多少被烧毁/铸造了？
4. 有没有可能后三个问题中的任何内容都会导致某种不平衡或积累？即 DEX 池以低流动性结束，或向一个池中存入如此多的存款，以至于收益率/利息因供应不平衡而下降。或者，如果这涉及到 NFT，对未来的买卖行为有什么影响（或者有导致这一交易的买卖行为）？

## 4. 创建您的查询

现在您已经确定了一个问题，真正的乐趣开始了。🧙

您会很快发现，函数调用数据和事件日志数据并不总是有您要找的所有参数。

通常缺少的罪魁祸首是交易签名者（在 `ethereum. "transactions"` 中找到）和转移的 ETH 值（在 `ethereum. "traces"` 中找到）。

通常情况下，您必须与基础表（交易、内部合约、日志）以及可能来自其他协议（如 DEX/交易所 协议）的数据表合作，以完成您的查询所需的数据。

要想知道从哪些表中提取什么数据，需要学习一段时间，而开始的最好方法通常是搜索现有的看板或尝试过类似东西的查询。

Dune 已经存在了很长时间，大多数查询模式在其他地方并不难找到。✨

## 5. 创建您的可视化

最后，您应该通过点击 "Query Results" 旁边的 "New visualization"，在图表中对查询进行可视化。 
    
    ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/8dbf893c-33f5-47cb-8d4f-41ff4b2df8d6/Untitled.png)
    
如果您显示的是代币数额，您可能需要[调整小数](https://dune.xyz/queries/85746)或乘以代币价格（在 `prices.usd` 或 `dex.trades` 中），以获得更可读的美元值。