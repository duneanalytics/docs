[View code on GitHub](https://dune.com/tree/master/doc\docs\json\docs\data tables\spellbook\contributing\examples)

This section of the app technical guide focuses on the Spellbook Examples for the Dune Docs project, specifically covering the daily aggregation of transfers, final daily balances, reformatted transfers, and rolling sum of daily transfers features. These modular spells demonstrate how to track daily balances for ERC-20 tokens that follow a contract standard set by the Ethereum Foundation. The guide is particularly useful for developers looking to track daily balances for ERC-20 tokens using the Dune Docs app.

The **Daily Aggregation** feature sums all transfers for the day and is incrementally loaded every 15 minutes. The guide explains the use of JINJA blocks and refs in this spellset, as well as providing examples of the `transfers_ethereum_erc20_agg_day.sql` file and the `transfers_ethereum_schema.yml` file.

The **Final Daily Balance** feature calculates the final daily Ethereum ERC20 token balances per wallet and contract address pair. The guide explains how price data is added, known rebase tokens are removed, and any tokens that resulted in large negative balances are removed. Examples of the `balances_ethereum_erc20_day.sql` file and the `transfers_ethereum_schema.yml` file are provided.

The **Reformatted Transfers** feature reformats the data from the `evt_Transfer` table to make it easier to work with. The guide explains how WETH requires special handling and how `zeroex_ethereum.weth9_evt_deposit` is added as a source to the model. Examples of the SQL code for the `transfers_ethereum_erc20` model, the YAML file for the model, and the `dbt_project.yml` file are provided.

The **Rolling Sum of Daily Transfers** feature applies a rolling sum window function to each daily transfer sum. The guide provides examples of the `transfers_ethereum_erc20_rolling_day.sql` file and the `transfers_ethereum_schema.yml` file.

In summary, this section of the app technical guide offers a comprehensive understanding of the Spellbook Examples for the Dune Docs project, focusing on the daily aggregation of transfers, final daily balances, reformatted transfers, and rolling sum of daily transfers features. The guide is beneficial for developers who want to implement these features in their own projects and gain a deeper understanding of how they work within the Dune Docs app.
