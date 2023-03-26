[View code on GitHub](https://dune.com/blob/master/data tables\community\reservoir\sales.md)

# Sales

This section of the app technical guide covers the `reservoir.sales` table, which contains records with information about each sale. The table includes various columns such as `id`, `contract`, `token_id`, `order_id`, `order_kind`, `order_side`, `order_source`, `from`, `to`, `price`, `usd_price`, `currency_address`, `currency_symbol`, `currency_price`, `amount`, `fill_source`, `aggregator_source`, `wash_trading_score`, `is_primary`, `tx_hash`, `tx_log_index`, `tx_batch_index`, `tx_timestamp`, `created_at`, and `updated_at`. Each column is described in detail, including its data type and a brief description of its purpose.

The guide also provides two query examples that can be used to retrieve data from the `reservoir.sales` table. These queries can be accessed via the links provided in the guide.

Overall, this section of the app technical guide is useful for developers who need to work with sales data in the Dune Docs project. It provides a clear understanding of the structure and contents of the `reservoir.sales` table, as well as examples of how to query the data.
## Questions: 
 1. What is the purpose of the `reservoir.sales` table in the context of blockchain technology? 
- The `reservoir.sales` table contains records with information about each sale, likely related to transactions on a blockchain.

2. How is the `usd_price` column calculated and what currency is it based on? 
- The `usd_price` column represents the sale price in USD, but it is unclear how this value is calculated or what currency exchange rate is used.

3. What is the significance of the `is_primary` column and how does it relate to blockchain technology? 
- The `is_primary` column indicates whether the sale is a paid mint, but it is unclear how this relates to blockchain technology or what a paid mint refers to in this context.