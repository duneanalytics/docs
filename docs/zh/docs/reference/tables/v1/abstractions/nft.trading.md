---
说明: >-
  NFT交易表 在 Dune 上向所有人提供 NFT 交易数据。
  NFT交易表 将跨多个 NFT 平台的数据聚合到一张简单的表格中。
---

# NFT 交易表（nft.trades）

## **一种查询 NFT 数据的简单方法**

NFT 交易表（`nft.trades`）旨在让 Dune 上的每个人都能轻松获得 NFT 交易数据。该表将不同数据平台之间的数据聚合和标准化，并在同一张表中提供辅助信息和元数据。

最重要的是使用该数据集，让在所有索引平台上查询任何与 NFT 相关的交易数据变得非常容易。

到目前为止，我们已经对以下平台的数据进行了索引：

* OpenSea
* Rarible
* SuperRare
* CryptoPunks（他们在自己的合约中进行交易）
* Foundation
* LooksRare

所有这些数据都可以通过非常简单的查询轻松访问，例如：

* [**给定 NFT 的所有交易**](https://dune.xyz/queries/146090)

![NFT](images/nft.png)

```sql
select * from nft.trades 

where nft_contract_address = '\xb47e3cd837ddf8e4c57f05d70ab865de6e193bbb' -- 这是 cryptopunks 的地址
```

* [**过去 24 小时内在给定平台上的交易**](https://dune.xyz/queries/146152)

```sql
select date_trunc('day', block_time), usd_amount, nft_contract_address, token_id from  

where platform = 'OpenSea' -- 仅显示给定平台上的交易

and block_time > now() - interval '24hours'
```

* [**去年的平台交易量**](https://dune.xyz/queries/146160)

```sql
select sum(usd_amount), date_trunc('day', block_time), platform from nft.trades 

where block_time > now() - interval '365 days'

group by 2,3
```

###

### 基本理解

#### 单品交易（Single Item Trade）

交易发生在“买方”（buyer）和“卖方”（seller）之间。

他们交换一个由 `nft_contract_address` 和 `token_id` 的组合唯一标识的项目。买方将以任何给定的 `original_currency` 向卖方支付给定的 `original_amount` 代币。为方便起见，我们已经为你计算了在交易时对应价值的 `usd_amount` 。大多数交易将以 ETH 或 WETH 进行，但尤其是非 OpenSea 交易通常包含其他货币类型。

交易在任何被索引的 `platforms` 上进行，并将通过这些平台的 `exchange_contract_address` 的智能合约来促进。每笔交易都会有诸如 `block_time` ， `tx_hash` ， `block_number` ， `platform version` ， `evt_index` 等元数据。

此外，我们还提供有关交易的 NFT 的元数据。`nft_project_name` 和 `erc_standard` 将帮助你更轻松地分析数据集。`nft_project_name` 数据将从 `nft.tokens` [数据表](https://github.com/duneanalytics/abstractions/blob/master/ethereum/nft/tokens.sql) 中提取，如果你的 NFT 在该表中不存在，欢迎你发PR来添加它。

**捆绑交易（Bundle Trade）**

单次交易也可能包含多个物品。这些物品中的每一个都通过 `nft_contract_address` 和 `token_id` 的组合来唯一标识。然而在这些交易中，没有明确的方法来确定每个物品对应的 `usd_amount` 。一种可能的解决方法是将商品数量除以捆绑商品的付款金额，但是当非实物/价值的商品捆绑出售时，这种逻辑就不成立了。我们建议从你正在使用的数据集中删除捆绑转移，因为它会严重影响任一方向的结果。请注意，如果在同一交易中转移具有不同Token ID 或 erc 类型的代币，则 `token_id` 和 `erc_standard` 将为空（Null）。

**聚合贸易（Aggregator Trade）**

在使用 NFT 聚合器平台时，也会出现单次交易包含多个物品的情况。我们的方法是分解聚合器交易，以便每一行对应一个被交易的唯一商品，及其关联的 ID、价格、分类等。重要的是，`trade_type` 将指示为`聚合贸易` ，平台名称和地址可以在 `nft.aggregators` [数据表](https://github.com/duneanalytics/abstractions/blob/master/ethereum/nft/aggregators.sql) 中找到。如果该表中缺少你的聚合平台，欢迎你提交 PR 以添加它。

**平台和版税费用**

在最新版本的 `nft.trades` 中，如果销售许可费(royalty fees)的原始金额，美元金额以及百分比的信息在数据库中存在，那么检索时是一并提供的。版税归创作者所有，平台费用由 NFT 平台收取。请注意，版税费用并非总是能检索，所以默认设置为 null。

### **示例看板**

**利用参数的看板**

[**https://dune.xyz/0xBoxer/NFT**](https://dune.xyz/0xBoxer/NFT)

[**https://dune.xyz/rantum/NFT-Sales-Overview-by-Project**](https://dune.xyz/rantum/NFT-Sales-Overview-by-Project)

**涵盖整个生态系统的看板**

[**https://dune.xyz/rantum/NFT-Collection-Dashboard**](https://dune.xyz/rantum/NFT-Collection-Dashboard)

[**https://dune.xyz/masquot/NFT-Sales-Trends**](https://dune.xyz/masquot/NFT-Sales-Trends)

## **您好，我的平台没有被索引**

处理每个市场数据的 SQL 代码是开源的，可在我们的 [github 存储库](https://github.com/duneanalytics/abstractions/tree/master/ethereum/nft/trades) 中找到。每个人都可以查看代码、提交拉取请求并提交代码以添加更多交易市场。

另请阅读有关此主题的“[数据抽象](index.md)”部分。

**数据表内容**

| 列名                | 数据类型              | 说明                                                                      |
| ---------------------------- | ------------------------ | --------------------------------------------------------------------------------- |
| block\_time                  | timestamp with time zone | 该交易何时执行的                                                    |
| nft\_project\_name           | text                     | NFT 项目名称（例如“the dudes”）                                              |
| nft\_token\_id               | text                     | 交易的 token\_id（例如 235）                                         |
| erc\_standard                | text                     | 交易代币的代币标准                                          |
| platform                     | text                     | 该交易是在哪个平台上执行的？                                        |
| platform\_version            | text                     | 使用了该平台的哪个版本？                                   |
| trade\_type                  | text                     | “单品销售”还是“捆绑销售”？                                           |
| number\_of\_items            | integer                  | 本次交易一共交易了多少个 NFT？                                        |
| category                     | text                     | 这是拍卖（auction）还是直销（direct sale）？                                           |
| evt\_type                    | text                     | 当前未使用，默认“Trade”                                           |
| aggregator                   | text                     | 此交易是否使用聚合器进行（是：聚合器名称，否：NULL）     |
| usd\_amount                  | numeric                  | 执行时交易的美元价值                                       |
| seller                       | bytea                    | NFT 卖家地址                                                                   |
| buyer                        | bytea                    | NFT 买家地址                                                                    |
| original\_amount             | numeric                  | 正确格式的金额                                                    |
| original\_amount\_raw        | numeric                  | 货币的原始金额                                                       |
| eth\_amount                  | numeric                  | 执行时交易的 ETH 价值                                     |
| royalty\_fees\_percent       | numeric                  | 支付给创作者的版税（百分比）                                          |
| original\_royalty\_fees      | numeric                  | 交易所用货币的特许权使用费                                  |
| usd\_royalty\_fees           | numeric                  | 执行时特许权使用费的美元价值                                    |
| platform\_fees\_percent      | numeric                  | 平台费用（百分比）                                                             |
| original\_platform\_fees     | numeric                  | 用于此交易的货币的平台费用                                 |
| usd\_platform\_fees          | numeric                  | 执行时平台费用的美元价值                                   |
| original\_currency           | text                     | 用于此交易的货币                                                  |
| original\_currency\_contract | bytea                    | 本次交易所用币种的 erc20 地址（不适用于原始ETH） |
| currency\_contract           | bytea                    | 修正后的货币合约                                                  |
| nft\_contract\_address       | bytea                    | 交易的 NFT 合约地址                                           |
| exchange\_contract\_address  | bytea                    | 促成此交易的平台合约                                |
| tx\_hash                     | bytea                    | 本次交易的哈希                                                     |
| block\_number                | integer                  | 该交易执行完成的区块编号                                    |
| tx\_from                     | bytea                    | 发起本次交易的地址                                                       |
| tx\_to                       | bytea                    | 接收这笔交易的地址                                                        |
| trace\_address               | ARRAY                    | n/a                                                                               |
| evt\_index                   | integer                  | 事件索引                                                                      |
| trade\_id                    | integer                  | n/a                                              
