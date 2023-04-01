[View code on GitHub](https://dune.com/docs/data-tables/raw/blocks.md)

# Blocks

This section of the app technical guide covers the concept of blocks in blockchains and rollups. A block is a collection of transactions that incrementally alter the state of an EVM system. Transactions within a block can only be executed one after the other, not in parallel. The purpose of this section is to provide an understanding of how blocks work in the context of the Dune Docs project.

## Tables

This section provides tables that are useful for identifying block activity and transaction changes over time. There are two tables provided, one for the V2 Engine (Spark SQL) and one for the V1 Engine (PosgreSQL). Each table contains information about the chains, tables, and notes for each chain. For example, the Ethereum Mainnet chain has a table called `ethereum.blocks` that contains information about blocks on the Ethereum Mainnet.

## Column Data

This section provides a description of the data contained in each column of the block tables. The table contains columns such as `time`, `number`, `hash`, `parent hash`, `gas limit`, `gas used`, `miner`, `difficulty`, `total difficulty`, `nonce`, `size`, and `base_fee_per_gas`. Each column is described in detail, including its data type and a brief description of its purpose.

### Example

This section provides an example of the data contained in the block tables. The example is in the form of a video that demonstrates how to use the block tables to identify block activity and transaction changes over time.

Overall, this app technical guide provides a comprehensive understanding of blocks in the context of the Dune Docs project. It covers the tables and column data that are useful for identifying block activity and transaction changes over time. The guide is useful for developers who are working on the Dune Docs project and need to understand how blocks work in the context of the project.
## Questions: 
 1. What is the purpose of the Dune Docs app and how does it relate to blockchain SQL analysis?
    
    The app technical guide describes the tables and column data related to blocks in various blockchain chains. A blockchain SQL analyst might want to know how this information can be used in their analysis and what specific insights they can gain from it.

2. Are there any limitations or gaps in the data provided by the Dune Docs app that might impact blockchain SQL analysis?

    The tables provided in the app technical guide do not contain certain information such as `nonce`, `miner`, `difficulty`, `total_difficulty`, `size`, and `base_fee_per_gas` for some chains. A blockchain SQL analyst might want to know how these limitations might impact their analysis and if there are any workarounds.

3. How does the Dune Docs app handle rollups and how can this information be used in blockchain SQL analysis?

    The app technical guide mentions that blocks are the building blocks of rollups, but it does not provide specific information on how rollups are handled in the app. A blockchain SQL analyst might want to know how rollups are represented in the app and how this information can be used in their analysis.