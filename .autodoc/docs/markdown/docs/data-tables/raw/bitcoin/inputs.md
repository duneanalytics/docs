[View code on GitHub](https://dune.com/docs/data-tables/raw/bitcoin/inputs.md)

# Inputs

The `Inputs` section of the app technical guide covers the `bitcoin.inputs` feature of the project. This feature provides a table with detailed information about the inputs of a Bitcoin transaction. The table includes columns such as `block_time`, `block_date`, `block_height`, `index`, `tx_id`, `spent_block_height`, `spent_tx_id`, `spent_output_number`, `value`, `address`, `type`, `coinbase`, `is_coinbase`, `script_asm`, `script_hex`, `script_desc`, `script_signature_asm`, `script_signature_hex`, `sequence`, and `witness_data`.

Each column is described in detail, including its data type and a brief explanation of its purpose. For example, the `block_time` column contains a timestamp of when the block was mined, while the `value` column contains the number of Satoshis attached to the input. The `address` column contains the address that owned or owns the output used as input, and the `type` column contains the address type of the input.

The `Inputs` section is useful for developers who need to access detailed information about Bitcoin transactions. For example, a developer building a Bitcoin wallet app might use this feature to display transaction details to the user. 

Example usage:
```python
import dune_docs

inputs_table = dune_docs.bitcoin.inputs
print(inputs_table.head())
```
This code imports the `dune_docs` module and accesses the `bitcoin.inputs` feature. It then prints the first few rows of the table using the `head()` method.
## Questions: 
 1. What is the purpose of this app and how does it relate to blockchain technology?
- The app is not explicitly stated in the provided technical guide, so a blockchain SQL analyst might need more information on the context and use case of the app to understand its relevance to blockchain technology.

2. How is the data in the `bitcoin.inputs` table sourced and updated?
- The technical guide does not provide information on the data source or update frequency of the `bitcoin.inputs` table, which could be important for a blockchain SQL analyst to understand the reliability and timeliness of the data.

3. Are there any limitations or known issues with the app's handling of bitcoin input data?
- The technical guide does not mention any potential issues or limitations with the app's handling of bitcoin input data, but a blockchain SQL analyst might want to know if there are any known bugs or edge cases that could affect the accuracy or completeness of the data.