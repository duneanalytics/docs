---
title: Available Chains
description: Here are the chains we have available to Query in Dune.
---

Here are the chains we have available to Query in Dune.

## Ethereum Mainnet

Ethereum was first launched in 2015 and is the original Blockchain that innovated and implemented the Ethereum Virtual Machine. Ethereum to this day remains a "truly" decentralized platform with many node operators all over the world securing the Blockchain. Ethereum is maintained and developed by independent developers all over the world.

Since it's inception in 2015, Ethereum has undergone a range of updates.

Explaining the Ethereum history, Roadmap and technical details goes beyond the scope of this documentation, therefore we encourage you to read the Documentation on [Ethereum.org](https://ethereum.org/en/developers/docs).

<div class="cards grid" markdown>
- [Ethereum Developer Docs](https://ethereum.org/en/developers/docs)
</div>

## Gnosis Chain (xDai)

Gnosis Chain is the predecessor of xDAI. It's a unique system in which the native fee currency is a bridged version of the stablecoin $DAI. The chain uses a unique dual-token model; $xDai is a stable token used for transactions, payments, and fees; Proof of Stake protection will be provided by $GNO with the consensus-layer Gnosis Beacon Chain.

Gnosis Chain is yet to complete it's transition to an open proof of stake system, in the meanwhile the chain is being maintained by the POSDAO. You can read more about this transitional state [here](https://developers.gnosischain.com/for-validators/consensus).

Gnosis Chain will continue xDai’s intent to follow the Ethereum roadmap as closely as possible. Future goals include:

* Offer the highest degree of compatibility between Gnosis Chain and Ethereum
* Set up a Gnosis Beacon Chain (in preparation of a later merge)
* Develop over time a role similar to what Kusama is to Polkadot

Gnosis Chain follows all standards and upgrades of Ethereum Mainnet, querying on Dune is exactly the same.

## Polygon POS

Polygon(formerly MATIC) is an Ethereum sidechain hosted and maintained by by Polygon Technology. Polygon PoS is a solution that achieves transaction speed and cost savings by utilizing a POS network. Polygon node requirements are significantly higher than Mainnet requirements as Polygon has a higher gas limit and shorter block time. 

You can read more about Polygon and their approach to scaling an EVM in their [documentation](https://docs.polygon.technology).

Polygon follows all the rules of ETH mainnet and querying on Dune works exactly the same.

## Optimism

!!! note
    We've included Optimism's OVM 1.0 base tables (blocks, logs, traces, transactions) in Dune V2, which can be found in the `optimism_legacy_ovm1` database. Data from these tables are labeled "Optimism (Legacy)" in the dropdown menu and use this icon: 
    
    ![optimism legacy icon](../images/optimism-legacy-icon.png)

    These tables are no longer updated as Optimism made significant changes with their [OVM 2.0 update](https://twitter.com/optimismFND/status/1458953238867165192).

    Data for the current version of Optimism's blockchain (November 11th, 2021 to present), is contained in the `optimism` database, are labeled "Optimism" in the dropdown menu, and use this icon:
    
    ![optimism icon](../images/optimism-icon.png)

!!! warning
    Due to an error with the current version of the Optimism client, we're missing about 235k Optimism blocks with no current timeline for a fix. [See the list of the exact missing blocks in this CSV](optimism-missing-blocks.csv) or [get the ranges of missing blocks from this Query](https://dune.com/queries/1328475?d=11).

Optimism is a Layer 2 Optimistic Rollup network designed to utilize the strong security guarantees of Ethereum while reducing its cost and latency. Optimism processes transactions outside of Ethereum Mainnet, reducing congestion on the base layer and improving scalability. For a Deep Dive into Optimism, we recommend reading through their [Documentation](https://community.optimism.io/docs/how-optimism-works).

Optimism differs in it's EVM implementation in the calculation of gas costs, since it also needs to pay for L1 resources.

### Gas costs on Optimism

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

## BNB Chain (BSC)

BNB Chain(formerly Binance Smart Chain, BSC) is an instance of the Ethereum Virtual Machine built and maintained by a team from the popular Crypto Exchange [Binance](https://binance.com). BNB Chain follows most of the rules of Ethereum Mainnet, but has not implemented EIP1559. Instead it relies on [BEP-95](https://github.com/bnb-chain/BEPs/blob/master/BEP95.md) to burn fees that accrue during usage of the platform. Furthermore, the gas limit per block is set to 100 mio, enabling more transactions to be processed in a given block. Transactions fees are paid in $BNB instead of $ETH.

You can read more about BNB Chain in [the documentation](https://docs.bnbchain.org/docs/bnbIntro).

On Dune, that means that the gas fields for EIP1559 transactions stay empty, everything else is the same.

<div class="cards grid" markdown>
- [BNB Chain Documentation](https://docs.bnbchain.org/docs/bnbIntro)
</div>

## Solana

Solana is a non-EVM blockchain that aims to have high transaction speeds without sacrificing decentralization. 

The chain employs a bunch of novel approaches, including the “proof of history” mechanism, which is why you'll find their data is quite different from EVM chains.

[Learn more about Solana's approach and details here](https://docs.solana.com/introduction).

## Arbitrum

Arbitrum is an optimistic rollup that settles it's transactions on Ethereum Mainnet. You can read all about Arbitrum's approach to scaling and building a rollup [in their docs](https://developer.offchainlabs.com/docs/inside\_arbitrum).

Arbitrum's execution environment differs from the Mainnet EVM implementation in it's calculation of gas costs. Since Arbitrum is an optimistic rollup that publishes it's transaction on Ethereum Mainnet, the gas calculations have to account for additional factors.

### Gas costs for L1

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

Looking at this formula, we can now understand that an increasing gas price on Arbitrum leads to cheaper transactions. This is due to the fact that Arbitrum will always publish it's transactions on Ethereum mainnet, whether there is one transaction that needs to be published on mainnet or a thousand. Fees on Arbitrum will only rise if there is an increased demand for blockspace. The increased demand for blockspace in return means that more Arbitrum transactions get published on mainnet in one "batch publish" transaction, significantly reducing the costs for individual transactions.

We are reflecting the L1 resources used for Arbitrum Transactions in the column `gas_used_for_l1`.

#### Gas Price Mechanism

Arbitrum does not follow the EIP1559 standard and instead has its own mechanism for determining gas costs. A transaction will have a `gas_price`, which is treated as the maximum price that the user is willing to pay for this transaction. The actual `gas_price` that is paid by the user will be determined by an [algorithm](https://developer.offchainlabs.com/docs/inside\_arbitrum#price-for-arbgas) within the Arbitrum EVM. This actual `gas_price` that the user pays is reflected in the column `effective_gas_price`.

#### Calculation of Gas Usage

Arbitrum does not follow the standard EVM standards and rules to calculate how much gas is being used by a transaction. That is including and excluding the L1 Resource costs, the costs within Arbitrum's EVM are just calculated differently all together. You can look at the specifications of Arbitrum's AVM opcode costs [in their documentation](https://developer.offchainlabs.com/docs/avm\_specification#instructions).

**You can't compare Arbitrum gas costs to other EVM chains gas costs!**

### TL;DR

Use `effective_gas_price` for calculating gas costs on Arbitrum.

To look at only the gas costs that occur within the Arbitrum EVM, subtract the `gas_used_for_l1` amount from the `effective_gas_price` field.

That being said, you can't compare Arbitrum's gas consumption to other EVM chains gas costs.

## Avalanche C-Chain

C-Chain is an instance of the Ethereum Virtual Machine powered by the Avalanche network. It follows the rules of Ethereum Mainnet and only differs in it's consensus mechanism, all other technical specification are exactly the same. Gas is paid in $AVAX instead of $ETH.

You can read more about Avalanche Network and C-Chain [in this article](https://learn.figment.io/protocols/avalanche).

Working with the C-Chain on Dune works exactly like querying Ethereum mainnet data. Only `avalanche_c.blocks` has slightly different properties as Avalanche C-Chain is already in a proof of stake(POS) consensus algorithm.

## Ethereum's Goerli Testnet

Created in September 2018 during ETHBerlin, [Goerli Testnet](https://goerli.net/) was the first proof-of-authority cross-client testnet, synching Parity Ethereum, Geth, Nethermind, Hyperledger Besu (formerly Pantheon), and EthereumJS.

This is the perfect solution for dapp developers looking to get stats before you launch on mainnet!

## Fantom

[Fantom](https://fantom.foundation/) is a layer 1 blockchain offering smart contract functionality.

It uses a Directed Acyclic Graph, which involves the seamless interaction of nodes in the network to ensure fast and secure transactions.