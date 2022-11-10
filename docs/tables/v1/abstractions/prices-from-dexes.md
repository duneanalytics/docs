---
description: >-
  This table provides a pricefeed for all assets that are traded on a
  decentralized exchange somewhere.
---

# 来源Dex的价格

### 根据交易数据计算的价格

我们创建了一个基于去中心化交易所交易数据的价格表。 该表涵盖的资产比“prices.usd”多得多，因为它涵盖了在“dex.trades”索引的任何去中心化交易所交易的所有资产。

**请记住，此脚本在极少数情况下会产生错误的价格**

此表非常耗费资源，因此只能每隔几个小时更新一次，使用时请记住这一点。 **** 此外，时间周期是每小时级别，所以如果您需要分钟级别价格，请参考 [`prices.usd`](../../prices.md).


该表目前仅存在于我们旧数据库架构上的Ethereum。

### 它是如何运转的

可以在我们的 [公共 github](https://github.com/duneanalytics/spellbook/tree/master/ethereum/prices) 库中访问该表的运行机制。

该脚本根据 dex.trades 中去中心化交易所的数据生成每小时价格中位数。它会基于`prices.usd`中有价格的交易对去确定资产的价格。


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

为了纠正极端异常值并使该表性能更好，该脚本将每小时将所有记录的数据聚合到一个“median_price”中。

### 已知的问题

在极少数情况下，此脚本会报错，因为计算并产出了基于非流动的代币对的价格数据流，。 当该代币的所有流动交易池在“prices.usd”中没有价格馈送时，就会发生这种情况。

An example of this would be $PLAY, a metaverse index from piedao. The liquid trading pair for this asset is $PLAY/$DOUGH. The "correct" price of $PLAY is represented in this pool, but the combination of `dex.trades` and `prices.prices_from_dex_data` are not able to pick up this price.
这方面的一个例子是 $PLAY，一个来自 piedao 的元索引。该资产的流动交易对为 $PLAY/$DOUGH。池子中的$PLAY的会有一个‘正确’的价格，但是通过`dex.trades` 和 `prices.prices_from_dex_data` 这两个表却无法获取此价格。

对于该资产的非流动性对，`dex.trades` 将只有一个 `usd_amount` 字段。在这种情况下，$PLAY/$ETH 池会偶尔进行一次交易，这些交易将在 `dex.trades` 中存有一个`usd_amount`字段。 $PLAY/$ETH 池的流动性非常低，几乎只包含套利交易。 因此，`prices.prices_from_dex_data` 中生成的 pricefeed 是错误的，因为它取决于 `dex.trades` 中的 `usd_amount`。

In order to check for this, you should manually verify the results of `prices.prices_from_dex_data` in order to make sure arbitrage trades do not disturb the price feed constructed. A simple way of validating that the script is working with the right pools is checking the `sample_size` column. If the number seems suspiciously low, the script probably doesn't pick up the right price.

为了检查这一点，您应该手动去验证 `prices.prices_from_dex_data` 的结果，以确保套利交易不会干扰形成的价格。 验证脚本是否使用正确的池的一种简单方法是检查“sample_size”列。 如果这个数字看起来低得可疑，则脚本可能没有找到合适的价格。

在这种情况下，您必须手动构建价格。

### Outro

我们一直在寻求改进此表，如果您有任何想法或意见，请不要犹豫打开 PR 或通过我们的 Discord 联系我们。
