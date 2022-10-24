---
title: 魔法书
---

**魔法书（Spellbook）是一个由Dune社区共同建设的数据转换层项目。**

魔法（Spell）可以用来构建高级抽象表格，魔法可以用来查询诸如 NFT 交易表等常用概念数据。您可以用 SQL 来编写魔法，并使用 [Jinja2](https://jinja.palletsprojects.com/)（一种 Python 模板语言）进行包装。

魔法书项目可自动构建并维护这些表格，且对其数据质量进行检测。 我们社区中的任何人都可以贡献魔法书中的魔法，无论是添加新的交易数据查询或是编写全新的魔法。

!!! 请注意
    魔法书目前仅在我们的 Dune V2 引擎上可用。有关 Dune V1 引擎中的数据抽象，请参阅[数据抽象](../tables/v1/abstractions/index.md)。

## 新功能解锁

在新的数据引擎发布后，现在是时候更新我们使用的工具了。

2020 年 1 月 31 日，我们发布了数据抽象（abstractions）定义库，作为巫师们创建视图和后续表格的参考。 从那时起，魔法书项目已有超过 300 名贡献者和近千次代码提交。

![Mats inaugural comment](images/mats-inaugural-comment.jpg)

数据抽象是 Dune 上查询最多的一类表，巫师们通过创建数据抽象来提高工作成果复用率。  **魔法书**正是用来改善此流程体验的。魔法书是对现有[数据抽象](https://github.com/duneanalytics/spellbook/index.md)定义库的重组，并结合了一流的开源分析工程工具 [dbt](https://docs.getdbt.com/docs/introduction)。

[dbt-core](https://docs.getdbt.com/docs/introduction)（data build tool 数据构建工具）是一个开源框架，通过将 SQL 与 Jinja 模板混合，使更多经典的软件工程实践注入到 SQL 开发中。 

![Succinct description of why we are appropriately hyped on dbt ](images/short-dbt-description.jpg)

数据抽象，现在既是 dbt 概念中的 **模型（models）**， 也是 Dune 系统中的 **魔法（spells）**，可以具体化为视图和表，同时现在还可进行许多功能上的改进，包括增量加载表、日期分区表等等。 这些都可以编译成 SQL 并在 dune.com 上运行。 新的代码提交都可以使用这个方法进行自主测试。

我们可以用 dbt 来为 SQL 编写和管理单元测试，以发现和防止数据抽象中可能出现的问题。

仅需在 YAML 文件中添加一行代码即可为数据添加完整性测试。从此测试模型的唯一主键、非空值、可接受的值和关系完整性都变得更加方便。

dbt 原生支持对模型依赖关系的理解。在我们旧的数据抽象中，我们手动管理依赖关系，这使得部署和维护它们变得十分繁琐。通过依赖管理，我们可以保证所有模型都以正确的顺序部署。

![Dependency graph created by dbt showing erc20 daily balances dependency tree](images/dbt-erc20-dependency-graph.jpg)

希望您和我们一样对这个新工具（魔法书）感到兴奋。魔法书现已在生产环境中上线，我们欢迎大家一起来共同编写魔法书。
