[View code on GitHub](https://dune.com/blob/master/data tables\raw\bitcoin\inputs.md)

The Inputs section of the app technical guide for the Dune Docs project provides a detailed description of the `bitcoin.inputs` table. This table contains information related to the inputs of Bitcoin transactions, including block time, block date, block height, index, transaction ID, spent block height, spent transaction ID, spent output number, value, address, type, coinbase, script ASM, script HEX, script description, script signature ASM, script signature HEX, sequence, and witness data. 

The guide provides a table that lists each column name, data type, and a brief description of what the column represents. For example, the `block_time` column represents the time at which the block containing the input was mined, while the `value` column represents the number of Satoshis attached to the input. 

The guide also provides additional information about certain columns, such as the `sequence` column, which is intended to allow unconfirmed time-locked transactions to be updated before being finalized. The guide notes that this column is not currently used except to disable locktime in a transaction. 

Overall, this section of the app technical guide provides developers with a comprehensive understanding of the `bitcoin.inputs` table and the information it contains. By providing detailed descriptions of each column, developers can more easily work with this data and integrate it into their applications.
## Questions: 
 1. What is the purpose of this app and how does it relate to blockchain technology?
- The app is not clearly described in this technical guide, so a blockchain SQL analyst might want to know more about its intended use and how it interacts with blockchain data.

2. Are there any limitations or known issues with the data being collected in the `bitcoin.inputs` table?
- The technical guide does not provide information on data quality or potential issues with the input data, so an analyst might want to investigate this further before using the data for analysis.

3. Is there any additional documentation or support available for using this app and its associated data tables?
- The technical guide only provides information on the `bitcoin.inputs` table, so an analyst might want to know if there are other tables or resources available for understanding the app and its data.