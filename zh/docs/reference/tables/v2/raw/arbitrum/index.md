---
description: 原始数据表是我们数据库的基本构建块。
---

# Arbitrum

Arbitrum是一个通过乐观的汇总（rollup）来结清其在以太坊主网上的交易的L2区块链。您可以在他们的[文档](https://developer.offchainlabs.com/docs/inside\_arbitrum)中阅读有关Arbitrum扩展和构建汇总的方法的所有信息。

Arbitrum的执行环境与主网EVM实施的不同之处在于它计算燃料成本的方式。由于Arbitrum是在以太坊主网上发布其交易的乐观汇总方案，因此其燃料计算必须考虑其他的因素。

## L1的燃料成本

Arbitrum上的交易必须同时为L1和L2资源支付燃料。L1资源本质上只是以太坊调用数据；即，您支付交易原始数据的大小乘以Arbitrum对L1调用数据的价格定价。这已经将L1的燃料价格波动考虑在内。给定交易中的L2资源是您在交易中调用的计算和存储的本地新增成本，类似于任何其他EVM链。

由于以太坊虚拟机的“正常”实现不具备多种支付燃料费用的方式，Arbitrum通过将L1资源的成本包含在使用的计算燃料单位（`gas_limit`或`gas_used`）中解决了这个问题。每当有人尝试在Arbitrum上进行交易时，RPC端点被调用以估算足够的“燃料限制”，其返回的计算燃料单位数量超过了“正常”EVM中会产生的标准成本。

```
P = Arbitrum上的“燃料价格” = Arbitrum的本地燃料价格 
G = 传统上的“燃料限制” = L2消耗的燃料 + L1资源消耗的燃料
```

Arbitrum的交易成本使用以下公式计算：

$$
P*G = 交易成本（Costs）
$$

G包括：

$$
(L2消耗的燃料) +\frac{(L1的燃料价格 * L1调用数据)}{P} = G
$$

因此，完整的计算包括：

$$
P * ((L2消耗的燃料) +\frac{(L1的燃料价格 * L1调用数据)}{P}) =  交易成本
$$

通过这个公式我们可以理解Arbitrum上的燃料价格上涨会导致交易更便宜。这是因为无论是需要发布一个还是一千个交易，Arbitrum将始终在以太坊主网上发布其交易。只有在对区块空间的需求增加时，Arbitrum的费用才会上涨。作为回报，对区块空间的需求增加意味着更多Abritrum交易在一次“批量发布”交易中被发布到主网上，因而显著降低了单个交易的成本。

我们在`gas_used_for_l1`列中反映了用于Arbitrum交易的L1资源的燃料消耗。

### 燃料价格机制

Arbitrum不遵循EIP1559标准，而是有自己的机制来确定燃料成本。一笔交易会有一个`gas_price`，它被视为用户愿意为此交易支付的最高价格。用户支付的实际`gas_price`将由Arbitrum EVM中的 [算法](https://developer.offchainlabs.com/docs/inside\_arbitrum#price-for-arbgas)确定。用户支付的实际`gas_price`反映在`effective_gas_price`列中。

### 燃料使用量计算

Arbitrum不遵循标准的EVM规范和规则来计算交易使用了多少燃料。Arbitrum的EVM中的成本以不同的方式计算到一起，其中涉及包括和排除相应的L1资源成本。您可以[在他们的文档中](https://developer.offchainlabs.com/docs/avm\_specification#instructions)查看Arbitrum的AVM操作码成本规范。

**您不能将Arbitrum的燃料成本与其他EVM链的燃料成本进行比较！**

### 简而言之

使用`effective_gas_price`计算Arbitrum上的燃料成本。

要查看仅在Arbitrum EVM中发生的燃料成本，请从`effective_gas_price`字段中减去`gas_used_for_l1`的金额。

话虽如此，您仍然不能将Arbitrum的燃料消耗与其他EVM链的燃料成本进行比较。

### 原始数据表

<div class="cards grid" markdown>
- [区块表（Blocks）](blocks.md)
- [交易表（Transactions）](transactions.md)
- [事件日志表（Logs）](event-logs.md)
- [内部合约调用表（Traces）](traces.md)
</div>
