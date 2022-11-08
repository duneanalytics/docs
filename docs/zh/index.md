---
title: 欢迎
description: 欢迎来到 Dune 文档
hide:
  - navigation
---

<style>
  .md-typeset h1,
  .md-content__button {
    display: none;
  }
  .md-header__topic{
    font-weight: bold;
  }
</style>

![Dune Docs cover](images/dune-docs-cover.jpg)

Dune 是一个强大的区块链研究工具，配备了您需要的所有工具，以发现、探索和可视化大量区块链数据。


 Dune 是您解答问题的关键，比如：

- [Uniswap 每天经手多少交易量？](https://dune.com/queries/3)
- [哪个 Dex 有最高的交易量？](https://dune.com/queries/1847)
- [重要的稳定币今天表现如何？](https://dune.com/hagaetc/stablecoins)

## 5 分钟 ⚡ 快速的 Dune 简介

![type:video](https://www.youtube.com/embed/S-cctFmR828)

## Dune 是如何运作的

首先，Dune 是一个数据平台，它摄取了难以获取的区块链数据，并通过一个 SQL 数据库使其可以访问。

使用 SQL 查询，您可以快速搜索并从我们的数据库中提取各种各样的区块链信息，然后将其转化为人类可读的数据表和可视化信息。

Dune 同时拥有原始区块链数据和解析后的区块链数据。

解析后的数据只有在有人特别要求我们对合约进行解析的情况下才可用，您可以通过我们的[提交表格](https://dune.com/contracts/new)（在登录到您的 Dune 账户时）进行解析。

您当前可以从以下数据源查询数据：

- **Ethereum**
- **Polygon**
- **Arbitrum**
- **BNB 链**
- **Optimism**
- **Gnosis 链**
- **Solana**

Dune 从我们索引的区块链中获取事件和内部合约调用，我们没有状态/存储数据。

## Dune.com

Dune.com 是建立在 Dune 数据平台之上的第一个杀手级应用，旨在让任何至少有一点 SQL、以太坊虚拟机和商业知识的人尽可能容易地以有趣的方式分析区块链数据。

Dune.com 应用程序的基本构成部分是：

- **数据看板：**一组包含可视化和文本的小部件，讲述了一个关于特定区块链数据组的故事。
- **可视化：**图表和图形，将难以理解的数据表形式的数据变成更容易理解的视觉形式。
- **查询：**从Dune的数据库中提取数据的命令，以便通过数据表和可视化显示在 Dune 看板中。

作为一名 Dune.com 的访问者，您会看到包含文本、数据表和可视化部件的看板，这些部件是由查询组建的。

作为一名 Dune 巫师（即比“区块链分析师”更酷的称呼），您将创建自定义查询来获取数据，将这些查询的结果可视化，然后用您的数据通过看板讲述故事。

### 查询

Dune 将区块链数据汇总到一个可以轻松查询的 SQL 数据库中。

[查询](features/queries/index.md)是用来指定在我们的数据库中找到区块链的哪些数据并返回。

也许您想知道 _今天发生的所有 Dex 交易_，或者 _今年铸造的稳定币的总价值_。不管是什么问题，探索答案都要从 Dune 查询开始！

查询返回数据的行和列（就像传统的 SQL 查询），然后可以用来创建可视化形式，并在看板上展示。

![SQL 查询——Uniswap USD 交易量](images/sql-query-uniswap-usd-volume.png)

区块链分析师（即 巫师 即你！）有几种方法可以开始运行查询：

1. 最简单的方法是使用 Dune [_数据抽象（Abstractions）_](tables/abstractions.md) 来查询常用的数据表格。一些流行的数据抽象包括 `dex.trades`, `lending.borrow`，和 `stablecoin.transfer`。
2. 查询原始以太坊数据，如区块、日志和交易。
3. 也可以查询中心化交易所的数据。如，您可以使用 `prices.usd` 来快速返回几乎所有加密资产的价格。

### 可视化

以表格形式呈现的数据（行和列）可能难以阅读。[可视化](features/visualizations/index.md) 将查询的结果以一种清晰、精确和 _可视化_ 的方式呈现出来。

通过 Dune 可视化，您可以很容易地开始用您的数据讲述一个故事，通过这样的转换：

![Table chart](images/table-chart.png)

变成这样：

![Bar chart](images/bar-chart.png)

可视化的柱状图使人清楚地看到，4月19日的转移总价值最高，以帮助您和其他人看到一段时间内的趋势。

Dune 提供了各种可视化，您可以用它来直观地展示数据，包括：

- **柱状图**
- **区域图**
- **散点图**
- **线状图**
- **饼状图**
- **计数器**
- **数据表**

### 数据看板

使用精心策划的可视化内容，聪明的区块链分析师（巫师！）可以通过 [Dune 数据看板](features/dashboards.md)讲述不同数据集合的故事。

例如，在下面看板中，[@hagaetc](https://dune.com/hagaetc) 创建的 [Dex Metrics](https://dune.com/hagaetc/dex-metrics)，在顶部可以清楚地看到 "DEX"（去中心化交易所）作为一个类别正在增长。在下面，访问者可以看到哪些 DEX 在交易量上最受欢迎，最后还可以看到一个堆叠的柱状图，显示随时间的变化。

仅仅通过查看这个单一的看板，任何人都可以清楚地了解整个 DEX 市场的情况。

![Dashboard](images/dashboard.png)

## Dune 是一个社区的努力

在 Dune.com 上，所有的查询和数据集默认都是公开的（如果您需要对您的查询进行保密，我们的 [Pro Plan](https://dune.com/pricing) 可以满足您的要求）。

这使得您，巫师，可以轻而易举地分叉和混合组建其他创造者的查询，以建立在他们的知识和洞察力之上。

反过来说，您创建的每一个新查询，都会帮助其他人通过 Dune 学习关于区块链和加密资产的新知识。

这种积极的反馈循环是 Dune 社区如何通过不断增长的查询，让我们大家学习更多的东西而共同成功的！

加入我们的[社区 Discord](https://discord.gg/BJBHFR6sdy)，从我们的团队和社区获得世界级的支持。

查看我们的[活动日历](resources/events.md)，加入有趣的**现场活动**。

如果您有任何反馈，无论是功能要求还是错误报告，请[在此](https://feedback.dune.com)提交。
