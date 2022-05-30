# Tips for querying

You can interact with the data tables through our interface at [dune.xyz](https://www.dune.xyz/).

To create a new query you simply click `New Query` in the top right corner

![](https://i.imgur.com/dMHavC8.png)

On your left you can select which database you want to use in the dropdown list and then see the data tables in the window. Just search for the project you are interested in working with.

## Use abstractions

The easiest way to do great analysis with Dune Analytics is to use prepared [abstractions](../../../data-tables/data-tables/abstractions.md) tables like `dex.trades`. All tables are cleaned and contains data and metadata (like human readable token symbols) that make them very straight forward to query.

## Using Inline Ethereum addresses

In Dune Ethereum addresses are stored as postgres bytearrays which are encoded with the `\x` prefix. This differs from the customary `0x` prefix. If you’d like to use an inline address, say to filter for a given token, you would do

```sql
WHERE token = '\x6b175474e89094c44da98b954eedeac495271d0f'
```

which is simply short for

```sql
WHERE token = '\x6b175474e89094c44da98b954eedeac495271d0f'::bytea
```

## Quote camel case column and table names

Column and table names are mostly taken directly from smart contract ABIs, with no modification. Since most smart contracts are written in Solidity, and written with a camelCased naming convention, so is many of Dune’s table and column names. Postgres requires you to quote columns and tablenames that are case sensitive:

```sql
SELECT “columnName”
FROM projectname.”contractName_evt_EventName”
LIMIT 10
```

In Postgres, double quotes are reserved for tables and columns, whereas single quotes are reserved for values:

```sql
SELECT “columnName”
FROM projectname.”contratName_evt_eventName”
WHERE contract_address = '\x6B175474E89094C44Da98b954EedeAC495271d0F'
LIMIT 10
```

Schemas are always lowercase in Dune.

## Remove decimals

Ether transfers and most ERC-20 tokens have 18 decimal places. To get a more human readable number you need to remove all the decimals. The table `erc20.tokens` gives you contract address, symbol and number of decimals for popular tokens. Token value transfers are then divided by 10 to the power of decimals from this table:

`transfer_value / 10^erc20.tokens.decimals`

## Use `date_trunc` to get time

We’ve added `evt_block_time` to decoded event tables for your convenience. A neat way to use it is with the `date_trunc` function like this

```sql
SELECT date_trunc('week', evt_block_time) AS time
```

Here you can use minute, day, week, month.

## How to get USD price

To get the USD volume of onchain activity you typically want to join the smart contract event you are looking at with the usd price and join on minute. Also make sure that asset matches asset.

```sql
LEFT JOIN prices.usd p 
ON p.minute = date_trunc('minute', evt_block_time)
AND event."asset" = p.contract_address
```

Then you can simply multiply the value or amount from the smart contract event with the usd price in your `SELECT` statement: `* p.price`.

## Token symbols

You often want to group your results by token address. For instance you want to see volume on a DEX grouped by token. However, a big list of token addresses are abstract and hard to digest.

Therefore you often want to use the token symbol instead. Simply join the table `erc20.tokens` with your event table where asset = token address. You then select symbol in your select statement instead of token address.

**NB** The `erc20.tokens` table cointains a selection of popular tokens. If you are working with more obscure tokens you should be careful with joining with this table because tokens that are not in the coincap table might be excluded from your results.

## Filter queries and dashboards with parameters

Parameters can turn your query or dashboard into an app for blockchain data.

Click `Add parameter` in the bottom right of the SQL editor on the query editor page

![](https://i.imgur.com/rYJVSqA.png)

Double curly bracets will appear in your query `{{}}`. Inside these you put the name of your paramter like `token symbol` or `holder address`.

Note that you need to put single quotes if you want to use the parameter in your query `WHERE token = '{{token symbol}}'`.

To save the user from having to put in `\x` for the address a useful formatting of addresses is this one:

```sql
WHERE contract_address = CONCAT('\x', substring('{{token address}}' from 3))::bytea
```

This let’s a user of your query simply paste in `0xc00e94cb662c3520282e6f5717214004a7f26888` instead of `\xc00e94cb662c3520282e6f5717214004a7f26888` when they filter.
