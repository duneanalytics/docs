# USD price for a token from Uniswap

The most common and easiest way to get token USD prices on Dune Analytics is with the `prices.usd` table. However, this data is fetched from centralised exchanges so for a long tail of tokens the best approach is to get prices from Uniswap.

This query uses WETH pairs, which is used to map to USD price. The query can be modified to work with any token that has a price in `prices.usd`

You can find this query on Dune [here](https://explore.dune.xyz/queries/11050/source?p\_Token%20address=0xeb4c2781e4eba804ce9a9803c67d0893436bb27d).

```sql
WITH weth_pairs AS ( -- Get exchange contract address and "other token" for WETH
    SELECT cr."pair" AS contract, 
        CASE WHEN cr."token0" = '\xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2' then '0' ELSE '1' END  AS eth_token,
        CASE WHEN cr."token1" = '\xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2' then cr."token0" ELSE cr."token1" END  AS other_token 
    FROM uniswap_v2."Factory_evt_PairCreated" cr
    WHERE token0 = '\xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2' OR  token1 = '\xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2'
    )

, swap AS ( -- Get all trades on the pair last 14 days
    SELECT
        CASE WHEN eth_token = '0' then sw."amount0In" + sw."amount0Out" ELSE sw."amount1In" + sw."amount1Out"
        END/1e18 AS eth_amt, 
        CASE WHEN eth_token = '1' then sw."amount0In" + sw."amount0Out" ELSE sw."amount1In" + sw."amount1Out"
        END/power(10, tok."decimals") AS other_amt, -- If the token is not in the erc20.tokens list you can manually divide by 10^decimals
        tok."symbol",
        tok."contract_address",
        date_trunc('hour', sw."evt_block_time") AS hour
    FROM uniswap_v2."Pair_evt_Swap" sw
    JOIN weth_pairs ON sw."contract_address" = weth_pairs."contract"
    JOIN erc20."tokens" tok ON weth_pairs."other_token" = tok."contract_address"
    WHERE other_token = '\xeb4c2781e4eba804ce9a9803c67d0893436bb27d' --renBTC example
    -- To allow users to submit token address in the Dune UI you can use the below line:
    -- WHERE other_token = CONCAT('\x', substring('{{Token address}}' from 3))::bytea -- Allow user to input 0x... format and convert to \x... format
    AND sw.evt_block_time >= now() - interval '14 days'
    )

, eth_prcs AS (
    SELECT avg(price) eth_prc, date_trunc('hour', minute) AS hour
    FROM prices.layer1_usd_eth
    WHERE minute >= now() - interval '14 days'
    group by 2
    )

SELECT
    AVG((eth_amt/other_amt)*eth_prc) AS usd_price,
    swap."symbol" AS symbol,
    swap."contract_address" AS contract_address,
    eth_prcs."hour" AS hour
FROM swap JOIN eth_prcs ON swap."hour" = eth_prcs."hour"
GROUP BY 2,3,4
;
```
