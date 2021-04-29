---
description: >-
  We decode the data emitted by smart contracts and store them in easy-to-use
  tables.
---

# Decoded Data

## Decoded smart contract data

Instead of working with the traces, logs, and traces, Dune decodes smart contract activity into nice human-readable tables.

We create tables for each event and function defined in the smart contract ABI. Subsequently, every event or function call on that contract is decoded and inserted as a row into these tables.

The tables are named accordingly

**events:**             `projectname."contractName_evt_eventName"`

**function calls:** `projectname."contractName_call_eventName"`

As an example, decoded data for the `swap`-event of the uniswap V2 exchange contract is found in the table [uniswap\_v2."pair\_swap"](https://duneanalytics.com/queries/38968).

Using the event tables is usually sufficient, but in some cases you will want to use the `call` tables. For instance Maker DAO which don’t give you too many events you can use tables like [maker."SaiTub\_call\_draw](https://duneanalytics.com/queries/38974)".

## What contracts have decoded data?

You can check if contracts are already decoded by querying "blockchain".contracts through our database or [this dashboard](https://duneanalytics.com/0xBoxer/Is-my-Contract-decoded-yet).

If the contract is not in our database yet, you can submit them here: [www.duneanalytics.com/decoding](https://duneanalytics.retool.com/embedded/public/892af55f-a6ff-41df-b203-f8acb6f0a38b).

We usually take about 24-48 hours to decode smart contracts.

## How to understand decoded data?

Decoded data sometimes is a bit tricky to work with since it requires you to understand what the events/calls mean in the context of the smart contract. Additionally you need to understand what kind of data the smart contract emits and understand the intricacies of the different smart contracts of the project interacting with each other. Often times the data you are looking for is scattered across multiple smart contracts and tables in Dune.

If you are not able to make sense of the data by just searching at the tables, it usually helps to look at single tx's using the transaction hash and etherscan.

If that also doesn't lead to satisfactory results, scouring the relevant docs and github of the project can lead you to the desired answers. Furthermore, talking to the developers and core community of a project can also get you to a good understanding of the contract. 

Some good showcasing of how to deal with decoded data can be found all throughout Dune, but especially our [abstraction repository](https://github.com/duneanalytics/abstractions) is full of great examples.   


**In Summary**:   
Dealing with decoded data allows you deep access to information stored on the blockchain and is very information rich, but understanding that data sometimes takes a bit of effort on your side since you are literally interacting with the data of the contract in a direct way.

## Scalable decoding across contracts

Many dApps have numerous smart contracts that are more or less similar, we have two main ways of handling this in a scalable way:

### Contracts with the same bytecode

Dune can dynamically add contracts to track by comparing the bytecode of deployed contracts to known bytecodes. If a known contract is “dynamic”, events and calls to a newly deployed contract with matching bytecode will find it’s way into the same tables as were defined by the base contract. Essentially this covers all factory-pattern contract architectures. As a result, `SELECT`-ing from a single table might yield data from multiple contracts. In decoded tables, the column `contract_address` tells you which smart contract the event or call is on. If you want to look at only a single contract you can filter by its address.

For example:

```sql
SELECT DISTINCT contract_address FROM uniswap_v2."Pair_evt_swap";
```

will give you all the unique Uniswap Pairs with a Token Purchase event.

[Query in action](https://duneanalytics.com/queries/39006)

### Interfaces

When we’re interested in a subset of events fired regardless of the origin contract, Dune uses interface-decoding. Notable examples include erc20, erc721 and erc1155 transfer events. This method is reserved for special cases. These tables make it easy to keep track of ERC20 tokens and NFT's flowing in and out of contracts and wallets and are widely used across dune.

**erc20."ERC20\_evt\_Transfer"**

| column name | **data type** | **description** |
| :--- | :--- | :--- |
| from | bytea | the transactions sender |
| to | bytea | the transaction receiver |
| value | numeric | the amount of erc20 tokens sent. Notice that you have divide this by the relevant decimals of the erc20 token. |
| contract\_address | bytea | the contract\_address of the erc20 token |
| evt\_tx\_hash | bytea | the transaction hash |
| evt\_index | numeric | the transaction index |
| evt\_block\_time | timestamptz | the time at which the transaction occurred |
| evt\_block\_number | int8 | the length of the blockchain |

[See this table in action](https://duneanalytics.com/queries/39012)

**erc721."ERC721\_evt\_Transfer"**

| **c**olumn name | **data type** | **description** |
| :--- | :--- | :--- |
| from | bytea | the transactions sender |
| to | bytea | the transaction receiver |
| tokenID | numeric | The Token ID which uniquely identifies this NFT |
| contract\_address | bytea | the contract\_address of the erc20 token |
| evt\_tx\_hash | bytea | the transaction hash |
| evt\_index | numeric | the transaction index |
| evt\_block\_time | timestamptz | the time at which the transaction occurred |
| evt\_block\_number | int8 | the length of the blockchain |

[See this table in action](https://duneanalytics.com/queries/38974)



## **Queries to explore decoded Contracts**

**See all projects we have decoded data for**

```sql
SELECT DISTINCT namespace FROM ethereum."contracts"; 
```

**Contracts that are “interface”-decoded**

```sql
SELECT * FROM ethereum."contracts" WHERE address IS NULL;
```

If you are working with a an event or call table directly you can see if there are several instances of that contract with

```sql
SELECT DISTINCT contract_address FROM projectname."contractName_evt_eventName"; 
```



