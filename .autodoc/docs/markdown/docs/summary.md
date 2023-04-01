[View code on GitHub](https://dune.com/docs)

The `decoding-contracts.md` guide in the `docs/data-tables/decoded` folder focuses on decoding smart contract activity into human-readable tables on the Dune platform. This guide is essential for analysts and developers who want to understand and access the decoded data of smart contracts, events, and function calls on the Dune platform.

The guide covers the following topics:

1. **Call Tables**: This section explains how Dune parses all message calls and transactions made to smart contracts in their own tables. It provides information on how the tables are named and how they are created on an individual contract level or a class of contracts. It also highlights a common misconception about `pure`, `read`, or `constant` functions not being recorded in Dune.

2. **Event Logs**: This section covers the concept of event logs in smart contracts and how they are decoded into tables named according to a specific schema. It provides examples of how to name tables for the V2 Engine (Spark SQL) and V1 Engine (PostgreSQL) and how to look at event logs of a transaction in Etherscan.

3. **Decoding Process**: This section explains how Dune uses the ABI (Application Binary Interface) for smart contracts and the interface standard for standardized token smart contracts (ERC20, ERC721, etc.) to create tables for each event and function defined in the smart contract's ABI. It provides an example of decoding an ERC20 transfer event log and how to understand decoded data.

4. **Accessing Decoded Data**: This section provides examples of how to access decoded data for specific events and function calls using the V2 Engine (Spark SQL) and V1 Engine (PostgreSQL). It also explains how to check if contracts are already decoded by querying the `[blockchain].contracts` tables or using a dashboard.

5. **Which Tables to Use**: This section discusses which tables to use (events or calls) and provides queries to explore decoded contracts, such as seeing all projects with decoded data or checking for multiple instances of a contract.

This guide is useful for analysts who want to access and analyze decoded data from smart contracts, events, and function calls on the Dune platform. For example, an analyst might use this guide to understand how to access decoded data for a specific ERC20 token transfer event or how to explore all projects with decoded data on the platform. By understanding the decoding process and how to access the decoded data, analysts can gain valuable insights into smart contract activity and interactions on the Dune platform.
