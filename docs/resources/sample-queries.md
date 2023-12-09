---
title: Sample Queries
description: Learn how to make use of popular tables and spells on Dune
---

# Sample Queries  
   
Refer to this [Dune Dashboard](https://dune.com/resident_wizards/sample-queries){:target="_blank"}, a collection of commonly requested queries over time, and this list will continue to grow! Don't find the query that you need? Check out the [Dune AI](https://dune.com/ai){:target="_blank"} or head down to our [Discord](https://discord.gg/dunecom).



### Getting Total Supply Of ERC20 Token 

[Getting Total Supply of ERC20 Token Query](https://dune.com/queries/3265730){:target="_blank"}

To get the total supply of ERC20 token, we can make use of the erc20's Transfer event that is emitted on every transfers. 

For every token that are minted, there will be an event emitted from these transfers from the blackhole address(`0x0000000000000000000000000000000000000000`), and when tokens are burned, they will usually get sent to the similar address as well.

```
SELECT SUM(case when "from" = 0x0000000000000000000000000000000000000000 THEN (value/1e18) ELSE -(value/1e18) END) as lp_supply
from erc20_ethereum.evt_transfer
where contract_address = 0x046eee2cc3188071c02bfc1745a6b17c656e3f3d -- erc20 token address
and ("from" = 0x0000000000000000000000000000000000000000 or "to" = 0x0000000000000000000000000000000000000000)
-- to filter transfers that are sent from or receiving from the blackhole address
```

What this query does:

- Get all erc20 token transfer that originates and received by the blackhole address

- Check if it is minted from blackhole address, sum them up, if not subtract them

We can make use of the `erc20_ethereum.evt_transfer` table, to get the total supply. As the `erc20_ethereum.evt_transfer` table contains all erc20 tokens' transfer, you have to filter by `contract_address`,sender(`from`) and recipient(`to`).


Next, you'll need to sum up all the transfer events, adding when token is minted `"from" = 0x0000000000000000000000000000000000000000` and subtracting when token is burned(sent to blackhole address(`to = 0x0000000000000000000000000000000000000000`))

This is done here, using `CASE` function to get the aggregated amount.

```
SELECT SUM(case when "from" = 0x0000000000000000000000000000000000000000 THEN (value/1e18) ELSE -(value/1e18) END)
```

You can then verify the token supply on blockchain explorer!

<a id="current-erc20-holder"></a>

### Getting All Token Holders Of ERC20 Token

[Getting All ERC20 Token Holders' Balance](https://dune.com/queries/2753189){:target="_blank"}

Similarly to getting total supply of ERC20 token, we will make use of the erc20's Transfer event table to achieve this.

For every erc20 transfers that each wallet received / sent out, we can just aggregate them up and grouping by the wallet address.

```
SELECT address,
       symbol,
       SUM(amount) as balance
FROM (
-- transactions that address having token outflows
SELECT tr."from" AS address,
       symbol,
       contract_address,
       -(tr.value/POW(10,decimals)) AS amount
FROM erc20_ethereum.evt_transfer tr JOIN tokens.erc20 USING (contract_address)
WHERE "from" != 0x0000000000000000000000000000000000000000 -- exclude mint/burn addresses
AND contract_address = 0x046eee2cc3188071c02bfc1745a6b17c656e3f3d -- contract_address of the erc20 token 
UNION ALL
-- transactions that address having token inflows
SELECT tr."to" AS address,
       symbol,
       contract_address,
       (tr.value/POW(10,decimals)) AS amount
FROM erc20_ethereum.evt_transfer tr JOIN tokens.erc20 USING (contract_address)
 WHERE "to" != 0x0000000000000000000000000000000000000000 -- exclude mint/burn addresses
 AND contract_address = 0x046eee2cc3188071c02bfc1745a6b17c656e3f3d -- contract_address of the erc20 token
 ) x
 GROUP BY address,symbol
 HAVING SUM(amount) > 0.1 --  having more than 0.1 balance
 ORDER BY 3 DESC
```

What this query does:

- Get all erc20 token transfer but exclude blackhole address 

- Get the token decimals from tokens.erc20 table

- Get the sum inflows and subtract outflows

```
FROM erc20_ethereum.evt_transfer tr JOIN tokens.erc20 USING (contract_address)
```

As token decimals varies, we can make use of the `tokens.erc20` table, which contains the token mapping to get the `symbol` and `decimals`.
We then divide the value by the token decimals(`tr.value/POW(10,decimals)`) to get the amount.

To get the balance of each user, you'll need to get to sum up inflows(`"to"`) and subtracting outflows(`"from"`) to get the current balance.
We then aggregate all the values from the events,to get the current balance of each holder(`GROUP BY address,symbol`).

- You can also add in a filter to remove holders that are holding dust amount (` HAVING SUM(amount) > 0.1`)
- You can also add in a filter to get the top X holders (`LIMIT 100`) at the end of query

### Getting Current ETH balance

```
    -- outbound transfers
    SELECT SUM(amount) as current_eth_balance FROM (
    SELECT "from" AS address,
           -CAST(tr.value AS DOUBLE)/POWER(10,18) AS amount,
           tx_hash
    FROM ethereum.traces tr
    WHERE "from" = 0x29ffea86733d7feac7c353343f300e99b8910c77
    AND success
    AND (call_type NOT IN ('delegatecall', 'callcode', 'staticcall') OR call_type IS null)

    UNION ALL

    -- inbound transfers
    SELECT to AS address, (CAST(value AS DOUBLE)/POWER(10,18)) AS amount,tx_hash
    FROM ethereum.traces
    WHERE to = 0x29ffea86733d7feac7c353343f300e99b8910c77
    AND success
    AND (call_type NOT IN ('delegatecall', 'callcode', 'staticcall') OR call_type IS null)

    UNION ALL
    
    -- gas costs
    SELECT "from" AS address, -(CAST(gas_used AS DOUBLE)/POWER(10,18) * CAST(gas_price AS DOUBLE)),hash
    FROM ethereum.transactions et
    WHERE "from" = 0x29ffea86733d7feac7c353343f300e99b8910c77
    ) x
```

What this query does:

- Get all outbound and inbound transfers from `traces` table

- Get all gas costs from the `transactions` table

- Aggregate all transfers, summing up the inflows and subtracting outflows and gas fee

For ETH on mainnet, you will have to use the `ethereum.traces`. They do not appear in erc20 transfer table as it is not an erc20 token.

### Getting Number Of ERC20 Token Holders Over Time

[Getting Number Of ERC20 Token Holders Over Time](https://dune.com/queries/2749329){:target="_blank"}

Getting the number of holders over time will require you to modify [the previous example](#current-erc20-holder). From the transfer events, you will only get records of addresses that have transfer events on the particular day. To ensure that there will be no gaps in between, you will need to generate a date series and backfill with the previous date's data.

```
WITH user_balance AS (
SELECT date,
       address,
       SUM(SUM(amount)) OVER (PARTITION BY address ORDER BY date) as daily_cumulative_balance -- get the cumulative balance of the holders
FROM (
SELECT date_trunc('day',evt_block_time) as date,
       tr."from" AS address,
       -(tr.value/1e18) AS amount
FROM erc20_ethereum.evt_transfer tr
WHERE "from" != 0x0000000000000000000000000000000000000000 -- exclude mint/burn addresses
AND contract_address = 0x046eee2cc3188071c02bfc1745a6b17c656e3f3d -- contract_address of the erc20 token 
UNION ALL
SELECT date_trunc('day',evt_block_time) as date,
tr."to" AS address,
(tr.value/1e18) AS amount
FROM erc20_ethereum.evt_transfer tr
 WHERE "to" != 0x0000000000000000000000000000000000000000 -- exclude mint/burn addresses
 AND contract_address = 0x046eee2cc3188071c02bfc1745a6b17c656e3f3d -- contract_address of the erc20 token 
 ) x
 GROUP BY date,address
),

setLeadData as (
SELECT *,lead(date,1,NOW()) OVER (PARTITION BY address ORDER BY date) as latest_day FROM user_balance
),

gs as (
SELECT date FROM UNNEST(sequence(CAST('2023-06-28' AS TIMESTAMP),CAST(NOW() AS TIMESTAMP),interval '1' day)) as tbl(date)
),

getUserDailyBalance as (
SELECT gs.date,
       address,
       daily_cumulative_balance
FROM setLeadData g
INNER JOIN gs ON g.date <= gs.date AND gs.date < g.latest_day
WHERE daily_cumulative_balance > 1/1e12
)

SELECT date,
       COUNT(address) as holders,
       COUNT(address) - LAG(COUNT(address)) OVER (ORDER BY date) as change 
FROM getUserDailyBalance
GROUP BY 1
ORDER BY 1 DESC
```

What this query does:

- Get addresses' balance of available dates

- Generate date series to ensure no gaps in between

- Subtract previous day data to get the daily change

```
SUM(SUM(amount)) OVER (PARTITION BY address ORDER BY date) as daily_cumulative_balance
```

This windows function will sum up all the amount(`token transfer amount`) cumulatively, to get the token balance of each address on that particular day, which you have to aggregate them by date and address (`GROUP BY date,address`)

```
setLeadData as (
SELECT *,lead(date,1,NOW()) OVER (PARTITION BY address ORDER BY date) as latest_day FROM user_balance
),

gs as (
SELECT date FROM UNNEST(sequence(CAST('2023-06-28' AS TIMESTAMP),CAST(NOW() AS TIMESTAMP),interval '1' day)) as tbl(date)
),
```

- `setLeadData`: This will get the next available date of the address (`PARTITION BY address`), in an ascending date order (`ORDER BY date`)
- `gs`: This will help you to generate a date series, which you can set the start and end date of the timeframe, in the above example its `2023-06-28` as start date and `NOW()` as current date

```
getUserDailyBalance as (
SELECT gs.date,
       address,
       daily_cumulative_balance
FROM setLeadData g
INNER JOIN gs ON g.date <= gs.date AND gs.date < g.latest_day
WHERE daily_cumulative_balance > 0.01
)
```

With the generated date series(`gs` CTE), you will just have to join it with the `setLeadData` CTE to get the daily balance of each address since inception!

- You can also add in a filter to remove dusts (`WHERE daily_cumulative_balance > 0.01`)

Once you have the daily balance of each user, you can now get the daily number of holders by simply aggregating the number of addresses on each day. You can also get the daily change in token holders by taking each day's holder count and subtracting previous day's holder count (`COUNT(address) - LAG(COUNT(address)) OVER (ORDER BY date) as change `)

### Getting ERC20 Token Transaction Value In USD

[Top 100 Transfers In USD Into Binance](https://dune.com/queries/3269085){:target="_blank"}

You are able to get the token amount for transfers from the `erc20 evt transfer` table, to get the usd amount, you will need to join with the prices table (`prices.usd`)

```
select "from" as sender,
       symbol,
       value/POW(10,decimals) as token_amount,
       value/POW(10,decimals) * price as token_usd
from erc20_ethereum.evt_transfer a 
LEFT JOIN prices.usd b ON date_trunc('minute',a.evt_block_time) = b.minute AND a.contract_address = b.contract_address
where "to" = 0x28c6c06298d514db089934071355e5743bf21d60
and evt_block_time >= NOW() - interval '24' hour
ORDER BY 4 DESC
LIMIT 1000
```

What this query does:

- Get token transfers into Binance 14 Hot Wallet

- Join the prices table to get token price

- Filter to only get latest 24 hour data and limiting to 1000 records

The above query shows you the top 1000 deposits in the past 24 hours (`evt_block_time >= NOW() - interval '24' hour`). You can simply just do a JOIN with the `prices.usd` table, with the erc20 token contract address (`contract_address`) and datetime of the transaction (`date_trunc('day',evt_block_time)`).

- The `date_trunc` here is required as there are milliseconds in the `evt_block_time`, to match the minute-level data in `prices.usd`


### Getting Current NFT Holders For A Specific Collection

[Getting Current NFT Holders](https://dune.com/queries/2858082){:target="_blank"}

You can make use of the `erc721_ethereum.evt_trasnfer` table to get the holders of a NFT collection. The example below identifies the current holders of Bored Ape Yacht Club(BAYC) collection. For ERC721 nft token, each of them have a unique token number (`tokenId`). 

```
SELECT "to" as address,
        COUNT(*) as nft_count,
        ARRAY_AGG(tokenId) as nft_list
FROM (
select contract_address,
       to,
       tokenId,
       ROW_NUMBER() OVER (PARTITION BY tokenId ORDER BY evt_block_time DESC,evt_index DESC) as rn
from erc721_ethereum.evt_transfer
where contract_address = 0xBC4CA0EdA7647A8aB7C2061c2E118A18a936f13D -- bayc address
) x
WHERE rn = 1
GROUP BY 1
```

What this query does:

- Get the recipients (`to`)

- Get the token number (`tokenId`)

- Create a sequential numbering of rows to rank the deposits using `ROW_NUMBER()` windows function

- To get the latest transfer of each token (`PARTITION BY tokenId ORDER BY evt_block_time DESC,evt_index DESC`)

We will just need to identify the latest recipient of each NFT token and we will just remove all other transactions (`WHERE rn = 1`).

Aggregate by address will get you all current holders of BAYC collection!

### Querying Logs Table For Specific Event (Topics)

[$ARKM Claimers From Logs Table](https://dune.com/queries/3269288){:target="_blank"}

```
SELECT block_time,
       varbinary_ltrim(topic1) as address,
       varbinary_to_uint256(topic2)/1e18 as amount_claimed
FROM ethereum.logs
where contract_address = 0x08c7676680f187a31241e83e6d44c03a98adab05
and topic0 = 0xd8138f8a3f377c5259ca548e70e4c2de94f129f5a11036a15b69513cba2b426a
order by 3 desc
```

What this query does:

- Querying logs table by filtering the contract address (`contract_address`) and event signature(`topic0`)

- Using varbinary functions to get the decoded data

The `ethereum.logs` table is one of the raw tables available that contains all events that are emitted. You will need to specify the contract address and topic0 to get the specific events you need. Each event has a unique signature (`topic0`), that you will be able to get this the logs page. [Here is a sample transaction hash of $ARKM claim](https://etherscan.io/tx/0xc127438f51ae6917d7b1b7709d50049162ae41bdac4201b5658cd9cc01c9c591){:target="_blank"}.

<p align="center">
  <img src="../images/etherscan_logs.png"/><br />
  </p>

  Click on the `Logs` tab.

  <p align="center">
  <img src="../images/etherscan-logs-event-sample.png"/><br />
  </p>

  In the `Claim` event, you will be able to identify:

  - Address : `contract_address`

  - Event signature  : `topic0`

  - Account : `topic1`

  - Amount : `topic2`


  ```
  varbinary_ltrim(topic1) as address, -- removes the zeros
  varbinary_to_uint256(topic2)/1e18 as amount_claimed -- converting varbinary to uint256
  ```

  In the `logs` table, they are raw data hence you will need to use [varbinary functions](https://dune.com/docs/query/DuneSQL-reference/Functions-and-operators/varbinary/?h=bytearray_to_uint#varbinary-functions){:target="_blank"} to decode them.

  Since $ARKM token has 18 decimals, we use `/1e18` to get the actual amount that each address claimed.

  It is advisable to get the contracts to be [decoded at Dune](https://dune.com/contracts/new){:target="_blank"} as querying from the raw tables can take a long time as they contain all the events emitted! To understand more about decoded tables, check out our [Decoding Docs](https://dune.com/docs/app/decoding-contracts/){:target="_blank"}.


### Querying Logs Table For Specific Event (Topics and Data)

[Swap Event From Logs Table](https://dune.com/queries/3269338){:target="_blank"}

```
select varbinary_ltrim(topic1) as sender, -- topic1
       varbinary_ltrim(topic2) as recipient, -- topic2
       varbinary_to_int256(varbinary_substring(data,1,32)) as amount0, -- int256
       varbinary_to_int256(varbinary_substring(data,33,32)) as amount1, -- int256
       varbinary_to_uint256(varbinary_substring(data,65,32)) as price, -- uint160
       varbinary_to_uint256(varbinary_substring(data,97,32)) as liquidity, -- uint128
       varbinary_to_int256(varbinary_substring(data,129,32)) as tick -- int24
from arbitrum.logs
where contract_address = 0x3ab5dd69950a948c55d1fbfb7500bf92b4bd4c48
and topic0 = 0xc42079f94a6350d7e6235f29174924f928cc2ac818eb64fed8004e115fbcca67
and tx_hash = 0x0807434b7d837f5feffe4cf3ee0c024bf38ebf58372dcb0e77f9b61b04ee6a1f
```

<p align="center">
  <img src="../images/etherscan-logs-event-data.png"/><br />
</p>

What this query does:

- Querying logs table by filtering the contract address (`contract_address`) and event signature(`topic0`)

- Using varbinary functions to get the decoded data from both topics and data column

In the `Swap` event, you will be able to identify:

- Sender : `topic1`

- Recipient : `topic2`

- amount0,amount1,price,liquidity,tick : `data` 

In the `data` column, it contains all the data payload for `amount0,amount1,price,liquidity,tick`. We will have to make use of the `varbinary functions` to slice the data and convert to the correct data type.

```
select varbinary_ltrim(topic1) as sender, -- topic1
    varbinary_ltrim(topic2) as recipient, -- topic2
    varbinary_to_int256(varbinary_substring(data,1,32)) as amount0, -- int256
    varbinary_to_int256(varbinary_substring(data,33,32)) as amount1, -- int256
    varbinary_to_uint256(varbinary_substring(data,65,32)) as price, -- uint160
    varbinary_to_uint256(varbinary_substring(data,97,32)) as liquidity, -- uint128
    varbinary_to_int256(varbinary_substring(data,129,32)) as tick -- int24
```

The above codes make use of the [varbinary functions](https://dune.com/docs/query/DuneSQL-reference/Functions-and-operators/varbinary/?h=bytearray_to_uint#varbinary-functions){:target="_blank"} to decode. We will be able to identify which varbinary function to use based on the datatype of each variable. 

  As it can get complicated as there is no restriction on the data payload, it is advisable to get the contracts to be [decoded at Dune](https://dune.com/contracts/new){:target="_blank"} as querying from the raw tables can take a long time as they contain all the events emitted! To understand more about decoded tables, check out our [Decoding Docs](https://dune.com/docs/app/decoding-contracts/){:target="_blank"}.







  


































