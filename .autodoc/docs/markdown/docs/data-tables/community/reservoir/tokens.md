[View code on GitHub](https://dune.com/docs/data-tables/community/reservoir/tokens.md)

# App Technical Guide: Tokens

## Reservoir.tokens

This section of the app technical guide covers the `reservoir.tokens` table, which contains records with information about each NFT token. The table includes various columns such as `id`, `contract`, `token_id`, `name`, `description`, `collection_id`, `owner`, `floor_ask_id`, `floor_ask_value`, `floor_ask_maker`, `floor_ask_valid_from`, `floor_ask_valid_to`, `floor_ask_source`, `last_sale_value`, `last_sale_timestamp`, `created_at`, and `updated_at`.

The `id` column represents the internal token ID, while the `contract` column contains the contract address. The `token_id` column represents the ID of the token in the collection, and the `name` and `description` columns contain the name and description of the NFT, respectively. The `collection_id` column represents the associated collection ID, and the `owner` column contains the wallet address of the owner.

The `floor_ask_id`, `floor_ask_value`, `floor_ask_maker`, `floor_ask_valid_from`, `floor_ask_valid_to`, and `floor_ask_source` columns represent the floor ask details, such as the ID, value, maker wallet address, listing start and end times, and source (e.g. opensea.io). The `last_sale_value` and `last_sale_timestamp` columns represent the associated transaction timestamp.

Finally, the `created_at` and `updated_at` columns represent the timestamps when the token was created and updated, respectively.

This section also includes query examples that can be found at the specified URLs. These examples can be used to retrieve information from the `reservoir.tokens` table.

Overall, this section of the app technical guide provides a detailed overview of the `reservoir.tokens` table and its various columns, as well as query examples that can be used to retrieve information from the table.
## Questions: 
 1. What is the purpose of the `reservoir.tokens` table in the context of blockchain? 
- The `reservoir.tokens` table contains records with information about each NFT token, which can be useful for tracking ownership and transaction history.

2. Are there any limitations or restrictions on the types of queries that can be run on this table? 
- The app technical guide does not provide information on any limitations or restrictions on queries that can be run on this table. 

3. How frequently is the `reservoir.tokens` table updated with new token information? 
- The app technical guide does not provide information on the frequency of updates to the `reservoir.tokens` table.