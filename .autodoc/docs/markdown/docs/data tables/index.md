[View code on GitHub](https://dune.com/blob/master/data tables\index.md)

# Tables and Chains Overview

This technical guide provides an overview of the tables and chains available in the Dune Analytics platform. The guide is divided into two main sections: the four kinds of tables and available chains. 

The first section explains the process of ingesting data from node providers to create raw tables, which are then decoded using contract ABIs to provide easier to work with decoded tables. The abstracted tables are then created to standardize and aggregate the data from all other tables, giving users the easiest to work with spell tables. The community providers like Reservoir and Flashbots are also explained, which can be thought of as spell level abstractions. 

The second section provides a list of available chains that can be queried in Dune Analytics. Each chain is explained in detail, including Ethereum, Gnosis Chain, Polygon POS, Optimism, BNB Chain, Arbitrum, Avalanche (C-Chain), Ethereum's Goerli Testnet, Fantom, Solana, and Bitcoin. 

The guide also includes links to relevant documentation for each chain, such as Ethereum.org for Ethereum, and the Binance Smart Chain documentation for BNB Chain. Additionally, the guide provides a brief history of Ethereum and its updates, as well as a deep dive into Optimism's Layer 2 Optimistic Rollup network. 

The guide also includes a suggestion to look in spellbook and community datasets first, and then if users can't find what they want, they can try decoded and raw tables. 

Overall, this technical guide provides a comprehensive overview of the tables and chains available in Dune Analytics, making it easier for users to navigate and query the platform. 

Example: 

If a user wants to query data from the Ethereum Mainnet, they can read the section on Ethereum, which explains the history of Ethereum, its updates, and provides a link to Ethereum.org for further documentation. The guide also explains that querying on Dune works exactly the same as querying on Ethereum Mainnet.
## Questions: 
 1. What kind of data is included in the raw and decoded tables for each chain?
- The raw tables contain unedited, raw, and encoded blockchain data, while the decoded tables provide decoded calls and events made to smart contracts.

2. How does querying data from Gnosis Chain (xDai) differ from querying data from Ethereum Mainnet?
- Gnosis Chain follows all standards and upgrades of Ethereum Mainnet, so querying on Dune works exactly the same.

3. What is the difference between Solana and EVM chains in terms of data?
- Solana is a non-EVM blockchain that employs a "proof of history" mechanism, so its data is quite different from EVM chains.