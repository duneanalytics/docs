# 调用表

### **对智能合约的调用以及发起的交易**

智能合约通常具有可由外部账户(EOA)或其他智能合约调用的函数。函数可以有任何功能，从简单的状态读取、返回到更改多个状态和调用其他智能合约的消息。

在Dune上，我们在相应的表中解析对智能合约进行的所有消息调用和交易。这些表被相应地命名为`projectname_blockchain.contractName_call_functionName`。

这可以在单个智能合约级别（如 uniswap v3 factory）或一类合约（如 uniswap v3 pairs）上完成。

例如，当我们通过 [uniswap v3 factory](https://etherscan.io/address/0x1f98431c8ad98523631ae4a59f267346ea31f984#code) 合约中的函数`createPool`（在以太坊上）创建 uniswap v3 池子的时候，Dune 将在表[ `uniswap_v3_ethereum.Factory_call_createPool`](https://dune.com/queries/735856)中记录该交易。无论是外部账户 (EOA) 通过交易还是智能合约通过消息调用，这些行为都会被记录。

**多个实例**

对于存在多个实例的智能合约，对该智能合约所有实例的所有调用都会被我们解码到一张表中。例如，如果有交易调用了 [uniswap v3 pairs](https://etherscan.io/address/0x8f8ef111b67c04eb1641f5ff19ee54cda062f163#writeContract) 这个智能合约的任何实例的`swap`函数，我们将在 `uniswap_v3_ethereum.Pair_call_swap`表中记录此数据 。

**常见的误解**

这里要记住的一件事是[web3.js](https://web3js.readthedocs.io)、[web3.py](https://web3py.readthedocs.io/en/stable)和通过所有其他方式在（本地）调用 `pure`,`read`,或者`constant`函数的人不会在区块链上广播或任何内容，因此不会记录在Dune中。


简而言之：**存储在智能合约内存中的状态数据在Dune上获取不到！**

一个很好的例子是 [erc20 代币合约](https://etherscan.io/token/0x1f9840a85d5af5bf1d1762f925bdaddc4201f984#readContract)`Uni`的函数`decimals`，它是一个通过自动创建的“[getter 函数](https://docs.soliditylang.org/en/v0.7.4/contracts.html#getter-functions)”可以访问的`constant`状态变量。如果智能合约在交易中调用此函数，则此消息调用将记录在Dune的表[`uniswap."UNI_call_decimals"`](https://dune.com/queries/741354)中。

这与使用 web3.py/web3.js 在本地调用此函数或使用Etherscan前端访问此状态的任何人形成对比。这些本地调用不会记录在Dune中。

**进一步阅读：**
[交易和调用有什么区别？](https://ethereum.stackexchange.com/questions/765/what-is-the-difference-between-a-transaction-and-a-call)

[Soliditylang.org 文档](https://docs.soliditylang.org/en/v0.8.13/contracts.html#function-visibility)
