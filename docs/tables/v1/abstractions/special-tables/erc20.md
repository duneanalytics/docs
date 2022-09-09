---
description: A smart contract interface standard for fungible tokens.
---

# ERC20

### **ERC20 definition**

The ERC20 standard is the token standard that is used for fungible assets on all EVM blockchains. ERC20s can represent anything from magic internet points to USD to gold tokens.

The ERC-20 standard was proposed by Fabian Vogelsteller in November 2015 and represents the first token standard that implements an API for tokens within Smart Contracts. This standardization of smart contracts solves the issue of interoperability with other applications on the blockchain. Since all tokens share the same interface, other smart contracts are easily able to interact with them.

A smart contract that contains the erc20 token standard is not limited to only having these functions, but it needs to contain these functions to be within the standard.

For more reading check out the [initial proposal](https://eips.ethereum.org/EIPS/eip-20) or the [ethereum.org documentation](https://ethereum.org/en/developers/docs/standards/tokens/erc-20).

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

In Dune, we decode all transfer events across all smart contracts that use the ERC20 token standard into the `erc20."ERC20_evt_Transfer"` table. 

Additionally, we parse all token approval events into the `erc20."ERC20_evt_Approval"` table.

#### erc20."ERC20\_evt\_Transfer"

This is the event that gets emitted upon successful transfer of a token within a ERC20 smart contract. This can be triggered by calling the `transfer` or `transferFrom` function.

| from               | bytea       | the sender of the `ERC20` token                                                                                                                                              |
| ------------------ | ----------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| to                 | bytea       | the receiver of the `ERC20` token                                                                                                                                            |
| value              | numeric     | the amount of `ERC20` tokens sent. Notice that you have to divide this by the relevant decimals of the `ERC20` token to get to the commonly used denomination of this token. |
| contract\_address  | bytea       | the contract\_address of the `ERC20` token                                                                                                                                   |
| evt\_tx\_hash      | bytea       | the hash of the transaction in which this log is contained                                                                                                                   |
| evt\_index         | numeric     | this logs index position in the block (cumulative amount of logs ordered by execution)                                                                                       |
| evt\_block\_time   | timestamptz | the time when the block was mined that includes this log                                                                                                                     |
| evt\_block\_number | int8        | the block\_number of the block that includes this log                                                                                                                        |

**erc20."ERC20\_evt\_Approval"**

ERC20 tokens can be moved by other smart contracts. In order to allow this action, user will call the `approve` function first. Should that transaction complete successfully, the `Approval` event will get emitted.

| owner              | bytea                    | the address giving the approval                                                        |
| ------------------ | ------------------------ | -------------------------------------------------------------------------------------- |
| spender            | bytea                    | the address which has approval to move the tokens                                      |
| value              | numeric                  | the spending limit                                                                     |
| contract\_address  | bytea                    | the contract address of the erc20 token that can be moved                              |
| evt\_tx\_hash      | bytea                    | the hash of the transaction in which this log is contained                             |
| evt\_index         | bigint                   | this logs index position in the block (cumulative amount of logs ordered by execution) |
| evt\_block\_time   | timestamp with time zone | the time when the block was mined that includes this log                               |
| evt\_block\_number | bigint                   | the block\_number of the block that includes this log                                  |

