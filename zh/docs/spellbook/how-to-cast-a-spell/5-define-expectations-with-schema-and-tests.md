---
title: 5. 🧪 使用模式和测试定义期望输出
description: 接下来，我们通过两种方式定义成功的魔法表需要输出什么。
---

接下来，我们通过两种方式定义成功的魔法表需要输出什么：

1. 要输出的列模式。
2. 确保将准确数据输出到这些列的单元测试。

## 定义模式（schema）

首先，我们从定义模型的模式开始——应该为我们的魔法表中的每个 .sql 文件输出哪些列。

我们的 `_schema.yml` 文件结构如下：

```sls

version: 2

models:

  - name: [model_name]

    meta:

      blockchain: [blockchain_name]

      project: [project_name]

      contributors: [your_name]

    config:

      tags: ["[blockchain]", "[project_name]", "[other_relevant_tags]"]

    description: [description]

    columns:

      - &[column_name]

        name: [column_name]

        description: "[description]"

        tests:

          - [generic_test_criteria]

  - name: [model_name_2]

    meta:

      blockchain: [blockchain_name]

      project: [project_name]

      contributors: [your_name]

    config:

      tags: ["[blockchain]", "[project_name]", "[other_relevant_tags]"]

    description: [description]

    columns:

      - *[previously_definied_column]

```

!!! 注意
    “&”用于某个列的第一个定义，之后的“*”将导致在不同模型中具有相同名称的列继承相同的名称、描述和通用测试。

我们在第四步中创建的每个 SQL 文件在这里都是一个模型，我们要输出的每个列都被命名和描述，并相应地提及应该用于检查它们的任何通用测试。

[在此处查看 Keep3r 魔法表的模式，了解我们的示例完成后的样子](https://github.com/duneanalytics/spellbook/blob/b9260a03351e562448c5c9e62529da7b2d94ca59/models/keep3r_network/ethereum/keep3r_network_ethereum_schema.yml).

## 设置单元测试种子文件结构

设置模式后，我们就可以定义我们的[单元测试](https://en.wikipedia.org/wiki/Unit_testing) - 这将帮助我们确保魔法表按预期工作。

从设置种子文件结构开始。

在 dbt 中，[种子文件是 CSV](https://docs.getdbt.com/docs/build/seeds)，我们用来存储我们可以在魔法表和单元测试中使用的参考数据；在这种情况下，我们将使用它来存储一些数据，我们可以使用这些数据来验证我们的魔法表是否符合网络无障碍倡议（WAI）。

导航到 `/seeds` 文件夹，就像我们对新项目所做的那样，我们在这里创建一个 `/[project_name]/[blockchain]` 子文件夹。

在我们的 Keep3r 示例中，文件夹路径是`/seeds/keep3r_network/ethereum`

有了它，我们需要使用以下格式创建一个具有描述性名称的 CSV 文件：

`[project_name]_[blockchain]_[spell_name]_test_data.csv`

在我们的例子中则是：

`keep3r_network_ethereum_view_job_log_test_data.csv`

## 查找单元测试的预期值

我们的单元测试将针对预期值列表运行，本质上我们要检查以确保我们的魔法表提供应有的结果。

我们应该期待什么结果？

为了弄清楚这一点，我们需要通过阅读 Keep3r 的网站、文档、Medium 博客、在他们的 discord 中提问等来更多地了解 Keep3r 网络。

对于我们的例子，重要的是要知道 Keep3r 网络是一个发布和接受工作以帮助运行去中心化基础设施的市场。

Keep3r 网络上的工作是智能合约，需要 Keepers 在其内部逻辑之外做一些事情。 完成这些任务会使 Keeper 获得奖励。

基于此理解，我们可以编写一个测试。在其中，给定一个交易哈希，我们可以看到为该工作支付的奖励金额、收到奖励的Keeper是谁以及他们收到的代币是什么。

因此，在我们的 CSV 文件中，我们首先定义要验证的测试数据列，在本例中为：`tx_hash`、`amount`、`keeper` 和 `token`。

接下来，我们将找到一些特定的交易，3 个就足够了，然后添加应该在每一列中的实际数据。

结果如下：

```csv

tx_hash,amount,keeper,token

0xca1ee6de6d2a776afda7d6ab6bc489d4554f69777725db58591a7ac0ef533c96,0.11,0x9429cd74a3984396f3117d51cde46ea8e0e21487,0x1cEB5cB57C4D4E2b2433641b95Dd330A33185A44

0xdd59724ee9a1f151706bc182be810483a35b36c2a82485469245887742996313,0.13,0xfb20864791b7dd70542dae2f4907ef0535a68cdc,0x1cEB5cB57C4D4E2b2433641b95Dd330A33185A44

0xa8c8383254bd4cda949de1e847f8ae0d7f765053ddeeca11a159ad8191d8cc85,0.35,0xfb20864791b7dd70542dae2f4907ef0535a68cdc,0x1cEB5cB57C4D4E2b2433641b95Dd330A33185A44

```

## 编写单元测试

现在我们已经有了要测试的预期结果，我们可以编写单元测试了！

首先，如您所料，我们在 `/tests` 文件夹中创建一个文件夹结构，以及一个用于测试的 SQL 文件。

Same naming conventions as before for the folders, for our SQL file we’ll name it `[project_name]_[spell_name]_test.sql`
文件夹的命名约定与之前相同。对于我们的 SQL 文件，我们将其命名为 `[project_name]_[spell_name]_test.sql`。

即:

`/keep3r_network/ethereum/keep3r_network_view_job_log_test.sql`

![keep3r test file](images/keep3r-test-file.jpg)

为了编写单元测试，我们将检查以确保我们将（最终）在下一步中定义的魔法表的结果与我们添加到预期值种子文件中的真实结果相匹配。

为此，我们将定义一个名为 `unit_test` 的[通用表表达式（CTE）](https://learnsql.com/blog/cte-with-examples/)，连接我们的测试和实际结果数据，并进行比较。如果不匹配，该数据将返回错误。

下面是这个例子的单元测试的样子，注释解释了详情：

```sql

-- CTEs 使用 WITH 语句创建

WITH unit_test AS (

    -- 这里我们将测试数据与实际数据进行比较，匹配则返回TRUE，不匹配则返回FALSE。ROUND 和 LOWER 确保我们不会因格式差异而出现错误。

    SELECT

        CASE

            WHEN test.amount = ROUND(

                actual.amount,

                2

            ) THEN TRUE

            ELSE FALSE

        END AS amount_test,

        CASE

            WHEN LOWER(

                test.keeper

            ) = LOWER(

                actual.keeper

            ) THEN TRUE

            ELSE FALSE

        END AS keeper_test,

        CASE

            WHEN LOWER(

                test.token

            ) = LOWER(

                actual.token

            ) THEN TRUE

            ELSE FALSE

        END AS token_test

   /* 在这里，我们使用 tx_hash 值来连接实际数据和测试数据。 注意“actual”我们引用我们实际的魔法表模型文件，以及我们的“test”测试数据文件。 {{}} 是 JINJA 模板，我们稍后会介绍。*/

    FROM

        {{ ref('keep3r_network_ethereum_view_job_log') }} AS actual

        INNER JOIN {{ ref('keep3r_network_ethereum_view_job_log_test_data') }} AS test

        ON LOWER(

            actual.tx_hash

        ) = LOWER(

            test.tx_hash

        )

)

-- 从 unit_test 加载所有列，我们返回任何 FALSE 结果

SELECT

    *

FROM

    unit_test

WHERE

    amount_test = FALSE

    OR keeper_test = FALSE

    OR token_test = FALSE

```