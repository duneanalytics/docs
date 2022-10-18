---
description: Raw data tables are the basic building blocks of our database.
---

# Optimism

Optimism is a Layer 2 Optimistic Rollup network designed to utilize the strong security guarantees of Ethereum while reducing its cost and latency. Optimism processes transactions outside of Ethereum Mainnet, reducing congestion on the base layer and improving scalability. For a Deep Dive into Optimism, we recommend reading through their [Documentation](https://community.optimism.io/docs/how-optimism-works).

Optimism differs in it's EVM implementation in the calculation of gas costs, since it also needs to pay for L1 resources.

## Gas costs on Optimism

Optimism settles it's transactions on Ethereum Mainnet. This happens via a sequencer contract on L1 that submits the raw calldata of any given transaction on Optimism's Network on L1 in batches. These costs for the batch settlement transactions needs to be accounted for in the Calculation of gas costs on Optimism. The transaction fees on Optimism are calculated with the following formula:

$$
Transaction\ Fees = L1\ fee + (L2\ gas\ price * L2\ gas\ used)
$$

**The L1 Fee consists of:**

$$
L1\ Fee = Fee\ Scalar * L1\ Gas\ Price * L1\ Gas\ Used
$$

`L1 Fee Scalar` is a variable that can be increased/decreased by the Optimism Team. It ensures that the gas costs for L1 are sufficiently covered and provides income to the Optimism Team. `L1 Gas Price` is an estimation of the gas price on Mainnet.

`L1 Gas used` **breaks down to:**

$$
L1\ Gas\ Used = Calldata\ gas + a\ fixed\ overhead\ gas\ cost
$$

**So the full calculation of gas costs on optimism consists of:**

$$
Transaction\ Fee = Fee\ Scalar * L1\ Gas\ Price * (L1 Calldata\ gas + a\ fixed\ overhead\ gas\ cost)
$$

You can read more about Optimism Gas Costs and the approach to minimize them in [this article](https://help.optimism.io/hc/en-us/articles/4411895794715-Transaction-fees).

### TL;DR

To calculate gas costs for a transaction on Optimism you need to follow this formula:

```
L1\_Fee + (gas_price*gas_used)
```

Additionally, Optimism hasn't implemented EIP1559, so it follows the "old" gas auction model.

### Raw data tables

<div class="cards grid" markdown>
- [Blocks](blocks.md)
- [Transactions](transactions.md)
- [Event logs](event-logs.md)
- [Traces](traces.md)
</div>
