---
title: prices
description: These tables allow you to get the price of almost all relevant erc20 tokens.
---
The price feeds are derived from [Coinpaprika](https://coinpaprika.com/)'s API. The price is the volume-weighted price based on real-time market data, translated to USD.


## prices.usd

### adding a token to price tracking

If the token has yet to be listed in here, please make a pull request to our [GitHub repository](https://github.com/duneanalytics/spellbook/blob/main/models/prices/prices_tokens.sql)(Make sure that the token is active on Coinpaprika!).

| Column Name       | Data Type     | Description                                                 |
|-------------------|---------------|-------------------------------------------------------------|
| `contract_address`| `varbinary`   | The contract address of the ERC20 token                     |
| `blockchain`      | `varchar`     | The blockchain associated with the ERC20 token              |
| `decimals`        | `int`         | The number of decimal places for the token's value          |
| `minute`          | `timestamp`   | The resolution of this data table in minutes                |
| `price`           | `double`      | The price of the asset in any given minute                  |
| `symbol`          | `varchar`     | The identifier of the asset (ticker)                        |


Note that `WETH` can be used for ETH price as it trades at virtually the same price.

```sql
-- getting the token price for WETH for the past 30 days
select * from prices.usd
where contract_address = 0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2
and blockchain = 'ethereum'
and minute >= NOW() - interval '30' day
```

## Getting the latest token price

We can use prices.usd_latest. Just as the table name suggest, this table contains the latest price available, derived from prices.usd

```sql
-- getting the latest price for 4 tokens 
select * from prices.usd_latest
where blockchain = 'ethereum'
and symbol IN ('WETH','WBTC','USDC','USDT')
```

## How we get prices from DEXs

We created a table that creates price feeds based on decentralized exchange trading data. This table covers much more assets than `prices.usd`, since it covers all assets that are traded on any  of the decentralized exchanges that are indexed in `dex.trades`.

**Please keep in mind that this script can generate wrong prices in rare cases.**

This table is very resource intensive and can therefore only be updated every few hours, please keep that in mind when utilizing it. Also the resolution is only hourly, so if you need minutely prices do refer to [`prices.usd`](prices.md).

The logic of how this table works can be accessed in our [public github](https://github.com/duneanalytics/spellbook/blob/main/models/dex/dex_prices.sql) repo.

This script generates median hourly prices based on data from decentralized exchanges found in `dex.trades`. It will assign asset prices based on a trading pair which has a pricefeed in `prices.usd`.

Let's take the $SPELL/ETH Pool for example.

* $ETH price is contained in `prices.usd`
* $SPELL price is not contained in `prices.usd`

In order to get the $SPELL price, the script will dynamically calculate the price of $SPELL based on the price of $ETH that was exchanged for it.

e.g. 5 $ETH were exchanged for 1,086,083 $SPELL.

Dex.trades will assign a `usd_amount` to this trade based on the $ETH price data in `prices.usd`.

That `usd_amount` is $23,498.

`5 * price of ETH (4.699,6) = $23,498`

Calculating the price of $SPELL is now as simple as dividing the amount of tokens exchanged with the `usd_amount` recorded in `dex.trades`.

`$23,498/1,086,083 ≈ $0,02163`

We now have successfully calculated the price of 1 $SPELL.

In order to correct for extreme outliers and in order for this table to be performant the script then aggregates all recorded data into one `median_price` per hour.

```sql
-- get daily average price of weth from dex.prices
select date_trunc('day',hour) as date,
       contract_address,
       AVG(median_price) as avg_price
from dex.prices
WHERE blockchain = 'ethereum'
AND contract_address = 0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2
AND hour >= NOW() - interval '3' day
GROUP BY 1,2
```

### Known issues

In rare cases this script will generate price feeds that are based on illiquid pairs and therefore report wrong data. This happens when all liquid trading pools of this token do not have a price feed in `prices.usd`.

An example of this would be $PLAY, a metaverse index from PieDAO. The liquid trading pair for this asset is $PLAY/$DOUGH. The "correct" price of $PLAY is represented in this pool, but the combination of `dex.trades` and `dex.prices` are not able to pick up this price.

Instead, `dex.trades` will only have a `usd_amount` for illiquid pairs of this asset. In this case, the $PLAY/$ETH pool has trades once in a while and these will have a `usd_amount` in `dex.trades`. The liquidity of the $PLAY/$ETH pool is very low and it pretty much only consists of arbitrage trades. Therefore, the resulting pricefeed in `dex.prices` is faulty since it depends on the `usd_amount` in `dex.trades`.

In order to check for this, you should manually verify the results of `dex.prices` in order to make sure arbitrage trades do not disturb the price feed constructed. A simple way of validating that the script is working with the right pools is checking the `sample_size` column. If the number seems suspiciously low, the script probably doesn't pick up the right price.

In cases like this, you have to manually construct a price feed.

We are always looking to improve this table, if you have any ideas or comments don't hesitate to open a PR or contact us in our Discord.



