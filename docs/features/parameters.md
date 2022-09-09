---
title: Parameters
description: >-
  Parameters are an easy and powerful way to add filters to your
  Query/dashboard. Allowing you and others to interact with the Query in the
  user interface without changing the SQL.
---

## What are Parameters?

**Parameters are a specialized feature of dune that allow you to implement variables in certain parts of your Query code. This variable can be changed from dashboards and therefore allows you to make an interactive dashboard.**

Parameters allow you to make changes to certain defined parameters of your code with a few simple clicks. For instance instead of hard coding `contract_address` , `symbol` or `date ranges` you can just use the parameter function to change these aspects of your code using a parameter. This allows you to build an interactive dashboard or customizable Query that the viewer can use to query for exactly the data he needs.

Parameters are defined in the Query code as `{{parametername}}` and will appear below the Query and in any dashboards in which a Query Visualization with parameters is used in.

You can pass on input to the parameter below the Query or in the parameter field on a dashboard.

Simply run the Query to apply the parameter for a Query within the Query editor.

On a dashboard you can either click `apply all` at the top or change the parameters individually and hit `Enter`. The `Enter` submission also works for dropdowns and the date picker.

Parameters in a Dashboard can be shared between different Queries, just make sure to use the same name, type and default value between all of them.

![Parameters overview 1](images/parameters-overview-1.png)

![Parameters overview 2](images/parameters-overview-2.png)

![Parameters overview 3](images/parameters-overview-3.png)

## How do I use Parameters?

You can simply add a parameter to your Queries by writing `{{parametername}}` or using the button below the Query.

You can edit the properties of single parameters by clicking on the gear wheel next to the parameter in the Query editor. This allows you to set a default value, define a list of possible parameters or change the type of of the parameter. If you want to share parameters between different Queries on a dashboard make sure they exactly match in regards to name, type and default value.

![Parameters how to use](images/parameters-how-to-use.gif)

## Example Query

This Query returns the running total of Gas Paid in USD.

The Query Author has chosen to include a parameter for `wallet address`, `start date` and `end date`.

```sql
with alltransactions
AS (
SELECT 
    block_time, 
    success, 
    gas_price/10^9 AS gas_prices, 
    gas_used,
    (gas_price*gas_used)/10^18 AS eth_paid_for_tx,
    hash
FROM ethereum.transactions
WHERE "from" = CONCAT('\x', substring('{{1. Eth Address}}' from 3))::bytea
AND block_time >= '{{2. Start Date}}'
AND block_time < '{{3. End Date}}')

SELECT
    date_trunc('minute', block_time),
    SUM(eth_paid_for_tx*price) over (ORDER BY date_trunc('minute', block_time)) AS "Total Gas Fees Paid in USD"
FROM alltransactions
LEFT JOIN 
    (SELECT
        minute,
        price
    FROM prices.usd
    WHERE 
        symbol = 'WETH' AND
        minute > '{{2. Start Date}}') AS prices
ON date_trunc('minute', block_time) = minute
ORDER BY block_time DESC
```

Find this Query [here](https://dune.com/queries/64430/128463)

## Example Dashboards

**Find interesting stats on Ethereum Wallets with this dashboard:**
[https://dune.com/kevdnlol/Transaction-Breakdown](https://dune.com/kevdnlol/Transaction-Breakdown)

_The author has included the parameters `wallet address`, `start date` and `end date` in this Dashboard._

**Drill down into the single pools of Barnbridge's Smart Yield Product:**
[https://dune.com/0xBoxer/Barnbridge-or-Smart-Yield](https://dune.com/0xBoxer/Barnbridge-or-Smart-Yield)

_The Author has chosen to make the parameter `poolsymbol` into a drop down list here. This allows for easy access to all the relevant pools and detailed statistics on those._

**Find out how many people are participating in Yearn Vaults:**
[https://dune.com/msilb7/Yearn-How-Many-Addresses-are-Participating](https://dune.com/msilb7/Yearn-How-Many-Addresses-are-Participating)

[https://dune.com/0xrusowsky/KLIMA-Wallet-Activity](https://dune.com/0xrusowsky/KLIMA-Wallet-Activity)

**Find out how your investment in $KLIMA is doing:**

[**https://dune.com/0xrusowsky/KLIMA-Wallet-Activity**](https://dune.com/0xrusowsky/KLIMA-Wallet-Activity)

## Summary

Parameters allow you to make a certain part of your SQL query dynamic and thereby offer you to make Queries and dashboards interactive. That way you can easily display detailed data on your dashboard since it allows the viewer to customize the dashboard for his needs.

You could think of parameters like filters, but the possibilities of using this feature go beyond that.
