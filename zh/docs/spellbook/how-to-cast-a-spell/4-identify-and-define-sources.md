---
title: 4. 📙 识别和定义依赖源
description: 通过我们的文件结构设置，让我们完成我们的 `_sources.yml` 文件。
---

通过我们的文件结构设置，让我们完成我们的 `_sources.yml` 文件。

这些文件的格式如下：

```sls

version: 2 # 魔法表都使用“version: 2”，因为这是他们使用的我们数据库引擎的版本。

sources:

  - name: [project_name]_[blockchain]

    description: [one line description] # 右箭头 > 允许我们添加多行描述

    tables:

      - name: [source_table_1]

      - name: [source_table_2]

      - name: [source_table_3]

```

我们需要命名哪些依赖源？

为了找到这个，我们再次遍历我们正在迁移的每个 V1 抽象，搜索 `FROM` 语句，这次我们正在寻找所有提到的*不是*抽象的表。

在我们的 Keep3r 示例中，为我们的主要抽象表和它的依赖项分别执行上述操作：

* `keep3r_network.view_job_log`
* `keep3r_network.view_job_liquidity_log`
* `keep3r_network.view_job_credits_log`
* `keep3r_network_ethereum_view_job_migrations`

我们最终得到一个如下所示的 `keep3r_network_ethereum_sources.yml` 文件：

```sls

version: 2

sources:

  - name: keep3r_network_ethereum

    description: >

      Decoded events for [keep3r.network](https://keep3r.network/), a marketplace for posting and accepting jobs to help run decentralized infrastructure.

      The scope of Keep3r Network is not to manage the jobs themselves, but to allow contracts to register as jobs for keepers, and keepers to register themselves as available to perform jobs. A "keeper" is a term used to refer to an external person and/or team that executes a job.

      See their [docs](https://docs.keep3r.network/) for more.

    tables:

      - name: Keep3r_evt_LiquidityAddition

      - name: Keep3r_v2_evt_LiquidityAddition

      - name: Keep3r_evt_LiquidityWithdrawal

      - name: Keep3r_v2_evt_LiquidityWithdrawal

      - name: Keep3r_evt_JobMigrationSuccessful

      - name: Keep3r_v2_evt_JobMigrationSuccessful

      - name: Keep3r_evt_KeeperWork

      - name: Keep3r_v2_evt_KeeperWork

      - name: Keep3r_evt_LiquidityCreditsReward

      - name: Keep3r_v2_evt_LiquidityCreditsReward

```