[View code on GitHub](https://dune.com/docs/reference/faq/how-does-dune-get-its-data.md)

# App Technical Guide: How does Dune get data?

This guide provides an overview of how Dune, the project being documented, obtains its data. The guide explains that Dune works with node providers across the industry to ingest raw historical data from various blockchains. However, it does not include state data. 

The guide also mentions that Dune does not discriminate against any smart contract and users can submit any contract via the decoding page. The decoding page is located in the data-tables folder under the decoded subfolder. The only prerequisite for submitting a contract is an ABI, which is used to decode the contract. In most cases, the ABI is already available on Etherscan, but there may be edge cases where it is not available. 

Overall, this guide provides a high-level understanding of how Dune obtains its data and how users can submit their own contracts for decoding. It is useful for anyone who wants to understand the data sources used by Dune and how to work with smart contracts on the platform. 

Example: 

Suppose a user wants to work with a smart contract on the Dune platform. They can submit the contract via the decoding page, which is located in the data-tables folder under the decoded subfolder. The user needs to provide the ABI for the contract, which is used to decode it. Once the contract is decoded, the user can work with it on the Dune platform in a matter of hours.
## Questions: 
 1. What blockchains does Dune Docs currently support for data ingestion?
- The app technical guide mentions that Dune Docs is working with node providers across the industry to ingest data from blockchains, but does not specify which blockchains are currently supported.

2. Does Dune Docs include state data in its database?
- The app technical guide states that Dune Docs ingests all raw historical data from blockchains, but explicitly mentions that it does not include state data. A blockchain SQL analyst may want to know if this limitation affects their ability to analyze data on the platform.

3. How does Dune Docs handle smart contracts without an ABI?
- The app technical guide mentions that an ABI is required to decode a smart contract, but does not provide information on how Dune Docs handles contracts without an ABI. A blockchain SQL analyst may want to know if there are any workarounds or limitations to working with contracts that do not have an ABI available.