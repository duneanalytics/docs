# USD value of token utilised for an event

### &#x20;<a href="#usd-value-of-token-utilised-for-an-event" id="usd-value-of-token-utilised-for-an-event"></a>

```sql
SELECT
date_trunc('week', evt_block_time),
SUM(amount/1e18 * p.price) AS staked
FROM numerai."SimpleGriefing_evt_StakeAdded" s --Replace with relevant event
LEFT JOIN prices.usd p ON p.minute = date_trunc('minute', evt_block_time)
WHERE p.symbol = 'NMR' --Replace with relevant token
-- WHERE p.contract_address = s.token_address --In case different tokens
GROUP BY 1;
```

