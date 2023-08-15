---
title: tokens
description: token transfers and metadata
---

You'll likely be working with tokens that are fungible (erc20) and nonfungible (erc721 and erc1155) a lot in your analysis. There are a couple tables that are must knows for this:

## Metadata tables:

1. [**`tokens.erc20`**](https://spellbook-docs.dune.com/#!/model/model.spellbook.tokens_erc20): contains useful information such as the token `symbol` and the `decimals` for any given `contract_address`, the latter of which is needed to get the actual amount from raw amounts in onchain data.

| Column Name       | Data Type   | Description                                            |
|-------------------|-------------|--------------------------------------------------------|
| `blockchain`      | _varchar_   | The blockchain associated with the ERC20 token         |
| `contract_address`| _varbinary_ | The contract address of the ERC20 token                |
| `decimals`        | _int_       | The number of decimal places for the token's value     |
| `symbol`          | _varchar_   | The identifier of the asset (ticker)                   |

2. [**`tokens.nft`**](https://spellbook-docs.dune.com/#!/model/model.spellbook.tokens_nft): contains the collection `name` and `symbol` for any given `contract_address`.

These tables are usually joined on `contract_address` at the end of a query to make everything more human readable.

## Transfer tables:

1. [**`erc20_ethereum.evt_Transfer`**](https://spellbook-docs.dune.com/#!/model/model.spellbook.transfers_ethereum_erc20): all transfer events for every erc20 token. You can find how to get erc20 balances, mints, and burns using [this guide](https://www.youtube.com/watch?v=LT_PB-Fso3M).

2. [**`nft.transfers`**](https://spellbook-docs.dune.com/#!/model/model.spellbook.nft_transfers): all transfer events for every erc721 or erc1155 token. You can learn how to leverage this to find nft balances, transfers, and mints in [this guide](https://web3datadegens.substack.com/p/web3-sql-weekly-3-finding-all-nfts)

If you're looking for how to calculate native token balances like ethereum (ETH) balances then check out [this guide](https://web3datadegens.substack.com/p/web3-sql-weekly-1-how-to-calculate)

