# Token (and USD value) per token over time for an address

Note that this query can get very heavy when there are many tokens and transfers over a long period of time.

```sql
WITH transfers AS (
    
    SELECT  day,
            address, 
            token_address, 
            sum(amount) AS amount -- Net inflow or outflow per day
    FROM
    
    (
        SELECT  date_trunc('day', evt_block_time) AS day,
                "to" AS address,
                tr.contract_address AS token_address,
                value AS amount
        FROM erc20."ERC20_evt_Transfer" tr
        WHERE "to" = '\x70c730465dff5447a12bae37090446745c9edccc' --Filter for holding address
        -- AND contract_address = '\xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2' -- Filter for token address if you only want to see a specific token
        
        UNION ALL
        
        SELECT  date_trunc('day', evt_block_time) AS day,
                "from" AS address,
                tr.contract_address AS token_address,
                -value AS amount
        FROM erc20."ERC20_evt_Transfer" tr
        WHERE "from" = '\x70c730465dff5447a12bae37090446745c9edccc' --Filter for holding address
        -- AND contract_address = '\xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2' -- Filter for token address if you only want to see a specific token
    ) t
   GROUP BY 1, 2, 3
   )

, balances_with_gap_days AS (
    SELECT  t.day,
            address,
            t.token_address,
            SUM(amount) OVER (PARTITION BY token_address, address ORDER BY t.day) AS balance, -- balance per day with a transfer
            lead(day, 1, now()) OVER (PARTITION BY token_address, address ORDER BY t.day) AS next_day -- the day after a day with a transfer
    FROM transfers t
    )
    
 , days AS (
    SELECT generate_series('2020-07-01'::timestamp, date_trunc('day', NOW()), '1 day') AS day -- Generate all days since the first contract
    )
    
, balance_all_days AS (
    SELECT  d.day,
            address,
            erc.symbol,
            b.token_address,
            SUM(balance/10^decimals) AS balance
    FROM balances_with_gap_days b
    INNER JOIN days d ON b.day <= d.day AND d.day < b.next_day -- Yields an observation for every day after the first transfer until the next day with transfer
    INNER JOIN erc20.tokens erc ON b.token_address = erc.contract_address
    GROUP BY 1, 2, 3, 4
    ORDER BY 1, 2, 3, 4
    )

SELECT  b.day,
        b.symbol,
        b.token_address,
        SUM(balance) AS token_balance,
        SUM(balance*p.price) AS balance_usd_value
FROM balance_all_days b
LEFT JOIN  ( 
                SELECT  date_trunc('day', p.minute) as day,
                        contract_address,
                        symbol,
                        decimals,
                        AVG(p.price) as price
                FROM prices."usd" p
                GROUP BY 1, 2, 3, 4
            ) p ON b.day = p.day AND b.token_address = p.contract_address
GROUP BY 1,2,3
ORDER BY 1,2,3
;

```
