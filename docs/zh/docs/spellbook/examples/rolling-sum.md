---
title: Rolling Sum of Daily Transfers
---

The next step is to apply the rolling sum window function to each daily transfer sum. This is a pretty straightforward query. We’d end here for balances if it was guaranteed that each wallet/contract pair made a transfer every day. But since that’s not the case we’ll finish the spell in the next model by filling in all the missing days and doing a few more clean up steps.

[transfers\_ethereum\_erc20\_rolling\_day.sql](https://github.com/duneanalytics/spellbook/blob/master/spellbook/models/transfers/ethereum/erc20/transfers\_ethereum\_erc20\_rolling\_day.sql)

```sql
{{ config(
       alias ='erc20_rolling_day')
}}

       select
           'ethereum' as blockchain,
           day,
           wallet_address,
           token_address,
           symbol,
           current_timestamp() as last_updated,
           row_number() over (partition by token_address, wallet_address order by day desc) as recency_index,
           sum(amount_raw) over (
               partition by token_address, wallet_address order by day
           ) as amount_raw,
           sum(amount) over (
               partition by token_address, wallet_address order by day
           ) as amount
       from {{ ref('transfers_ethereum_erc20_agg_day') }}
```

[transfers\_ethereum\_schema.yml](https://github.com/duneanalytics/spellbook/blob/master/spellbook/models/transfers/ethereum/transfers\_ethereum\_schema.yml)

```yaml
  - name: transfers_ethereum_erc20_rolling_hour
    meta:
      blockchain: ethereum
      sector: transfers
      project: erc20
      contibutors: soispoke, dot2dotseurat
    config:
      tags: ['transfers', 'ethereum', 'erc20', 'rolling_hour', 'soispoke', 'dot2dotseurat']
    columns:
      - *blockchain
      - *hour
      - *wallet_address
      - *token_address
      - name: symbol
        description: "ERC20 token symbol"
      - *amount_raw
      - name: amount
        description: "Rolling sum of raw amount of ERC20 token held *after* taking into account token decimals"
      - name: amount_usd
        description: "Rolling sum of amount of ERC20 token held in USD (fiat value at time of transaction)"
      - name: updated_at
        description: "UTC timestamp when table was last updated"
      - name: recency_index
        description: "Index of most recent balance ascending. recency_index=1 is the wallet/contract pair's most recent balance"
```

