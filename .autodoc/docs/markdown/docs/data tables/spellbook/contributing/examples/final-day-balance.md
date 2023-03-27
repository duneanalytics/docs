[View code on GitHub](https://dune.com/blob/master/data tables\spellbook\contributing\examples\final-day-balance.md)

# Final Daily Balance

This technical guide is focused on the `app` folder of the Dune Docs project. The guide explains the final daily Ethereum ERC20 token balances spell. The spell is expanded to cover all days, not just the days with transfer activity. The guide also explains how price data is added, known rebase tokens are removed, and any tokens that resulted in large negative balances are removed.

The `balances_ethereum_erc20_day.sql` file contains the SQL code for the spell. The code uses the `transfers_ethereum_erc20_rolling_day` table to derive the `balances_ethereum_erc20_noncompliant` table. The `balances_ethereum_erc20_noncompliant` table looks for unique token addresses with larger negative balances, which indicate the contract may not be compliant with ERC20. The `tokens_ethereum_rebase` table is a static list of known rebase tokens that are managed.

The SQL code in `balances_ethereum_erc20_day.sql` calculates the daily token balances of ERC20 Ethereum tokens per wallet and contract address pair. The code uses the `prices` table to calculate the amount in USD. The code also removes rebase tokens from balances and likely non-compliant tokens due to negative balances.

The `transfers_ethereum_schema.yml` file contains the schema for the `balances_ethereum_erc20_day` table. The table has columns for the blockchain, day, wallet address, token address, amount raw, amount, amount USD, and symbol.

Overall, this technical guide provides a detailed explanation of the final daily Ethereum ERC20 token balances spell and how it works. It also explains the tables used and how they are derived. The guide is useful for developers who want to understand how the spell works and how to use it in their projects.
## Questions: 
 1. What is the purpose of the `transfers_ethereum_erc20_rolling_day` table and how is it used in the `balances_ethereum_erc20_day` query?
   
   The blockchain SQL analyst might want to know more about the `transfers_ethereum_erc20_rolling_day` table and how it is used in the `balances_ethereum_erc20_day` query to understand how daily token balances are calculated.

2. How are rebase tokens identified and removed from the final daily Ethereum ERC20 token balances spell?
   
   The blockchain SQL analyst might want to know more about how rebase tokens are identified and removed from the final daily Ethereum ERC20 token balances spell to understand how the spell handles these types of tokens.

3. What is the significance of the `balances_ethereum_erc20_noncompliant` table and how is it derived?
   
   The blockchain SQL analyst might want to know more about the `balances_ethereum_erc20_noncompliant` table and how it is derived to understand how the spell identifies non-compliant ERC20 tokens.