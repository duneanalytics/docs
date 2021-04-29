# Users and amount over a trailing period

```sql
SELECT  date_trunc('day', evt_block_time),
        COUNT (DISTINCT buyer),
        SUM(eth_bought / 1e18)
FROM uniswap."Exchange_evt_EthPurchase" p
WHERE evt_block_time > now() - interval '7 days'
GROUP BY 1
ORDER BY 1;
```

