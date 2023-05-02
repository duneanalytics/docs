---
title: nft.trades
description: nft.trades is an effort to make NFT trading data easily available to everyone on Dune.
---

`nft.trades` is an effort to make NFT trading data easily available to everyone on Dune. This table aggregates and standardizes the data between different data platforms and provides auxiliary information and metadata all in one table.

The culmination of this is a dataset which makes it extremely easy to query for any NFT related trading data across all indexed platforms.

You can find the specifications for nft.trades on our [Spellbook documentation](https://dune.com/spellbook#!/model/model.spellbook.nft_trades).

So far we have indexed the data of the following platforms:

- OpenSea
- Rarible
- SuperRare
- CryptoPunks (They get traded in their own contracts)
- Foundation
- LooksRare

## How it works

### Single Item Trade

A trade occurs between a `buyer`and a `seller`.

They exchange an item which is uniquely identified by the combination of `nft_contract_address` and `token_id`. The Buyer will pay the Seller a given `original_amount`of tokens in any given `original_currency`. To make it easier, we have calculated the `usd_amount` that this was worth at the time of the trade for you. Most trades will be done in ETH or WETH, but especially non OpenSea trades often contain other currencies.

The trade is committed on any of the indexed `platforms`and will be facilitated through a smart contract of those platform's `exchange_contract_address`. Each trade will have metadata like `block_time`, `tx_hash`_,_ `block_number`, `platform version`, `evt_index` etc.

Additionally, we also provide metadata about the traded NFT. `nft_project_name` and `erc_standard` will help you in analyzing your dataset more easily. `nft_project_name` data gets pulled from the `nft.tokens` [table](https://github.com/duneanalytics/spellbook/blob/master/ethereum/nft/tokens.sql), if your NFT is missing in that table, you are welcome to make a PR to add it.

### Bundle Trade

There can also be trades in which a single trade transaction contains multiple Items. Each of these Items is uniquely identified through a combination of `nft_contract_address` and `token_id`. Unfortunately, in these trades there is not a clear way to determine a corresponding `usd_amount` for each of the items.

A possible workaround is to divide the number of items by the payment made for the bundle, but this logic very quickly falls apart when Items that are not one in kind/value get sold in a bundle.

We recommend removing bundle transfers from the dataset that you are working with since it can heavily influence the results in either direction. Note that `token_id` and '`erc_standard` will be null if tokens with different tokens IDs or erc type are transferred within the same transaction.

### Aggregator Trade

There can also be trades in which a single trade transaction contains multiple items, especially when using NFT aggregator platforms. Our approach is to unravel aggregator trades so that each row correspond to a unique item that was traded, with its associated ID, price, collection, etc.

Importantly, the `trade_type` will be indicated as `Aggregator Trade`, and platform names and address can be found in the `nft.aggregators` [table](https://github.com/duneanalytics/spellbook/blob/master/ethereum/nft/aggregators.sql).

If your aggregator platform is missing in that table, you are welcome to make a PR to add it.

### Platform and Royalty Fees

In the most recent version of `nft.trades`, information about the amount and percent of royalty fees in the original amount and in USD is available when this information was able to be retrieved.

Royalty fees are going to the creator, and Platform fees are collected by the NFT platform. Note that royalty fees cannot always be retrieved, and are set to null by default.

## Examples

### Queries

#### All trades for a given NFT

**_SQL_**

```sql
select * from nft.trades 

where nft_contract_address = '\xb47e3cd837ddf8e4c57f05d70ab865de6e193bbb' --this is the cryptopunks address
```

**_Results_**

![type:video](https://dune.com/embeds/146090/288199/bc835020-f730-4348-b749-abd94277b0f7)

#### Trades in the last 24 hour on a given platform

**_SQL_**

```sql
select date_trunc('day', block_time), usd_amount, nft_contract_address, token_id from nft.trades 

where platform = 'OpenSea' --only shows trades on given Platform

and block_time > now() - interval '24hours'
```

**_Results_**

![type:video](https://dune.com/embeds/1622909/2690008/ce6aa75e-b94c-4dcf-a1f0-020d2cb5fa9b)

#### Platform volumes in the last year

**_SQL_**

```sql
select  sum(usd_amount), 
        date_trunc('day', block_time) as day, 
        platform 
from nft.trades 
where block_time > now() - interval '365 days'
group by platform, day
```

**_Results_**

![type:video](https://dune.com/embeds/146160/288002/cc990e4d-21e8-43a7-9bc3-2357a72be7b0)

### Dashboards

#### That utilize parameters

<div class="cards grid" markdown>
- [NFT by @0xBoxer](https://dune.com/0xBoxer/NFT)
- [NFT Sales Overview by Project by @rantum](https://dune.com/rantum/NFT-Sales-Overview-by-Project)
</div>

#### That look across the entire Ecosystem

<div class="cards grid" markdown>
- [NFT Collection Dashboard by @rantum](https://dune.com/rantum/NFT-Collection-Dashboard)
- [NFT by @sealaunch](https://dune.com/sealaunch/NFT)
</div>

## Column Data

| Column name | Data type | Description |
| - | :-: | - |
| `block_time` | _timestamp with time zone_ | When was this trade executed |
| `block_time` | _varchar_ | NFT project name (e.g. "the dudes") |
| `nft_token_id` | _varchar_ | The token_id that was traded (e.g. 235) |
| `erc_standard` | _varchar_ | The Token Standard of the traded token `ERC-721` or `ERC-1155` |
| `platform` | _varchar_ | Which Platform the trade was executed on |
| `platform_version` | _varchar_ | Which version of this platform was utilized? |
| `trade_type` | _varchar_ | "Single Item Sale" or "Bundle Sale" |
| `number_of_items` | _integer_ | How many NFTs were included in this trade |
| `category` | _varchar_ | Was this an auction or a direct sale |
| `evt_type` | _varchar_ | Currently not in use, default 'Trade' |
| `aggregator` | _varchar_ | Was this trade made using an aggregator (Yes : Name of aggregator, No : Null) |
| `usd_amount` | _numeric_ | USD value of the trade at time of execution |
| `seller` | _varbinary_ | Seller of NFTs |
| `buyer` | _varbinary_ | Buyer of NFTs |
| `amount_original` | _numeric_ | The amount in the right format |
| `amount_original_raw` | _numeric_ | Raw amount of the currency |
| `amount_eth` | _numeric_ | ETH value of the trade at time of execution |
| `royalty_fees_percent` | _numeric_ | Royalty fees going to the creator (in %) |
| `original_royalty_fees` | _numeric_ | Royalty fees in the currency used for this trade |
| `usd_royalty_fees` | _numeric_ | USD value of royalty fees at time of execution |
| `platform_fees_percent` | _numeric_ | Platform fees (in %) |
| `original_platform_fees` | _numeric_ | Platform fees in the currency used for this trade |
| `usd_platform_fees` | _numeric_ | USD value of platform fees at time of execution |
| `original_currency` | _varchar_ | The Currency used for this trade |
| `original_currency_contract` | _varbinary_ | The ERC-20 address of the currency used in this trade (does not work with raw ETH) |
| `currency_contract` | _varbinary_ | The corrected currency contract |
| `nft_contract_address` | _varbinary_ | The contract address of the NFT traded |
| `exchange_contract_address` | _varbinary_ | The platform contract that facilitated this trade |
| `tx_hash` | _varbinary_ | The hash of this transaction |
| `block_number` | _integer_ | The block_number that this trade was done in |
| `tx_from` | _varbinary_ | Initiated this transaction |
| `tx_to` | _varbinary_ | Received this transaction |
| `trace_address` | _ARRAY_ | n/a |
| `evt_index` | _integer_ | Event index |
| `trade_id` | _integer_ | n/a |

## Ser, my platform is not indexed

The SQL code that processes the data for every market place is open source and available in our [github repository](https://github.com/duneanalytics/spellbook/tree/master/ethereum/nft/trades). Everyone can review the code, make pull requests and submit code to add more marketplaces.
