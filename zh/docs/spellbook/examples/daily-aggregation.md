---
title: Daily Aggregation
---

This sums all transfers for the day. This table is materialized as an incrementally loaded table updated every 15 minutes because the next step includes a slower \`[window](https://spark.apache.org/docs/latest/sql-ref-syntax-qry-select-window.html)\` function to capture a rolling sum.

There are a few novel components to make this spell incremental:

The `<div data-gb-custom-block data-tag="if"> </div>` JINJA block allows us to add an arbitrary filter when running in “incremental” mode. Incremental mode is default and a full refresh is denoted by a command line arg to completely recreate the table.

Here we use this block to filter for all data timestamped in the last two days. We are running this model every fifteen minutes, but we allow a look back of 2 days to account for data arriving late from the blockchain.

Does that create duplicates? It would, but we are also using a “`merge`” incremental\_strategy. Merge strategies require a unique key and deduplicate the table upon each update. You’ll see above in the transfers view, we created our own `'unique_transfer_id'` by coalescing several transfer features together that we utilize here.

You’ll also note that this is the first use of “refs” in this spellset. A ref, like `{{ ref('tokens_ethereum_erc20') }}` is simply a reference to another model in the DBT project. It doesn’t matter what the name of the view or table is. The ref references the name of the file itself. That means, we can’t have duplicate file names.

[transfers\_ethereum\_erc20\_agg\_day.sql](https://github.com/duneanalytics/spellbook/blob/master/spellbook/models/transfers/ethereum/erc20/transfers\_ethereum\_erc20\_agg\_day.sql)

```sql
{{ config(
       alias ='erc20_agg_day',
       materialized ='incremental',
       file_format ='delta',
       incremental_strategy='merge',
       unique_key='unique_transfer_id'
       )
}}

select
   'ethereum' as blockchain,
   date_trunc('day', tr.evt_block_time) as day,
   tr.wallet_address,
   tr.token_address,
   t.symbol,
   sum(tr.amount_raw) as amount_raw,
   sum(tr.amount_raw / power(10, t.decimals)) as amount,
   unique_tx_id || '-' || wallet_address || '-' || token_address || '-' || sum(tr.amount_raw)::string as unique_transfer_id
from {{ ref('transfers_ethereum_erc20') }} tr
left join {{ ref('tokens_ethereum_erc20') }} t on t.contract_address = tr.token_address

{% raw %}
{% if is_incremental() %}
-- this filter will only be applied on an incremental run
where date_trunc('day', tr.evt_block_time) > now() - interval 2 days
{% endif %}
{% endraw %}
group by
   date_trunc('day', tr.evt_block_time), tr.wallet_address, tr.token_address, t.symbol,unique_tx_id
```

[transfers\_ethereum\_schema.yml](https://github.com/duneanalytics/spellbook/blob/master/spellbook/models/transfers/ethereum/transfers\_ethereum\_schema.yml)

```yaml
  - name: transfers_ethereum_erc20_agg_hour
    meta:
      blockchain: ethereum
      sector: transfers
      project: erc20
      contibutors: soispoke, dot2dotseurat
    config:
      tags: ['transfers', 'ethereum', 'erc20', 'agg_hour', 'soispoke', 'dot2dotseurat']
    columns:
      - *blockchain
      - &hour
        name: hour
        description: "UTC event block time truncated to the hour mark."
      - *wallet_address
      - *token_address
      - name: symbol
        description: "ERC20 token symbol"
      - *amount_raw
      - name: amount
        description: "Raw amount of ERC20 token held *after* taking into account token decimals"
      - name: amount_usd
        description: "Amount of ERC20 token held in USD (fiat value at time of transaction)"
```
