---
title: 数据抽象 (V1)
---

您可以在我们的 [公共 github 资源库](https://github.com/duneanalytics/abstractions) 中的`deprecated-dune-v1-abstractions` 查看现有的数据抽象。

您通常可以将它们分为 2 个不同的类别：

### 行业数据抽象

行业数据抽象是指 dex.trades、erc20.stablecoins、lending.borrow 等表。

这些数据抽象从多个合约和项目中获取数据，标准化它们之间的数据，因此可以很容易地查询这些数据并比较不同项目的指标。

大多数[行业](../../about/usecases/sector-dashboards.md) 看板都依赖于行业数据抽象。这引入了一个有趣的动态，项目可以通过向我们的公共 [github 资源库](https://github.com/duneanalytics/abstractions)发出拉取请求轻松地将其数据放入这些看板。
Dune 团队和社区一直在改进这些细分行业数据抽象，我们总是欢迎对现有数据的所有新添加。

### 项目数据抽象
我们往往有需求去将某个项目所需要的所有的数据汇集到一张简洁的表中。您可以在我们的数据抽象中构造视图或表来实现它
与仅构建视图相比，这里的主要优势是您可以在我们的数据抽象中处理大量数据，因为我们可以每隔几个小时在后台自动运行它们。

## 为数据抽象做贡献

我们不再对v1的数据抽象开放贡献。
如果您想为沙丘抽象做出贡献，请查看[魔法书](../../../../spellbook/index.md)。
