[View code on GitHub](https://dune.com/docs/app/queries/tips.md)

# Query Tips

This technical guide provides tips for using queries in the Dune app. It covers various topics such as using Spells, formatting Ethereum addresses, quoting column and table names, removing decimals, getting time with `date_trunc`, getting USD price, using token symbols, and filtering queries and dashboards with parameters.

The guide starts with an introduction to Spells, which are well-organized tables that contain cleaned data and metadata that make them easy to query. The guide then explains how to format Ethereum addresses in Dune V1 engine, which uses PostgreSQL byte arrays encoded with the `\x` prefix. The guide also provides a warning that column and table names are case sensitive in PostgreSQL and that double quotes are reserved for tables and columns, whereas single quotes are reserved for values.

The guide then explains how to remove decimals from Ether transfers and ERC-20 tokens, which have 18 decimal places, making them difficult to read. The guide suggests using the `erc20.tokens` table and dividing the token's `transfer_value` by 10. The guide also provides examples of how to use `date_trunc` function to get time and how to get USD price by joining the smart contract event with the `prices.usd` on the `minute` for a given `asset`.

The guide also explains how to use token symbols instead of token addresses to group results by token address. To do this, the guide suggests joining the `erc20.tokens` table with the event table where `asset` = `{{token_address}}`. The guide also provides examples of how to filter queries and dashboards with parameters, which can turn a Query or Dashboard into an app for blockchain data.

Overall, this technical guide provides useful tips for using queries in the Dune app. It is a valuable resource for anyone looking to become a more powerful user of Dune.
## Questions: 
 1. What is the purpose of the Dune V1 engine and what features are only available in it?
- The Dune V1 engine is mentioned in several sections of the technical guide, and a blockchain SQL analyst might want to know what it is and what features are exclusive to it. The guide states that the V1 engine is required for certain features such as inline Ethereum address formatting and camelCase table and column name references.

2. How can token symbols be used instead of token addresses in queries?
- The guide explains that token symbols can be more user-friendly than token addresses, but also warns that the erc20.tokens table only contains popular tokens and may exclude more obscure ones. A blockchain SQL analyst might want to know how to join the erc20.tokens table with their event table to select symbols instead of addresses.

3. How can parameters be used to filter queries and dashboards?
- The guide explains how parameters can be used to turn queries and dashboards into blockchain data apps, and provides an example of how to add a parameter for token symbol or holder address. A blockchain SQL analyst might want to know how to use parameters in their queries and how to format addresses to save users from having to input the `\x` prefix.