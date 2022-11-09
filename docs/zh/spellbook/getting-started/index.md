---
title: 魔法书入门
---

**Spellbook 本质上是一个在 Dune 的数据平台上运行的 DBT 项目。**

在高水平上，你需要在本地设置我们的 DBT 项目，用 Jinja-templated 的 SQL 研发一个魔法，并让它在我们的数据平台上运行。

首先，克隆[魔法书](https://github.com/duneanalytics/spellbook/)资源库，并按照 README 设置你的本地开发环境。

决定你要解决什么问题。思考一下[数据模型](data-modelling.md)。

写下你的魔法。至少，你将需要：

- 引用您的[数据源](data-sources.md)，包括测试和新鲜度检查
- 为您的魔法定义一个单元[测试](tests.md)
- 用 Jinja templating 的 SQL select 语句[写下您的魔法](spells.md)
- 在单独的一个 YAML 文件中写下一个图式

要了解更多关于 DBT 的所有功能，请看他们的[文档](https://docs.getdbt.com/docs/introduction)。我们已经写了一些指南[例子](../examples/index.md)，用于创建 ERC20 的魔法。

!!! tip
    在你进行的过程中，你可以使用 `dbt compile` 来生成一个 SQL 语句，并在 dune.com 的查询编辑器中对其进行验证。

一旦你对你的魔法感到满意，你就可以[提交给 Dune](submissions.md)：

- 分叉魔法书资源库并提交一个 pull request
- 标记 duneanalytics/data-experience，并写下你的魔法的简短描述
- 您的 PR 将触发在暂存数据库中创建你的魔法，并运行测试
- 如果一切顺利，Dune 将合并你的修改，并将其部署到生产中

之后，您的魔法将会在 dune.com 里面的 "Spells"（魔法）里可见。LFG！


## 社区教程

我们的一些社区成员已经为魔法书制作了很好的教程：

- @ilemi aka Andrew Hong 发布了教程 - [阅读它](https://ath.mirror.xyz/K-S_Mwhj7osTBqN-AOWbCmfNn9TZViEkzICCmK-oObM)，并观看[视频](https://www.youtube.com/watch?v=7zReSzVdV2s)！
