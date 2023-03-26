[View code on GitHub](https://dune.com/blob/master/data tables\raw\bitcoin\outputs.md)

The app technical guide provides documentation for the `dune docs` project, specifically focusing on the `Outputs` feature of the app. The guide contains a table with detailed information on the `bitcoin.outputs` data table, which includes column names, data types, and descriptions of each column. 

The `block_time` column provides the timestamp of the block, while the `block_date` column provides the date of the block. The `block_height` column provides the block number, and the `block_hash` column provides the hash of the block. The `tx_id` column provides the hash of the transaction that the output is from, and the `index` column provides the 0-indexed number of the output within the transaction. 

The `value` column provides the number of Satoshis attached to the output, while the `script_asm` column provides a symbolic representation of the bitcoin's script language op-codes. The `script_hex` column provides a hexadecimal representation of the bitcoin's script language op-codes. The `address` column provides the address that owns the output, and the `type` column provides the address type of the output. 

This guide is useful for developers who are working on the `Outputs` feature of the `dune docs` app. It provides a clear understanding of the data table and its columns, which can be used to build queries and analyze data. For example, a developer could use this guide to understand how to retrieve the block time and date of a specific output, or how to identify the address type of an output. 

Overall, the app technical guide provides a comprehensive overview of the `Outputs` feature of the `dune docs` app, making it easier for developers to work with the data and build new features.
## Questions: 
 1. What data source does this app technical guide pull from to generate the `bitcoin.outputs` table?
- This information is not provided in the app technical guide and would require further investigation or documentation.

2. Can this app technical guide be used to analyze outputs from other cryptocurrencies besides Bitcoin?
- No, this app technical guide is specifically for analyzing Bitcoin outputs and does not provide information on other cryptocurrencies.

3. Is there any information provided in this app technical guide about the inputs that correspond to each output in the `bitcoin.outputs` table?
- No, this app technical guide only provides information on the outputs themselves and does not include any information on the corresponding inputs.