[View code on GitHub](https://dune.com/blob/master/data tables\raw\transactions.md)

# Transactions

This section of the app technical guide covers transactions in the Ethereum network. Transactions are cryptographically signed instructions from accounts that initiate a transaction to update the state of the Ethereum network. Transactions always originate from externally owned accounts, and a smart contract cannot initiate a transaction. Transactions need to be broadcast to the whole network, and any node can broadcast a request for a transaction to be executed on the EVM. After this happens, a miner will execute the transaction and propagate the resulting state change to the rest of the network. 

The section also provides a link to the official Ethereum documentation for more information on transactions.

## Tables

This section provides a table that lists the different chains and tables that contain transaction data. The tables are divided into two engines: V2 Engine (Spark SQL) and V1 Engine (PosgreSQL). The table lists the chains, tables, and notes for each table. For example, the Ethereum Mainnet chain has a table named `ethereum.transactions`, and the Gnosis Chain has a table named `gnosis.transactions`.

## Column Data

This section provides a table that lists the different columns and their data types for the transaction data. The table also provides a description of each column. For example, the `block_time` column is of type `_timestamptz_` and represents the time when the block was mined that includes this transaction. The `value` column is of type `_numeric_` and represents the amount of `[chain_gas_token]` sent in this transaction in `wei`. Note that ERC20 tokens do not show up here. 

The section also provides an example of the column data in the form of an embedded video. 

Overall, this section of the app technical guide provides a comprehensive overview of transactions in the Ethereum network, including tables and column data.
## Questions: 
 1. What is the purpose of the Transactions table in this app and what data does it contain?
   
   The Transactions table contains information about transactions on various blockchain networks, including Ethereum Mainnet, Gnosis Chain, Polygon, Optimism, BNB Chain, Arbitrum, and Avalanche C-Chain. It includes data such as the block time, block number, value, gas limit, gas price, gas used, max fee per gas, max priority fee per gas, priority fee per gas, nonce, index, success, from address, to address, block hash, data, hash, type, access list, effective gas price, gas used for L1, L1 gas used, L1 gas price, L1 fee, L1 fee scalar, L1 block number, L1 timestamp, and L1 tx origin.
   
2. Does this app support EIP1559 and how is it reflected in the Transactions table?
   
   The app supports EIP1559 on some networks, but not on others. The Transactions table includes columns for max fee per gas, max priority fee per gas, and priority fee per gas, which are introduced by EIP1559. However, for networks where EIP1559 is not supported, these columns do not contain data and the type column is always set to Legacy.
   
3. How is gas measured in this app and is it consistent across all networks?
   
   Gas is measured in wei for most networks, but for Arbitrum it is measured in ArbGas and for Avalanche C-Chain it is measured in nanoavax. Therefore, gas measurement is not consistent across all networks in this app.