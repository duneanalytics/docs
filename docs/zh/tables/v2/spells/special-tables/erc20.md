---
description: A smart contract interface standard for fungible tokens.
---

# ERC20

### **ERC20定义**

ERC20标准是用于所有EVM区块链上的同质化代币的代币标准。ERC20可以代表任何东西，从神奇的互联网积分到美元再到黄金代币。

ERC-20标准由Fabian Vogelsteller于2015年11月提出，它代表了第一个在智能合约中实现代币API的代币标准。这种智能合约的标准化解决了与区块链上其他应用程序的互操作性问题。 由于所有代币共享相同的接口，其他智能合约可以轻松地与它们交互。

包含ERC-20代币标准的智能合约不仅限于具有这些功能，还需要包含这些功能才能在标准范围内。

想要了解更多信息，可以查看 [initial proposal] (https://eips.ethereum.org/EIPS/eip-20)或者[ethereum.org documentation](https://ethereum.org/en/developers/docs/standards/tokens/erc-20).

_Please note that Binance Smart Chain chose to rename ERC to BEP, this is reflected in out tables._

**Methods**

```solidity
function name() public view returns (string) 
/* returns the full name of this token */
function symbol() public view returns (string) 
/* returns the ticker of this token */
function decimals() public view returns (uint8) 
/* returns the amount of decimals of this token */
function totalSupply() public view returns (uint256) 
/* returns the current circulating supply of this token */
function balanceOf(address _owner) public view returns (uint256 balance) 
/* returns the balance of the specified address */ 
function transfer(address _to, uint256 _value) public returns (bool success) 
/* is used to transfer the specified quantity(_value) of tokens to the address specified*/ 
function transferFrom(address _from, address _to, uint256 _value) public returns (bool success) 
/* is used when a third address has permission to move tokens from the sender(_from) to the receiver(_to)*/
function approve(address _spender, uint256 _value) public returns (bool success) 
/* is used to approve a spender for a specific quantitiy(_value) of tokens*/
function allowance(address _owner, address _spender) public view returns (uint256 remaining)
/* returns the quantity(_value) of tokens that the spender is still allowed to spend from the owners address*/
```

**Events**

```solidity
event Transfer(address indexed _from, address indexed _to, uint256 _value)
/* gets emitted upon successfull transfer of tokens*/
event Approval(address indexed _owner, address indexed _spender, uint256 _value)
/* gets emitted upon successful approval of an owner address with an allowed quantity(_value) of tokens that can be moved*/
```

### Tables on Dune

In Dune, we decode all transfer events across all smart contracts that use the ERC20 token standard into the `erc20_blockchain.ERC20_evt_Transfer` table.

Additionally, we parse all token approval events into the `erc20_blockchain.ERC20_evt_Approval` table.

#### erc20\_blockchain.ERC20\_evt\_Transfer

This is the event that gets emitted upon successful transfer of a token within a ERC20 smart contract. This can be triggered by calling the `transfer` or `transferFrom` function.

| from               | string      | the sender of the `ERC20` token                                                                                                                                              |
| ------------------ | ----------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| to                 | string      | the receiver of the `ERC20` token                                                                                                                                            |
| value              | numeric     | the amount of `ERC20` tokens sent. Notice that you have to divide this by the relevant decimals of the `ERC20` token to get to the commonly used denomination of this token. |
| contract\_address  | string      | the contract\_address of the `ERC20` token                                                                                                                                   |
| evt\_tx\_hash      | string      | the hash of the transaction in which this log is contained                                                                                                                   |
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
