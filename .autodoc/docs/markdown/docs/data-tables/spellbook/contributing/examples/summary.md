[View code on GitHub](https://dune.com/docs/data-tables/spellbook/contributing/examples)

This folder contains a series of technical guides focused on the `app` folder of the Dune Docs project, specifically covering the process of tracking daily balances for Ethereum ERC-20 tokens. The guides provide detailed explanations of various features and functionalities, including reformatted transfers, daily aggregation, rolling sum, and final daily balances. These guides are essential for analysts who want to understand the inner workings of the Dune Docs project and how to use it effectively.

The `reformatted.md` guide explains the reformatted transfers feature, which simplifies the process of summing up transfers by creating a union of sent and received transactions. It covers the handling of WETH, the use of JINJA config blocks, and provides examples of the `transfers_ethereum_erc20.sql` and `transfers_ethereum_schema.yml` files.

The `daily-aggregation.md` guide covers the daily aggregation feature, which sums all transfers for the day. It explains the incremental nature of the feature, the use of merge strategies, and the concept of refs. The guide also provides examples of the `transfers_ethereum_erc20_agg_day.sql` file and the `transfers_ethereum_schema.yml` file.

The `rolling-sum.md` guide focuses on the rolling sum window function applied to each daily transfer sum. It explains how to calculate the rolling sum of raw amounts of ERC20 tokens held, using the `transfers_ethereum_erc20_rolling_day.sql` file. The guide also includes the schema for the `transfers_ethereum_erc20_rolling_hour` table, as found in the `transfers_ethereum_erc20_schema.yml` file.

The `final-day-balance.md` guide covers the Final Daily Balance feature, which provides a comprehensive view of daily Ethereum ERC20 token balances, including price data and compliance checks. It explains the use of the `balances_ethereum_erc20_day.sql` file and the schema for the `balances_ethereum_erc20_day` table, as found in the `transfers_ethereum_schema.yml` file.

Lastly, the `index.md` guide provides an overview of the entire process of tracking daily balances for ERC-20 tokens using the Dune app. It introduces the concept of ERC-20 tokens and their contract standard, as well as the modular series of spells used to track daily balances.

These guides are useful for analysts who want to gain a deeper understanding of the Dune Docs project and its features. By following the examples provided in the guides, analysts can effectively track daily balances for ERC-20 tokens and make informed decisions based on the data.
