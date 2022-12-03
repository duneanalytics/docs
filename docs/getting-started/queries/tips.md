---
title: Query Tips
description: Below you'll find a selection of Query related tips to help you become a more powerful 🧙.
---

Below you'll find a selection of Query related tips to help you become a more powerful 🧙.

If you have a tip you think we should add, [propose a change on this doc in our GitHub repository](https://github.com/duneanalytics/docs/blob/master/docs/getting-started/queries/tips.md)!

## Use Spells

The easiest way to do great analysis with Dune is to use the well-organized data you'll find in [Spells](../../reference/tables/spells/index.md) (Dune V2) and [Abstractions](../../reference/tables/spells/index.md) (Dune V1).

Theses tables, like `dex.trades`, are cleaned and contain data/metadata (like human readable token symbols) that make them very straight forward to query.

## V1 Inline Ethereum Addresses Formatting

!!! warning
    This feature is only available in the Dune V1 engine.

In Dune Ethereum addresses are stored as PostgreSQL byte arrays which are encoded with the `\x` prefix. This differs from the customary `0x` prefix. If you’d like to use an inline address, say to filter for a given token, you would do

```sql
WHERE token = '\x6b175474e89094c44da98b954eedeac495271d0f'
```

which is simply short for

```sql
WHERE token = '\x6b175474e89094c44da98b954eedeac495271d0f'::bytea
```

## Quote Column and Table Names in camelCase

!!! warning
    This feature is only available in the Dune V1 engine.

Column and table names are mostly taken directly from smart contract Application Binary Interfaces (ABIs), with no modification.

Since most smart contracts are written in Solidity, and written with a camelCased naming convention, so are many of Dune’s table and column names

PostgreSQL (Dune V1) requires you to column and table name references are case sensitive:

```sql
SELECT “columnName”
FROM projectname.”contractName_evt_EventName”
LIMIT 10
```

In PostgreSQL, double quotes are reserved for tables and columns, whereas single quotes are reserved for values:

```sql
SELECT “columnName”
FROM projectname.”contratName_evt_eventName”
WHERE contract_address = '\x6B175474E89094C44Da98b954EedeAC495271d0F'
LIMIT 10
```

Schemas are always lowercase in Dune.

## Remove Decimals

Ether transfers and most ERC-20 tokens have 18 decimal places, which most humans agree is too many to read.

To transmute these into a more human-friendly form, use the `erc20.tokens` table and divide the token's `transfer_value` by 10:

=== "PostgreSQL"

    ```sql
    transfer_value / 10^erc20.tokens.decimals
    ```

=== "Spark SQL"

    ```sql
    transfer_value / x*power(10,y)` or `transfer_value / x*1e*y
    ```

## Get time with `date_trunc`

We’ve added `evt_block_time` to [decoded event tables](../../reference/tables/decoded/index.md) for your convenience. 

A neat way to use it is with the `date_trunc` function like this:

```sql
SELECT date_trunc('week', evt_block_time) AS time
```

You can use `minute`, `day`, `week`, or `month`.

## How to get USD price

To get the USD price of on-chain activity, you typically want to `JOIN` the smart contract event you are looking at with the `prices.usd` on the `minute` for a given `asset`:

```sql
LEFT JOIN prices.usd p 
ON p.minute = date_trunc('minute', evt_block_time)
AND event."asset" = p.contract_address
```

Then you can simply multiply the value or amount from the smart contract event with the USD price in your `SELECT` statement: `* p.price`.

## Token symbols

You'll often want to group your results by token address e.g. to see volume on a DEX grouped by token. But a big list of token addresses are abstract and hard to digest!

So use the token symbol instead. 🪄

To do this, `JOIN` the table `erc20.tokens` with your event table where `asset` = `{{token_address}}`. You then select symbol in your select statement instead of token address.

=== "PostgreSQL"

    **NB** The `erc20.tokens` table contains a selection of popular tokens. If you are working with more obscure tokens you should be careful with joining with this table because tokens that are not in the coincap table might be excluded from your results.

=== "Spark SQL"

    **NB** The `tokens_blockchain.erc20` table contains a selection of popular tokens. If you are working with more obscure tokens you should be careful with joining with this table because tokens that are not in the coincap table might be excluded from your results.

## Filter Queries and Dashboards with Parameters

Parameters can turn your Query or Dashboard into an app for blockchain data.

Click `Add parameter` in the bottom right of the SQL editor on the Query editor page

![Add parameter](images/add-parameter.png)

Double curly brackets will appear in your Query `{{}}`. Put the name of your parameter inside, e.g. `{{token symbol}}` or `{{holder address}}`.

Note that you need to put single quotes if you want to use the parameter in your Query `WHERE token = '{{token symbol}}'`.

!!! warning
    The below feature is only available in the Dune V1 engine.

To save the user from having to put in `\x` for the address a useful formatting of addresses is this one:

```sql
WHERE contract_address = CONCAT('\x', substring('{{token address}}' from 3))::bytea
```

This let’s a user of your Query simply paste in `0xc00e94cb662c3520282e6f5717214004a7f26888` instead of `\xc00e94cb662c3520282e6f5717214004a7f26888` when they filter.
