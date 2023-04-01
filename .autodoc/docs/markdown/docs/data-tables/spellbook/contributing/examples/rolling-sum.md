[View code on GitHub](https://dune.com/docs/data-tables/spellbook/contributing/examples/rolling-sum.md)

# Rolling Sum of Daily Transfers

This section of the app technical guide covers the rolling sum window function applied to each daily transfer sum. The purpose of this query is to calculate the rolling sum of raw amounts of ERC20 tokens held after taking into account token decimals. The query is contained in the `transfers_ethereum_erc20_rolling_day.sql` file located in the `app` folder of the project. 

The query selects the blockchain, day, wallet address, token address, symbol, last updated timestamp, recency index, and the rolling sum of the raw amount of ERC20 tokens held. The `transfers_ethereum_erc20_agg_day` reference is used to partition the data by token address and wallet address and order it by day. 

The `transfers_ethereum_erc20_schema.yml` file in the `app` folder of the project contains the schema for the `transfers_ethereum_erc20_rolling_hour` table. The table includes columns for blockchain, hour, wallet address, token address, symbol, amount raw, amount, amount USD, updated at, and recency index. 

Overall, this section of the app technical guide provides information on how to calculate the rolling sum of raw amounts of ERC20 tokens held using a window function. It also includes the schema for the table that stores the results of this calculation.
## Questions: 
 1. What is the purpose of the `rolling sum window function` in this app technical guide?
    
    The purpose of the `rolling sum window function` is to apply it to each daily transfer sum in order to calculate the rolling sum of raw amount of ERC20 token held.

2. What is the significance of the `recency_index` column in the `transfers_ethereum_erc20_schema.yml` file?
    
    The `recency_index` column is an index of the most recent balance ascending, where `recency_index=1` is the wallet/contract pair's most recent balance.

3. How does the `transfers_ethereum_erc20_rolling_hour` table differ from the `transfers_ethereum_erc20_agg_day` table?
    
    The `transfers_ethereum_erc20_rolling_hour` table calculates the rolling sum of raw amount of ERC20 token held after taking into account token decimals, while the `transfers_ethereum_erc20_agg_day` table does not.