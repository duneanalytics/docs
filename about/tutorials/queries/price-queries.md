# price queries

### Centralized exchange price data

```sql
Select 
    minute, 
    price, 
    symbol 
from prices.usd

WHERE symbol = '{{1. Symbol}}'

and minute > now() - interval '1hour'
```

### Decentralized exchange price data

```sql
Select 
    hour, 
    median_price, 
    d."contract_address"
from dex."view_token_prices" d
left join erc20.tokens e on d.contract_address = e.contract_address
WHERE symbol = '{{1. Symbol}}'

and hour > now() - interval '1000hour'
```

This Query depends on the erc20.tokens table and can have gaps when there are no trades that been committed in that hour.

For a better but more complicated to navigate version use this:

```sql
with dex_trades AS (
        SELECT 
            token_a_address as contract_address, 
            usd_amount/token_a_amount as price,
            block_time
        FROM dex.trades
        WHERE 1=1
        AND usd_amount  > 0
        AND category = 'DEX'
        AND token_a_amount > 0
        AND token_a_address  = CONCAT('\x', substring('{{1. token_address}}' from 3))::bytea
        
        UNION ALL 
        
        SELECT 
            token_b_address as contract_address, 
            usd_amount/token_b_amount as price,
            block_time
        FROM dex.trades
        WHERE 1=1
        AND usd_amount  > 0
        AND category = 'DEX'
        AND token_b_amount > 0
        AND token_b_address  = CONCAT('\x', substring('{{1. token_address}}' from 3))::bytea
        
    ),
    
    
    rawdata as (

    SELECT 
        date_trunc('hour', block_time) as hour,
        d.contract_address,
        e.symbol as asset,
        (PERCENTILE_CONT(0.5) WITHIN GROUP (ORDER BY price)) AS price,
        count(1) AS sample_size
    FROM dex_trades d
    left join erc20.tokens e on e.contract_address = d.contract_address
    GROUP BY 1, 2, 3

    )

    ,leaddata as 
    (
    SELECT
    hour,
    contract_address,
    asset,
    price,
    sample_size,
    lead(hour, 1, now() ) OVER (PARTITION BY contract_address ORDER BY hour asc) AS next_hour
    from rawdata
    where sample_size > 3
    )
    
    ,hours AS
    (
    SELECT
    generate_series('2020-01-01'::TIMESTAMP, date_trunc('hour', NOW()), '1 hour') AS hour
    )


    
    SELECT
    d.hour as hour,
    contract_address,
    asset,
    price,
    sample_size
    from leaddata b
    INNER JOIN hours d ON b.hour <= d.hour
    AND d.hour < b.next_hour -- Yields an observation for every hour after the first transfer until the next hour with transfer
```

This will return the price by hour according to dex trading data and fill in gaps where there have been no trades commited. You can adjust the sample size of trades required to carry the price data forward in line 53. This can help ammend edge cases where arbritrage bots get weird prices on dexes. If you have issues with this, please reach out to us on Discord.
