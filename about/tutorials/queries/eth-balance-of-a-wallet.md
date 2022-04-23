# ETH Balance of a wallet

This Query yields the ETH balance of a wallet over time.

```sql
Select sum(transfer) over (order by day asc), day
from (

SELECT date_trunc('day', block_time) as day, sum(-value/1e18) as transfer
        FROM ethereum."traces"
        WHERE "from" = '\xb66284947F9A35bD9FA893D444F19033FeBdA4A1' --optimism bridge
        AND (LOWER(call_type) NOT IN ('delegatecall', 'callcode', 'staticcall') or call_type is null)
        AND "tx_success" = true
        AND success = true
        GROUP BY 1
        
        UNION all
        
        SELECT
        date_trunc('day', block_time) as day, sum(value/1e18) as transfer
        FROM ethereum."traces"
        WHERE "to" = '\xb66284947F9A35bD9FA893D444F19033FeBdA4A1' --optimism bridge
        AND (LOWER(call_type) NOT IN ('delegatecall', 'callcode', 'staticcall') or call_type is null)
        AND "tx_success" = true
        AND success = true
        GROUP BY 1
        
        UNION ALL --gas costs
        
        SELECT
        date_trunc('day', block_time) as day, -SUM(gas_price*"gas_used")/1e18 as transfer
        FROM ethereum."transactions"
        WHERE "from" = '\xb66284947F9A35bD9FA893D444F19033FeBdA4A1' --optimism bridge
        GROUP BY 1
    ) as x
```

Original author: [https://twitter.com/MSilb7](https://twitter.com/MSilb7)
