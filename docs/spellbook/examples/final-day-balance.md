---
title: Final Daily Balance
---

This is our final daily Ethereum ERC20 token balances spell. We expand our spell to cover all days, not just the days with transfer activity. We add price data, we remove known rebase tokens and any tokens that resulted in large negative balances.

The ref tokens\_ethereum\_rebase is a static list of known rebase tokens that we manage. Whereas, the ref `'balances_ethereum_erc20_noncompliant'` is a table we derive from transfers\_ethereum\_erc20\_rolling\_day. That table looks for unique token\_addresses with larger negative balances which indicate the contract may not be compliant with ERC20.

[balances\_ethereum\_erc20\_day.sql](https://github.com/duneanalytics/spellbook/blob/master/spellbook/models/balances/ethereum/erc20/balances\_ethereum\_erc20\_day.sql)

```sql
{{ config(
       alias='erc20_day'
       )
}}

with
   days as (
       select
           explode(
               sequence(
                   to_date('2015-01-01'), date_trunc('day', now()), interval 1 day
               )
           ) as day
   )

, daily_balances as
(SELECT
   wallet_address,
   token_address,
   amount_raw,
   amount,
   day,
   symbol,
   lead(day, 1, now()) OVER (PARTITION BY token_address, wallet_address ORDER BY day) AS next_day
   FROM {{ ref('transfers_ethereum_erc20_rolling_day') }})

SELECT
   'ethereum' as blockchain,
   d.day,
   b.wallet_address,
   b.token_address,
   b.amount_raw,
   b.amount,
   b.amount * p.price as amount_usd,
   b.symbol
FROM daily_balances b
INNER JOIN days d ON b.day <= d.day AND d.day < b.next_day
LEFT JOIN {{ source('prices', 'usd') }} p
   ON p.contract_address = b.token_address
   AND d.day = p.minute
   AND p.blockchain = 'ethereum'
-- Removes rebase tokens from balances
LEFT JOIN {{ ref('tokens_ethereum_rebase') }}  as r
   ON b.token_address = r.contract_address
-- Removes likely non-compliant tokens due to negative balances
LEFT JOIN {{ ref('balances_ethereum_erc20_noncompliant') }}  as nc
   ON b.token_address = nc.token_address
WHERE r.contract_address is null
and nc.token_address is null
```

[transfers\_ethereum\_schema.yml](https://github.com/duneanalytics/spellbook/blob/master/spellbook/models/transfers/ethereum/transfers\_ethereum\_schema.yml)

```yaml
  - name: balances_ethereum_erc20_day
    meta:
      blockchain: ethereum
      sector: balances
      project: erc20
      contibutors: soispoke, dot2dotseurat
    config:
      tags: ['balances', 'ethereum', 'erc20', 'day', 'soispoke', 'dot2dotseurat']
    description: >
        Daily token balances of ERC20 Ethereum tokens per wallet and contract address pair.
        Depends on erc20_ethereum_transfers.
    columns:
      - *blockchain
      - &day
        name: day
        description: "UTC event block time truncated to the day mark"
      - *wallet_address
      - *token_address
      - *amount_raw
      - *amount
      - *amount_usd
      - *symbolyam
```
