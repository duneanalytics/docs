# ETH Balance of a wallet

This Query yields the ETH balance of a wallet over time.

```sql
SELECT date_trunc('day', block_time) as day, sum(-value/1e18) as transfer
        FROM ethereum."traces"
        WHERE "from" = '\x99C9fc46f92E8a1c0deC1b1747d010903E884bE1' --optimism bridge
        AND (LOWER(call_type) NOT IN ('delegatecall', 'callcode', 'staticcall') or call_type is null)
        AND "tx_success" = true
        AND success = true
        GROUP BY 1
        
        UNION all
        
        SELECT
        date_trunc('day', block_time) as day, sum(value/1e18) as transfer
        FROM ethereum."traces"
        WHERE "to" = '\x99C9fc46f92E8a1c0deC1b1747d010903E884bE1' --optimism bridge
        AND (LOWER(call_type) NOT IN ('delegatecall', 'callcode', 'staticcall') or call_type is null)
        AND "tx_success" = true
        AND success = true
        GROUP BY 1
        
        UNION ALL --gas costs
        
        SELECT
        date_trunc('day', block_time) as day, -SUM(gas_price*"gas_used")/1e18 as transfer
        FROM ethereum."transactions"
        WHERE "from" = '\x99C9fc46f92E8a1c0deC1b1747d010903E884bE1' --optimism bridge
        GROUP BY 1
```

Original author: [https://twitter.com/MSilb7](https://twitter.com/MSilb7)
