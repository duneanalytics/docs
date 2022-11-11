---
description: >-
  nft.trades makes NFT trading data available to everyone on Dune Analytics.
  NFT.trades aggregates data across multiple NFT platforms into one simple
  table.
---

# nft.trades

## **An easy way of querying for NFT data**

`nft.trades` is an effort to make NFT trading data easily available to everyone on Dune Analytics. This table aggregates and standardizes the data between different data platforms and provides auxiliary information and metadata all in one table.

The culmination of this is a dataset which makes it extremely easy to query for any NFT related trading data across all indexed platforms.

So far we have indexed the data of the following platforms:

* OpenSea
* Rarible
* SuperRare
* CryptoPunks (They get traded in their own contracts)
* Foundation
* LooksRare

All of this data is easily accessible with very simple queries like these:

* [**all trades for a given NFT**](https://dune.com/queries/146090)

![NFT](images/nft.png)

```sql
select * from nft.trades 

where nft_contract_address = '\xb47e3cd837ddf8e4c57f05d70ab865de6e193bbb' --this is the cryptopunks address
```

* [**trades in the last 24 hour on a given platform**](https://dune.com/queries/146152)

```sql
select date_trunc('day', block_time), usd_amount, nft_contract_address, token_id from nft.trades 

where platform = 'OpenSea' --only shows trades on given Platform

and block_time > now() - interval '24hours'
```

* [**platform volumes in the last year**](https://dune.com/queries/146160)

```sql
select  sum(usd_amount), 
        date_trunc('day', block_time) as day, 
        platform 
from nft.trades 
where block_time > now() - interval '365 days'
group by platform, day
```

###

### Basic Understanding

#### Single Item Trade

A trade occurs between a `buyer`and a `seller`.

They exchange an item which is uniquely identified by the combination of `nft_contract_address` and `token_id`. The Buyer will pay the Seller a given `original_amount`of tokens in any given `original_currency`. To make it easier, we have calculated the `usd_amount` that this was worth at the time of the trade for you. Most trades will be done in ETH or WETH, but especially non OpenSea trades often contain other currencies.

The trade is committed on any of the indexed `platforms`and will be facilitated through a smart contract of those platform's `exchange_contract_address`. Each trade will have metadata like `block_time`, `tx_hash`_,_ `block_number`, `platform version`, `evt_index` etc.



Additionally, we also provide metadata about the traded NFT. `nft_project_name` and `erc_standard` will help you in analysing your dataset more easily. `nft_project_name` data gets pulled from the `nft.tokens` [table](https://github.com/duneanalytics/spellbook/blob/master/ethereum/nft/tokens.sql), if your NFT is missing in that table, you are welcome to make a PR to add it.

**Bundle Trade**

There can also be trades in which a single trade transaction contains multiple Items. Each of these Items is uniquely identified through a combination of `nft_contract_address` and `token_id`. Unfortunately, in these trades there is not a clear way to determine a corresponding `usd_amount` for each of the items. A possible workaround is to divide the number of items by the payment made for the bundle, but this logic very quickly falls apart when Items that are not one in kind/value get sold in a bundle. We recommend removing bundle transfers from the dataset that you are working with since it can heavily influence the results in either direction. Note that `token_id` and '`erc_standard` will be null if tokens with different tokens IDs or erc type are transfered within the same transaction.

**Aggregator Trade**

There can also be trades in which a single trade transaction contains multiple items, especially when using NFT aggregator platforms. Our approach is to unravel aggregator trades so that each row correspond to a unique item that was traded, with its associated ID, price, collection, etc. Importantly, the `trade_type` will be indicated as `Aggregator Trade`, and platform names and address can be found in the `nft.aggregators` [table](https://github.com/duneanalytics/spellbook/blob/master/ethereum/nft/aggregators.sql). If your aggregator platform is missing in that table, you are welcome to make a PR to add it.

**Platform and Royalty Fees**

In the most recent version of `nft.trades`, information about the amount and percent of royalty fees in the original amount and in USD is available when this information was able to be retrieved. Royalty fees are going to the creator, and Platform fees are collected by the NFT platform. Note that royalty fees cannot always be retrieved, and are set to null by default.

### **Sample dashboards**

**Dashboard that utilize parameters**

[**https://dune.com/0xBoxer/NFT**](https://dune.com/0xBoxer/NFT)

[**https://dune.com/rantum/NFT-Sales-Overview-by-Project**](https://dune.com/rantum/NFT-Sales-Overview-by-Project)

**Dashboards that look across the entire Ecosystem**

[**https://dune.com/rantum/NFT-Collection-Dashboard**](https://dune.com/rantum/NFT-Collection-Dashboard)

[**https://dune.com/sealaunch/NFT**](https://dune.com/sealaunch/NFT)\


***

## **Ser, my platform is not indexed**

The SQL code that processes the data for every market place is open source and available in our [github repository](https://github.com/duneanalytics/spellbook/tree/master/ethereum/nft/trades). Everyone can review the code, make pull requests and submit code to add more marketplaces.

Also read the section "[abstractions](index.md)" about this topic.

## **Table contents**

| column\_name                 | data\_type               | description                                                                       |
| ---------------------------- | ------------------------ | --------------------------------------------------------------------------------- |
| block\_time                  | timestamp with time zone | When was this trade exectuted                                                     |
| nft\_project\_name           | text                     | NFT project name (e.g. "the dudes")                                               |
| nft\_token\_id               | text                     | The token\_id that got trades (e.g. 235)                                          |
| erc\_standard                | text                     | The Token Standard of the traded token ERC721 or ERC1155                          |
| platform                     | text                     | Which Platform was this trade executed on?                                        |
| platform\_version            | text                     | Which version of this platform was utilized?                                      |
| trade\_type                  | text                     | "Single Item Sale" or "Bundle Sale"?                                              |
| number\_of\_items            | integer                  | How many NFTs were traded in this trade?                                          |
| category                     | text                     | Was this an auction or a direct sale?                                             |
| evt\_type                    | text                     | currently not in use, default 'Trade'                                             |
| aggregator                   | text                     | Was this trade made using an aggregator (Yes : Name of aggregator, No : Null)     |
| usd\_amount                  | numeric                  | USD value of the trade at time of execution                                       |
| seller                       | bytea                    | Seller of NFTs                                                                    |
| buyer                        | bytea                    | Buyer of NFTs                                                                     |
| original\_amount             | numeric                  | The amount in the right format                                                    |
| original\_amount\_raw        | numeric                  | raw amount of the currency                                                        |
| eth\_amount                  | numeric                  | ETH value of the trade at time of execution                                       |
| royalty\_fees\_percent       | numeric                  | Royalty fees going to the creator (in %)                                          |
| original\_royalty\_fees      | numeric                  | Royalty fees in the currency used for this trade                                  |
| usd\_royalty\_fees           | numeric                  | USD value of royalty fees at time of execution                                    |
| platform\_fees\_percent      | numeric                  | Platform fees (in %)                                                              |
| original\_platform\_fees     | numeric                  | Platform fees in the currency used for this trade                                 |
| usd\_platform\_fees          | numeric                  | USD value of platform fees at time of execution                                   |
| original\_currency           | text                     | The Currency used for this trade                                                  |
| original\_currency\_contract | bytea                    | The erc20 address of the currency used in this trade (does not work with raw ETH) |
| currency\_contract           | bytea                    | the corrected currency contract                                                   |
| nft\_contract\_address       | bytea                    | The contract address of the NFT traded                                            |
| exchange\_contract\_address  | bytea                    | The platform contract that facilitated this trade                                 |
| tx\_hash                     | bytea                    | the hash of this transaction                                                      |
| block\_number                | integer                  | the block\_number that this trade was done in                                     |
| tx\_from                     | bytea                    | Initiated this transaction                                                        |
| tx\_to                       | bytea                    | Received this transaction                                                         |
| trace\_address               | ARRAY                    | n/a                                                                               |
| evt\_index                   | integer                  | event index                                                                       |
| trade\_id                    | integer                  | n/a                                                                               |
