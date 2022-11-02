---
description: Raw data tables are the basic building blocks of our database.
---

# Arbitrum

Arbitrum is an optimistic rollup that settles it's transactions on Ethereum Mainnet. You can read all about Arbitrum's approach to scaling and building a rollup [in their docs](https://developer.offchainlabs.com/docs/inside\_arbitrum).

Arbitrum's execution environment differs from the Mainnet EVM implementation in it's calculation of gas costs. Since Arbitrum is an optimistic rollup that publishes it's transaction on Ethereum Mainnet, the gas calculations have to account for additional factors.

## Gas costs for L1

Transactions on Arbitrum have to pay for both L1 and L2 resources. The L1 resources are essentially just Ethereum calldata; i.e., you pay the size in raw data of your transaction times Arbitrum's view of the L1 calldata price. This already factors in L1's fluctuating gas prices. The L2 resources in a given transaction are the natively emerging costs for computation and storage that you invoke with your transaction, similar to any other EVM.

Since the "normal" implementation of the Ethereum Virtual Machine does not possess multiple ways to pay gas fees, Arbitrum solved this by including the cost for L1 resources inside of the computational gas units used (`gas_limit` or `gas_used`). Whenever somebody tries to transact on Arbitrum, the RPC endpoint that is called for estimating a sufficient "gas limit" returns an amount of computational gas units that exceeds the standard costs that would incur in a "normal" EVM.

```
P = "Gas Price" on Arbitrum = Arbitrum's native gas price 
G = traditionally "Gas Limit" = L2 gas used + L1 resources used
```

Arbitrum's transactions costs are calculated with the following formula:

$$
P*G = Costs
$$

G consists of:

$$
(L2 \ gas \ used) +\frac{(L1 \ gas \ price * L1\ calldata)}{P} = G
$$

The complete calculation therefore consists of:

$$
P * ((L2 \ gas \ used) +\frac{(L1 \ gas \ price * L1\ calldata)}{P}) =  Costs
$$

Looking at this formula, we can now understand that an increasing gas price on Arbitrum leads to cheaper transactions. This is due to the fact that Arbitrum will always publish it's transactions on Ethereum mainnet, whether there is one transaction that needs to be published on mainnet or a thousand. Fees on Arbitrum will only rise if there is an increased demand for blockspace. The increased demand for blockspace in return means that more abritrum transactions get published on mainnet in one "batch publish" transaction, significantly reducing the costs for individual transactions.

We are reflecting the L1 resources used for Arbitrum Transactions in the column `gas_used_for_l1`.

### Gas Price Mechanism

Arbitrum does not follow the EIP1559 standard and instead has its own mechanism for determining gas costs. A transaction will have a `gas_price`, which is treated as the maximum price that the user is willing to pay for this transaction. The actual `gas_price` that is paid by the user will be determined by an [algorithm](https://developer.offchainlabs.com/docs/inside\_arbitrum#price-for-arbgas) within the Arbitrum EVM. This actual `gas_price` that the user pays is reflected in the columnn `effective_gas_price`.

### Calculation of Gas Usage

Arbitrum does not follow the standard EVM standards and rules to calculate how much gas is being used by a transaction. That is including and excluding the L1 Resource costs, the costs within Arbitrum's EVM are just calculated differently all together. You can look at the specifications of Arbitrum's AVM opcode costs [in their documentation](https://developer.offchainlabs.com/docs/avm\_specification#instructions).

**You can't compare Arbitrum gas costs to other EVM chains gas costs!**

### TL;DR

Use `effective_gas_price` for calculating gas costs on Arbitrum.

To look at only the gas costs that occur within the Arbitrum EVM, substract the `gas_used_for_l1` amount from the `effective_gas_price` field.

That being said, you can't compare Arbitrum's gas consumption to other EVM chains gas costs.

### Raw data tables

<div class="cards grid" markdown>
- [Blocks](blocks.md)
- [Transactions](transactions.md)
- [Event logs](event-logs.md)
- [Traces](traces.md)
</div>
