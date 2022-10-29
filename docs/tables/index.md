---
标题: 数据表
---

**Dune让你在已支持的链上的不同层次抽象表中检索数据。**

首先，你可以浏览各支持链上的原始数据，像 `blocks`和`transactions`。这是最灵活的方式。这是最灵活的方式。 

为了更方便地分析智能合约, Dune同时提供了一些独立的、易于阅读的解码数据表。我们为智能合约使用ABI，并为标准化代币(ERC20, ERC721 etc.)使用接口标准。 截至编写本文档，我们已为超过28万份的合约编制了索引，你可以在这里 [提交新合约](../features/decoded-contracts.md).

在此基础上，我们在构建一系列的 [Spells](spells.md) 为了一些常见的使用场景 (e.g. NFTs or DEX)和第三方的数据集.

以下列出了所有的数据种类:

- [原始数据](raw.md): 未经编辑和解码的原始链上数据
- [解码数据](decoded.md): (**最常用**) 根据命令和事件解码的智能合约数据 
- [Spells](spells.md): Dune和社区定制和维护的数据表
- [Community](community.md): 与某些组织合作取得的链下数据
- [Prices](prices.md): 第三方提供的价格数据
- [User generated](user-generated.md): 在提供数据基础上，构建自己的看板，功能和表格

The details of the data model depends on the blockchain and engine. We've compiled detailed references for tables on our [Dune V1 Engine](v1/raw/index.md) (PostgreSQL) and [Dune V2 Engine](v2/raw/index.md) (Databricks SQL).

## How Tables are Generated from Raw Ethereum Data

!!! note
    Table generation is similar to this for all EVM based blockchains. The labels below follow Dune V1 naming conventions and are slightly different in Dune V2 Tables. Learn about the [differences in V2's data structure here](http://localhost:8000/docs/features/dune-v2/). And learn [how to search V2 data here](http://localhost:8000/docs/features/queries/data-explorer/#v2).

There are three main tables in Dune generated from raw Ethereum data, which are the source truth for everything else on the platform.

![token data to dune tables graph](images/token-data-to-dune-tables-graph.jpg)

The rest of Dune's tables are built from these three:

![tables levels of abstraction graph](images/tables-levels-of-abstraction-graph.jpg)

If you can't figure out the table to query from, you'll need to dig through an example transaction hash on [the relevant chain's blockchain explorer](../resources/wizard-tools/blockchain-explorers.md) to figure out the call/evt Contract.

Essentially go `tx_hash` → `contract` in "to" → `code` and pull the contract name from there. If it's a proxy, the blockchain explorer should link you to an implementation address. 

Dune V2 data also has a handy Lineage Graph that lets you explore how all of Dune's data tables are related to each other - [learn more about that in the Lineage Graph section here](../spellbook/spellbook-model-docs/).

![what should a trade table look like](images/what-should-a-trade-table-look-like.png)

You should always try to use the [Decoded](decoded.md) or [Spell](spells.md) tables when you can as these are human-readable and pre-organized so they're much easier to use.
