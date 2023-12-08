---
title: Call Tables
description: On Dune, we parse all message calls and transactions made to smart contracts in their own tables.
---

**We parse all message calls and transactions made to smart contracts in their own tables.**

### Smart Contract Functionality

Smart contracts can have various functions which can be invoked by either an Externally Owned Account (EOA) or other smart contracts. These functions range from simple state read-and-return operations to complex tasks involving multiple state changes and sending message calls to other smart contracts.

### Data Tracking in Dune

In Dune, we meticulously track all message calls and transactions directed towards smart contracts and categorize them in designated tables. These tables follow the naming convention: `[projectname_blockchain].contractName_call_functionName`.

This tracking can occur at an individual contract level, such as for the Uniswap v3 factory, or encompass a class of contracts like the Uniswap v3 pairs.

**Example**: When a Uniswap v3 pool is created using the `createPool` function via the [Uniswap v3 factory](https://etherscan.io/address/0x1f98431c8ad98523631ae4a59f267346ea31f984#code) (on Ethereum), Dune logs this transaction in the table named `uniswap_v3_ethereum.Factory_call_createPool`.

![type:video](https://dune.com/embeds/3032985/5041726)

This tracking is implemented regardless of whether the action was initiated by an EOA via a transaction or a smart contract through a message call.

### Monitoring Multiple Instances
### Monitoring Multiple Instances

In cases where multiple instances of a contract are present, Dune consolidates all calls to these instances into a singular table. For instance, any transaction invoking the `swap` function on any instance of a [Uniswap v3 pair](https://etherscan.io/address/0x8f8ef111b67c04eb1641f5ff19ee54cda062f163#writeContract) contract will be aggregated in the `uniswap_v3_ethereum.Pair_call_swap` table.

![type:video](https://dune.com/embeds/3032979/5041712)
In cases where multiple instances of a contract are present, Dune consolidates all calls to these instances into a singular table. For instance, any transaction invoking the `swap` function on any instance of a [Uniswap v3 pair](https://etherscan.io/address/0x8f8ef111b67c04eb1641f5ff19ee54cda062f163#writeContract) contract will be aggregated in the `uniswap_v3_ethereum.Pair_call_swap` table.

![type:video](https://dune.com/embeds/3032979/5041712)

### Common Misconceptions
### Common Misconceptions

It's important to note that methods for locally calling `pure`, `read`, or `constant` functions, such as [web3.js](https://web3js.readthedocs.io) and [web3.py](https://web3py.readthedocs.io/en/stable), don't record or broadcast any information on the blockchain, hence they are not stored in Dune.
It's important to note that methods for locally calling `pure`, `read`, or `constant` functions, such as [web3.js](https://web3js.readthedocs.io) and [web3.py](https://web3py.readthedocs.io/en/stable), don't record or broadcast any information on the blockchain, hence they are not stored in Dune.

However, if a smart contract invokes one of these functions during a transaction, it gets broadcasted on the blockchain and is therefore retrievable in Dune. To put it succinctly, **data only stored or accessed in a smart contract's memory is not accessible on Dune**.

For instance, the `decimals` function of the [ERC20 token contract](https://etherscan.io/token/0x1f9840a85d5af5bf1d1762f925bdaddc4201f984#readContract) `Uni` is a `constant` state variable accessible via an auto-generated "[getter function](https://docs.soliditylang.org/en/v0.7.4/contracts.html#getter-functions)". If a smart contract calls this function within a transaction context, the message call will be documented in the Dune table [`uniswap."UNI_call_decimals"`](https://dune.com/queries/741354). In contrast, local calls made using web3.py/web3.js or through the Etherscan interface to access this state won't be logged in Dune.

However, if a smart contract invokes one of these functions during a transaction, it gets broadcasted on the blockchain and is therefore retrievable in Dune. To put it succinctly, **data only stored or accessed in a smart contract's memory is not accessible on Dune**.

For instance, the `decimals` function of the [ERC20 token contract](https://etherscan.io/token/0x1f9840a85d5af5bf1d1762f925bdaddc4201f984#readContract) `Uni` is a `constant` state variable accessible via an auto-generated "[getter function](https://docs.soliditylang.org/en/v0.7.4/contracts.html#getter-functions)". If a smart contract calls this function within a transaction context, the message call will be documented in the Dune table [`uniswap."UNI_call_decimals"`](https://dune.com/queries/741354). In contrast, local calls made using web3.py/web3.js or through the Etherscan interface to access this state won't be logged in Dune.


## Further Reading

<div class="cards grid" markdown>
- [What is the difference between a transaction and a call?](https://ethereum.stackexchange.com/questions/765/what-is-the-difference-between-a-transaction-and-a-call)
- [Soliditylang.org documentation](https://docs.soliditylang.org/en/v0.8.13/contracts.html#function-visibility)
- [How Calldata is Encoded](https://degatchi.com/articles/reading-raw-evm-calldata)
</div>