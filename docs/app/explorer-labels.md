---
title: Data Explorer Labels
description: While using the Data Explorer and these docs, you'll encounter a variety of labels. Here's what they all mean.
---

While using the [Data Explorer](queries/data-explorer.md) (and in reading these docs), you'll encounter a variety of labels.

Here's what they all mean.

## Blockchain Icons

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

## Dataset Icons

| Icon      | Description                          |
| ----------- | ---------------------------------------- |
| ![table icon 1](images/explorer-labels/table-icon-1.png)![table icon 2](images/explorer-labels/table-icon-2.png) | Data Table (Raw Data, Spell, or smart contract Event or Function) |
| ![decoded project icon](images/explorer-labels/decoded-project-icon.png) | Decoded Project (protocol or protocol version eg "opensea" or "aave_v2") |
| ![spell icon](images/explorer-labels/spell-icon.png) | Spell set (eg cow_protocol contains "batches" and "solvers" Spells) |
| ![community data icon](images/explorer-labels/community-data-icon.png) | Community Data Set |

## Dataset Labels

| Label      | Description                          |
| ----------- | ---------------------------------------- |
| `project` | A Spell set for a specific project eg `aave` |
| `sector` | A Spell set for a sector eg `dex` |
| `event` | A smart contract event dataset |
| `function` | A smart contract function dataset |

## Data Type Labels

You can find the full [Spark SQL data types documentation here](https://docs.databricks.com/sql/language-manual/sql-ref-datatypes.html). For types not found there, see [Apache Spark SQL data types here](https://spark.apache.org/docs/latest/sql-ref-datatypes.html).

For V1 Data here are the [official PostgreSQL data types](https://www.postgresql.org/docs/current/datatype.html).

| Label      | Description                          |
| ----------- | ---------------------------------------- |
| `string` | Character sequences of any length greater or equal to 0. |
| `long` | Represents 8-byte signed integer numbers. The range of numbers is from -9223372036854775808 to 9223372036854775807. |
| `integer` | Represents 4-byte signed integer numbers. The range of numbers is from -2147483648 to 2147483647. |
| `double` | Represents 8-byte double-precision floating point numbers. |
| `boolean` | Represents boolean values. (TRUE|FALSE) |
| `date` | Represents values comprising values of fields year, month and day, without a time-zone. |
| `timestamp` | Represents values comprising values of fields year, month, day, hour, minute, and second, with the session local time-zone. The timestamp value represents an absolute point in time. |
| `decimal({{p}},{{s}})` | Represents numbers with a specified maximum precision (p, 1 - 38) and fixed scale (s, the number of digits to the right of the decimal, 0 to p). |
| `array<{{xx}}>` | An array of `{{xx}}` data. (`long`, `string`, etc) |