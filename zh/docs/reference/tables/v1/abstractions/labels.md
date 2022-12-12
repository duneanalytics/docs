# 标签（Labels）

您是否曾经在Dune上查询得到一堆地址列表以及想知道这些美妙的随机十六进制编码字符串背后是什么东西？我们也遇到过这种情况。

**地址标签** 是Dune 上的一项功能，您作为用户可以为任何地址添加、更新标签数据或者查询这些标签

## 什么是标签？

标签是**关于某个地址的元数据**、或者说是一个标记或元数据。它以键值对的形式出现。键是标签的类型，值是标签名称。

在 [**标签页面**](https://dune.xyz/labels) 浏览地址和标签。

## 标签看长什么样子？

查看 [这个看板](https://dune.xyz/hagaetc/labels) 了解可以使用标签创建的示例。

**地址标签示例**

地址 [0xD551234Ae421e3BCBA99A0Da6d736074f22192FF](https://dune.xyz/ethereum/address/0xD551234Ae421e3BCBA99A0Da6d736074f22192FF) 可以被这样标记：

| **type**    | **name** |
| ----------- | -------- |
| owner       | binance  |
| wallet type | exchange |

此地址归属交易所Binance。

地址 [0xe65040f61701940b62e18da7a53126a58525588b](https://dune.com/ethereum/address/0xe65040f61701940b62e18da7a53126a58525588b) 可以被这样标记：

| **type**   | **name**     |
| ---------- | ------------ |
| dapp usage | uniswap user |
| activity   | dex trader   |

这个地址曾经与 Uniswap 进行过交互。

您可以随意想出新的类型和标签名称，因为 Dune 上的标签是开放式的并且**众包**的。

添加标签的方法有两种：

使用 Dune 查询来标记地址。一种非常强大且可扩展的方式来添加标签，例如“所有这些地址都使用过 Uniswap”等等。

请参阅我们的 [Github](https://github.com/duneanalytics/abstractions/tree/master/labels)，了解使用您自己的查询和PR 创建标签的示例！

Examples of what you can do:

* 标记所有使用某个Dapp的地址
* 标记所有持有一定数量某种代币的地址
* 标记每月使用某个Dapp超过X次的所有地址
* 标记所有向Binance转账的地址
* Label all addresses that use a dapp more than X times per month


您还可以围绕用户模式做更多新颖和复杂的事情，例如谁进行了套利交易或从闪电贷款中获利等等。

请注意，在 [dune.xyz](http://dune.xyz/) 上添加标签后，在您可以在 SQL 中查询它之前可能会有几分钟延迟。

## 标签表

标签存储在新的 `labels.labels` 表中，该表具有以下图式：

| 列名 | 数据类型   | 说明                                              |
| ----------- | ----------- | -------------------------------------------------------- |
| id          | int         | 自增整数                                    |
| address     | bytea       | 此标签描述的合约或钱包的地址 |
| name        | text        | 标签名称                                               |
| type        | text        | 标签类型                                               |
| author      | text        | 创建此标签的用户的用户名         |
| source      | text        | 此标签的来源，由 Dune 自动填充          |
| updated\_at | timestamptz | 最近更改此标签的时间                     |

## 使用标签
请注意，该表为每个地址中包含多行记录，因此对它进行连接可能会很棘手。出于这个原因，我们制作了方便的功能：

`labels.get(address bytea, type text default null) RETURNS text[]`

我们预计这将是使用标签的主要方式。请参阅下面的示例。

通常，如果您执行返回 `address` 的查询，您可以使用 `labels.get(address)` 来获取该地址的所有标签，而与标签类型无关。如果您想查看 `owner` 类型的标签，可以执行  `labels.get(address, 'owner')` 。您还可以将此函数传递给您想要包含的几种标签类型，例如：`labels.get(address, 'owner', 'project')` 。

我们还添加了函数 `labels.url(address bytea)` 。从您的查询中传递给该函数一个地址，您的结果表将包含一个可点击的链接，例如：

[https://dune.xyz/ethereum/address/0xD551234Ae421e3BCBA99A0Da6d736074f22192FF](https://dune.xyz/ethereum/address/0xD551234Ae421e3BCBA99A0Da6d736074f22192FF)


### 用例：我想显示地址列表的标签 <a href="#usecase-i-want-to-display-labels-for-a-list-of-addresses" id="usecase-i-want-to-display-labels-for-a-list-of-addresses"></a>

> 我们鼓励您在阅读本文时在 Dune 中运行这些查询

假设您正在查看过去 24 小时内所有 dex 中 DAI 的前 10 名交易者：

```sql
SELECT trader_a, SUM(token_a_amount)
FROM dex.trades
WHERE token_a_symbol = 'DAI'
AND block_time > now() - interval '24 hours'
GROUP BY 1
ORDER BY 3 DESC
LIMIT 10;
```

如果您想为这些地址添加标签，只需将 `trader_a` 列更改为 `labels.get(trader_a)` 。

> 注意：在下面的示例中，`---` 表示删除的行，而 `+++` 表示添加的行。

```sql
SELECT trader_a, labels.get(trader_a) as label, SUM(token_a_amount)
    FROM dex.trades
    WHERE token_a_symbol = 'DAI'
    AND block_time > now() - interval '24 hours'
    and not labels.get(trader_a) isnull
    GROUP BY 1
    ORDER BY 2 DESC
    LIMIT 100;
```

现在您已将地址替换为交易者a（trader\_a）的所有标签列表。有时您只对标签的一个子集感兴趣：`labels.get` 接受一个可选的类型名称列表，用于过滤您获得的标签类型。假设您只对 `‘activity’` 标签感兴趣：

```sql
 SELECT trader_a, labels.get(trader_a, 'activity') as label, SUM(token_a_amount)
    FROM dex.trades
    WHERE token_a_symbol = 'DAI'
    AND block_time > now() - interval '24 hours'
    and not labels.get(trader_a) isnull
    GROUP BY 1
    ORDER BY 2 DESC
    LIMIT 100;
```

当然您也可以显示地址，同时过滤多种标签类型

```sql
    SELECT trader_a, labels.get(trader_a, 'activity', 'project', 'contract_name') as label, SUM(token_a_amount)
    FROM dex.trades
    WHERE token_a_symbol = 'DAI'
    AND block_time > now() - interval '24 hours'
    and not labels.get(trader_a) isnull
    GROUP BY 1
    ORDER BY 2 DESC
    LIMIT 100;
```

您还可以使用 `labels.url` 使地址可点击：

```sql
SELECT labels.url(trader_a), labels.get(trader_a, 'activity') as labels, SUM(token_a_amount)
    FROM dex.trades
    WHERE token_a_symbol = 'DAI'
    AND block_time > now() - interval '24 hours'
GROUP BY 1, 2
    ORDER BY 3 DESC
    LIMIT 10;
```

这样，查看您的看板的人可以轻松地为其添加更好的标签！

### 用例：我想按存在的标签过滤我的查询。<a href="#usecase-i-want-to-filter-my-query-by-labels-that-exist" id="usecase-i-want-to-filter-my-query-by-labels-that-exist"></a>

在这个用例中，您不想使用 `labels.get`，因为它操作起来可能很慢。相反，您将在 SQL 中使用奇妙的 `EXISTS` 函数。

例如：您正在查询 _Uniswap_，但对之前在 _1inch_ 上交易过的用户的行为感兴趣。以下是您的处理方式：

```sql
SELECT "to"
FROM uniswap_v2."Pair_evt_Swap" 
WHERE EXISTS(
            SELECT *
            FROM labels.labels
            WHERE address="to"
            AND type='dapp usage'
            AND name='1inch user'
            )
LIMIT 10;
```

上面的查询将为您提供 10 个在 Uniswap 上交换并在 1inch 上交易过的地址。

当然，您可以结合使用这两种模式！ 如果您确实对这些地址上的标签感兴趣，请继续使用 `labels.get` 和 `WHERE EXISTS` 模式：

```sql
--- SELECT "to"
+++ SELECT "to", labels.get("to")
    FROM uniswap_v2."Pair_evt_Swap" 
    WHERE EXISTS(SELECT * FROM labels.labels WHERE address="to" AND type='dapp usage' AND name='1inch user')
    LIMIT 10;
```

您得到：您看到在 Uniswap 和 1inch 上交易的地址_以及_所有相关的地址标签。
