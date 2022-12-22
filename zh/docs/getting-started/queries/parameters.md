---
title: 参数
description: >-
  参数是一种简单而强大的方式，可以将筛选器添加到您的
  查询/看板。允许您和其他人在用户界面上与查询进行互动，而无需改变 SQL。
---

## 什么是参数？

**参数是 Dune 一个专门的功能，允许您在查询代码的某些部分使用变量。这个变量可以从看板上更改，因此允许您做一个交互式看板。**

参数允许您通过几个简单的点击对您的代码的某些定义参数进行修改。例如，您可以使用参数功能来改变您的代码的这些方面——`contract_address`、`symbol` 或 `date ranges`——而不是手动输入。这允许您建立一个交互式看板或可定制的查询，浏览者可以用它来查询他需要的数据。

参数在查询代码中定义为 `{{parametername}}`，并将出现在查询的下方和任何使用了参数的查询可视化的数据看板中。

您可以在查询下面的参数中或在看板的参数栏目中传递输入。

只需运行查询就可以在查询编辑器中为查询应用参数。

在看板上，您可以点击顶部的 `apply all`，或者单独改变参数并点击 `Enter`。`Enter` 的提交方式也适用于下拉菜单和日期选择器。

看板中的参数可以在不同的查询之间共享，只要确保在所有的查询之间使用相同的名称、类型和默认值。

![Parameters overview 1](images/parameters-overview-1.png)

![Parameters overview 2](images/parameters-overview-2.png)

![Parameters overview 3](images/parameters-overview-3.png)

## 我如何使用参数？

您可以通过输入 `{{parametername}}` 或使用查询下面的按钮，简单地在您的查询中添加一个参数。

您可以通过点击查询编辑器中参数旁边的齿轮来编辑单个参数的属性。这允许您设置一个默认值，定义一个可选用的参数列表或改变参数的类型。如果您想在一个看板上的不同查询之间共享参数，请确保它们在名称、类型和默认值方面完全匹配。

![Parameters how to use](../images/parameters-how-to-use.gif)

## 查询示例

该查询返回以美元计算的已付燃料费总额。

查询作者选择将一个参数用于 `wallet address`、`start date` 和 `end date`。

```sql
with alltransactions
AS (
SELECT 
    block_time, 
    success, 
    gas_price/10^9 AS gas_prices, 
    gas_used,
    (gas_price*gas_used)/10^18 AS eth_paid_for_tx,
    hash
FROM ethereum.transactions
WHERE "from" = CONCAT('\x', substring('{{1. Eth Address}}' from 3))::bytea
AND block_time >= '{{2. Start Date}}'
AND block_time < '{{3. End Date}}')

SELECT
    date_trunc('minute', block_time),
    SUM(eth_paid_for_tx*price) over (ORDER BY date_trunc('minute', block_time)) AS "Total Gas Fees Paid in USD"
FROM alltransactions
LEFT JOIN 
    (SELECT
        minute,
        price
    FROM prices.usd
    WHERE 
        symbol = 'WETH' AND
        minute > '{{2. Start Date}}') AS prices
ON date_trunc('minute', block_time) = minute
ORDER BY block_time DESC
```

[在此](https://dune.com/queries/64430/128463)找到此查询

## 看板示例

**通过这个看板找到关于以太坊钱包的有趣统计数据：**
[https://dune.com/kevdnlol/Transaction-Breakdown](https://dune.com/kevdnlol/Transaction-Breakdown)

_作者在这个看板中包含了 `wallet address`、`start date` 和 `end date` 的参数。_

**深入研究 Barnbridge 的智能收益产品单池：**
[https://dune.com/0xBoxer/Barnbridge-or-Smart-Yield](https://dune.com/0xBoxer/Barnbridge-or-Smart-Yield)

_作者选择在这里将参数 `poolsymbol` 变成一个下拉列表。这样就可以方便地访问所有相关的池子，并对这些池子进行详细的统计。_

**了解有多少人在参与 Yearn Vaults：**
[https://dune.com/msilb7/Yearn-How-Many-Addresses-are-Participating](https://dune.com/msilb7/Yearn-How-Many-Addresses-are-Participating)

[https://dune.com/0xrusowsky/KLIMA-Wallet-Activity](https://dune.com/0xrusowsky/KLIMA-Wallet-Activity)

**了解您在 $KLIMA 中的投资情况：**

[**https://dune.com/0xrusowsky/KLIMA-Wallet-Activity**](https://dune.com/0xrusowsky/KLIMA-Wallet-Activity)

## 总结

参数允许您使您的 SQL 查询的某一部分动态化，从而为您提供使查询和看板互动化的机会。这样您就可以很容易地在您的看板上显示详细的数据，因为它允许浏览者根据自己的需要定制看板。

您可以把参数看作是筛选器，但使用这一功能的可能性超出了这个范围。