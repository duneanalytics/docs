---
title: 7. 🎨 配置别名和物化策略
description: 定义了魔法表的 SQL 后，就该配置我们的别名了。
---

定义了魔法表的 SQL 后，就可以配置我们的别名了。这样我们就可以在其他魔法表和查询中引用这些文件，以及我们希望 dbt 如何物化我们的工作。

## dbt 物化（materialization）

在 dbt 中，[物化](https://docs.getdbt.com/docs/build/materializations) 是将数据保存在我们的数据湖仓库的策略。

dbt中有4种物化策略：

* `table`
* `ephemeral`
* `view`
* `incremental`

对于魔法书，我们只使用 `view` 和 `incremental`策略。

### `view` 视图

`view` 是魔法书中的默认物化策略 - 因此不需要在使用它的魔法表中将其指定为我们的策略。

这些魔法表每次运行时都会重建，这意味着每次有人查询 `view` 魔法表时，都会运行 SQL，这意味着根据我们魔法表的 SQL 逻辑收集最新数据。

基本上，`view` 魔法表只是存储的 SQL 逻辑，没有额外的数据作为魔法表的一部分存储。

优点是 `view` 魔法表总是有新鲜数据，缺点是如果涉及大量数据，它们可能需要很长时间才能运行完成。

### `incremental` 增量

`incremental` 魔法表允许 dbt 根据我们定义的逻辑在表中插入或更新记录。

好处是这些魔法表可以运行得更快，尽管它们的数据不会像 `view` 魔法表那样新鲜。

要创建 `incremental` 魔法表，我们需要在文件的配置部分中添加一些内容：

```sql

-- 每次递增时我们应该将新数据连接到现有数据中的哪一列的声明； 在此示例中，我们使用 block_date，这通常是最好的使用方式

partition_by = ['block_date'],

-- 这里我们指定这是一个增量（incremental）魔法表

materialized = 'incremental',

-- 有关 dbt 应如何组合新/旧数据的说明；这里我们使用“merge”

incremental_strategy = 'merge',

```

我们还需要将 `if` 语句添加到我们想要为其递增数据的任何 `FROM` 中。

在这个例子中，我们在 `partition_by = ['block_date']` 中添加了if语句来刷新一周以内的数据：

```sql
{% if is_incremental() %}

    WHERE evt_block_time >= date_trunc("day", now() - interval '1 week')

{% endif %}
```

## 配置别名和物化

要配置魔法表的别名和物化，您需要将这些配置项添加到每个 SQL 文件的顶部。

请注意，这里假设我们正在使用 `view` 物化策略；有关如何实施 `incremental` 策略的信息，请参见上文。

```sql
{{ config (

    -- 为将出现在 dune.com 用户界面中的魔法表文件创建一个别名

    alias = 'job_log',

    -- 这进一步定义了该文件如何存储和在 UI 中被分类，首先是它与哪个区块链相关联

    post_hook = '{{ expose_spells(\'["ethereum"]\',


         -- 然后我们定义这是针对特定项目还是整个行业的魔法表


        "project", 


         -- 接下来，我们命名项目/行业


            "Keep3r",


         -- 最后，我们命名贡献者，包括我们自己，在本例中是 V1 抽象的创建者！


             \'["wei3erHase", "agaperste"]\') }}'

) }}
```

## 将新模型添加到 dbt_project.yml 文件

进入最后阶段，我们需要将新模型添加到魔法书根文件夹中的 `dbt_project.yml` 文件中。

首先找到这些行：

```sls

# Configuring models

# Full documentation: https://docs.getdbt.com/docs/configuring-models

models:

	spellbook:

```

在下面，我们为整个项目指定项目名称、模式和物化策略，以及我们为其创建魔法表的特定区块链。

对于 Keep3r，添加后的条目如下所示：

```sls

   keep3r_network:

      +schema: keep3r_network

      +materialized: view

      ethereum:

        +schema: keep3r_network_ethereum

        +materialized: view

```