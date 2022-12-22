---
title: 6. 🖋️ 将您的魔法表写成 SELECT 语句
description: 现在我们准备好*正式*开始创建我们的魔法表了！
---

现在我们准备好*正式*开始创建我们的魔法表了！

虽然我们的终点是 `_view_job_log.sql`，但我们需要从 `_view_job_migrations.sql` 开始。

## `_view_job_migrations.sql`

为什么从这里开始？ 因为它是我们最低层级的依赖表！

记住 `keep3r_network_ethereum_view_job_log.sql` 依赖于 `keep3r_network_ethereum_view_job_liquidity_log.sql` 和 `keep3r_network_ethereum_view_job_credits_log.sql`，而它们都依赖于 `keep3r_network_ethereum_view_job_migrations.sql`。

因此，通过从 `_migrations.sql` 开始，我们将能够在创建魔法表时进行测试，而不会因为没有构建依赖关系而出现任何中断。

要从 V1 的抽象迁移，我们首先将 V1 文件的内容（`/spellbook/deprecated-dune-v1-abstractions/ethereum/keep3r_network/view_job_migrations.sql`）复制到我们的`keep3r_network_ethereum_view_job_migrations.sql` 文件中：

```sql

CREATE OR REPLACE VIEW keep3r_network.view_job_migrations AS (

    SELECT

        evt_block_time AS timestamp,

        '0x' || encode(evt_tx_hash, 'hex') AS tx_hash,

        evt_index + s.step AS evt_index,

        CASE s.step

        WHEN (0) THEN

            'JobMigrationOut'

        WHEN (1) THEN

            'JobMigrationIn'

        END AS event,

        '0x' || encode(contract_address, 'hex') keep3r,

        '0x' || encode(

            CASE s.step

            WHEN (0) THEN

                m. "_fromJob"

            WHEN (1) THEN

                m. "_toJob"

            END, 'hex') AS job

    FROM (

        SELECT

            *

        FROM

            keep3r_network. "Keep3r_evt_JobMigrationSuccessful"

        UNION

        SELECT

            *

        FROM

            keep3r_network. "Keep3r_v2_evt_JobMigrationSuccessful") AS m

        INNER JOIN (

            SELECT

                generate_series(0, 1) AS step) AS s ON TRUE);

```

我们不需要 `CREATE` 或 `REPLACE` 定义语句，所以我们只需要从第一个 `SELECT` 到最后一个 `TRUE` 之间的所有内容。

然后对于我们的 FROM 语句，我们需要用新语法替换旧的表引用，并仔细检查我们在 `_sources.yml` 文件中提到的这些依赖源。

```sql

-- 移除了 CREATE/REPLACE 语句

SELECT

    evt_block_time AS timestamp,

    '0x' || encode(evt_tx_hash, 'hex') AS tx_hash,

    evt_index + s.step AS evt_index,

    CASE s.step

    WHEN (0) THEN

        'JobMigrationOut'

    WHEN (1) THEN

        'JobMigrationIn'

    END AS event,

    '0x' || encode(contract_address, 'hex') keep3r,

    '0x' || encode(

        CASE s.step

        WHEN (0) THEN

            m. "_fromJob"

        WHEN (1) THEN

            m. "_toJob"

        END, 'hex') AS job

FROM (

    SELECT *

    -- 用我们的新语法更新了我们引用的两个表，确认它们都在我们的源文件中。

    FROM

            keep3r_network_ethereum.Keep3r_evt_JobMigrationSuccessful

    UNION

    SELECT *

    FROM

            keep3r_network_ethereum.Keep3r_v2_evt_JobMigrationSuccessful
    
    ) AS m

    INNER JOIN (

        SELECT

            generate_series(0, 1) AS step
    ) AS s ON TRUE

```

注意旧的抽象有一个“SELECT *”语句。最好的做法是在执行 `UNION` 时只 `SELECT` 我们需要的实际列，这样我们的魔法表就不会在我们的引用表之一被更新时被中断。

在我们的第一个 `SELECT *` 语句上方，我们将找到我们需要的特定列，我们的两个SELECT语句最终如下所示：

```sql

SELECT

    evt_block_time,

    evt_tx_hash,

    evt_index,

    contract_address,

    _fromJob,

    _toJob

```

接下来，我们需要将语法从 V1 抽象风格更改为 V2 魔法表风格，这意味着要做几件事：

1. 我们不需要对合约地址进行 `encode`（在 V1 中它们是 `bytea` 格式，在 V2 中它们是 `string`）
2. 列引用不再需要双引号所以 `m.“_fromJob”` -> `m._fromJob`

完成后，让我们将 SQL 复制到 dune.com 的一个新查询中，看看它是否有效。

如果遇到任何错误，请借助错误代码修复它们； 在构建此示例时，我们遇到了一个 `generate_series` 未定义的函数错误，V1 抽象中使用的这个函数在 V2 中不存在。

我们知道 Dune V1 是 PostgreSQL，V2 是 Spark SQL。在这种情况下，通过谷歌搜索“generate series Spark SQL”，我们能够找到这个 [StackExchange 答案](https://stackoverflow.com/questions/43141671/sparksql-on- pyspark-how-to-generate-time-series) ，用于使用 Spark 功能执行相同的转换。

如果您在 Google 上不是那么幸运，请在我们的 [#spellbook Discord 频道](https://discord.com/channels/757637422384283659/999683200563564655) 中寻求帮助！

## `_liquidity_log.sql` ， `_credit_log.sql` ，和 `_log.sql`

该过程与我们的其他文件基本相同（将语法修改为 V2 Spark SQL的格式）。

由于 `_liquidity_log.sql` 和 `_credits_log.sql` 都依赖于我们刚刚创建但尚未添加到生产环境中的魔法表的 `_migrations.sql` ，我们需要复制/粘贴刚刚创建的逻辑，定义为一个 `WITH` 语句。

所以在 `_liquidity_log.sql` 中，我们有这个参考： `keep3r_network.view_job_migrations migs`

让我们将其更新为 `keep3r_network.view_job_migrations_temp migs`

然后在我们的 SQL 文件的顶部定义 `_temp` CTE ：

```sql

WITH 

keep3r_network.view_job_migrations_temp as (

-- [在此处插入我们刚刚创建的 _migrations 代码]

)

```

然后我们可以将我们的新 SQL 复制/粘贴到 dune.com 并像上面那样测试修复可能遇到的错误。

## 用 JINJA 模板替换硬编码引用

将我们的 SQL 从 PostgreSQL 翻译成 Spark 并单独测试后，我们需要添加我们的 JINJA 模板，以便这一切都可以在生产环境中使用！

首先，让我们澄清几个术语：

* **Sources** 是 Dune 团队添加的数据——原始区块链数据表、已解析数据表、价格和社区表——基本上是任何不是魔法表的数据表。
    * 使用 JINJA，对模型的引用被格式化为 `{{ source() }}`
* **Models** 是社区用户在我们的 `spellbook/models` 目录中存储的 `.sql` 文件中定义的 `SELECT` 语句。
    * 使用 JINJA，引用模型被格式化为 `{{ ref() }}`

对于 `sources()` 引用，我们首先需要传递 `_sources.yml` 文件的名称，然后是依赖源的名称。

所以我们的 V1 抽象引用的 `keep3r_network.“Keep3r_evt_JobMigrationSuccessful”` 变为 `{{ source('keep3r_network_ethereum','Keep3r_evt_JobMigrationSuccessful') }}`。其中：

* `keep3r_network_ethereum` 是我们的 `_sources.yml` *不包括* `_sources.yml` 部分的名称，并且
* `Keep3r_evt_JobMigrationSuccessful` 是我们包含在 `keep3r_network_ethereum_sources.yml` 中的已解析数据表的名称

对于我们的 `ref()` 引用，我们只需要在不包括 `.sql` 的情况下命名我们创建的 SQL 文件。

所以我们的 V1 抽象引用 `keep3r_network.view_job_liquidity_log` 变成了 `{{ ref('keep3r_network_ethereum_view_job_liquidity_log') }}`。

将 JINJA 格式添加到引用后，运行 `dbt compile` 并修复所有错误！

同样，谷歌搜索“xxx error dbt”或“JINJA”或“Spark SQL”可以提供很多帮助。如果我们的 Google 霸主搜索失败了，请在我们的 [#spellbook Discord 频道](https://discord.com/channels/757637422384283659/999683200563564655) 中提问！