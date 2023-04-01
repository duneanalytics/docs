[View code on GitHub](https://dune.com/docs/data-tables/community/reservoir/bids.md)

# Bids

## Reservoir.bids

This section of the app technical guide covers the `reservoir.bids` table, which contains records with information about each bid. The table includes various columns such as `id`, `kind`, `status`, `contract`, `token_set_id`, `maker`, `taker`, `price`, `value`, `currency_address`, `currency_symbol`, `currency_price`, `quantity`, `quantity_filled`, `quantity_remaining`, `valid_from`, `valid_until`, `nonce`, `source`, `fee_bps`, `expiration`, `raw_data`, `created_at`, and `updated_at`.

The `id` column represents the internal order id, while the `kind` column represents the protocol name (e.g. seaport). The `status` column represents the order status (active, inactive), and the `contract` column represents the contract address. The `token_set_id` column represents the id of the token set, while the `maker` and `taker` columns represent the maker and taker wallet addresses, respectively.

The `price` column represents the current price in native currency, while the `value` column represents the current value in native currency. The `currency_address` column represents the currency address, and the `currency_symbol` column represents the currency symbol. The `currency_price` column represents the currency price.

The `quantity` column represents the amount of tokens that is listed, while the `quantity_filled` column represents the amount of tokens that was filled. The `quantity_remaining` column represents the amount of tokens remaining, and the `valid_from` and `valid_until` columns represent the listing start and end times, respectively.

The `nonce` column represents the order nonce of the maker, while the `source` column represents the source of the listing (e.g. opensea.io). The `fee_bps` column represents the listing fee, and the `expiration` column represents the associated transaction hash. The `raw_data` column represents the raw order data (format will vary per source).

Finally, the `created_at` and `updated_at` columns represent the timestamps the listing was created and updated, respectively.

Query examples for this table can be found at the link provided in the guide.
## Questions: 
 1. What is the purpose of the dune docs project and how does this table fit into it?
- This app technical guide only provides information about the `reservoir.bids` table and does not give context about the overall purpose of the dune docs project.

2. How is the data in this table being collected and updated?
- The app technical guide does not provide information about the data collection and update process for this table.

3. Are there any constraints or limitations on the data types or values that can be stored in this table?
- The app technical guide does not mention any constraints or limitations on the data types or values that can be stored in this table.