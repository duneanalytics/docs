# Circulating supply over time of a token with mint/burn functions



###  <a id="Circulating-supply-over-time-of-a-token-with-mintburn-functions"></a>

```text
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

