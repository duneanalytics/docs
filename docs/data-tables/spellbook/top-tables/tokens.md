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


```sql
-- querying using ethereum's weth contract_address
select * from tokens.erc20
WHERE contract_address = 0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2
```

| Blockchain | Contract Address                           | Symbol | Decimals |
|------------|-------------------------------------------|--------|---------- |
| Ethereum   | 0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2 | WETH   | 18       |

2. [**`tokens.nft`**](https://spellbook-docs.dune.com/#!/model/model.spellbook.tokens_nft): contains the collection `name` and `symbol` for any given `contract_address`.

These tables are usually joined on `contract_address` at the end of a query to make everything more human readable.

```sql
-- querying using bayc contract
select * from tokens.nft
where contract_address = 0xbc4ca0eda7647a8ab7c2061c2e118a18a936f13d
```

| Blockchain | Contract Address                           | Name                | Symbol | Token Standard |
|------------|-------------------------------------------|---------------------|--------|---------------- |
| Ethereum   | 0xbc4ca0eda7647a8ab7c2061c2e118a18a936f13d | Bored Ape Yacht Club | BAYC   | ERC721        |

## Transfer tables:

1. [**`erc20_ethereum.evt_Transfer`**](https://spellbook-docs.dune.com/#!/model/model.spellbook.transfers_ethereum_erc20): all transfer events for every erc20 token. 

| Column Name        | Data Type        | Description                                       |
|--------------------|------------------|---------------------------------------------------|
| `contract_address` | _varbinary_      | The contract address.                             |
| `from`             | _varbinary_      | The sender's address.                             |
| `value`            | _uint256_        | The value of the transaction.                     |
| `evt_block_number` | _bigint_         | The block number of the event.                    |
| `evt_block_time`   | _timestamp_      | The timestamp of the event's block.               |
| `evt_index`        | _bigint_         | The index of the event within the block.          |
| `evt_tx_hash`      | _varbinary_      | The transaction hash of the event.                |

#### Get the total inflow and outflow of USDT token from an address in the past 3 days

```sql
SELECT CASE WHEN "from" = 0xdfd5293d8e347dfe59e90efd55b2956a1343963d THEN 'Outflow' ELSE 'Inflow' END AS token_flow,
       SUM(value/POW(10,decimals)) as total_amount
FROM erc20_ethereum.evt_transfer a JOIN tokens.erc20 b ON a.contract_address = b.contract_address  
WHERE a.contract_address = 0xdac17f958d2ee523a2206206994597c13d831ec7
AND ("from" = 0xdfd5293d8e347dfe59e90efd55b2956a1343963d OR "to" = 0xdfd5293d8e347dfe59e90efd55b2956a1343963d)
AND evt_block_time >= NOW() - interval '3' day
GROUP BY 1
```

<iframe src="https://dune.com/embeds/2914344/4843642" width="100%" height="400" frameborder="0"></iframe>

#### Get all holders with their ens and balances of an erc20 token contract

```sql
SELECT address,
       symbol,
       ARRAY_AGG(distinct name) as ens,
       SUM(amount) as balance
FROM (
SELECT tr."from" AS address,
       symbol,
       contract_address,
       -(tr.value/POW(10,decimals)) AS amount
FROM erc20_ethereum.evt_transfer tr JOIN tokens.erc20 USING (contract_address)
WHERE "from" != 0x0000000000000000000000000000000000000000 -- exclude mint/burn addresses
AND contract_address = 0x046eee2cc3188071c02bfc1745a6b17c656e3f3d -- contract_address of the erc20 token 
-- AND evt_block_time <= TIMESTAMP '2023-01-01' -- you can use this to get snapshot data
UNION ALL
SELECT tr."to" AS address,
       symbol,
       contract_address,
       (tr.value/POW(10,decimals)) AS amount
FROM erc20_ethereum.evt_transfer tr JOIN tokens.erc20 USING (contract_address)
 WHERE "to" != 0x0000000000000000000000000000000000000000 -- exclude mint/burn addresses
 AND contract_address = 0x046eee2cc3188071c02bfc1745a6b17c656e3f3d -- contract_address of the erc20 token
-- AND evt_block_time <= TIMESTAMP '2023-01-01' -- you can use this to get snapshot data
 ) x LEFT JOIN labels.ens USING (address)
 GROUP BY 1,2
 HAVING SUM(amount) > 0.1 --  having more than 0.1 balance
 ORDER BY 4 DESC
```

<iframe src="https://dune.com/embeds/2753189/4581118" width="100%" height="400" frameborder="0"></iframe>

If you're looking for how to calculate native token balances like ethereum (ETH) balances then check out [this guide](https://web3datadegens.substack.com/p/web3-sql-weekly-1-how-to-calculate)

You can find how to get erc20 balances, mints, and burns using [this guide](https://www.youtube.com/watch?v=LT_PB-Fso3M).

2. [**`nft.transfers`**](https://spellbook-docs.dune.com/#!/model/model.spellbook.nft_transfers): all transfer events for every erc721 or erc1155 token. 

| Column Name       | Data Type   | Description                                       |
|-------------------|-------------|---------------------------------------------------|
| `contract_address`| _varbinary_ | The contract address                              |
| `from`            | _varbinary_ | The sender's address                              |
| `to`              | _varbinary_ | The recipient's address                           |
| `tokenId`         | _uint256_   | The token ID of the transaction                   |
| `evt_block_number`| _bigint_    | The block number of the event                     |
| `evt_block_time`  | _timestamp_ | The timestamp of the event's block                |
| `evt_index`       | _bigint_    | The index of the event within the block           |
| `evt_tx_hash`     | _varbinary_ | The transaction hash of the event                 |

#### Get all erc721 token transfers to an addresses in the past 30 days

```sql
SELECT date_trunc('day',evt_block_time) as date,
       name,
       COUNT(*) as transfer_count
FROM erc721_ethereum.evt_transfer LEFT JOIN labels.contracts on to = address
where to = 0xdb5485c85bd95f38f9def0ca85499ef67dc581c0
AND evt_block_time >= NOW() - interval '30' day
GROUP BY 1,2
order by 1 desc
```

<iframe src="https://dune.com/embeds/2914105/4843579" width="100%" height="400" frameborder="0"></iframe>

#### Get all holders with their ens,labels and balances of an erc721 token contract

```sql
SELECT z.name,
       contract_address,
       address,
       a.name as ens_name,
       ARRAY_AGG(DISTINCT b.name) as labels_list,
       nft_list,
       number_of_nft_held,
       total_nft_supply
FROM (
SELECT contract_address,
       to as address,
       ARRAY_AGG(tokenId) as nft_list,
       COUNT(*) as number_of_nft_held,
       SUM(COUNT(*)) OVER () as total_nft_supply
FROM (
select contract_address,
       to,
       tokenId,
       ROW_NUMBER() OVER (PARTITION BY contract_address,tokenId ORDER BY evt_block_time DESC,evt_index DESC) as rn
from erc721_ethereum.evt_transfer
where contract_address = 0xBC4CA0EdA7647A8aB7C2061c2E118A18a936f13D
) x 
WHERE rn = 1
GROUP BY 1,2
) p
LEFT JOIN tokens.nft z USING (contract_address)
LEFT JOIN ens.reverse_latest a USING (address)
LEFT JOIN labels.addresses   b USING (address)
GROUP BY 1,2,3,4,6,7,8
ORDER BY 7 DESC
```

<iframe src="https://dune.com/embeds/2858082/4779585" width="100%" height="400" frameborder="0"></iframe>

You can learn how to leverage this to find nft balances, transfers, and mints in [this guide](https://web3datadegens.substack.com/p/web3-sql-weekly-3-finding-all-nfts)