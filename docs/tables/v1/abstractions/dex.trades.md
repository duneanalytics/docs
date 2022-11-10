---
description: >-
  dex.trades makes erc20 trading data available to everyone on Dune Analytics.
  Dex.trades aggregates data across multiple DEX platforms into one simple
  table.
---

# dex.trades

### 去中心化交易所的交易数据


去中心化交易所是该行业的脉搏。您可以通过智能合约将任何ERC20代币换成任何ERC20代币。但是这里的问题是：这里有太多dex了，以几乎没有人能拿到所有这些dex智能合约的完整数据。这就是我们创建dex.trades的原因。

该表对几乎所有的去中心化交易所的交易数据进行了标准化和规范化。这将使您可以轻松查询您喜欢的代币的交易数据，而无需自己处理所有不同的dex智能合约。

生成表dex.trades的脚本可以在这个[公共github](https://github.com/duneanalytics/spellbook/tree/master/ethereum/dex) 存储库中找到。

### dex.trades

| block\_time                 | timestamptz | 交易的时间戳                                                                |
| --------------------------- | ----------- | ------------------------------------------------------------------------------------------------------------------------ |
| token\_a\_symbol            | text        | 参与交易的2个代币中的其中1个的符号                                                                     |
| token\_b\_symbol            | text        | 参与交易的2个代币中的其中1个的符号                                                                      |
| token\_a\_amount            | numeric     | 被交易的代币A的数量|
| token\_b\_amount            | numeric     | 被交易的代币B的数量|                                                                            |
| project                     | text        | 交易是在哪个dex上发生的                                                                            |
| version                     | text        | dex的版本                                                                                              |
| category                    | text        | 这是一个聚合器或者是一个单纯的dex           |
| trader\_a                   | bytea       | 哪个地址请求了dex 的智能合约                                                                                  |
| trader\_b                   | bytea       | 在某些特殊情况下，实际上交易的对手方，如果有会显示在这里 | |
| token\_a\_amount\_raw       | numeric     | 被交易的代币A的原始数量                                                                                |
| token\_b\_amount\_raw       | numeric     | 被交易的代币B的原始数量                                                                          |
| usd\_amount                 | numeric     | 该笔交易的USD价值                                                                                              |
| token\_a\_address           | bytea       | 代币A的ERC20合约地址                                                                              |
| token\_b\_address           | bytea       | 代币B的ERC20合约地址                                                                              |                                                                             |
| exchange\_contract\_address | bytea       | Dex的智能合约地址                                         |
| tx\_hash                    | bytea       | 包含着笔交易的哈希           |
| tx\_from                    | bytea       | 交易的发起者                                                                                |
| tx\_to                      | bytea       | 这个tx调用的第一个智能合约                                                        |
| trace\_address              | ARRAY       | 交易执行在图树中的哪个位置？                                                  |
| evt\_index                  | integer     | 在区块中的索引位置（按执行排序的累计日志量）                                  |
| trade\_id                   | integer     | 处于database magic的需要                                                                                                 |
