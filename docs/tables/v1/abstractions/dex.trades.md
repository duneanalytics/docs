---
description: >-
  dex.trades makes erc20 trading data available to everyone on Dune Analytics.
  Dex.trades aggregates data across multiple NFT platforms into one simple
  table.
---

# dex.trades

### Decentralized exchange trading data

Decentralized exchanges are the beating heart of the industry. You can swap any ERC20 token for any ERC20 token through the magic of smart contracts. The problem here though: there is so many decentralized exchanges out there that it is hardly possible for any single person to work with the smart contract data for all of them. That's why we created dex.trades.

This table standardizes and normalizes the trading data across virtually all relevant decentralized exchanges. This in turn allows you to easily query for trading data for your favorite tokens without having to deal with all of the different dex smart contracts yourself.

The scripts that generate the table dex.trades can be found in this [public github](https://github.com/duneanalytics/spellbook/tree/master/ethereum/dex) repo.

### dex.trades

| block\_time                 | timestamptz | the timestamp of the block that included this transaction                                                                |
| --------------------------- | ----------- | ------------------------------------------------------------------------------------------------------------------------ |
| token\_a\_symbol            | text        | the symbol of one of the two tokens that got traded                                                                      |
| token\_b\_symbol            | text        | the symbol of one of the two tokens that got traded                                                                      |
| token\_a\_amount            | numeric     | the amount of token A that got traded                                                                                    |
| token\_b\_amount            | numeric     | the amount of token B that got traded                                                                                    |
| project                     | text        | On which dex did this trade get executed?                                                                                |
| version                     | text        | which version of the dex got used?                                                                                       |
| category                    | text        | is this project and aggregator or a decentralized exchange?                                                              |
| trader\_a                   | bytea       | Which contract called the dex contract?                                                                                  |
| trader\_b                   | bytea       | in some special cases there actually is a counterparty to transactions, this party will get displayed here if applicable |
| token\_a\_amount\_raw       | numeric     | the raw amount of token A that got traded                                                                                |
| token\_b\_amount\_raw       | numeric     | the raw amount of token B that got traded                                                                                |
| usd\_amount                 | numeric     | The USD value of this trade                                                                                              |
| token\_a\_address           | bytea       | the erc20 token contract address of token A                                                                              |
| token\_b\_address           | bytea       | the erc20 token contract address of token B                                                                              |
| exchange\_contract\_address | bytea       | the address of the decentralized exchange contract that made this trade possible                                         |
| tx\_hash                    | bytea       | the hash of the transaction that contained this trade                                                                    |
| tx\_from                    | bytea       | Which address initiated this transaction?                                                                                |
| tx\_to                      | bytea       | What was the first smart contract that got called during this tx?                                                        |
| trace\_address              | ARRAY       | Which position in the graph tree does the execution of the trade have?                                                   |
| evt\_index                  | integer     | this logs index position in the block (cumulative amount of logs ordered by execution)                                   |
| trade\_id                   | integer     | just for database magic                                                                                                  |
