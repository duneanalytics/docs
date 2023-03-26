[View code on GitHub](https://dune.com/blob/master/data tables\community\reservoir\asks.md)

# Reservoir.asks Table

The `reservoir.asks` table is a part of the Dune Docs project and contains records with information about each listing. The table has various columns such as `id`, `kind`, `status`, `contract`, `token_id`, `maker`, `taker`, `price`, `start_price`, `end_price`, `currency_address`, `currency_symbol`, `currency_price`, `dynamic`, `quantity`, `quantity_filled`, `quantity_remaining`, `valid_from`, `valid_until`, `nonce`, `source`, `fee_bps`, `expiration`, `raw_data`, `created_at`, and `updated_at`. Each column has a specific data type and description.

The purpose of this table is to provide information about each listing, including the listing's status, price, quantity, and other relevant details. The table can be queried using various query examples, which are provided in the documentation. 

For example, to query all active listings, one can use the following SQL query:

```
SELECT * FROM reservoir.asks WHERE status = 'active';
```

This will return all records from the `reservoir.asks` table where the `status` column is set to 'active'.

Overall, the `reservoir.asks` table is an essential part of the Dune Docs project, providing valuable information about each listing. The documentation provides a detailed description of each column in the table, along with query examples to help users retrieve the data they need.
## Questions: 
 1. What is the purpose of the `reservoir.asks` table in the Dune Docs app?
- The `reservoir.asks` table contains records with information about each listing in the app.

2. What type of data is stored in the `price` column of the `reservoir.asks` table?
- The `price` column in the `reservoir.asks` table stores the current price in native currency.

3. Is there any information in the `reservoir.asks` table about the buyer of a listing?
- No, there is no information in the `reservoir.asks` table about the buyer of a listing. The table only contains information about the maker and taker wallet addresses.