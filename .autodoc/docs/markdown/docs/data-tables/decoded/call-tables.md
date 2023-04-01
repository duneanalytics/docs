[View code on GitHub](https://dune.com/docs/data-tables/decoded/call-tables.md)

# Call Tables

This technical guide explains how Dune parses all message calls and transactions made to smart contracts in their own tables. The guide provides information on how the tables are named and how they are created on an individual contract level or a class of contracts. 

The guide also explains how Dune records transactions in the table when a smart contract is called by an externally owned account (EOA) or another smart contract. The guide provides an example of how Dune records a transaction when a Uniswap v3 pool gets created via the Uniswap v3 factory function `createPool`. 

The guide also explains how Dune decodes all calls to all instances of a smart contract into one table when multiple instances of a contract exist. The guide provides an example of how Dune collects data in the table when there is a transaction calling the `swap` function of any instance of a Uniswap v3 pair contract. 

The guide also highlights a common misconception that web3.js, web3.py, and all other methods of locally calling a `pure`, `read`, or `constant` function do not broadcast or publish anything on the blockchain and are therefore not recorded in Dune. However, if one of these functions is invoked by another smart contract in the context of a transaction, this will be broadcast on the chain and therefore accessible in Dune. 

The guide concludes by providing further reading materials on the difference between a transaction and a call, Soliditylang.org documentation, and how Calldata is encoded. 

Overall, this technical guide provides a comprehensive understanding of how Dune parses all message calls and transactions made to smart contracts in their own tables. It is a useful resource for developers who want to understand how Dune records transactions and how to access the data recorded in Dune.
## Questions: 
 1. What specific blockchain networks does Dune Docs support for parsing message calls and transactions? 
- The app technical guide does not provide information on the specific blockchain networks supported by Dune Docs for parsing message calls and transactions.

2. Can Dune Docs record message calls made by smart contracts to external systems or APIs? 
- The app technical guide does not provide information on whether Dune Docs can record message calls made by smart contracts to external systems or APIs.

3. How does Dune Docs handle state data stored in the memory of a smart contract? 
- The app technical guide states that state data stored in the memory of a smart contract is not available on Dune, but it does not provide information on how Dune Docs handles this type of data.