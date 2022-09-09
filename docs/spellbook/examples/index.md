---
title: Spellbook Examples
---

As an example, we'll look at ERC-20. [ERC-20](https://ethereum.org/en/developers/docs/standards/tokens/erc-20) tokens are fungible tokens that all follow a contract standard set by the Ethereum Foundation. To track daily balances, we need to first identify the transfers.

The main base Dune table we’ll use for this purpose is `erc20_ethereum.evt_Transfer` which you can find via the data explorer.
![type:video](https://www.loom.com/embed/198148674ded4f5e944f65452852482b)

In our case, we have broken down the spell into a more modular series of spells:

- [Reformatted](reformatted.md) transfers
- [Daily aggregation](daily-aggregation.md) of transfers
- [Rolling sum](rolling-sum.md) of daily transfers
- [Final daily balances](final-day-balance.md) for Ethereum ERC20 tokens
