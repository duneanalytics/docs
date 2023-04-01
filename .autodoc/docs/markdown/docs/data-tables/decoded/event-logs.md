[View code on GitHub](https://dune.com/docs/data-tables/decoded/event-logs.md)

# Event Logs

This technical guide covers the concept of event logs in smart contracts. Smart contracts emit event logs when certain predefined actions are completed. The structure published in these logs is predefined by the developer of the smart contract, and the content is dynamically created during the transaction. 

The guide explains that logs are useful for monitoring, alerting, and keeping track of what happens inside a smart contract. Logs are also useful for data analysis since they reliably present data that is intended to be analyzed post factum. The guide provides an example of how to search for the keyword `emit` in the source code of a smart contract to see which logs can be emitted by a smart contract.

The guide also explains how event logs for smart contracts are decoded into tables named accordingly to a specific schema. The schema is different for the V2 Engine (Spark SQL) and V1 Engine (PosgreSQL). The guide provides examples of how to name tables for each engine.

The guide provides an example of how to look at the event logs of a transaction in Etherscan. The example is in the context of the uniswap v3 factory, and the event that gets emitted upon the creation of a new pool. The event is called `PoolCreated`, and it gives information like the tokens in the pool, the fee tier of this pool, and the tick spacing. The guide provides examples of how to name tables for each engine.

The guide explains that if there are multiple instances of a contract, all event logs across all instances of this smart contract are collected in one table. The guide provides an example of how all uniswap v3 pool `swap` events (on ethereum) are stored in a table.

Finally, the guide provides further reading resources on understanding event logs on the Ethereum blockchain and everything you ever wanted to know about events and logs on Ethereum. 

Overall, this guide provides a comprehensive explanation of event logs in smart contracts and how they are decoded into tables. It also provides examples of how to name tables for each engine and how to look at event logs of a transaction in Etherscan.
## Questions: 
 1. What is the purpose of the Dune Docs app and how does it relate to blockchain SQL analysis?
   
   The Dune Docs app provides technical documentation for decoding event logs emitted by smart contracts on the blockchain. This information is useful for blockchain SQL analysts who want to monitor, alert, and keep track of what happens inside a smart contract.

2. How are event logs stored in Dune Docs and what is the naming convention for the tables?

   Event logs for smart contracts are decoded into tables named according to the schema `[projectname_blockchain].[contractName]_evt_[eventName]` for the V2 Engine (Spark SQL) and `[projectname]."[contractName]_evt_[eventName]"` for the V1 Engine (PosgreSQL). For example, the event log for the Uniswap V3 pool creation event is stored in the table `uniswap_v3_ethereum.Factory_evt_PoolCreated` for the V2 Engine and `uniswap_v3."Factory_evt_PoolCreated"` for the V1 Engine.

3. How are event logs from multiple instances of a contract handled in Dune Docs?

   Event logs from multiple instances of a contract are collected in one table. For example, all Uniswap V3 pool swap events on Ethereum are stored in the table `uniswap_v3_ethereum.Pair_evt_Swap` for the V2 Engine and `uniswap_v3."Pair_evt_Swap"` for the V1 Engine. The `contract_address` column indicates which smart contract emitted the event.