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


