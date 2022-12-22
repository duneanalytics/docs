---
title: Dune V2
description: Dune Engine V2 is an update to our Query engine that brings a new level of performance, scalability and functionality to the core tools that enable Wizards to query, extract, and visualize blockchain data.
---

**Dune Engine V2** 是 Dune 的新版查询引擎，它将 Dune 的核心工具集的性能、可扩展性和功能带到了一个新的水平，使 wizards 能够查询、提取和可视化区块链上的大量数据。

它利用 **[Apache Spark SQL](https://spark.apache.org/docs/latest/sql-programming-guide.html)** 来提高复杂查询的性能、处理数据规模扩张，并能够在同一个[查询编辑 UI](../../getting-started/queries/index.md) 中实现跨链查询。

本节中包含的所有数据源现在都可用于使用新版查询引擎进行查询。目前我们有以下数据可供查询：

- [**原始数据表**](../../reference/tables/v2/raw/index.md)
- [**已解码数据表**](../../reference/tables/decoded.md)
- [**魔法**](../../reference/tables/spells.md)
- [**社区数据表**](../../reference/tables/community.md)

## 新版查询引擎

DuneV2 改变了我们的整个数据库架构。 我们正在从 PostgresQL 数据库过渡到托管在 Databricks 上的 Apache Spark 实例。两种系统的区别可以总结如下：

* 我们现在使用 Databricks SQL，而不是 PostgresQL。SQL 关键字的变化很小，但可能与您的某些查询书写习惯有关。
* 与 PostgresQL 的面向行的方法相反，Spark 是一个面向列的数据库。
* 传统的索引被列块级别的 最小/最大 值替换。

**您可以在此处阅读有关SQL变化的更多信息:**

<div class="cards grid" markdown>
- [查询引擎](query-engine.md)
</div>

**Or start getting your wand dirty by following along here:**

<div class="cards grid" markdown>
- [@springzhang](https://dune.com/springzhang/)'s [Tips and Tricks for Dune V2 Queries and Visualizations](https://dune.com/springzhang/tips-and-tricks-for-query-and-visualization-in-v2-engine)
</div>
 

## 魔法书

数据抽象已被升级成为魔法，储存于 Dune V2 的[魔法书](../../spellbook/index.md)中。

它们在[数据构建工具 （dbt）](https://docs.getdbt.com/docs/introduction)上运行。dbt 使分析工程师能够过通过简单地编写选择语句来转换期数据仓库中的数据，并将这些选择语句处理转换为[数据表](https://docs.getdbt.com/terms/table)和[视图](https://docs.getdbt.com/terms/view).

这将使数据抽象更加健全、可扩展且更易用。

<div class="cards grid" markdown>
- [Dune V2 中的数据抽象/魔法](../../spellbook/index.md)
</div>

## 反馈

最后, 由于查询引擎仍处于测试 **beta** 阶段，您可能会遇到漏洞或者有改进它的想法，请随时在我们的[#general-feedback Discord 频道](https://discord.com/channels/757637422384283659/1012706316755664926) 和 [Canny 面板](https://dune.canny.io)上与我们分享。
