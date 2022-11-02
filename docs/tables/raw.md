---
标题: 原始数据表
---

**原始数据表提供了原始未经过滤和编辑的数据。**

这允许你跨Dune支持的区块链查询任何交易、区块、事件日志或记录。原始数据表对于获取有关区块链、交易、记录或特定事件的元信息非常有用。

此外，通过一些技巧，你实际上可以使用编码数据深入了解智能合约系统。[Alex Kroeger](https://twitter.com/alex\_kroeger) 关于这个话题写了[一篇很棒的文章](https://alexkroeger.mirror.xyz/0C3EQBtFqAK4k2TAGPZhg0JMY-upfTAxuTD-o91vBPc)。

我们有几个[SQL函数](https://github.com/duneanalytics/spellbook/tree/master/ethereum/public)在我们的数据库中，你可以通过它们更轻松地处理编码数据。

然而，由于这些表中常见的编码数据的性质，使用原始数据表编写的查询很难理解和审阅。此外，原始数据表具有非常多的行，因此查询速度可能很慢。

大多数时候，你最好是[提交合同进行解码]（../features/decoded contracts.md）和使用[解码数据]（decoded.md）。

## EVM链的差异

EVM链大体上遵循相同的执行模型，但有时共识算法、gas成本甚至gas成本的计算存在差异。

您可以在文档中找到有关各个链的信息：

<div class="cards grid" markdown>
- [V1引擎](v1/raw/index.md) (PostgreSQL)
- [V2引擎](v2/raw/index.md) (Databricks SQL)
</div>




