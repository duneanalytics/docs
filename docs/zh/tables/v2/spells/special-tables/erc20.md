---
description: A smart contract interface standard for fungible tokens.
---

# ERC20

### **ERC20定义**

ERC20标准是用于所有EVM区块链上的同质化代币的代币标准。ERC20可以代表任何东西，从神奇的互联网积分到美元再到黄金代币。

ERC-20标准由Fabian Vogelsteller于2015年11月提出，它代表了第一个在智能合约中实现代币API的代币标准。这种智能合约的标准化解决了与区块链上其他应用程序的互操作性问题。 由于所有代币共享相同的接口，其他智能合约可以轻松地与它们交互。

包含ERC-20代币标准的智能合约不仅限于具有这些功能，还需要包含这些功能才能在标准范围内。

想要了解更多信息，可以查看 [initial proposal](https://eips.ethereum.org/EIPS/eip-20) 或者 [ethereum.org documentation](https://ethereum.org/en/developers/docs/standards/tokens/erc-20).

_请注意，币安智能链选择将ERC重命名为BEP，从表名中就可以看到这个变化。_

**方法**

```solidity
function name() public view returns (string) 
/* 返回Token的全称 */
function symbol() public view returns (string) 
/* 返回Token的ticker*/
function decimals() public view returns (uint8) 
/* 返回Token的精度 */
function totalSupply() public view returns (uint256) 
/* 返回Token当前的循环供应量 */
function balanceOf(address _owner) public view returns (uint256 balance) 
/* 返回指定地址的余额 */ 
function transfer(address _to, uint256 _value) public returns (bool success) 
/* 将指定数量的代币转移到指定地址*/ 
function transferFrom(address _from, address _to, uint256 _value) public returns (bool success) 
/* 如果存在当除发送者接受者之外的第三个地址有权限完成转账，这个时候可以使用此方法*/
function approve(address _spender, uint256 _value) public returns (bool success) 
/* 用于授权花费代币的数量*/
function allowance(address _owner, address _spender) public view returns (uint256 remaining)
/* 返回当前代币消耗者可使用的剩余代币数量（_value）*/
```

**事件**

```solidity
event Transfer(address indexed _from, address indexed _to, uint256 _value)
/* 在成功转出代币时发出*/
event Approval(address indexed _owner, address indexed _spender, uint256 _value)
/* 在给某个地址成功授权一定数量代币的时候发出*/
```

### Dune上的表

在Dune中，我们将使用ERC20代币标准的所有智能合约中的所有传输事件解码到 `erc20_blockchain.ERC20_evt_Transfer` 表中。
此外，我们将所有Token授权事件解析到 `erc20_blockchain.ERC20_evt_Approval` 表中。

#### erc20\_blockchain.ERC20\_evt\_Transfer

这是在ERC20智能合约中成功转移代币时发出的事件。这可以通过调用 `transfer` 或 `transferFrom` 函数来触发。

| from               | string      | `ERC20`代币的发送者                                                                                                                                         |
| ------------------ | ----------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| to                 | string      | `ERC20`代币的接收者                                                                                                                                              |
| value              | numeric     | 发送的“ERC20”代币数量。 请注意，您必须将其除以“ERC20”代币的相关的精度，才能得到该代币的常用面额。 |
| contract\_address  | string      | `ERC20`代币的智能合约地址                          |
| evt\_tx\_hash      | string      | 包含这个转移代币事件log的 transactionhash                                                                                                                 |
| evt\_index         | numeric     | this logs index position in the block (cumulative amount of logs ordered by execution)                                                                                       |
| evt\_block\_time   | timestamptz | the time when the block was mined that includes this log                                                                                                                     |
| evt\_block\_number | int8        | the block\_number of the block that includes this log                                                                                                                        |

**erc20\_blockchain.ERC20\_evt\_Approval**

ERC20 tokens can be moved by other smart contracts. In order to allow this action, user will call the `approve` function first. Should that transaction complete successfully, the `Approval` event will get emitted.

| owner              | string                   | the address giving the approval                                                        |
| ------------------ | ------------------------ | -------------------------------------------------------------------------------------- |
| spender            | string                   | the address which has approval to move the tokens                                      |
| value              | numeric                  | the spending limit                                                                     |
| contract\_address  | string                   | the contract address of the erc20 token that can be moved                              |
| evt\_tx\_hash      | string                   | the hash of the transaction in which this log is contained                             |
| evt\_index         | bigint                   | this logs index position in the block (cumulative amount of logs ordered by execution) |
| evt\_block\_time   | timestamp with time zone | the time when the block was mined that includes this log                               |
| evt\_block\_number | bigint                   | the block\_number of the block that includes this log                                  |
