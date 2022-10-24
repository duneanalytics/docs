---
description: 原始数据表是我们数据库的基本构建块。
---

# Avalanche C-Chain

C-Chain是由Avalanche网络提供支持的以太坊虚拟机的一个实例。它遵循以太坊主网规则，只是共识机制不同，其他技术规范完全相同。 燃料以$AVAX而不是$ETH支付。

您可以在[这篇文章](https://learn.figment.io/protocols/avalanche)中阅读更多关于Avalanche网络和C-Chain的信息。

在Dune上使用C-Chain的工作方式与查询以太坊主网数据完全一样。只有`avalanche_c.blocks`的属性略有不同，因为Avalanche C-Chain已经使用权益证明（POS）共识算法。

### 原始数据表

<div class="cards grid" markdown>
- [区块表（Blocks）](blocks.md)
- [交易表（Transactions）](transactions.md)
- [事件日志表（Logs）](event-logs.md)
- [内部合约调用表（Traces）](traces.md)
</div>
