---
标题: 数据表
---

**Dune 支持以不同的抽象级别查询已接入的链上数据。**

您可以从已接入的区块链原始表开始，例如像`blocks`和`transactions`数据表。这些原始表有着最原始的链上数据，可用于灵活的数据分析。

与此同时，为了更轻松地分析智能合约，Dune还提供了具有可读性的解码数据表。我们使用智能合约的 ABI(Application Binary Interface) 和标准化代币智能合约的接口标准（ERC20、ERC721 等）用于解码数据。截止撰写此文档时，我们已经索引了超过超过28万份智能合约。你可以[在此提交新的合约](../features/adding-new-contracts.md)与Dune进行解码。

此外，我们正在将常用链上数据（如 NFT 与 DEX 数据）和第三方数据集共同构建组成一系列抽象组合。

以下是可用内容的概览：

- [Raw data](raw.md): 未经编辑、原始编码的区块链数据
- [Decoded data](decoded.md): (**目前使用最广泛的数据源**) 经过解码后的智能合约事件及调用数据
- [Abstractions, or Spells](abstractions.md): 由Dune和社区一起维护建设的数据表
- [Community](community.md): 由指定合作组织提供的链下数据源
- [Prices](prices.md): 由第三方数据源提供的代币价格数据
- [User generated](user-generated.md): 在我们的数据库中构建您自定义的视图、函数或数据表

数据模型的细节取决于区块链和引擎。 我们已为 [Dune V1 引擎](v1/raw/index.md) (PostgreSQL) 以及 [Dune V2 引擎](v2/raw/index.md) (Databricks SQL) 上的数据编制了详细的参考资料。
