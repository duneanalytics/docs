---
title: Tables and Chains Overview
---

## The Four Kinds of Tables

Dune ingests data from [node providers](https://www.quicknode.com/case-study/dune-analytics) to directly fill our **raw tables** for each chain. This data is then decoded using contract ABIs to provide easier to work with **decoded tables**. Then we create abstracted tables that standardize and aggregate the data (from all other tables) - giving you the easiest to work with **spell tables**. 

We also ingest data from **community providers** like [Reservoir](community/reservoir/index.md) and [Flashbots](community/flashbots/index.md), which you can think of as spell level abstractions.

!!! suggestion "Easy Tables"
    We highly recommend you use spellbook and decoded tables first, and then if you can't find the data you want try raw tables.

In each section below, you'll find details on how the tables are created and some table definitions/descriptions.

- [**Raw data**](raw/index.md): unedited, raw and encoded blockchain data

- [**Decoded data**](decoded/index.md): view the decoded calls and events made to smart contracts. This data is still unedited.

- [**Spellbook**](spellbook/index.md): Easy to work with aggregated tables that are maintained by Dune and our community.

- [**Community**](community/index.md): Enhanced tables that combine onchain and offchain data together.
## Available Chains

Here are the chains we have available to Query in Dune.

**Non-EVM Chains**

- Solana

- Bitcoin

**EVM Chains**

- Ethereum Mainnet

- Gnosis (previously xDai)
  
- Polygon (POS)
  
- Optimism
  
- BNB (Binance Smart Chain)
  
- Arbitrum
  
- Avalanche (c-chain)
  
- Goerli (Ethereum)
  
- Fantom

### Non-EVM Chains
#### Solana

Solana is a non-EVM blockchain that aims to have high transaction speeds without sacrificing decentralization. The chain employs a bunch of novel approaches, including the “proof of history” mechanism, which is why you'll find their data is quite different from EVM chains.

[You can learn to get started with Solana data analysis here](https://web3datadegens.substack.com/p/starter-guide-to-solana-data-analysis)

#### Bitcoin

The original blockchain launched by Satoshi in 2009, using a UTXO and ledger structure. You can get started with Bitcoin analysis using [this guide](https://web3datadegens.substack.com/p/how-to-analyze-bitcoin-data-with)

### EVM Chains
#### Ethereum Mainnet

Ethereum was first launched in 2015 and is the original Blockchain that innovated and implemented the Ethereum Virtual Machine. Ethereum to this day remains a "truly" decentralized platform with many node operators all over the world securing the Blockchain. Ethereum is maintained and developed by independent developers all over the world.

You can get started with EVM data analysis [with this guide](https://web3datadegens.substack.com/p/a-basic-wizard-guide-to-dune-sql).

<div class="cards grid" markdown>
- [Ethereum Developer Docs](https://ethereum.org/en/developers/docs)
</div>

#### Gnosis Chain (xDai)

Gnosis Chain is the predecessor of xDAI. It's a unique system in which the native fee currency is a bridged version of the stablecoin $DAI. The chain uses a unique dual-token model; $xDai is a stable token used for transactions, payments, and fees; Proof of Stake protection will be provided by $GNO with the consensus-layer Gnosis Beacon Chain.

Gnosis Chain is yet to complete it's transition to an open proof of stake system, in the meanwhile the chain is being maintained by the POSDAO. You can read more about this transitional state [here](https://developers.gnosischain.com/for-validators/consensus).

Gnosis Chain will continue xDai’s intent to follow the Ethereum roadmap as closely as possible. Future goals include:

* Offer the highest degree of compatibility between Gnosis Chain and Ethereum
* Set up a Gnosis Beacon Chain (in preparation of a later merge)
* Develop over time a role similar to what Kusama is to Polkadot

Gnosis Chain follows all standards and upgrades of Ethereum Mainnet, querying on Dune is exactly the same.

#### Polygon POS

Polygon(formerly MATIC) is an Ethereum sidechain hosted and maintained by by Polygon Technology. Polygon PoS is a solution that achieves transaction speed and cost savings by utilizing a POS network. Polygon node requirements are significantly higher than Mainnet requirements as Polygon has a higher gas limit and shorter block time. 

You can read more about Polygon and their approach to scaling an EVM in their [documentation](https://docs.polygon.technology).

Polygon follows all the rules of ETH mainnet and querying on Dune works exactly the same.

#### Optimism

!!! note
    We've included Optimism's OVM 1.0 base tables (blocks, logs, traces, transactions) in Dune V2, which can be found in the `optimism_legacy_ovm1` database. Data from these tables are labeled "Optimism (Legacy)" in the dropdown menu and use this icon: 
    
    ![optimism legacy icon](../app/query-editor/images/explorer-labels/optimism-legacy-icon.png)

    These tables are no longer updated as Optimism made significant changes with their [OVM 2.0 update](https://twitter.com/optimismFND/status/1458953238867165192).

    Data for the current version of Optimism's blockchain (November 11th, 2021 to present), is contained in the `optimism` database, are labeled "Optimism" in the dropdown menu, and use this icon:
    
    ![optimism icon](../app/query-editor/images/explorer-labels/optimism-icon.png)

Optimism is a Layer 2 Optimistic Rollup network designed to utilize the strong security guarantees of Ethereum while reducing its cost and latency. Optimism processes transactions outside of Ethereum Mainnet, reducing congestion on the base layer and improving scalability. For a Deep Dive into Optimism, we recommend reading through their [Documentation](https://community.optimism.io/docs/how-optimism-works).

Optimism differs in it's EVM implementation in the calculation of gas costs, since it also needs to pay for L1 resources.

#### BNB Chain (BSC)

BNB Chain(formerly Binance Smart Chain, BSC) is an instance of the Ethereum Virtual Machine built and maintained by a team from the popular Crypto Exchange [Binance](https://binance.com). BNB Chain follows most of the rules of Ethereum Mainnet, but has not implemented EIP1559. Instead it relies on [BEP-95](https://github.com/bnb-chain/BEPs/blob/master/BEP95.md) to burn fees that accrue during usage of the platform. Furthermore, the gas limit per block is set to 100 mio, enabling more transactions to be processed in a given block. Transactions fees are paid in $BNB instead of $ETH.

You can read more about BNB Chain in [the documentation](https://docs.bnbchain.org/docs/bnbIntro).

On Dune, that means that the gas fields for EIP1559 transactions stay empty, everything else is the same.

<div class="cards grid" markdown>
- [BNB Chain Documentation](https://docs.bnbchain.org/docs/bnbIntro)
</div>

#### Arbitrum

Arbitrum is an optimistic rollup that settles it's transactions on Ethereum Mainnet. You can read all about Arbitrum's approach to scaling and building a rollup [in their docs](https://developer.offchainlabs.com/docs/inside\_arbitrum).

Arbitrum's execution environment differs from the Mainnet EVM implementation in it's calculation of gas costs. Since Arbitrum is an optimistic rollup that publishes it's transaction on Ethereum Mainnet, the gas calculations have to account for additional factors.

#### Avalanche (C-Chain)

C-Chain is an instance of the Ethereum Virtual Machine powered by the Avalanche network. It follows the rules of Ethereum Mainnet and only differs in it's consensus mechanism, all other technical specification are exactly the same. Gas is paid in $AVAX instead of $ETH.

You can read more about Avalanche Network and C-Chain [in this article](https://learn.figment.io/protocols/avalanche).

Working with the C-Chain on Dune works exactly like querying Ethereum mainnet data. Only `avalanche_c.blocks` has slightly different properties as Avalanche C-Chain is already in a proof of stake(POS) consensus algorithm.

#### Ethereum's Goerli Testnet

Created in September 2018 during ETHBerlin, [Goerli Testnet](https://goerli.net/) was the first proof-of-authority cross-client testnet, synching Parity Ethereum, Geth, Nethermind, Hyperledger Besu (formerly Pantheon), and EthereumJS.

This is the perfect solution for dapp developers looking to get stats before you launch on mainnet!

#### Fantom

[Fantom](https://fantom.foundation/) is a layer 1 blockchain offering smart contract functionality.

It uses a Directed Acyclic Graph, which involves the seamless interaction of nodes in the network to ensure fast and secure transactions.