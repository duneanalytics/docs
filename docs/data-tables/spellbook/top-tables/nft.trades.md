---
title: nft.trades
description: nft.trades is an effort to make NFT trading data easily available to everyone on Dune.
---

`nft.trades` is an effort to make NFT trading data easily available to everyone on Dune. This table aggregates and standardizes the data between different data platforms and provides auxiliary information and metadata all in one table.

The culmination of this is a dataset which makes it extremely easy to query for any NFT related trading data across all indexed platforms.

You can find the specifications for nft.trades on our [Spellbook documentation](https://dune.com/spellbook#!/model/model.spellbook.nft_trades).

## Column Data

| Column Name             | Data Type         | Description                                              |
|-------------------------|-------------------|----------------------------------------------------------|
| `nft_contract_address`  | _varbinary_       | The contract address of the NFT                         |
| `number_of_items`       | _decimal(38,0)_   | The number of NFT items in this trade                   |
| `project`               | _varchar_         | The platform where the NFT is traded                    |
| `project_contract_address` | _varbinary_     | The contract address of platform                       |
| `seller`                | _varbinary_       | The seller's address of the NFT transaction            |
| `token_id`              | _varchar_         | The ID of the NFT token                                 |
| `token_standard`        | _varchar_         | The standard of the NFT token (ERC-721 / ERC-1155)      |
| `trade_category`        | _varchar_         | The category of the NFT trade (e.g., Buy/Sell/Auction)  |
| `trade_type`            | _varchar_         | The type of the NFT trade (e.g., Single Item Trade/Bundle Trade) |
| `tx_from`               | _varbinary_       | The address that initiated the transaction             |
| `tx_hash`               | _varbinary_       | The hash of the NFT transaction                         |
| `tx_to`                 | _varbinary_       | The destination address of the NFT transaction         |
| `unique_trade_id`       | _varchar_         | A unique identifier for the NFT trade                  |
| `version`               | _varchar_         | The version of the platform                            |
| `aggregator_address`    | _varbinary_       | The address of the aggregator                          |
| `aggregator_name`       | _varchar_         | The name of the aggregator                             |
| `amount_original`       | _double_          | The original amount of currency in the trade           |
| `amount_raw`            | _decimal(38,0)_   | The raw amount of currency in the trade                |
| `amount_usd`            | _double_          | The USD value of the trade                             |
| `block_number`          | _double_          | The block number of the NFT transaction                |
| `block_time`            | _timestamp_       | The timestamp of the block of the NFT transaction      |
| `blockchain`            | _varchar_         | The blockchain of the NFT transaction                 |
| `buyer`                 | _varbinary_       | The buyer's address in the NFT trade                   |
| `collection`            | _varchar_         | The NFT collection name                                |
| `currency_contract`     | _varbinary_       | The contract address of the currency used in the trade |
| `currency_symbol`       | _varchar_         | The symbol of the currency used in the trade           |
| `evt_type`              | _varchar_         | The type of event associated with the NFT transaction  |

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

#### Trading price for a given NFT in the past 7 days

```sql
-- get trade details of specific NFT collection (y00ts on polygon)
select * from nft.trades 
where nft_contract_address = 0x670fd103b1a08628e9557cd66b87ded841115190
AND block_time >= NOW() - interval '7' day
```

<iframe src="https://dune.com/embeds/2914584/4844017" width="100%" height="400" frameborder="0"></iframe>


#### Top collection in terms of volume traded in the last 72 hour on a given platform

```sql
SELECT ROW_NUMBER() OVER (ORDER BY total_volume DESC) as ranking,
       *
FROM (
SELECT COALESCE(collection,CAST(nft_contract_address AS VARCHAR)) as collection, -- using coalesce here will get you the nft_contract_address
       blockchain,                                                               -- instead of null if collection name does not exist
       SUM(amount_usd) as total_volume 
FROM nft.trades 
where project = 'opensea' --only shows trades on Opensea
and block_time > now() - interval '72' hour
GROUP BY 1,2
ORDER BY 3 DESC
limit 100
) 
```

<iframe src="https://dune.com/embeds/2914602/4843928" width="100%" height="400" frameborder="0"></iframe>

#### Platform daily and cumulative volume over time in the last year

```sql
select date_trunc('day', block_time) as day,
       project,
       sum(amount_usd) as daily_project_amount_usd,
       sum(sum(amount_usd)) OVER (PARTITION BY project ORDER BY date_trunc('day',block_time)) as project_cumulative_volume_usd
from nft.trades 
where block_time > now() - interval '365' day
group by 1,2
ORDER BY 1 DESC,4 DESC
```
<iframe src="https://dune.com/embeds/2914617/4843982" width="100%" height="400" frameborder="0"></iframe>

<iframe src="https://dune.com/embeds/2914617/4843954" width="100%" height="400" frameborder="0"></iframe>


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

## Ser, my platform is not indexed

The SQL code that processes the data for every market place is open source and available in our [github repository](https://github.com/duneanalytics/spellbook/tree/master/ethereum/nft/trades). Everyone can review the code, make pull requests and submit code to add more marketplaces.
