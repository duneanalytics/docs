---
标题: 价格
描述: 这些数据表让您能够获取几乎所有ERC20代币的价格。
---

## 来自第三方数据供应方的价格数据 <a href="#centralised-exchanges-trading-data" id="centralised-exchanges-trading-data"></a>

我们通过[coinpaprika](https://coinpaprika.com) 的API获取价格数据。

价格是基于实时市场数据的成交量加权价格，换算成美元。

### prices.usd

这个表提供了一些列的erc20.tokens。

如果您想要的代币没有在这里列出，请向我们的 [GitHub repository](https://github.com/duneanalytics/spellbook/blob/main/models/prices/prices_tokens.sql)提交一个pull request。 (对于V1引擎，您可以使用来自去中心化交易所的价格 **dex.view\_token\_prices.**)

| <p></p><p><strong>变量名</strong></p> | **描述**                               |
| ------------------------------------------ | --------------------------------------------- |
| contract\_address                          | erc20代币的合约地址       |
| symbol                                     | 资产的标识符（代币代码、现金标签） |
| price                                      | 任意一分钟内资产的价格    |
| minute                                     | 这个表的时间尺度是每分钟   |

请注意 `WETH`会用做 ETH 的价格，因为它的交易价格相同。

### prices.layer\_usd

此表支持其他区块链上的一层资产。

| contract\_address | erc20代币的合约地址       |
| :---------------: | --------------------------------------------- |
|       symbol      | 资产的标识符（代币代码、现金标签） |
|       price       | 任意一分钟内资产的价格   |
|       minute      | 这个表的时间尺度是每分钟    |
