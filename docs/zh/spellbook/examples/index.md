---
title: 魔法书示例
---

作为例子，我们可以看看 ERC-20。[ERC-20](https://ethereum.org/en/developers/docs/standards/tokens/erc-20) 代币是同质化代币，都遵循以太坊基金会制定的合约标准。为了追踪每日余额，我们需要首先识别转账。

为此，我们将使用的主要基础 Dune 数据表是您可以在数据浏览器找到的 `erc20_ethereum.evt_Transfer`。
![type:video](https://www.loom.com/embed/198148674ded4f5e944f65452852482b)

在我们的例子中，我们将魔法分解成更多模块化的系列魔法：

- [重新更改格式的](reformatted.md)转账
- [每日汇总的](daily-aggregation.md)转账
- [滚动总和的](rolling-sum.md)每日转账
- [最终每日余额](final-day-balance.md)（Ethereum ERC20 代币）
