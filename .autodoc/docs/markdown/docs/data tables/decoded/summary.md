[View code on GitHub](https://dune.com/tree/master/doc\docs\json\docs\data tables\decoded)

The Decoded Data Tables folder in the Dune Docs project focuses on providing technical guides for understanding and working with decoded smart contract activity in human-readable tables. These guides are essential for developers and analysts who want to analyze and monitor smart contract transactions and events on the Ethereum blockchain using Dune.

The folder contains three main guides:

1. **Call Tables**: This guide explains how Dune parses all message calls and transactions made to smart contracts into tables named according to the project name, contract name, and function name. It provides examples of how Dune records transactions, such as when a Uniswap v3 pool gets created via the Uniswap v3 factory function `createPool`. The guide clarifies common misconceptions and highlights that only transactions broadcasted on the blockchain are recorded in Dune. This guide is useful for developers who want to understand how Dune works and how to use it to analyze smart contract transactions.

2. **Event Logs**: This guide focuses on how smart contracts emit event logs when certain predefined actions are completed. It explains the schema for decoding all event logs for smart contracts into tables and provides examples using the Uniswap V3 factory. The guide also covers how event logs across multiple instances of a smart contract are collected in one table. This guide is essential for developers and analysts who want to monitor, alert, and keep track of what happens inside a smart contract, as well as analyze the data post factum.

3. **Decoded Tables**: This guide covers the process of decoding smart contract activity into human-readable tables using the ABI and the interface standard for standardized token smart contracts. It explains how Dune creates tables for each event and function defined in the smart contract's ABI and provides examples of table naming conventions. The guide also includes a section on understanding decoded data and provides example queries to explore decoded contracts. This guide is crucial for analysts who want to make sense of the data and decide which tables to use for their analysis.

Overall, the Decoded Data Tables folder in the Dune Docs project provides comprehensive guides for understanding and working with decoded smart contract activity in human-readable tables. These guides are essential for developers and analysts who want to analyze and monitor smart contract transactions and events on the Ethereum blockchain using Dune.
