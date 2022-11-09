---
title: 数据源
---

在魔法书中，数据源（即构建魔法所依赖的原始数据表和解码数据表）必须在 YAML 文件中定义。 一个数据源在魔法书中只需定义一次。

仅需添加其模式和名称就可以简单地定义数据源。 但要充分利用该工具的全部功能，我们还需要定义测试、数据更新周期，以及对每一列添加描述。

以下是一个定义数据源的示例，我们先添加表名和该表描述。

```yaml
 sources:
  - name: erc20_ethereum
    description: "Transfers events for ERC20 tokens."
    tables:
      - name: evt_transfer
```

然后我们添加更新检查。 更新检查使用时间戳类型字段来验证最后几行数据的加载时间。 在这里，我们将使用 `evt_block_time` 并使用 DBT 默认的警告和错误检查。

```yaml
sources:
  - name: erc20_ethereum
    description: "Transfers events for ERC20 tokens."
    tables:
      - name: evt_transfer
        loaded_at_field: evt_block_time
        description: "Transfers events for ERC20 tokens."
        freshness:
          warn_after: { count: 12, period: hour }
          error_after: { count: 24, period: hour }
```

接着添加列描述和测试。 关于测试，通常您需要使主键既唯一又非空。

您可以在列名之前使用符号`&`，以便稍后在同一 YAML 文件中重用其描述。

`*`列名将重用之前定义的列描述。

```yaml
sources:
  - name: erc20_ethereum
    description: "Transfers events for ERC20 tokens."
    tables:
      - name: evt_transfer
        loaded_at_field: evt_block_time
        description: "Transfers events for ERC20 tokens."
        freshness:
          warn_after: { count: 12, period: hour }
          error_after: { count: 24, period: hour }
        columns:
        - name: contract_address
          description: "ERC20 token contract address"       
        - &evt_tx_hash
          name: evt_tx_hash
          description: "Transaction hash of the event"
        - &evt_index
          name: evt_index
          description: "Event index"   
        - &evt_block_time
          name: evt_block_time
          description: "Timestamp for block event time in UTC"
        - &evt_block_number
          name: evt_block_number
          description: "Event block number"  
        - *from
        - *to
        - name: value
          description: "Amount of ERC20 token transferred" 
```

这些描述将被 dbt 渲染生成文档。 您可以在本地通过 Spellbook 目录中的 CLI 中运行 `dbt docs generate` 和 `dbt docs serve` 来打开它们。 我们的 [魔法书文档](https://spellbook-docs.dune.com/#!/overview)就是由它们自动发布的。

![dbt 文档页面](https://lh6.googleusercontent.com/vr9DleUs\_HcdzMZ6mWq81l-IRq1C\_utHCVB5WddOHy9Z1\_fSyz8GcB8Cyj877nKNHsXLh3K3-owFssNIl4ZaJS27clEeBppHBi8DlNjzVKGeGZdF\_AE8VxRj0pziR-2jGTA-MED7OtTq3GhuwQM)
