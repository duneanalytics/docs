---
description: 原始数据表是我们数据库的基本构建块。
---

# BNB Chain (BSC)

BNB链（原币安智能链，BSC）是以太坊虚拟机的一个实例，由来自流行的加密交易所[Binance]（https://binance.com）的团队构建和维护。BNB链遵循以太坊主网的大部分规则，但尚未实现 EIP1559。相反，它依赖[BEP-95](https://github.com/bnb-chain/BEPs/blob/master/BEP95.md)来燃烧平台使用期间所产生的费用。此外，每个区块的燃料限制设置为100 mio，从而可以在给定区块中处理更多交易。交易费用以$BNB而不是$ETH支付。

您可以在[这份文档](https://docs.bnbchain.org/docs/bnbIntro)中阅读有关BNB链的更多信息。

这意味着在Dune上除了保存EIP1559交易的燃料数据的字段保持空白外，其他的一切都相同。

### 原始数据表

<div class="cards grid" markdown>
- [区块表（Blocks）](blocks.md)
- [交易表（Transactions）](transactions.md)
- [事件日志表（Logs）](event-logs.md)
- [内部合约调用表（Traces）](traces.md)
</div>