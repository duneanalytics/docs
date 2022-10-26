---
title: Creation Traces
description: Create traces are used to create a smart contract then transfer ether to it.
---

## gnosis.creation_traces

Transactions can trigger smaller atomic actions that modify the internal state of an Ethereum Virtual Machine. 

One type of trace, `create`, is used to create a smart contract then transfer ether to it.

Read more [here](https://medium.com/chainalysis/ethereum-traces-not-transactions-3f0533d26aa).

| **Column Name** | **datatype** | **Description** |
| --------------- | ------------ | --------------- |
| block\_time     | timestamptz  | the time when the block was mined |
| block\_number   | long         | the length of the blockchain in blocks |
| tx\_hash        | string       | the transaction hash of the event |
| address         | string       | the address of the created contract |
| from            | string       | address of the contract that generated the `create` trace |
| code            | string       | the function executed |