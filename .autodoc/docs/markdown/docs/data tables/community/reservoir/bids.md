[View code on GitHub](https://dune.com/blob/master/data tables\community\reservoir\bids.md)

# Dune Docs App Technical Guide: Bids

## Reservoir.bids

This section of the guide covers the `reservoir.bids` table, which contains records with information about each bid. The table includes columns such as `id`, `kind`, `status`, `contract`, `maker`, `taker`, `price`, `value`, `currency_address`, `currency_symbol`, `currency_price`, `quantity`, `quantity_filled`, `quantity_remaining`, `valid_from`, `valid_until`, `nonce`, `source`, `fee_bps`, `expiration`, `raw_data`, `created_at`, and `updated_at`. 

The purpose of this section is to provide a detailed description of each column in the `reservoir.bids` table, including the column name, type, and description. For example, the `id` column is a string that represents the internal order id, while the `kind` column is a string that represents the protocol name (e.g. seaport). 

Additionally, this section provides a link to query examples for the `reservoir.bids` table, which can be found at [TBD](TBD). 

Overall, this section of the guide is useful for developers who are working with the `reservoir.bids` table and need to understand the purpose and structure of each column. 

Example: If a developer needs to retrieve the `maker` and `price` columns from the `reservoir.bids` table, they can use the following SQL query: 

```
SELECT maker, price
FROM reservoir.bids;
```
## Questions: 
 1. What is the purpose of the dune docs app and how does it relate to blockchain technology?
- The app technical guide only provides information about a specific table called "reservoir.bids" and does not give an overview of the entire app. Therefore, a blockchain SQL analyst might have questions about the overall purpose of the app and how it utilizes blockchain technology.

2. How is the data in the "reservoir.bids" table being collected and stored?
- The app technical guide does not provide information on how the data is being collected and stored, which might be important for a blockchain SQL analyst to understand in order to properly analyze the data.

3. Are there any security measures in place to protect the data in the "reservoir.bids" table?
- The app technical guide does not mention any security measures, such as encryption or access controls, which might be a concern for a blockchain SQL analyst working with sensitive data.