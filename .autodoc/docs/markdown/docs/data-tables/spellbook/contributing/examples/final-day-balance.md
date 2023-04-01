[View code on GitHub](https://dune.com/docs/data-tables/spellbook/contributing/examples/final-day-balance.md)

# Final Daily Balance

This technical guide covers the Final Daily Balance feature of the Dune Docs project. The feature is located in the `app` folder of the project. 

The Final Daily Balance feature is an Ethereum ERC20 token balances spell that expands the Spell to cover all days, not just the days with transfer activity. The feature adds price data, removes known rebase tokens, and any tokens that resulted in large negative balances. 

The `balances_ethereum_erc20_day.sql` file contains the SQL code for the feature. It uses the `transfers_ethereum_erc20_rolling_day` table to derive the `balances_ethereum_erc20_noncompliant` table, which looks for unique token addresses with larger negative balances that indicate the contract may not be compliant with ERC20. The `balances_ethereum_erc20_day` table then removes rebase tokens from balances and likely non-compliant tokens due to negative balances. 

The `transfers_ethereum_schema.yml` file contains the schema for the `balances_ethereum_erc20_day` table. The table provides daily token balances of ERC20 Ethereum tokens per wallet and contract address pair. The table depends on `erc20_ethereum_transfers`. 

Overall, the Final Daily Balance feature provides a comprehensive view of daily Ethereum ERC20 token balances, including price data and compliance checks.
## Questions: 
 1. What is the purpose of the `transfers_ethereum_erc20_rolling_day` table and how is it used in the `balances_ethereum_erc20_day` SQL query?
   
   The blockchain SQL analyst might want to know more about the `transfers_ethereum_erc20_rolling_day` table and how it is used in the `balances_ethereum_erc20_day` SQL query to understand how the daily token balances are calculated.

2. How are rebase tokens and non-compliant tokens identified and removed from the final daily balances?

   The blockchain SQL analyst might want to know more about how rebase tokens and non-compliant tokens are identified and removed from the final daily balances to understand the accuracy and reliability of the data.

3. What is the significance of the `prices` table and how is it used in the `balances_ethereum_erc20_day` SQL query?

   The blockchain SQL analyst might want to know more about the `prices` table and how it is used in the `balances_ethereum_erc20_day` SQL query to understand how the daily token balances are converted to USD.