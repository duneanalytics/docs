---
description: Raw data tables are the basic building blocks of our database.
---

# Avalanche C-Chain

C-Chain is an instance of the Ethereum Virtual Machine powered by the Avalanche network. It follows the rules of Ethereum Mainnet and only differs in it's consensus mechanism, all other technical specification are exactly the same. Gas is paid in $AVAX instead of $ETH.

You can read more about Avalanche Network and C-Chain [in this article](https://learn.figment.io/protocols/avalanche).

Working with the C-Chain on Dune works exactly like querying Ethereum mainnet data. Only `avalanche_c.blocks` has slightly different properties as Avalanche C-Chain is already in a proof of stake(POS) consensus algorithm.

### Raw data tables

<div class="cards grid" markdown>
- [Blocks](blocks.md)
- [Transactions](transactions.md)
- [Event logs](event-logs.md)
- [Traces](traces.md)
</div>
