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

**events:** `projectname."contractName_evt_eventName"`

**function calls:** `projectname."contractName_call_eventName"`

As an example, decoded data for the `swap`-event of the uniswap V2 exchange contract is found in the table [uniswap\_v2."pair\_swap"](https://dune.xyz/queries/38968).

Using the event tables is usually sufficient, but in some cases you will want to use the `call` tables. For instance Maker DAO which don’t give you too many events you can use tables like [maker."SaiTub\_call\_draw](https://dune.xyz/queries/38974)".

## What contracts have decoded data?

You can check if contracts are already decoded by querying "blockchain".contracts through our database or [this dashboard](https://dune.xyz/0xBoxer/Is-my-Contract-decoded-yet).

If the contract is not in our database yet, you can submit it for [Decoding](../../duneapp/adding-new-contracts.md) here: [dune.xyz/decode](http://dune.xyz/decode)

We usually take about 24-48 hours to decode smart contracts.

Check out [this guide](../../duneapp/adding-new-contracts.md) to learn more about the Decoding process.

## How to understand decoded data?

Decoded data sometimes is a bit tricky to work with since it requires you to understand what the events/calls mean in the context of the smart contract. Additionally you need to understand what kind of data the smart contract emits and understand the intricacies of the different smart contracts of the project interacting with each other. Often times the data you are looking for is scattered across multiple smart contracts and tables in Dune.

If you are not able to make sense of the data by just searching at the tables, it usually helps to look at single tx's using the transaction hash and etherscan.

If that also doesn't lead to satisfactory results, scouring the relevant docs and github of the project can lead you to the desired answers. Furthermore, talking to the developers and core community of a project can also get you to a good understanding of the contract.

Some good showcasing of how to deal with decoded data can be found all throughout Dune, but especially our [abstraction repository](https://github.com/duneanalytics/abstractions) is full of great examples.

**In Summary**:

Dealing with decoded data allows you deep access to information stored on the blockchain and is very information rich, but understanding that data sometimes takes a bit of effort on your side since you are interacting with the data of the contract in a direct way.

## Scalable decoding across contracts

Many dApps have numerous smart contracts that are deployed with the same bytecode. This can be: yield aggregator pools,distinctive options, liquidity pools etc.

We can automatically pull these similar contracts into the same tables and thereby make it way easier for you to work with that data. Instead of having to query for all distinctive smart contracts you can then just query one table which will have the `contract_address` of that specific smart contract as an identifier.

To be able to use this function you have to submit the contract as one of the two bottom options while submitting it to decoding.

![](<../../.gitbook/assets/image (23).png>)

As a result, `SELECT`-ing from a single table might yield data from multiple contracts. In decoded tables, the column `contract_address` tells you which smart contract the event or call is on. If you want to look at only a single contract you can filter by its address.

For example:

```sql
SELECT DISTINCT contract_address FROM uniswap_v2."Pair_evt_swap";
```

will give you all the unique Uniswap Pairs with a Token Purchase event.

[Query in action](https://dune.xyz/queries/39006)

## **Queries to explore decoded Contracts**

**See all projects we have decoded data for**

```sql
SELECT DISTINCT namespace FROM ethereum."contracts";
```

If you are working with a an event or call table directly you can see if there are several instances of that contract with this query.

```sql
SELECT DISTINCT contract_address FROM projectname."contractName_evt_eventName";
```
