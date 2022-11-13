# Call tables

### **Message** **calls and transactions made to smart contracts**

Smart contracts generally have functions that are able to be called by either an externally owned account(EOA) or other smart contracts. Functions can be anything from a simple state read and return to changing multiple states and invoking message calls to other smart contracts.

On Dune, we parse all message calls and transactions made to smart contracts in their own tables. The tables are then accordingly named `projectname."contractName_call_functionName"`.

This is either done on an individual contract level like for the uniswap v3 factory, or a class of contracts like the uniswap v3 pairs.

For example, when a uniswap v3 pool gets created via the [uniswap v3 factory](https://etherscan.io/address/0x1f98431c8ad98523631ae4a59f267346ea31f984#code) function `createPool`, Dune will record that transaction in the table [`uniswap_v3."Factory_call_createPool"`](https://dune.com/queries/735856). This will happen whether this was done by an externally owned account (EOA) through a transaction or a smart contract by the means of a message call.

**Multiple Instances**

For a contract where multiple instances exist, we will decode all calls to all instances of this smart contract into one table. If there is a transaction calling the `swap` function of any instance of a [Uniswap v3 pair](https://etherscan.io/address/0x8f8ef111b67c04eb1641f5ff19ee54cda062f163#writeContract) contract, we will collect this data in the table `uniswap_v3."Pair_call_swap"`.

**Common misconceptions**

One thing to keep in mind here is that [web3.js](https://web3js.readthedocs.io), [web3.py](https://web3py.readthedocs.io/en/stable) and all other methods of (locally) calling a `pure`, `read`, or `constant` function do not broadcast or publish anything on the blockchain and are therefore not recorded in Dune. 

However, if one of these functions is invoked by another smart contract in the context of a transaction, this will be broadcast on the chain and therefore accessible in Dune.

In short: **State data stored in the memory of a smart contract is not available on Dune!**

A good example of this is the function `decimals` of the [erc20 token contract](https://etherscan.io/token/0x1f9840a85d5af5bf1d1762f925bdaddc4201f984#readContract) `Uni` which is a `constant` state variable that is able to be accessed through an automatically created "[getter function](https://docs.soliditylang.org/en/v0.7.4/contracts.html#getter-functions)". Should a smart contract invoke this function in the context of transaction, this message call will be recorded in the Dune table [`uniswap."UNI_call_decimals"`](https://dune.com/queries/741354). 

This is in contrast to anyone calling this function locally using web3.py/web3.js or using the Etherscan frontend to access this state. These local calls are not recorded in Dune.

**Further Reading:**
****[What is the difference between a transaction and a call?](https://ethereum.stackexchange.com/questions/765/what-is-the-difference-between-a-transaction-and-a-call)

[Soliditylang.org documentation](https://docs.soliditylang.org/en/v0.8.13/contracts.html#function-visibility)
