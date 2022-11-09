---
description: Raw data tables are the basic building blocks of our database.
---

# Optimism


Optimism 是一个2层乐观卷积（Optimistic Rollup）网络，旨在利用以太坊提供的强大安全保证，同时降低其交易成本和延迟。 Optimism在以太坊主网之外处理交易，减少基础层的拥塞并提高可扩展性。 要深入了解乐观卷积，我们建议阅读他们的 [文档](https://community.optimism.io/docs/how-optimism-works)。

<div class="cards grid" 降价>
- [Optimism如何运作](https://community.optimism.io/docs/how-optimism-works)
</div>

Optimism的不同之处在于它在计算 gas 成本时的 EVM 实现，因为它还需要为 L1 资源付费。

## Optimism的Gas费用


Optimism讲其交易合并到以太坊主网，这是通过 L1 上的排序器合约解决的，该合约将Optimism网络上的交易数据打包提交L1上，批量结算交易的这些成本需要在 Optimism 的 gas 成本计算中考虑， Optimism 的交易费用使用以下公式计算：

$$
Transaction\ Fees = L1\ fee + (L2\ gas\ price * L2\ gas\ used)
$$

**L1费用组成:**

$$
L1\ Fee = Fee\ Scalar * L1\ Gas\ Price * L1\ Gas\ Used
$$


`L1 Fee Scalar` 是一个可以由Optimism团队控制的可以增加/减少的变量，它确保 L1 的 gas 成本得到充分覆盖，并为 Optimism 团队提供收入， `L1 Gas Price` 是对 Mainnet 上的 gas 价格的估计。

`L1 Gas used` **分解为:**

$$
L1\ Gas\ Used = Calldata\ gas + a\ fixed\ overhead\ gas\ cost
$$

**因此，optimism的gas气成本的完整计算包括:**

$$
Transaction\ Fee = Fee\ Scalar * L1\ Gas\ Price * (L1 Calldata\ gas + a\ fixed\ overhead\ gas\ cost)
$$

您可以阅读更多关于 Optimism Gas 成本以及将其最小化的方法：[这篇文章](https://help.optimism.io/hc/en-us/articles/4411895794715-Transaction-fees).

### TL;DR

要计算 Optimism 交易的 gas 成本，您需要遵循以下公式：

```
L1\_Fee + (gas_price*gas_used)
```
此外，Optimism 尚未实施 EIP1559，因此它遵循“旧”的gas拍卖模型。

### Raw data tables

<div class="cards grid" markdown>
- [Blocks](blocks.md)
- [Transactions](transactions.md)
- [Event logs](event-logs.md)
- [Traces](traces.md)
</div>
