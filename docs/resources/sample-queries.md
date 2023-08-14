---
title: Sample Queries
description: Learn how to write queries using popular datasets
---

# Writing Queries Using Popular Datasets

There are plenty of dataset created that you can use to query what you need. Here are some commonly requested queries using popular datasets

## prices.usd 

The prices.usd table contains price feed data derived from [Coinpaprika API](https://coinpaprika.com/). 
You can also do a pull request in the [here](https://github.com/duneanalytics/spellbook/tree/main/models/prices) to have your token added in prices.usd (Make sure that the token is active on Coinpaprika!)

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


```sql
-- getting the token price for WETH for the past 30 days
select * from prices.usd
where contract_address = 0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2
and blockchain = 'ethereum'
and minute >= NOW() - interval '30' days
```