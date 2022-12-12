---
description: Raw data tables are the basic building blocks of our database.
---

# BNB Chain (BSC)

BNB链(之前叫币安智能链，BSC)是一个以太坊虚拟机的实例，由流行的加密货币交易所[Binance](https://binance.com)的团队建立和维护。BNB链遵循以太坊主网的大部分规则，但没有实施EIP1559。相反，它依靠[BEP-95](https://github.com/bnb-chain/BEPs/blob/master/BEP95.md)来燃烧平台使用过程中累积的费用。此外，每个区块的gas限制被设置为100 mio，使更多的交易能够在一个给定的区块中被处理。交易费用是以$BNB而不是$ETH支付的。

您可以在[文档]（https://docs.bnbchain.org/docs/bnbIntro）中阅读更多关于BNB链的信息。

在Dune上，这意味着EIP1559交易的gas字段保持为空，其他都是一样的。


<div class="cards grid" markdown>
- [BNB链文档](https://docs.bnbchain.org/docs/bnbIntro)
</div>

### Raw data tables

<div class="cards grid" markdown>
- [Blocks](blocks.md)
- [Transactions](transactions.md)
- [Event logs](event-logs.md)
- [Traces](traces.md)
</div>
