# Circulating supply over time of a token



You can either use that tokens specific tables as long as they are [decoded](../../data-tables/data-tables/decoded-data.md):

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

\(Please note that while this works for most tokens, some tokens do have slight changes in their structure that break this query\)

```sql
 SELECT
        HOUR,
        SUM(minted) over (order by hour asc) - SUM(burned) over (order by hour asc) as circsupply
        FROM
            (
            SELECT
            t.HOUR,
            SUM(minted) as minted,
            SUM(burned) as burned
            FROM
                (
                select 
                date_trunc('HOUR', time) as HOUR
                from ethereum."blocks"
                Where date_trunc('HOUR', time) >= '2021-01-22'
                group by hour
                order by HOUR asc
                ) as t
                LEFT JOIN
                (
                SELECT date_trunc('HOUR', evt_block_time) AS HOUR,       
                CASE WHEN "from" = '\x0000000000000000000000000000000000000000' THEN (value/10^decimals) ELSE 0 END AS minted,
                CASE WHEN "to"   = '\x0000000000000000000000000000000000000000' THEN (value/10^decimals) ELSE 0 END AS burned
                FROM erc20."ERC20_evt_Transfer" e
                left join erc20.tokens t on t.contract_address = e.contract_address
                WHERE e.contract_address = '\x429881672B9AE42b8EbA0E26cD9C73711b891Ca5'
                ) as raw on t.hour = raw.hour
        group by 1
        order by 1
        ) as agg
```

