[View code on GitHub](https://dune.com/blob/master/data tables\spellbook\top tables\dex.trades.md)

# Dex.Trades App Technical Guide

This technical guide provides an overview of the dex.trades feature of the Dune Docs project. Dex.trades is a table that aggregates data across multiple decentralized exchange (DEX) platforms into one simple table. The purpose of this table is to standardize and normalize trading data across virtually all relevant DEXs, making it easier for users to query trading data for their favorite tokens without having to deal with all of the different DEX smart contracts themselves.

## Column Data

The guide provides a detailed breakdown of the column data contained in the dex.trades table. The column names, data types, and descriptions are all listed in a table format. Some of the key columns include:

- `block_time`: The timestamp of the block that included the transaction
- `token_a_symbol` and `token_b_symbol`: The symbols of the two tokens that were traded
- `token_a_amount` and `token_b_amount`: The amounts of token A and token B that were traded
- `project`: The DEX on which the trade was executed
- `usd_amount`: The USD value of the trade

## Github Repo

The guide also provides a link to the public Github repo where the scripts that generate the dex.trades table can be found. The repo is located in the `ethereum/dex` folder of the Dune Analytics Spellbook.

Overall, this technical guide provides a high-level overview of the dex.trades feature of the Dune Docs project, including its purpose, column data, and Github repo.
## Questions: 
 1. What blockchains does dex.trades support?
- The `blockchain` column in the table provides information on which blockchain the trade occurred on.

2. Can dex.trades handle trades from all decentralized exchanges?
- The app technical guide states that dex.trades standardizes and normalizes trading data across "virtually all relevant decentralized exchanges," but it is unclear if there are any exchanges that are not supported.

3. How is the USD value of a trade calculated?
- The `usd_amount` column in the table provides the USD value of a trade, but it is unclear how this value is calculated.