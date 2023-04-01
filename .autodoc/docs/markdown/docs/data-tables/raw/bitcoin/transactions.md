[View code on GitHub](https://dune.com/docs/data-tables/raw/bitcoin/transactions.md)

# Transactions

The Transactions section of the Dune Docs project provides a detailed guide on the `bitcoin.transactions` feature. The guide contains a table with column names, types, and descriptions of the data that can be accessed through this feature. The table includes information such as the block time, block date, block height, block hash, index, ID, input value, output value, fee, input count, output count, size, virtual size, whether the transaction is a coinbase transaction, and the transaction encoded as hexadecimal.

The guide also provides definitions for the `input`, `input.script_signature`, `input.script_pub_key`, `output`, and `output.script_pub_key` fields. These fields are of type `STRUCT` and allow for representing nested hierarchical data with key-value pairs. The `input` field contains information about transaction inputs, such as the number of Satoshis attached to the output, the height of the output, the transaction ID of the output, the number of the output in the transaction's outputs, and the script signature and public key. The `output` field contains information about transaction outputs, such as the number of Satoshis attached to the output, the public key, and the index of the output within a transaction.

The guide notes that the `input` field is an `array(row(map))` type, and provides examples of how to work with the columns using syntax such as `input[1].witness_data[2]` or `input[3].script_pub_key.address`, depending on the lengths of arrays within each value.

Overall, the Transactions section of the Dune Docs project provides a comprehensive guide to the `bitcoin.transactions` feature, including detailed information on the data that can be accessed and how to work with the nested hierarchical data types.
## Questions: 
 1. What data source does this app technical guide pull from to populate the `bitcoin.transactions` table?
- The app technical guide does not provide information on the data source used to populate the `bitcoin.transactions` table.

2. Can this app technical guide be used to query transactions from other cryptocurrencies besides Bitcoin?
- The app technical guide does not provide information on whether it can be used to query transactions from other cryptocurrencies besides Bitcoin.

3. How can the `input` and `output` fields be used to track the flow of funds in a Bitcoin transaction?
- The `input` and `output` fields can be used to track the flow of funds in a Bitcoin transaction by providing information on the value, height, transaction ID, output number, coinbase data, sequence number, witness data, script signature, and script public key for each input and output.