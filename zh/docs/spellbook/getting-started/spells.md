---
title: 魔法
---

每一个 `.sql` 文件应该只能含有一个 `select` 主体查询。

您无需在SQL语句中声明 `create view`（创建视图）或者 `create table`（创建表）。 [具现化策略](https://docs.getdbt.com/docs/building-a-dbt-project/building-models/materializations)将直接在 JINJA 设置块或者 YAML 模式文件中声明。

在默认情况下，模型将被定义为视图，但我们也可以通过定义使他们成为表或者增量加载表。

创建视图速度快，不需要额外的存储空间，但查询速度较慢。 表的创建速度要慢得多，并且确实需要额外的存储空间，但查询速度更快。 通常情况下，我们坚持使用视图，除非遇到性能问题时，我们才会考虑升级到表或增量加载表。

如果您想了解更多关于 DBT 的全部功能, 请查看[DBT官方文档](https://docs.getdbt.com/docs/introduction)。我们已编写了一些[示范样例](../examples/index.md)作为ERC20的魔法编写指南.

## 核验您的魔法

从目标（target）文件夹中复制编译后的魔法，然后您可以在 dune.com 上打开新查询窗口尝试运行。

我们正在努力开发一个可以直接从 DBT 中安全运行魔法的沙盒。 但与此同时，在本地检查您的工作的最佳方法是“编译”您的魔法。

在您用 \`dbt init\` 完成[DBT初始化](https://github.com/duneanalytics/spellbook/blob/master/README.md)之后，您可以尝试运行 \`dbt compile\` 。这将创建一个名为“target”的新文件夹。 在目标文件夹内将是编译成普通 SQL 的所有魔法。您可以复制您的魔法并直接在 dune.com 上运行。

![type:video](https://www.youtube.com/embed/9sut8560oUE)
