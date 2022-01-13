# total supply over time of a token



You can either use that token's specific tables as long as they are [decoded](../../../data-tables/data-tables/decoded-data.md):

```sql
SELECT
week,
SUM(transfer) over (order by week)
FROM 
 (
    SELECT
    date_trunc('week', evt_block_time) as week,
    sum(amount/1e18) as transfer
    FROM ptokens."pBTC_evt_Minted" tr
    GROUP BY 1
UNION
    SELECT
    date_trunc('week', evt_block_time) as week,
    sum(-amount/1e18) as transfer
    FROM ptokens."pBTC_evt_Burned" tr
    GROUP BY 1
) as net;
```

Or you can use a more general purpose query like this one:

(Please note that while this works for most tokens, some tokens do have slight changes in their structure that break this query)

```sql
Select 
   sum(amount),
    day
   
from erc20."view_token_balances_daily"
where token_address = '\x429881672B9AE42b8EbA0E26cD9C73711b891Ca5'
and wallet_address != '\x0000000000000000000000000000000000000000' --mint address
and wallet_address != '\x000000000000000000000000000000000000dead' --burn address
group by 2

--mint and burn address are not standardized, make sure to query for the right ones
```

