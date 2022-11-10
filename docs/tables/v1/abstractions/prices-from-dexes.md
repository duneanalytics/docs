---
description: >-
  This table provides a pricefeed for all assets that are traded on a
  decentralized exchange somewhere.
---

# 来源Dex的价格

### 根据交易数据计算的价格

We created a table that creates price feeds based on decentralized exchange trading data. This table covers much more assets than `prices.usd`, since it covers all assets that are traded on any  of the decentralized exchanges that are indexed in `dex.trades`.
我们创建了一个基于去中心化交易所交易数据的价格表。 该表涵盖的资产比“prices.usd”多得多，因为它涵盖了在“dex.trades”索引的任何去中心化交易所交易的所有资产。

**请记住，此脚本在极少数情况下会产生错误的价格**

此表非常耗费资源，因此只能每隔几个小时更新一次，使用时请记住这一点。 **** 此外，时间周期是每小时级别，所以如果您需要分钟级别价格，请参考 [`prices.usd`](../../prices.md).


该表目前仅存在于我们旧数据库架构上的Ethereum。

### 它是如何运转的

可以在我们的 [公共 github](https://github.com/duneanalytics/spellbook/tree/master/ethereum/prices) 库中访问该表的运行机制。

This script generates median hourly prices based on data from decentralized exchanges found in `dex.trades`. It will assign asset prices based on a trading pair which has a pricefeed in `prices.usd`.
该脚本根据 dex.trades 中去中心化交易所的数据生成每小时价格中位数。 


让我们以 $SPELL/ETH 池为例。

* $ETH 价格包含在 `prices.usd` 中
* `prices.usd` 中不包含 $SPELL 价格

为了获得 $SPELL 价格，脚本将根据所兑换的 $ETH 价格动态计算 $SPELL 的价格。
例如，5 $ETH were exchanged for 1,086,083 $SPELL.

Dex.trades 将根据“prices.usd”中的 $ETH 价格数据为该交易分配一个“usd_amount”。

这里 `usd_amount` 是 $23,498.

`5 * price of ETH (4.699,6) = $23,498`

计算 $SPELL 的价格现在就像用 `dex.trades` 中记录的 `usd_amount` 一样简单。

`$23,498/1,086,083 ≈ $0,02163`

我们现在已经成功计算出 1 $SPELL 的价格。

为了纠正极端异常值并使该表具有性能，该脚本将每小时将所有记录的数据聚合到一个“median_price”中。

### Known issues

In rare cases this script will generate price feeds that are based on illiquid pairs and therefore report wrong data. This happens when all liquid trading pools of this token do not have a price feed in `prices.usd`.

An example of this would be $PLAY, a metaverse index from piedao. The liquid trading pair for this asset is $PLAY/$DOUGH. The "correct" price of $PLAY is represented in this pool, but the combination of `dex.trades` and `prices.prices_from_dex_data` are not able to pick up this price.

Instead, `dex.trades` will only have a `usd_amount` for illiquid pairs of this asset. In this case, the $PLAY/$ETH pool has trades once in a while and these will have a `usd_amount` in `dex.trades`. The liquidity of the $PLAY/$ETH pool is very low and it pretty much only consists of arbitrage trades. Therefore, the resulting pricefeed in `prices.prices_from_dex_data` is faulty since it depends on the `usd_amount` in `dex.trades`.

In order to check for this, you should manually verify the results of `prices.prices_from_dex_data` in order to make sure arbitrage trades do not disturb the price feed constructed. A simple way of validating that the script is working with the right pools is checking the `sample_size` column. If the number seems suspiciously low, the script probably doesn't pick up the right price.

In cases like this, you have to manually construct a price feed.

### Outro

We are always looking to improve this table, if you have any ideas or comments don't hesistate to open a PR or contact us in our Discord.
