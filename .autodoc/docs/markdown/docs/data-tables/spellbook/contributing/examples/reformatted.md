[View code on GitHub](https://dune.com/docs/data-tables/spellbook/contributing/examples/reformatted.md)

# Reformatted Transfers

This technical guide is focused on the `app` folder of the Dune Docs project and covers the reformatted transfers feature. The purpose of this feature is to make it easier to sum up transfers by munging the base table into a union of sent transactions and received transactions. 

The guide explains that WETH requires special handling due to the additional functions of deposit and withdrawal. Therefore, `zeroex_ethereum.weth9_evt_deposit` is added as a source. The model is defined in a YAML file where the description, tests, and metadata are defined. Contributors are also tracked in this file. 

The JINJA config block is used to define the alias for this view as `erc20`. Without this alias, the table name would default to the file name. The schema name for this view is defined in the `dbt_project.yml` file in the root of the Spellbook project. Schema’s are defined there by the directory structure. The name of this view would be `transfers_ethereum.erc20` given the current structure.

The guide provides an SQL example of the `transfers_ethereum_erc20.sql` file, which includes four CTEs: `sent_transfers`, `received_transfers`, `deposited_weth`, and `withdrawn_weth`. These CTEs are used to select unique transaction IDs, wallet addresses, token addresses, event block times, and raw amounts for each transfer type. The `unique_tx_id`, `blockchain`, `wallet_address`, `token_address`, `evt_block_time`, and `amount_raw` columns are then selected from each CTE and unioned together to create the final table.

The `transfers_ethereum_schema.yml` file is also provided as an example. This file includes metadata such as the blockchain, sector, project, contributors, tags, and description for the `transfers_ethereum_erc20` model. The `dbt_project.yml` file is also included as an example, which defines the schema and materialized view for the `transfers` and `ethereum` folders.

Overall, this technical guide provides a detailed explanation of the reformatted transfers feature in the Dune Docs app. It covers the purpose of the feature, how it works, and provides examples of the SQL, YAML, and `dbt_project.yml` files used to implement it.
## Questions: 
 1. What is the purpose of the dune docs app and how does it relate to blockchain SQL analysis?
   
   The app is a documentation platform for spells used in Dune Analytics, which is a platform for blockchain SQL analysis. Blockchain SQL analysts may use this app to understand the data models and schemas used in Dune Analytics.

2. What is the purpose of the `transfers_ethereum_erc20` model and how is it defined?
   
   The `transfers_ethereum_erc20` model is used to track ERC20 token transfers on the Ethereum blockchain. It is defined in a YAML file and a SQL file, where the SQL file defines the logic for the model and the YAML file defines metadata such as the description, tests, and contributors.

3. How does the app handle WETH deposits and withdrawals?
   
   The app handles WETH deposits and withdrawals by adding `zeroex_ethereum.weth9_evt_deposit` as a source and defining two SQL queries to handle deposited and withdrawn WETH. These queries are then combined with queries for sent and received transfers to create a union of all transfer types.