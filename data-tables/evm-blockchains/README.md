# EVM Blockchains

## Introduction

All EVM blockchains and rollups fundamentally share the same Ethereum virtual machine(EVM) execution environment. Therefore, the concepts explained in the following apply to the following blockchains that are currently available on Dune:

* Ethereum Mainnet
* Gnosis Chain (formerly xDai)
* BNB Smart Chain (formerly Binance Smart Chain)
* Polygon
* Optimism
* Arbitrum

If not specified otherwise, all information in the EVM Blockchain sections apply to all blockchains which share the EVM execution model.

### Data for EVM chains

For the listed EVM chains above we offer you **raw data** and **decoded data**. We further work with these tables in our [abstraction](../abstractions/) tables to standardize and normalize this data.

### ****[**Raw data**](raw-data/)****

Raw data is just that: unedited, raw and encoded blockchain data. \
These tables are notoriously hard to work with since the data is encoded, but these tables do contain all the information you could ever need. You might be using these tables to pull metadata for transactions, look at the network as a whole or to work with contracts which are not able to be decoded due to missing smart contract source code.&#x20;

### ****[**Decoded data**](./#decoded-data)****

The tables on Dune which contain decoded data allow you to view the decoded calls and events made to smart contracts. We use the ABI for smart contracts and the interface standard for standardised token smart contracts (ERC20, ERC721 etc.) to decode data and produce nice human readable tables.

These are the tables that you will mainly be working with while working on Dune. They provide you with easy access to relevant data. Not all smart contracts are decoded on Dune by default, you need to signal to us that you want to work with this data in order for us to decode the data.\
Learn more about this in "[Adding new contracts](../../duneapp/adding-new-contracts.md)". However at time of writing, we have indexed over 280k contracts, so chances are pretty high that the smart contracts you want to work with are already decoded.



