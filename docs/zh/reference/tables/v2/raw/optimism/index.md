---
description: 原始数据表是我们数据库的基本构建块。
---

# Optimism

Optimism是一个第2层乐观汇总网络，旨在利用以太坊的强大安全保证，同时降低其成本和延迟。Optimism在以太坊主网之外处理交易，减少基础层的拥塞并提高可扩展性。要深入了解Optimism，我们建议阅读他们的[文档](https://community.optimism.io/docs/how-optimism-works)。

Optimism的不同之处在于其EVM实现中计算燃料成本的方式，因为它还需要为L1资源付费。

## Optimism的燃料成本

Optimism在以太坊主网上结清它的交易。通过在L1上的排序器合约将Optimism网络上的任意给定交易的原始调用数据批量提交到L1网络。批量结清交易的这些成本需要包括在Optimism的燃料成本计算中。Optimism的交易费用使用以下公式计算：

$$
交易费用 = L1费用 + (L2燃料价格 * L2燃料消耗数量)
$$

**L1费用包括：**

$$
L1费用 = L1费用标量 * L1燃料价格 * L1燃料消耗数量
$$

`L1费用标量`是一个可以由Optimism团队增加或减少的变量。它确保L1的燃料成本得到充分覆盖，并为Optimism团队提供收入。`L1燃料价格`是对以太坊主网上的燃料价格的估计。

`L1燃料消耗数量` **可以分解为：**

$$
L1燃料消耗数量 = 调用数据消耗的燃料 + 一个固定的间接燃料成本
$$

**因此，Optimism的燃料成本的完整计算包括：**

$$
交易费用 = L1费用标量 * L1燃料价格 * (L1调用数据消耗的燃料 + 一个固定的间接燃料成本)
$$

您可以在[这篇文章](https://help.optimism.io/hc/en-us/articles/4411895794715-Transaction-fees)中阅读更多关于Optimism燃料成本以及将其最小化的方法。

### 简而言之

要计算Optimism交易的燃料成本，您需要遵循以下公式：

```
L1费用 + (燃料价格 * 燃料消耗数量)
```

此外，Optimism尚未实施EIP1559，因此它遵循“旧”的燃料拍卖模型。

### 原始数据表

<div class="cards grid" markdown>
- [区块表（Blocks）](blocks.md)
- [交易表（Transactions）](transactions.md)
- [事件日志表（Logs）](event-logs.md)
- [内部合约调用表（Traces）](traces.md)
</div>
