---
title: 2. 🤔 决定要创建为魔法表的目标
description: 接下来，您需要决定要创建为魔法表的目标。
---

接下来，您需要决定要创建为魔法表的目标。

有几种方法可以做到这一点：

1. 如果您对 Dune 的使用足够多，知道您在哪里需要比您能够找到的更多的抽象数据，您可能已经有了一个想法。
2. [您还可以查看我们在 Dework 中的 Spellbook 赏金项目](https://app.dework.xyz/dune/spellbook-86233/overview).
3. 欢迎在我们的 [#spellbook Discord 频道](https://discord.com/channels/757637422384283659/999683200563564655) 中提问，看看人们需要什么帮助或者建议您做什么！

对于本指南，我们将制作一个迁移魔法表——将 Keep3r 网络 `view_job_log` 抽象从 Dune 的 v1 数据库转换为 V2 魔法表。

在 VSCode 中，找到“deprecated-dune-v1-abstractions”文件夹，然后向下展开目录以找到“view_job_log.sql”文件。

完整路径是：

`[你克隆spellbook的文件夹]/deprecated-dune-v1-abstractions/ethereum/keep3r_network/view_job_log.sql`

![keep34 v1 abstraction location](images/keep3r-v1-abstraction-location.jpg)

现在我们已经准备好为我们的魔法表的SQL模式和依赖源文件设置文件结构。