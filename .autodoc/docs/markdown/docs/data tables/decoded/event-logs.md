[View code on GitHub](https://dune.com/blob/master/data tables\decoded\event-logs.md)

The Event Logs technical guide explains how smart contracts emit event logs when certain predefined actions are completed. The structure of these logs is predefined by the smart contract developer, and the content is dynamically created during the transaction. The guide highlights the usefulness of logs for monitoring, alerting, and keeping track of what happens inside a smart contract. Logs are also useful for data analysis since they present data that can be analyzed post factum. 

The guide provides a schema for decoding all event logs for smart contracts into tables named accordingly. The schema is different for the V2 Engine (Spark SQL) and V1 Engine (PosgreSQL). The guide uses the Uniswap V3 factory as an example and explains how to look at the event logs of a transaction in Etherscan. The guide also provides the table name where the event will be stored in Dune. 

The guide explains that if there are multiple instances of a contract, all event logs across all instances of the smart contract will be collected in one table. The guide provides an example of how all Uniswap V3 pool swap events on Ethereum are stored in a table. The column `contract_address` indicates which smart contract emitted the event. 

The guide concludes by providing further reading resources on understanding event logs on the Ethereum blockchain. Overall, the guide provides a detailed explanation of event logs and how they are used in the Dune Docs project.
## Questions: 
 1. What is the format of the tables that will be created for decoding event logs in Dune Docs?
   
   The tables for decoding event logs in Dune Docs will be named according to the schema `[projectname_blockchain].[contractName]_evt_[eventName]` for V2 Engine (Spark SQL) and `[projectname]."[contractName]_evt_[eventName]"` for V1 Engine (PosgreSQL).

2. How can a blockchain SQL analyst access the event logs of a transaction in Etherscan?
   
   A blockchain SQL analyst can access the event logs of a transaction in Etherscan by opening the logs tab of the transaction.

3. How are event logs stored in Dune Docs when there are multiple instances of a contract?
   
   When there are multiple instances of a contract, all event logs across all instances of the smart contract are collected in one table, with the `contract_address` column indicating which smart contract emitted the event.