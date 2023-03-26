[View code on GitHub](https://dune.com/blob/master/app\queries\tips.md)

The Query Tips technical guide provides users with tips and tricks to help them become more proficient in querying data using Dune. The guide is divided into several sections, each of which focuses on a specific feature of the Dune app. 

The first section of the guide is titled "Use Spells" and explains how users can use the well-organized data found in Spells to perform great analysis. Spells are tables that are cleaned and contain data/metadata that make them very straightforward to query. 

The second section of the guide is titled "V1 Inline Ethereum Addresses Formatting" and explains how Ethereum addresses are stored as PostgreSQL byte arrays, which are encoded with the `\x` prefix. This section provides users with an example of how to use an inline address to filter for a given token. 

The third section of the guide is titled "Quote Column and Table Names in camelCase" and explains how column and table names are mostly taken directly from smart contract Application Binary Interfaces (ABIs), with no modification. This section provides users with an example of how to reference column and table names in PostgreSQL. 

The fourth section of the guide is titled "Remove Decimals" and explains how to transmute ERC-20 tokens into a more human-friendly form by using the `erc20.tokens` table and dividing the token's `transfer_value` by 10. This section provides users with examples of how to perform this operation in both PostgreSQL and Spark SQL. 

The fifth section of the guide is titled "Get time with `date_trunc`" and explains how to use the `date_trunc` function to get the time from decoded event tables. This section provides users with an example of how to use `date_trunc` to get the week from an event table. 

The sixth section of the guide is titled "How to get USD price" and explains how to get the USD price of on-chain activity by joining the smart contract event with the `prices.usd` on the `minute` for a given `asset`. This section provides users with an example of how to perform this operation in PostgreSQL. 

The seventh section of the guide is titled "Token symbols" and explains how to group results by token address using the token symbol instead. This section provides users with examples of how to perform this operation in both PostgreSQL and Spark SQL. 

The eighth section of the guide is titled "Filter Queries and Dashboards with Parameters" and explains how to use parameters to turn a Query or Dashboard into an app for blockchain data. This section provides users with an example of how to add a parameter to a Query and how to use the parameter in a WHERE clause. 

Overall, the Query Tips technical guide provides users with a comprehensive overview of how to use Dune to query data effectively.
## Questions: 
 1. What is the purpose of the app and what kind of data does it analyze?
- The app is called Dune Docs and it provides Query related tips to help users become more powerful in analyzing data. It analyzes blockchain data.

2. What is the difference between Dune V1 and other versions of the app?
- Dune V1 engine has features that are not available in other versions of the app, such as V1 Inline Ethereum Addresses Formatting and Quote Column and Table Names in camelCase.

3. How can parameters be used to filter queries and dashboards in the app?
- Parameters can be added to the SQL editor on the Query editor page by clicking `Add parameter` in the bottom right corner. The name of the parameter is put inside double curly brackets, and if it is used in the WHERE clause, it needs to be enclosed in single quotes.