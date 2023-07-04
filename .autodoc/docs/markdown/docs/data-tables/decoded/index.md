[View code on GitHub](https://dune.com/docs/data-tables/decoded/index.md)

The Decoded Tables guide covers the process of decoding smart contract activity into human-readable tables on the Dune platform. It explains how Dune uses the ABI (Application Binary Interface) for smart contracts and the interface standard for standardized token smart contracts (ERC20, ERC721, etc.) to create tables for each event and function defined in the smart contract's ABI. 

The guide provides examples of how to access decoded data for specific events and function calls using the V2 Engine (Spark SQL) and V1 Engine (PostgreSQL). It also explains how to check if contracts are already decoded by querying the `[blockchain].contracts` tables or using a dashboard.

The guide further explains how decoding works, using the ABI to call a smart contract or interpret the data it emits. It provides an example of decoding an ERC20 transfer event log and how to understand decoded data.

The guide also discusses which tables to use (events or calls) and provides queries to explore decoded contracts, such as seeing all projects with decoded data or checking for multiple instances of a contract.
## Questions: 
 1. **How can I check if a specific contract has already been decoded in the Dune database?**

You can check if a contract has been decoded by querying the `[blockchain].contracts` tables through the database or by using the provided dashboard links for V2 Engine (Spark SQL) and V1 Engine (PostgreSQL) in the app technical guide.

2. **How long does it take to decode a smart contract once it has been submitted?**

It usually takes about 24 hours to initially decode a smart contract. You can check the status of your contract's decoding process using the "Is my Contract decoded yet?" dashboard link provided in the app technical guide.

3. **How can I submit multiple contracts for decoding at the same time?**

To submit a batch of contracts for decoding, use the provided CSV template in the app technical guide and fill it in with the appropriate information for the contracts you want to decode. Then, send the completed CSV file to decoding@dune.com.
