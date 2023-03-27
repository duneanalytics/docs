[View code on GitHub](https://dune.com/blob/master/data tables\community\reservoir\tokens.md)

# Tokens

This section of the app technical guide covers the `reservoir.tokens` table, which contains records with information about each NFT token. The table includes columns such as `id`, `contract`, `token_id`, `name`, `description`, `collection_id`, `owner`, `floor_ask_id`, `floor_ask_value`, `floor_ask_maker`, `floor_ask_valid_from`, `floor_ask_valid_to`, `floor_ask_source`, `last_sale_value`, `last_sale_timestamp`, `created_at`, and `updated_at`. 

The `id` column represents the internal token id, while the `contract` column contains the contract address. The `token_id` column represents the id of the token in the collection, and the `name` and `description` columns contain the name and description of the NFT. The `collection_id` column represents the associated collection id, and the `owner` column contains the wallet address of the owner. 

The `floor_ask_id`, `floor_ask_value`, `floor_ask_maker`, `floor_ask_valid_from`, `floor_ask_valid_to`, and `floor_ask_source` columns represent information about the floor ask, such as the id, value, maker wallet address, listing start and end times, and source. The `last_sale_value` and `last_sale_timestamp` columns represent the associated transaction timestamp. Finally, the `created_at` and `updated_at` columns contain timestamps for when the token was created and updated, respectively.

The guide also provides query examples for the `reservoir.tokens` table, which can be found at the links provided. These examples can be used to retrieve specific information from the table, such as the floor ask value for a particular token.

Overall, this section of the app technical guide provides a detailed overview of the `reservoir.tokens` table and its columns, as well as query examples for retrieving information from the table.
## Questions: 
 1. What is the purpose of the dune docs app and how does it relate to blockchain technology?
- The app technical guide does not provide information on the purpose of the dune docs app or its relation to blockchain technology.

2. Can the reservoir.tokens table be used to track the ownership and transaction history of NFTs on a blockchain?
- Yes, the reservoir.tokens table contains information about each NFT token, including the owner wallet address and associated transaction timestamps.

3. Are there any limitations or restrictions on the types of NFTs that can be tracked using the reservoir.tokens table?
- The app technical guide does not provide information on any limitations or restrictions on the types of NFTs that can be tracked using the reservoir.tokens table.