---
title: 3. 🛣️ 为 SQL、模式和源文件设置文件结构
description: 接下来，让我们检查项目的现有文件夹，如果不存在则创建一个。
---

接下来，让我们检查项目的现有文件夹，如果不存在则创建一个。

所有魔法表（spells）都按项目名称、区块链名称的结构存储在 `/spellbook/models` 目录中。

名称全部使用小写字母，单词之间用`_`分隔。

例如： `/spellbook/models/[project_name]/[blockchain_name]`

所以在我们的 Keep3r 网络示例中，对应的文件夹将是 `/spellbook/models/keep3r_network/ethereum`。

由于此文件夹已经存在（因为我们之前已经这样做过），在这种情况下，我们将在那里构建魔法表。

如果该项目不存在，我们将使用其所在区块链的名称创建该文件夹；如果项目文件夹存在但我们正在为新区块链创建一个魔法表（例如，该项目刚刚添加了对Polygon区块链的支持），那么我们将为新区块链创建一个文件夹。

有了相应的文件夹结构之后，我们需要创建 3 个文件：

1. 我们的 Spell 逻辑所在的 `.sql` 文件。
2. 一个 `_schema.yml`文件，我在其中定义我的魔法表的目的并添加通用测试、描述、元数据等。
3. 包括任何特定于项目的表依赖源的 `_sources.yml` 文件。

![spell folder file structure](images/spell-folder-file-structure.jpg)

魔法表文件命名如下：

* 对于模式文件：`[project_name]_[blockchain]_schema.yml`
* 对于依赖源文件：`[project_name]_[blockchain]_sources.yml`
* 对于魔法表的SQL文件：`[project_name]_[blockchain]_[spell_name].sql`

在这个特定的从 v1 迁移示例中，我们还需要创建 3 个额外的 `.sql` 文件，`keep3r_network_ethereum_view_job_log.sql` 依赖于这些文件。

它们是 `keep3r_network_ethereum_view_job_liquidity_log.sql` ，`keep3r_network_ethereum_view_job_credits_log.sql` 和 `keep3r_network_ethereum_view_job_migrations.sql`。

我们怎么知道我们需要这些文件呢？

查看原始的 `view_job_log.sql` V1 抽象表定义，我们看到两个 `FROM` 语句：

```sql

FROM

        keep3r_network.view_job_liquidity_log

```

```sql

FROM

        keep3r_network.view_job_credits_log

```

当我们查看 V1 Keep3r 网络文件夹时，我们会看到这两个文件在那里 - 这意味着它们也是需要转换为 Spells 的抽象。

![keep3r other abstractions to translate](images/keep3r-other-abstractions-to-translate.png)

我们还需要进行递归检查，以查看这些抽象是否依赖于尚未迁移到 Spells 的任何其他抽象。

为此，我们打开这两个抽象并搜索 `FROM` 语句。

在这里，我们找到了几个引用的表，其中包括“_evt_”，这是 [已解析事件表](../../reference/tables/v2/decoded/event-logs.md) 的命名约定。

You’ll find other Raw and Decoded data table naming conventions in our [Tables documentation here](../../reference/tables/index.md). 
您可以在我们的 [表格文档](../../reference/tables/index.md)中找到其他原始和已解析数据表的命名约定。

V1 抽象表命名如下：

`[project_name].[abstraction_name]`

当我们搜索 `view_job_log.sql` 中引用的两个抽象时，我们还找到了对 `keep3r_network_ethereum_view_job_migrations` 的引用，因此它也必须成为一个魔法表。