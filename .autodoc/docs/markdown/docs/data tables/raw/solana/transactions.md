[View code on GitHub](https://dune.com/blob/master/data tables\raw\solana\transactions.md)

# Transactions

The Transactions section of the Dune Docs project focuses on the Solana.transactions table, which contains transaction data within Solana's blockchain. This table provides relevant data related to account, protocol, and program activity. The guide provides a detailed description of each column in the table, including the column name, column type, and description. 

The guide also includes query examples that demonstrate how to use the Solana.transactions table to extract data. For example, the guide provides a query that shows the number of Solana instructions by day for DEXes. 

The guide also includes several struct definitions that allow for representing nested hierarchical data and have key-value pairs. These structs can be used to group fields together to make them more accessible. The guide provides a detailed description of each struct, including the field name, data type, and description. 

The token_balance struct, for example, includes the account key of the account that the token balance is provided for, the public key of the token's mint, and the derived amount from the token balance's raw amount and the number of decimals. 

The instructions struct includes an ordered list of accounts to pass to the program, program input data in a base-58 string, and the account key of the program that executed this instruction. 

The inner_instructions struct includes an ordered list of accounts to pass to the program, program input data in a base-58 string, and the account key of the program that executed this instruction. 

Finally, the error struct includes the instruction number that failed and the error message. 

Overall, the Transactions section of the Dune Docs project provides a comprehensive guide to the Solana.transactions table and the structs used to represent nested hierarchical data. The guide includes detailed descriptions of each column and struct, as well as query examples that demonstrate how to use the data in the table.
## Questions: 
 1. What data is available in the Solana.transactions table?
- The Solana.transactions table contains transaction data within Solana's blockchain, including relevant data related to account, protocol, and program activity.

2. What is the purpose of the STRUCT data type in this app?
- The STRUCT data type allows for representing nested hierarchical data and has key-value pairs, similar to a dictionary in Python. It can be used to group fields together to make them more accessible.

3. Are there any examples of how to extract data from the token_balance field?
- Yes, there is an example query provided in the app technical guide that shows how to extract the number of Solana instructions by day for DEXes using the token_balance field.