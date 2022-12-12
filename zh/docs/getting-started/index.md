---
title: 入门
description: Getting Started is the place to get oriented and learn how to use Dune!
---

入门是了解方向和学习如何使用 Dune 的地方！

## Dune 是为技术性和非技术性用户制作的。

无论您是一位经验丰富的 SQL 开发人员，区块链研究者，商业分析师或以上都不是——您可以使用 Dune 在瞬间开始分析区块链数据。

在我们社区的帮助下，我们已经创建了很多有用的指南和工具，以帮助您成为一位成熟的 Dune 巫师。

开始使用 Dune 的绝对最快的方法是跟随我们的[入门视频系列](guides/video-tutorial.md)，并在这里查看我们的[入门看板](https://dune.com/dune/get-started)。

接下来是否要深入取决于您是否：

1. 已经了解 SQL 
2. 是倾向于预备学习（Just-in-Case）还是适时学习（Just-in-Time）

=== "预备学习"
    预备学习是学校式的——先阅读和观看大量内容以获得大致的理解，然后开始尝试动手。

    如果这是您喜欢的学习方式，我们的长篇[《Dune 指南》](guides/dune-guides.md)比我们的视频要深入得多，同时仍然通过简单的项目引导您，让您对如何用 Dune 进行创作有一个大致的了解。

    [OurNetwork 课程](dune-guides/#ournetwork-course)也提供了一个详尽的、广泛的概述。

=== "适时学习"
    适时学习是为那些在实践中学习的人准备的。如果您已经对您想用 Dune 做什么有了想法，只是需要通过寻找一些具体的策略知识来释放自己的想法，那么[核心功能](queries/index.md)很可能包含您需要的信息。

    [数据表](../reference/tables/index.md)和[魔法书](../spellbook/index.md)是更高级的功能，一旦您理解了基础知识，就值得去尝试。

    请务必在[#beginners Discord channel](https://discord.com/channels/757637422384283659/1016725609797402634)中提出您的任何问题！


=== "不了解 SQL？"
    如果您对 SQL 不是很熟悉，可以从这里开始探索我们的 [SQL Guides 指南](guides/sql-guides.md)。


## 要成为一名伟大的巫师，您需要知道什么？

![it's easy for Hermione](images/wingardium.gif)

### 如何使用 SQL

为了能够成功地在 Dune 上查询数据，用户需要对 SQL 有一个基本的了解。

[SQL](https://www.w3schools.com/sql/sql_intro.asp) 在软件开发行业中被广泛使用，您可以找到很多关于它的非 Dune 特定文档。这往往有助于回答与查询有关的问题，因为大多数答案可以在互联网上很容易找到。


!!! note
    默认情况下，该文档显示了我们的 Dune V1 引擎的信息，该引擎在 PostgreSQL 数据库上运行。
    我们的新数据平台，[Dune 引擎 V2](https://dune.com/blog/dune-engine-v2) 目前处于测试阶段，其采用的是 Databricks SQL 的查询引擎。它提供了令人兴奋的功能，如更好的扩容，跨链查询和[魔法书](../spellbook/index.md)。Dune 引擎 V2 在接下来的几个月里，将成为默认引擎，所以我们建议您尝试一下！

=== "基础 SQL"
    如果您对 SQL 不是特别熟悉，我们建议从我们的 [SQL 指南](guides/sql-guides.md)开始。

=== "PostgreSQL"
    官方 [PostgreSQL 文档](https://www.postgresql.org/docs/12/index.html)很棒。Dune 在 PostgreSQL 12.2 上运行。

=== "Databricks SQL"
    官方 [Databricks SQL ](https://docs.databricks.com/sql/language-manual/index.html) 文档非常有帮助。

### 如何解析以太坊虚拟机数据

您将在链上和 Dune 的数据库中找到的数据几乎都是从基于 Ethereum 虚拟机的环境中提取的。

因此，了解以太坊虚拟机和智能合约的整体工作方式，是能够找到、理解和使用 Dune 中许多可用数据的重要基础。

如果您能够读取 Etherscan 中的大部分数据，那么您已经在用 Dune 创建有洞察力的查询和可视化的路上走得很远了。

不幸的是，我们目前还没有找到一个很好的资源可以指给您看，因为每个智能合约都有它自己的规则。我们已经在我们的[已解析数据](../reference/tables/decoded.md)部分写了一些关于这个问题的文字。

### 社区、协议和企业关心什么

这一点可能会让您感到惊讶，但成为一个有效的数据分析巫师的一个关键组成部分是了解如何将“信号与噪音”区分开。

有些数据是有趣和有价值的，有些数据则不是。知道如何将有趣的部分挑选出来，使其清晰易懂，是成为一个伟大的数据分析巫师的基本。

问你自己：

!!! quote "什么数据是我的受众/社区/项目/公司感兴趣和需要的，以便做出更好的决定？"

有数以千计的方法去寻找有趣的指标，尽管与社区或创始人交谈通常是最好的起点。

## 如何找到一个自由职业者来帮助您建立 Dune 看板

在加密货币行业中，有相当多的人要么专门在 Dune 上进行建设，要么拥有必要的技能，可以迅速掌握具体细节。

为了接触到这些自由职业者，您可以[**填写此问卷**](http://bounties.dune.com)，希望自由职业者能在短时间内给您答复。如果没有结果，在相关的社会渠道上发布悬赏信息，并在您的网络中传播，可能会有帮助。

如果您是第一次雇用自由职业者，请务必回顾他们过去的工作和看板，以验证他们确实有能力解决您需要的那种问题。

## 额外的工具和支持

查看我们的[帮助](../reference/support-feedback.md)页面，了解如果您在我们的文档中找不到您想要的答案，可以通过什么方式获得帮助。

也可以看看我们的[巫师工具](../reference/wizard-tools/index.md)页面，了解更多关于我们的巫师用来制作 🎇 的所有很棒的非 Dune 工具。