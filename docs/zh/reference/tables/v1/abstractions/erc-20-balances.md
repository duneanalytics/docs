---
description: >-
  ERC20 token analysis is a fundamental part of any analysis of DeFi products,
  these tables and views will provide you with all the necessary information.
---

# ERC-20 代币余额

## 随着时间的推移轻松跟踪钱包和代币余额

下列表格允许随时间变化或按快照格式轻松跟踪钱包余额、代币分配或代币供应量。

在原始数据级别上，使用 erc20 代币非常困难，因为你需要对所有地址的所有代币转移进行汇总。这不必要地使查询膨胀并迅速导致人为错误。为了防止这种情况发生，我们构建了几个视图和表，可以帮助你轻松查询 erc20 代币数据。

这些表可用于各种有趣的分析，但在使用它们时你仍需要注意一些事项：

* **铸造/燃烧地址** 没有标准化，因此你需要找出这些地址并在查询中手动应用修复。在大多数情况下，用于铸造和燃烧的将是 `x0000000000000000000000000000000000000000` ，但请始终确保确实如此。在下面给出的示例中，情况并非如此。

**示例:**

```sql
Select 
    wallet_address, 
    amount,
    day,
    token_symbol
from erc20."view_token_balances_daily"
where token_address = '\x429881672B9AE42b8EbA0E26cD9C73711b891Ca5'
and wallet_address != '\x0000000000000000000000000000000000000000' --mint address
and wallet_address != '\x000000000000000000000000000000000000dead' --burn address
```

* 使用这些表格工作会很快产生很多单独的数据点，我们的可视化引擎并不总是能够完美处理这些数据点。与其尝试显示每个唯一的持有者，不如将它们按特定标准分组并以这种方式显示数据集。这对于每个代币都是唯一的，你可能需要进行一些试验以查看什么分类方式能在你的查询中有效工作。

```sql
Select 

     CASE   WHEN wallet_address = '\xbBCf169eE191A1Ba7371F30A1C344bFC498b29Cf' then 'dill'
            WHEN wallet_address = '\xdc98556Ce24f007A5eF6dC1CE96322d65832A819' then 'uniswap'
            WHEN wallet_address = '\xC52139a20A57c9002e9F5188901EF0ffC63c7205' then 'smart_treasury'
            WHEN wallet_address = '\x40ec5b33f54e0e8a33a975908c5ba1c14e5bbbdf' then 'polygon'
            WHEN wallet_address = '\x6cc5f688a315f3dc28a7781717a9a798a59fda7b' then 'OKEX'
            WHEN amount     between  0      and 10        then 'Plankton(0-10)'
            WHEN amount     between 10     and 100        then 'shrimp(10-100)'
            WHEN amount     between 100    and 1000       then 'fish(100-1,000)'
            WHEN amount     between 1000    and 10000     then 'dolphin(1,000-10,000)'
            WHEN amount     > 10000                       then 'whale (>10000)' 
           --请注意，case 表述的顺序在这里很重要
    end as classification,

sum(amount) as amount,
token_symbol
from erc20."view_token_balances_latest"
where token_address = '\x429881672B9AE42b8EbA0E26cD9C73711b891Ca5'
and wallet_address != '\x0000000000000000000000000000000000000000'
and wallet_address != '\x000000000000000000000000000000000000dead'
and amount > 0.1 --过滤掉极小的交易，可能需要根据代币的不同进行调整
group by 1,3
```

## 看板示例:

此看板包含与用作治理代币的单个 erc20 代币相关的最重要用例。
[https://dune.xyz/0xBoxer/pickle-finance\_1](https://dune.xyz/0xBoxer/pickle-finance\_1)

## erc20.view\_token\_balances\_latest

此视图依赖于 erc20.token\_balances 表，并为你提供该代币的最新分布信息。

| column name                   | data type   | description                                                                                |
| ----------------------------- | ----------- | ------------------------------------------------------------------------------------------ |
| amount                        | numeric     | 该代币的正确显示格式的金额                                                 |
| amount\_raw                   | numeric     |该代币的原始金额（需要除以小数位数！）                                 |
| amount\_usd                   | float8      | 当前价格（如果我们有价格数据）                                           |
| last\_transfer\_\_\_timestamp | timestamptz | 此特定钱包地址中此代币余额最后更改的日期|
| token\_address                | bytea       | 代币地址                                                                      |
| token\_symbol                 | text        | 代币符号                                                                       |
| wallet\_address               | bytea       | 持有该代币的钱包地址                                              |

## erc20.view\_token\_balances\_hourly

此表将按小时提供有关所有代币余额的信息。在大多数情况下，它还已经包含小数和价格，因此它们已经准备好可开箱即用。

| 列名     | 数据类型   | 描述                                                |
| --------------- | ----------- | ---------------------------------------------------------- |
| amount          | numeric     | 该代币的正确显示格式的金额                 |
| amount\_raw     | numeric     | 该代币的原始金额（需要除以精度！） |
| amount\_usd     | float8      | 当前价格（如果我们有价格数据）            |
| hour            | timestamptz | 以小时为单位的时间                        |
| token\_address  | bytea       | 代币合约地址                                        |
| token\_symbol   | text        | 代币符号                                        |
| wallet\_address | bytea       | 持有该代币的钱包地址              |

## erc20.view\_token\_balances\_daily

**此表的性能将比 `erc20.view_token_balances_hourly` 好得多，因为它仅按天查询数据**。如果你想进行高阶分析，这是你应该选择的表。

| 列名     | 数据类型   | 描述                                                |
| --------------- | ----------- | ---------------------------------------------------------- |
| amount          | numeric     | 该代币的正确显示格式的金额                  |
| amount\_raw     | numeric     | 该代币的原始金额（需要除以精度！） |
| amount\_usd     | float8      | 当前价格（如果我们有价格数据）           |
| day             | timestamptz | 以天为单位的时间                        |
| token\_address  | bytea       | 代币合约地址                                 |
| token\_symbol   | text        | 代币符号                                   |
| wallet\_address | bytea       | 持有该代币的钱包地址                |

## erc20.token\_balances

该表包含所有 erc20 代币在这些代币存在期间的每小时余额。如果我们上面提供的视图不足以满足你尝试建立的用例，你可以使用此表作为备用选项。
| 列名     | 数据类型   | 描述                                                |
| --------------- | ----------- | ---------------------------------------------------------- |
| amount          | numeric     | 该代币的正确显示格式的金额                  |
| amount\_raw     | numeric     | 该代币的原始金额（需要除以精度） |
| timestamp       | timestamptz | 以小时为单位的时间                        |
| token\_address  | bytea       | 代币合约地址                                        |
| token\_symbol   | text        | 代币符号                                    |
| wallet\_address | bytea       | 持有该代币的钱包地址               |
