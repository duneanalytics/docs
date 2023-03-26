[View code on GitHub](https://dune.com/blob/master/data tables\decoded\index.md)

The Decoded Tables guide covers the process of decoding smart contract activity into human-readable tables using the ABI (Application Binary Interface) for smart contracts and the interface standard for standardized token smart contracts (ERC20, ERC721, etc.). The guide explains how Dune creates tables for each event and function defined in the smart contract's ABI, and how every event, message call, or transaction made to that contract is decoded and inserted as a row into these tables.

The guide provides examples of table naming conventions for both V2 Engine (Spark SQL) and V1 Engine (PosgreSQL). It also explains how to identify specific smart contracts using the `contract_address` column and how to check if contracts are already decoded by querying the `[blockchain].contracts` tables.

The guide includes a section on understanding decoded data, which emphasizes the importance of analyzing events and transactions, and provides tips on how to make sense of the data. It also discusses which tables to use, suggesting that events are generally the easiest and most accessible way to analyze blockchain data, but in some cases, it might be necessary to use transaction and message calls (found in call tables).

Finally, the guide provides example queries to explore decoded contracts, such as seeing all projects with decoded data, and checking for multiple instances of a contract.
## Questions: 
 1. **How can I check if a specific contract has already been decoded in the Dune database?**

   You can check if a contract has been decoded by querying the `[blockchain].contracts` tables through the Dune database or by using the provided dashboard links for the V2 Engine (Spark SQL) and V1 Engine (PosgreSQL) in the app technical guide.

2. **How long does it take to initially decode a smart contract once it has been submitted?**

   It usually takes about 24 hours to initially decode a smart contract. You can check the status of your contract's decoding process using the "Is my Contract decoded yet?" dashboard link provided in the app technical guide.

3. **What is the difference between event tables and call tables in the decoded data?**

   Event tables contain data related to events emitted by smart contracts, while call tables contain data related to transactions and message calls made between smart contracts. In most cases, analyzing events is easier and more accessible, but in some cases, you might need to use call tables for additional information or when events are not emitted.