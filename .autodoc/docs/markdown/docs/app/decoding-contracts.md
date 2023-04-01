[View code on GitHub](https://dune.com/docs/app/decoding-contracts.md)

# Decoding Contracts

This technical guide provides a comprehensive overview of Decoded Contracts in Dune, including how to submit them for decoding. Decoded Contracts are human-readable tables for each event and function defined in the smart contract's ABI. The guide explains how to submit a new contract for decoding, track submissions, and provides answers to frequently asked questions.

The guide starts by explaining how Decoding works and what Decoded tables are available. It then goes on to explain how to submit a new contract for decoding. Contracts can be submitted through the New contract form, the My Creations > Contracts Tab, or within the dataset explorer in the Query editor's sidebar. The contract submission form consists of two steps: Blockchain and address, and Contract details. The guide provides examples of how to submit a contract, including an example of submitting the USDT contract in Optimism.

The guide also explains advanced options for submitting contracts, such as indexing multiple contract addresses under the same submission. It provides two strategies for detecting other contracts for decoding: bytecode match and factory instances. The guide warns that these options should only be used if the user is extremely familiar with the project's architecture and deployment hierarchy.

The guide also explains how to track submissions and their processing status. Users can view their submissions at any time by navigating to My Creations > Contracts. The guide also provides answers to frequently asked questions, such as how to submit contract information manually, how to submit a Proxy contract, how to re-submit a contract, and how to submit Diamond Proxy contracts.

Overall, this guide provides a detailed explanation of how to submit contracts for decoding in Dune, including advanced options and frequently asked questions. It is a valuable resource for anyone looking to submit contracts for decoding in Dune.
## Questions: 
 1. What is the purpose of submitting contracts for decoding in Dune Docs?
- Contracts are decoded into human-readable tables for each event and function defined in the smart contract's ABI, making it easier to work with raw transaction, log, and trace data.

2. How can Dune Docs automatically detect and index multiple contract addresses under the same submission?
- Dune Docs has two strategies for detecting other contracts for decoding: bytecode match and factory instances.

3. What should be done if a submission gets rejected in Dune Docs?
- To avoid rejection, accurate contract information should be submitted. If a submission gets rejected, users can head over to the #decoding Discord channel for assistance.