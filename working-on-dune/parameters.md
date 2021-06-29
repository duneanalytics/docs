---
description: >-
  Parameters are an easy way to make an interactive dashboard or query in which
  multiple parameters/variables can change.
---

# Parameters

### What are Parameters?

Parameters allow you to make changes to certain defined parameters of your code with a few simple clicks. Instead of hard coding `contract_address` , `symbol` or `date ranges` you can just use the parameter function to change these aspects of your code using a parameter. This allows you to build an interactive dashboard that the viewer can use to query for exactly the data he needs.

You can pass on input to the parameter below the query or at the top of your dashboard. Simply run the query  or click `apply` in your dashboard to rerun the queries/dashboard with the newly put in parameters.

Parameters in a Dashboard can be shared between different queries, just make sure to use the same name between all of them.

![](../.gitbook/assets/image%20%2833%29.png)

![](../.gitbook/assets/image%20%2830%29.png)

![](../.gitbook/assets/image%20%2829%29.png)

### How to use Parameters?

You can simply add a parameter to your queries by writing `{{parametername}}` or using the button below the query. You can order them by prefacing them with the corresponding position you want the Parameter to appear in the User Interface : `{{1.  parametername}}`.   
  
You can edit the properties of single parameters by clicking on the litte gear wheel next to the parameter in the query editor. This allows you to set a default value, define a list of possible parameters and change the type of the parameter.



### Example Query

This query returns the running total of Gas Paid in USD.

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

Find this query [here](https://duneanalytics.com/queries/64430/128463)

### **Example Dashboards**

**Find interesting stats on Ethereum Wallets with this dashboard:**  
[https://duneanalytics.com/kevdnlol/Transaction-Breakdown](https://duneanalytics.com/kevdnlol/Transaction-Breakdown)  
  
_The author has included the parameters `wallet address`, `start date` and `end date` in this Dashboard._ 

**Drill down into the single pools of Barnbridge's Smart Yield Product:**  
[https://duneanalytics.com/0xBoxer/Barnbridge-or-Smart-Yield](https://duneanalytics.com/0xBoxer/Barnbridge-or-Smart-Yield)   
  
_The Author has chosen to make the parameter `poolsymbol` into a drop down list here. This allows for easy access to all the relevant pools and detailed statistics on those._

**Find out how many people are participating in Yearn Vaults:**  
[https://duneanalytics.com/msilb7/Yearn-How-Many-Addresses-are-Participating](https://duneanalytics.com/msilb7/Yearn-How-Many-Addresses-are-Participating)

### Summary

Parameters allow you to make a certain part of your SQL query dynamic and thereby offer you to make  queries and dashboards interactive. That way you can easily display detailed data on your dashboard since it allows the viewer to customize the dashboard for his needs.  
You could think of parameters like filters, but the possibilities of using this feature go beyond that.

