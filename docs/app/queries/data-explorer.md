---
title: How to Explore Data
description: The Data Explorer allows you to search for blockchain and other data to use in your Queries. Here's how it works.
---

The left sidebar of the query editor is the Data Explorer. It allows you to search for blockchain and other data to use in your queries.

You can learn about Dune's data tables [in the data tables section](../../data-tables/index.md).

## Browsing data

Here is a simple example of how to use the Data Explorer to find the data you need:

1. Click on one of the categories in the left sidebar to see the tables available in that category.
2. Filter the tables through the dropdowns in the top right corner.
3. Check out the table preview to see what data is available in that table.
4. Click on the arrow next to the table name to include it in your query.

<div style="position: relative; padding-bottom: calc(61.916666666666664% + 41px); height: 0;"><iframe src="https://demo.arcade.software/IWTNiiQ9np1JWSe7FRJs?embed" frameborder="0" loading="lazy" webkitallowfullscreen mozallowfullscreen allowfullscreen style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;color-scheme: light;" title="Dune"></iframe></div>

## Finding specific tables

You can also search for specific tables in the Data Explorer.   

1. Choose the "decoded projects" category.
2. Type the projects name in the search bar.
3. Choose the project you want to explore.
4. Type the smart contract name in the search bar.
5. Choose the smart contract you want to explore.

<div style="position: relative; padding-bottom: calc(67.66666666666666% + 41px); height: 0;"><iframe src="https://demo.arcade.software/I28EsaPHjpRQZPLbLTu2?embed" frameborder="0" loading="lazy" webkitallowfullscreen mozallowfullscreen allowfullscreen style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;color-scheme: light;" title="Dune"></iframe></div>

## Finding a smart contract by address

Unfortunately, the Data Explorer does not allow you to search for a smart contract by address. However, you can use [this dashboard](https://dune.com/dune/is-my-contract-decoded-yet-v2) to find the smart contract's name by address. If it doesn't show up, you can submit it for decoding [here](https://dune.com/decoding).

<div style="position: relative; padding-bottom: calc(67.66666666666666% + 41px); height: 0;"><iframe src="https://demo.arcade.software/RJ799xCLgFOc3Vof1quV?embed" frameborder="0" loading="lazy" webkitallowfullscreen mozallowfullscreen allowfullscreen style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;color-scheme: light;" title="Is My Contract Decoded Yet - Dune Engine V2"></iframe></div>


### Blockchain Icons

Some data sets will have multiple blockchain icons - meaning data from each of those blockchains is available within that data set!


| Icon      | Description                          |
| ----------- | ---------------------------------------- |
|    ![ethereum icon](images/explorer-labels/ethereum-icon.png)    | Ethereum blockchain Raw Data, Decoded Project, or Spell |
|![gnosis chain icon](images/explorer-labels/gnosis-chain-icon.png)| Gnosis Chain Raw Data, Decoded Project, or Spell |
| ![polygon icon](images/explorer-labels/polygon-icon.png) | Polygon blockchain Raw Data, Decoded Project, or Spell |
| ![optimism icon](images/explorer-labels/optimism-icon.png) | Optimism blockchain Raw Data, Decoded Project, or Spell |
| ![optimism legacy icon](images/explorer-labels/optimism-legacy-icon.png) | Optimism (legacy) blockchain Raw Data, Decoded Project, or Spell |
| ![bnb chain icon](images/explorer-labels/bnb-chain-icon.png) | BNB Chain Raw Data, Decoded Project, or Spell |
| ![solana icon](images/explorer-labels/solana-icon.png) | Solana blockchain Raw Data, Decoded Project, or Spell |
| ![arbitrum icon](images/explorer-labels/arbitrum-icon.png) | Arbitrum blockchain Raw Data, Decoded Project, or Spell |
| ![avalanche icon](images/explorer-labels/avalanche-icon.png) | Avalanche C-Chain Raw Data, Decoded Project, or Spell |
| ![goerli testnet icon](images/explorer-labels/goerli-testnet-icon.png) | Ethereum Goerli Testnet Raw Data, Decoded Project, or Spell |
| ![fantom icon](images/explorer-labels/fantom-icon.png) | Fantom Raw Data, Decoded Project, or Spell |

### Dataset Icons

| Icon      | Description                          |
| ----------- | ---------------------------------------- |
| ![table icon 1](images/explorer-labels/table-icon-1.png)![table icon 2](images/explorer-labels/table-icon-2.png) | Data Table (Raw Data, Spell, or smart contract Event or Function) |
| ![decoded project icon](images/explorer-labels/decoded-project-icon.png) | Decoded Project (protocol or protocol version eg "opensea" or "aave_v2") |
| ![spell icon](images/explorer-labels/spell-icon.png) | Spell set (eg cow_protocol contains "batches" and "solvers" Spells) |
| ![community data icon](images/explorer-labels/community-data-icon.png) | Community Data Set |

### Dataset Labels

| Label      | Description                          |
| ----------- | ---------------------------------------- |
| `project` | A Spell set for a specific project eg `aave` |
| `sector` | A Spell set for a sector eg `dex` |
| `event` | A smart contract event dataset |
| `function` | A smart contract function dataset |