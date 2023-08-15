---
title: Sample Queries
description: Learn how to write queries using popular datasets
---

# Writing Queries Using Popular Datasets

There are plenty of dataset created that you can use to query what you need. Here are some commonly requested queries using popular datasets

## prices.usd 

The prices.usd table contains price feed data derived from [Coinpaprika API](https://coinpaprika.com/). 
You can also do a pull request in the [here](https://github.com/duneanalytics/spellbook/tree/main/models/prices) to have your token added in prices.usd (Make sure that the token is active on Coinpaprika!)

<div style="text-align: center;">
<table>
  <tr>
    <th>Column Names</th>
    <th>Data Type</th>
    <th>Description</th>
  </tr>
  <tr>
    <td>contract_address</td>
    <td>varbinary</td>
    <td>contract_address of the token</td>
  </tr>
  <tr>
    <td>blockchain</td>
    <td>varchar</td>
    <td>blockchain that the token is on</td>
  </tr>
  <tr>
    <td>decimals</td>
    <td>int</td>
    <td>number of decimals</td>
  </tr>
  <tr>
    <td>minute</td>
    <td>timestamp</td>
    <td>timestamp of price feed</td>
  </tr>
    <tr>
    <td>price</td>
    <td>double</td>
    <td>token price</td>
  </tr>
    </tr>
    <tr>
    <td>symbol</td>
    <td>varchar</td>
    <td>token symbol</td>
  </tr>
</table>
</div>

```sql
-- getting the token price for WETH for the past 30 days
select * from prices.usd
where contract_address = 0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2
and blockchain = 'ethereum'
and minute >= NOW() - interval '30' day
```

## prices.usd_latest

Just as the table name suggest, this table contains the latest price available, derived from prices.usd

```sql
-- getting the latest price for 4 tokens 
select * from prices.usd_latest
where blockchain = 'ethereum'
and symbol IN ('WETH','WBTC','USDC','USDT')
```

## erc20_ethereum.evt_transfer

The erc20_ethereum.evt_transfer contains all erc20 token transfer events that occured. With this table, you will be able to get information such as number of token holders,token balances and many more! This table is available for other EVM chain too, just change the suffix to the chain desired(eg.erc20_arbitrum.evt_transfer,erc20_bnb.evt_transfer)

<div style="text-align: center;">
<table>
    <tr>
      <th>Column Names</th>
      <th>Data Type</th>
      <th>Description</th>
    </tr>
    <tr>
      <td></td>
    </tr>
    <tr>
      <td>contract_address</td>
      <td>varbinary</td>
      <td>erc20 token contract address</td>
    </tr>
    <tr>
      <td>from</td>
      <td>varbinary</td>
      <td>Address tokens are transferred from</td>
    </tr>
    <tr>
      <td>to</td>
      <td>varbinary</td>
      <td>Address tokens are transferred to</td>
    </tr>
    <tr>
      <td>value</td>
      <td>uint256</td>
      <td>Number of tokens transferred</td>
    </tr>
    <tr>
      <td>evt_block_number</td>
      <td>bigint</td>
      <td>Block number in which the event occurred</td>
    </tr>
    <tr>
      <td>evt_block_time</td>
      <td>timestamp</td>
      <td>Timestamp of the event occurrence</td>
    </tr>
    <tr>
      <td>evt_index</td>
      <td>bigint</td>
      <td>Index of the event within the block</td>
    </tr>
    <tr>
      <td>evt_tx_hash</td>
      <td>varbinary</td>
      <td>Transaction hash of the event</td>
    </tr>
</table>
</div>

```sql
-- get total amount of weth sent daily in the past 3 days 
SELECT DATE_TRUNC('day', evt_block_time) AS date,
       SUM(value / 1e18) AS daily_amount
FROM erc20_ethereum.evt_transfer
WHERE contract_address = 0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2
AND evt_block_time >= NOW() - INTERVAL '3' day
GROUP BY 1
```

You can also get your wallet erc20 token balances! There is a evms.erc20_transfers table that contains all evms erc20 token transfer event

```sql
-- getting erc20 token balances for 0xbe0eb53f46cd790cd13851d5eff43d12404d33e8
SELECT * FROM (
select blockchain,symbol,SUM(CASE WHEN "from" = 0xbe0eb53f46cd790cd13851d5eff43d12404d33e8 THEN -(value/POW(10,decimals)) ELSE (value/POW(10,decimals)) END) AS token_balance 
from evms.erc20_transfers JOIN tokens.erc20 USING (contract_address,blockchain)
where ("from" = 0xbe0eb53f46cd790cd13851d5eff43d12404d33e8 OR "to" = 0xbe0eb53f46cd790cd13851d5eff43d12404d33e8)
GROUP BY 1,2
) 
WHERE token_balance > 0
```

## dex.trades

The dex.trades table contains  transfer events that occured. With this table, you will be able to get information such as number of token holders,token balances and many more! This table is available for other EVM chain too, just change the suffix to the chain desired(eg.erc20_arbitrum.evt_transfer,erc20_bnb.evt_transfer)

<div style="text-align: center;">
<table>
    <tr>
      <th>Column Names</th>
      <th>Data Type</th>
      <th>Description</th>
    </tr>
    <tr>
      <td>amount_usd</td>
      <td>double</td>
      <td>Equivalent amount in USD</td>
    </tr>
    <tr>
      <td>block_date</td>
      <td>timestamp</td>
      <td>Date of the block</td>
    </tr>
    <tr>
      <td>block_time</td>
      <td>timestamp</td>
      <td>Time of the block</td>
    </tr>
    <tr>
      <td>blockchain</td>
      <td>varchar</td>
      <td>Blockchain identifier</td>
    </tr>
    <tr>
      <td>evt_index</td>
      <td>int</td>
      <td>Index of the event within the block</td>
    </tr>
    <tr>
      <td>maker</td>
      <td>varbinary</td>
      <td>Address of the maker</td>
    </tr>
    <tr>
      <td>project</td>
      <td>varchar</td>
      <td>Project name</td>
    </tr>
    <tr>
      <td>project_contract_address</td>
      <td>varbinary</td>
      <td>Contract address of the project</td>
    </tr>
    <tr>
      <td>taker</td>
      <td>varbinary</td>
      <td>Address of the taker</td>
    </tr>
    <tr>
      <td>token_bought_address</td>
      <td>varbinary</td>
      <td>Address of the token bought</td>
    </tr>
    <tr>
      <td>token_bought_amount</td>
      <td>double</td>
      <td>Amount of token bought</td>
    </tr>
    <tr>
      <td>token_bought_amount_raw</td>
      <td>decimal(38,0)</td>
      <td>Raw amount of token bought</td>
    </tr>
    <tr>
      <td>token_bought_symbol</td>
      <td>varchar</td>
      <td>Symbol of token bought</td>
    </tr>
    <tr>
      <td>token_pair</td>
      <td>varchar</td>
      <td>Token pair identifier</td>
    </tr>
    <tr>
      <td>token_sold_address</td>
      <td>varbinary</td>
      <td>Address of the token sold</td>
    </tr>
    <tr>
      <td>token_sold_amount</td>
      <td>double</td>
      <td>Amount of token sold</td>
    </tr>
    <tr>
      <td>token_sold_amount_raw</td>
      <td>decimal(38,0)</td>
      <td>Raw amount of token sold</td>
    </tr>
    <tr>
      <td>token_sold_symbol</td>
      <td>varchar</td>
      <td>Symbol of token sold</td>
    </tr>
    <tr>
      <td>trace_address</td>
      <td>varchar</td>
      <td>Trace address</td>
    </tr>
    <tr>
      <td>tx_from</td>
      <td>varbinary</td>
      <td>Transaction sender address</td>
    </tr>
    <tr>
      <td>tx_hash</td>
      <td>varbinary</td>
      <td>Transaction hash</td>
    </tr>
    <tr>
      <td>tx_to</td>
      <td>varbinary</td>
      <td>Transaction receiver address</td>
    </tr>
    <tr>
      <td>version</td>
      <td>varchar</td>
      <td>Version of the trade</td>
    </tr>
</table>
</div>




