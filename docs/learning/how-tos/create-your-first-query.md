---
title: Create your first query
description: How to write a query to find out the monthly $ gas spent for your wallet
---

New to Dune? Embark on your analytical adventure with us! In this guide, we provide a detailed walkthrough to craft your inaugural query, revealing your wallet's monthly gas spent in USD.

Here is a visual click-through version if you are more of a visual learner. Below is a written version. 

<div style="position: relative; padding-bottom: calc(55.052083333333336% + 41px); height: 0;"><iframe src="https://demo.arcade.software/F5MszooI7BGb7kaAHwUI?embed" frameborder="0" loading="lazy" webkitallowfullscreen mozallowfullscreen allowfullscreen style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;color-scheme: light;"></iframe></div>

## Getting Started

**Initiate a New Query**: Begin by selecting ["Create New Query"](https://dune.com/queries). Start laying the basic structure of your query. 

```sql
SELECT 
FROM 
WHERE
GROUP BY 
```

## Choosing the Right Table

1. **Determine Your Data Source**: Instead of delving into the intricate [raw blockchain tables](../../data-tables/raw/index.md) to fetch gas expenditures for your wallet, utilize the pre-built, analytics-ready [Spell table](../../data-tables/spellbook/index.md) named [`gas.fees`](https://github.com/duneanalytics/spellbook/tree/main/models/gas). This table facilitates an effortless aggregation of gas expenses across eight EVM chains specifically for your wallet.

2. **What's the Spellbook?** Think of Spellbook as a transformative layer that aggregates and standardizes blockchain data, both raw and decoded. With thousands of models both contributed by our active community and curated by the Dune team, it's an invaluable resource. For a deeper dive into Spellbook, [explore here](../../data-tables/spellbook/index.md).

```sql
SELECT 
FROM gas.fees
WHERE
GROUP BY 
```

## Crafting Your Query

1. **Identify Your Columns**: Once you've zeroed in on the right table, pinpoint the `tx_fee_usd` column to track USD gas expenditures. To specify the wallet you're examining, use the `tx_sender` field. For demonstration purposes, we'll be using Vitalik's wallet (0xd8dA6BF26964aF9D7eEd9e03E53415D37aA96045).

2. **Aggregation & Time Period**: Our goal is to get monthly gas spendings, so we need to truncate the `block_date` to month and applying the `SUM()` function, then group by each month go derive the results.

_Sum of sum was applied to get the cumulatively gas spendings._

```sql
SELECT
  DATE_TRUNC('month', block_date) AS period,
  SUM(tx_fee_usd) AS monthly_gas_spent,
  SUM(SUM(tx_fee_usd)) OVER (ORDER BY DATE_TRUNC('month', block_date)) AS cumulative_gas_spent
FROM gas.fees
WHERE
  tx_sender = 0xd8dA6BF26964aF9D7eEd9e03E53415D37aA96045 -- vitalik.eth 
GROUP BY
  1
ORDER BY
  1
```

Here is the [link to demo query](https://dune.com/queries/3100875). 


## Boost Flexibility with Parameters

In the example, you'll see `tx_sender = {{Your Wallet Address}} -- default is vitalik.eth`. This denotes the use of the parameter feature, enhancing the query's flexibility. To mark a field as a parameter, wrap it in "{{}}". Alternatively, activate the "Add Parameter" button.

<div style="position: relative; padding-bottom: calc(55.052083333333336% + 41px); height: 0;"><iframe src="https://demo.arcade.software/zTKnTWQCbjTh2fcRsCaR?embed" frameborder="0" loading="lazy" webkitallowfullscreen mozallowfullscreen allowfullscreen style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;color-scheme: light;"></iframe></div>

```sql 
SELECT
  DATE_TRUNC('month', block_date) AS period,
  SUM(tx_fee_usd) AS monthly_gas_spent,
  SUM(SUM(tx_fee_usd)) OVER (ORDER BY DATE_TRUNC('month', block_date)) AS cumulative_gas_spent
FROM gas.fees
WHERE
  tx_sender = {{Your Wallet Address}} -- default is vitalik.eth
GROUP BY
  DATE_TRUNC('month', block_date)
ORDER BY
  1
```


## Execute & Fetch the Result

All set! Click "Run" and behold the outcome. Kudos on crafting your first query! 🎉

!!! note
    For a more intuitive insight, consider visualizing this data. Navigate to [Create your first visualization](./create-your-first-visualization.md) and conjure up some graphical magic!