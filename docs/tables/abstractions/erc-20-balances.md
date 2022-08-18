---
description: >-
  ERC20 token analysis is a fundamental part of any analysis of DeFi products,
  these tables and views will provide you with all the necessary information.
---

# ERC-20 balances

## Easily track wallets and token balances over time.

The following tables allow for easy tracking or wallet-balances, token allocations or supply of a token over time or in a snapshot format.

On a raw data level it's pretty hard to work with erc20 tokens since you need to sum all transfers for all addresses over time. This unnecessarily bloats queries and quickly leads to human errors. To prevent that from happening we have constructed several views and tables that will help you query for erc20 data with ease.

These tables can be used for all kinds of interesting analysis, but you still need to watch out for a few things while working with them:

* the **mint/burn address** is not standardized, so you need to find out those addresses and manually apply a fix in your queries. In most cases it will be `x0000000000000000000000000000000000000000` for minting and burning, but always make sure that that is indeed the case. In the example given that's exactly not the case, there is an additional burn address `x000000000000000000000000000000000000dead`.

**example:**

```sql
Select 
    wallet_address, 
    amount,
    day,
    token_symbol
from erc20."view_token_balances_daily"
where token_address = '\x429881672B9AE42b8EbA0E26cD9C73711b891Ca5'
and wallet_address != '\x0000000000000000000000000000000000000000' --mint address
and wallet_address != '\x000000000000000000000000000000000000dead' --burn address
```

* working with these tables quickly leads to a lot of individual data points that our visualization engine is not always able to handle perfectly. Instead of trying to display every unique holder it makes sense to group them by certain criteria and display the dataset that way. This is unique for every token, you might need to experiment a bit to see what works in your queries.

```sql
Select 

     CASE   WHEN wallet_address = '\xbBCf169eE191A1Ba7371F30A1C344bFC498b29Cf' then 'dill'
            WHEN wallet_address = '\xdc98556Ce24f007A5eF6dC1CE96322d65832A819' then 'uniswap'
            WHEN wallet_address = '\xC52139a20A57c9002e9F5188901EF0ffC63c7205' then 'smart_treasury'
            WHEN wallet_address = '\x40ec5b33f54e0e8a33a975908c5ba1c14e5bbbdf' then 'polygon'
            WHEN wallet_address = '\x6cc5f688a315f3dc28a7781717a9a798a59fda7b' then 'OKEX'
            WHEN amount     between  0      and 10        then 'Plankton(0-10)'
            WHEN amount     between 10     and 100        then 'shrimp(10-100)'
            WHEN amount     between 100    and 1000       then 'fish(100-1,000)'
            WHEN amount     between 1000    and 10000     then 'dolphin(1,000-10,000)'
            WHEN amount     > 10000                       then 'whale (>10000)' 
           --note that the order of case statements matters here
    end as classification,

sum(amount) as amount,
token_symbol
from erc20."view_token_balances_latest"
where token_address = '\x429881672B9AE42b8EbA0E26cD9C73711b891Ca5'
and wallet_address != '\x0000000000000000000000000000000000000000'
and wallet_address != '\x000000000000000000000000000000000000dead'
and amount > 0.1 --filter out dust amounts, adjust this for different tokens based on economic value
group by 1,3
```

## Dashboard example:

This dashboard contains the most important use cases related to a single erc20 token that is used as gov token.

[https://dune.com/0xBoxer/pickle-finance\_1](https://dune.com/0xBoxer/pickle-finance\_1)

## erc20.view\_token\_balances\_latest

This view depends on the erc20.token\_balances table and gives you the information of the latest distribution of that token.

| column name                   | data type   | description                                                                                |
| ----------------------------- | ----------- | ------------------------------------------------------------------------------------------ |
| amount                        | numeric     | the correct display format for that token                                                  |
| amount\_raw                   | numeric     | the raw amount of that token (need to divide by decimals!)                                 |
| amount\_usd                   | float8      | the current price (if we have data on the price)                                           |
| last\_transfer\_\_\_timestamp | timestamptz | the date on which the balance of this token last changed in this particular wallet address |
| token\_address                | bytea       | the address of the token                                                                   |
| token\_symbol                 | text        | the symbol of the token                                                                    |
| wallet\_address               | bytea       | the address of the wallet holding this token                                               |

## erc20.view\_token\_balances\_hourly

This table will provide information about all token balances on an hourly basis. It also already includes decimals and prices in most cases, so they are pretty much ready to go out of the box.

| column name     | data type   | description                                                |
| --------------- | ----------- | ---------------------------------------------------------- |
| amount          | numeric     | the correct display format for that token                  |
| amount\_raw     | numeric     | the raw amount of that token (need to divide by decimals!) |
| amount\_usd     | float8      | the current price (if we have data on the price)           |
| hour            | timestamptz | the time in the resolution of hours                        |
| token\_address  | bytea       | the address of the token                                   |
| token\_symbol   | text        | the symbol of the token                                    |
| wallet\_address | bytea       | the address of the wallet holding this token               |

## erc20.view\_token\_balances\_daily

**This table will perform much better than `erc20.view_token_balances_hourly` since it's only querying for data on a daily basis**. If you want to make high level analysis, this is your way to go.

| column name     | data type   | description                                                |
| --------------- | ----------- | ---------------------------------------------------------- |
| amount          | numeric     | the correct display format for that token                  |
| amount\_raw     | numeric     | the raw amount of that token (need to divide by decimals!) |
| amount\_usd     | float8      | the current price (if we have data on the price)           |
| day             | timestamptz | the time in the resolution of days                         |
| token\_address  | bytea       | the address of the token                                   |
| token\_symbol   | text        | the symbol of the token                                    |
| wallet\_address | bytea       | the address of the wallet holding this token               |

## erc20.token\_balances

This table contains the hourly balance of all erc20 tokens over the entire existence of these tokens. You can use this table as a fallback option might the views we have provided above not be sufficient for the usecase you are trying to establish.

| column name     | data type   | description                                                |
| --------------- | ----------- | ---------------------------------------------------------- |
| amount          | numeric     | the correct display format for that token                  |
| amount\_raw     | numeric     | the raw amount of that token (need to divide by decimals!) |
| timestamp       | timestamptz | the time in the resolution of hours                        |
| token\_address  | bytea       | the address of the token                                   |
| token\_symbol   | text        | the symbol of the token                                    |
| wallet\_address | bytea       | the address of the wallet holding this token               |
