# 📑 Documentation

![](https://i.imgur.com/RURn3Pa.png)

## 📑 Documentation <a id="&#x1F4D1;-Documentation"></a>

> ### Dune v2 is now live! 🎉 <a id="Dune-v2-is-now-live-&#x1F389;"></a>
>
> See the [blog post](https://duneanalytics.com/blog/dune-v2) and learn more about the upgrade in our [changelog](https://hackmd.io/YOP3YIgaRAejTPE190sOjw?view#March-2021---Dune-v2).

Here are some tips and tricks on how to get started with the data and interface.

**👇 Top links**

* Create a user for free at [duneanalytics.com](https://www.duneanalytics.com/) 👍
* Submit contracts for decoding at [duneanalytics.com/decode](https://www.duneanalytics.com/decode) 📥
* Browse curated dashboards, queries and data tables for top projects [duneanalytics.com/projects]() or [add a project](https://github.com/duneanalytics/projects) via a simple markdown file 🗂
* Find and create data abstractions via our public [Github](http://github.com/duneanalytics/) 💻
* Can’t find what you’re looking for? Ask our community on our [Discord server](https://discord.gg/ErrzwBz) or email us at [support@duneanalytics.com](mailto:support@duneanalytics.com) 👩‍🔧

**📚 Need some help getting started with queries?**

* See [this 20 min intro video](https://www.youtube.com/watch?v=AWlwO9T8dkY) on how to create queries on Dune 📹
* Here’s a good [getting started article](https://duneanalytics.com/blog/get-started-guide), even if you don’t know SQL 🗒

Many non-technical users have mastered Dune with no prior codeing experience. Dune is powered by the very common database PostgreSQL and you can find a ton of resources by searching online, both for getting started with SQL \(udemy, codecademy etc.\) and for any query specific question 🧠

### Dune Analytics TLDR <a id="Dune-Analytics-TLDR"></a>

**1. Query human-readable smart contract data with PostgreSQL 🔍**

**2. Visualize your findings 📊**

**👉 Create a user for free at duneanalytics.com**

### Table of contents <a id="Table-of-contents"></a>

* [📑 Documentation]()
  * [Dune Analytics TLDR]()
  * [Table of contents]()
* [🗂 Data tables]()
  * * [Decoded smart contract data]()
    * [Abstractions/table views]()
    * [Centralised exchanges trading data]()
* [👨‍🏫 Tips for querying the data]()
  * * [Use view abstractions and tables]()
    * [Using Inline Ethereum addresses]()
    * [Quote camel case column and table names]()
    * [Remove decimals]()
    * [Use date\_trunc to get time]()
    * [How to get USD price]()
    * [Token symbols]()
    * [Filter queries and dashboards with parameters]()
* [🏷 Address Labels]()
  * * [🪧 What is a label?]()
    * [🖼 What labels looks like]()
    * [📥 Adding labels]()
    * [🗄 The labels table]()
    * [🧑‍🔧 Using labels]()
    * [📜 Usecase: I want to display labels for a list of addresses]()
    * [🧼 Usecase: I want to filter my query by labels that exist.]()
* [🧐 Understanding data decoding in Dune Analytics]()
  * [What contracts have decoded data?]()
    * [Decoded data]()
    * [Abstractions and views]()
    * [A few handy queries to explore decoded tables]()
  * [Scalable decoding across contracts]()
    * [Contracts with the same bytecode]()
    * [Interfaces]()
  * [How Dune handles Proxy contracts]()
* [📬 Get any smart contract decoded]()
* [👩‍🏭 Change log]()
* [👉 Some sample queries]()
  * [Growth rate]()
  * [Users and amount over a trailing period]()
  * [Filter query by an address in the interface]()
  * [Circulating supply over time of a token with mint/burn functions]()
  * [Circulating supply over time with mint/burn from 0x000... address]()
  * [USD value of token utilised for an event]()
  * [USD trading volume per token over time]()
  * [USD price for a token from Uniswap]()
  * [Token \(and USD value\) per token over time for an address]()
* [🤕 Known issues]()
  * * [Function overloading]()

## 🗂 Data tables <a id="&#x1F5C2;-Data-tables"></a>

You can currently query data from **Ethereum mainnet** and **xdai**.

To query xDai data change the data source in the dropdown list above the data table list on the query page.

* [Decoded smart contract data]()
* [Abstractions/table views]()
* [Centralised exchanges trading data]()
* [Raw Ethereum data]()

The most commonly used tables are

* **Event and call data** for each project where you typically get the action that occured in the smart contract. Simply search for project name to find the relevant tables.
* **Abstractions/view tables** containing abstractions that makes various data very straight forward to query. Examples
  * `dex.trades`
  * `lending.borrow`, `lending.collateral_change`, `lending.repay`
  * `stablecoin.transfer`, `stablecoin.mint`, `stablecoin.burn`
  * See the full list and add your own via our [Github](https://github.com/duneanalytics/abstractions)
* **prices.usd** which gives you USD price of various assets per minute. Typically joined on minute with the event data and multiplied by the on-chain value \(trade, transfer etc\).
* **erc20.tokens** gives you contract address, symbol and number of decimals for popular tokens. Token value transfers are then divided by `10` to the power of `decimals` from this table.
* **Ethereum transactions** to get ETH transfers. Typically join with event on `ethereum.transactions.hash = evt_tx_hash`.

#### Decoded smart contract data <a id="Decoded-smart-contract-data"></a>

Instead of working with the traces, logs, and receipts, Dune decodes smart contract activity into nice human-readable tables. See the [this section for more info]().

Submit contracts for decoding at [duneanalytics.com/decode]().

#### Abstractions/table views <a id="Abstractionstable-views"></a>

These are the cleanest and easiest to use tables on Dune. We have abstractions for dex trades in the `dex.trades` table.

You can also search for `view` in our table list to find all the various views.

Together with various teams and community members we’ve created table views that make the blockchain data even easier to work with. This typically entails removing decimals for ETH and token transfers, adding human readable symbols, joining relevant tables together, adding USD value of events and more.

You can always see the underlying tables derived directly from the blockchain if you need more details or are curious about how the views are created: [check out our Github](https://github.com/duneanalytics/abstractions), you can even do a pull request to create your own abstractions.

**Raw Ethereum data**

* Blocks
* Logs
* Transactions
* Receipts
* Traces

You probably won’t use this too much when doing analysis with Dune \(see [decoded data]()\), but it’s always nice to have just in case.

You can [click here](https://ethereum.stackexchange.com/questions/268/ethereum-block-architecture) to learn more about Ethereum’s data structure, but again it’s not really needed for using Dune.

#### Centralised exchanges trading data <a id="Centralised-exchanges-trading-data"></a>

Token volume is great, but more often than not you want to know the USD value of smart contract activity.

You can easily get and join that information with onchain data using the data we pull from the coincap API. See how to use it below.

* `prices.usd` - assets on Ethereum
  * contract\_address
  * price
  * minute
  * symbol \(ticker\)

Note that `WETH` can be used for ETH price.

* `prices.layer_1usd` - native layer 1 assets
  * price
  * minute
  * symbol \(ticker\)

Price is the volume-weighted price based on real-time market data every minute, translated to USD.

The data is fetched from the [Coinpaprika API](https://coinpaprika.com/api/).

## 👨‍🏫 Tips for querying the data <a id="&#x1F468;&#x200D;&#x1F3EB;-Tips-for-querying-the-data"></a>

You can interact with the [data tables]() through our interface at [duneanalytics.com](https://www.duneanalytics.com/).

To create a new query you simply click `New Query` in the top right corner

![](https://i.imgur.com/dMHavC8.png)

On your left you can select which database you want to use in the dropdown list and then see the data tables in the window. Just search for the project you are interested in working with.

#### Use view abstractions and tables <a id="Use-view-abstractions-and-tables"></a>

The easiest way to do great analysis with Dune Analytics is to use prepared views named `namespace.view_` or abstraction tables like `dex.trades`. All the view tables are cleaned and contains data and metadata \(like human readable token symbols\) that make them very straight forward to query.

#### Using Inline Ethereum addresses <a id="Using-Inline-Ethereum-addresses"></a>

In Dune Ethereum addresses are stored as postgres bytearrays which are encoded with the `\x` prefix. This differs from the customary `0x` prefix. If you’d like to use an inline address, say to filter for a given token, you would do

```text
WHERE token = '\x6b175474e89094c44da98b954eedeac495271d0f'
```

which is simply short for

```text
WHERE token = '\x6b175474e89094c44da98b954eedeac495271d0f'::bytea
```

#### Quote camel case column and table names <a id="Quote-camel-case-column-and-table-names"></a>

Column and table names are mostly taken directly from smart contract ABIs, with no modification. Since most smart contracts are written in Solidity, and written with a camelCased naming convention, so is many of Dune’s table and column names. Postgres requires you to quote columns and tablenames that are case sensitive:

```text
SELECT “columnName”
FROM projectname.”contractName_evt_EventName”
LIMIT 10
```

In Postgres, double quotes are reserved for tables and columns, whereas single quotes are reserved for values:

```text
SELECT “columnName”
FROM projectname.”contratName_evt_eventName”
WHERE contract_address = '\x6B175474E89094C44Da98b954EedeAC495271d0F'
LIMIT 10
```

Schemas are always lowercase in Dune.

#### Remove decimals <a id="Remove-decimals"></a>

Ether transfers and most ERC-20 tokens have 18 decimal places. To get a more human readable number you need to remove all the decimals. The table `erc20.tokens` gives you contract address, symbol and number of decimals for popular tokens. Token value transfers are then divided by 10 to the power of decimals from this table:

`transfer_value / 10^erc20.tokens.decimals`

#### Use `date_trunc` to get time <a id="Use-date_trunc-to-get-time"></a>

We’ve added `evt_block_time` to decoded event tables for your convenience. A neat way to use it is with the `date_trunc` function like this

```text
SELECT date_trunc('week', evt_block_time) AS time
```

Here you can use minute, day, week, month.

#### How to get USD price <a id="How-to-get-USD-price"></a>

To get the USD volume of onchain activity you typically want to join the smart contract event you are looking at with the usd price and join on minute. Also make sure that asset matches asset.

```text
LEFT JOIN prices.usd p 
ON p.minute = date_trunc('minute', evt_block_time)
AND event."asset" = p.contract_address
```

Then you can simply multiply the value or amount from the smart contract event with the usd price in your `SELECT` statement: `* p.price`.

#### Token symbols <a id="Token-symbols"></a>

You often want to group your results by token address. For instance you want to see volume on a DEX grouped by token. However, a big list of token addresses are abstract and hard to digest.

Therefore you often want to use the token symbol instead. Simply join the table `erc20.tokens` with your event table where asset = token address. You then select symbol in your select statement instead of token address.

**NB** The `erc20.tokens` table cointains a selection of popular tokens. If you are working with more obscure tokens you should be careful with joining with this table because tokens that are not in the coincap table might be excluded from your results.

#### Filter queries and dashboards with parameters <a id="Filter-queries-and-dashboards-with-parameters"></a>

Click `Add parameter` in the bottom right of the SQL editor on the query editor page

![](https://i.imgur.com/rYJVSqA.png)

## 🏷 Address Labels <a id="&#x1F3F7;-Address-Labels"></a>

Have you ever made a query on Dune where you get a list of addresses, only to stop and wonder what’s behind these beautiful, random hexadecimal encoded strings? So have we.

**Address labels** is a new feature on Dune where you as a user can _add_, _update_ and _query_ labels for any address. All for free!

#### 🪧 What is a label? <a id="&#x1FAA7;-What-is-a-label"></a>

A label is **a piece of metadata about an address**, a tag or metadata if you will. It comes in the form of a key-value pair. The key is the label _type_, and the value the label _name_.

Browse addresses and and labels at the [**labels page**](https://duneanalytics.com/labels).

#### 🖼 What labels looks like <a id="&#x1F5BC;-What-labels-looks-like"></a>

Check out [this dashboard](https://duneanalytics.com/hagaetc/labels) for examples on what can be created with labels.

**Address label examples**

The address [0xD551234Ae421e3BCBA99A0Da6d736074f22192FF](https://duneanalytics.com/ethereum/address/0xD551234Ae421e3BCBA99A0Da6d736074f22192FF) can be labeled

| type | name |
| :--- | :--- |
| owner | binance |
| wallet type | exchange |

Because the address is controlled by the exchange Binance.

The address [0xe65040f61701940b62e18da7a53126a58525588b](https://duneanalytics.com/ethereum/address/0xe65040f61701940b62e18da7a53126a58525588b) can be labeled

| type | name |
| :--- | :--- |
| dapp usage | uniswap user |
| activity | dex trader |

Because the address in the past interacted with Uniswap.

You are free to come up with both new types and label names, as labels on Dune are open ended and **crowdsourced** 🎉.

#### 📥 Adding labels <a id="&#x1F4E5;-Adding-labels"></a>

There are two ways to add labels:

**1. Directly to an address via our labels page**

Good for specific labels like “this is a binance wallet”

**2. Via a Dune query**

Use Dune queries to label addresses 🤯 A very powerful and scalable way to add labels like “all these addresses used Uniswap”, and much much more.

Please see our [Github](https://github.com/duneanalytics/abstractions/tree/master/labels) for examples of labels created with queries and PR in your own!

Examples of what you can do:

* Label all addresses that used a certain dapp
* Label all addresses that hold a certain amount of a token
* Label all addresses that use a dapp more than X times per month
* Label all addresses that sent money to Binance

You could also do more novel and involved things around user patterns like who did arbitrage trades or profited from flash loans and so much more.

Note that there might be a few minutes delay from adding the label on [duneanalytics.com](http://duneanalytics.com/) until you can query it in SQL.

#### 🗄 The labels table <a id="&#x1F5C4;-The-labels-table"></a>

Labels are stored in the new `labels.labels` table which has the following schema:

```text
CREATE TABLE IF NOT EXISTS labels.labels (
    
    id integer PRIMARY KEY,               
    
    address bytea NOT NULL,            
    
    name text NOT NULL, 
    
    type text NOT NULL,
    
    author text NOT NULL,                 
    
    source text NOT NULL,                 
    
    updated_at timestamptz NOT NULL       
);                                        
```

#### 🧑‍🔧 Using labels <a id="&#x1F9D1;&#x200D;&#x1F527;-Using-labels"></a>

Note that this table holds multiple rows per address, and therefore joins against it can be tricky to get right. For that reason we’ve made the convenient function:

`labels.get(address bytea, type text default null) RETURNS text[]`

which we anticipate will be the primary way to use labels. See examples below.

Typically if you do a query that returns `address` you can use `labels.get(address)` to get all labels for that address independent of label type. If you want to see labels of the type `owner` you can do `labels.get(address, 'owner')`. You can also pass this function several label types you want included like: `labels.get(address, 'owner', 'project')`.

We’ve also added the function `labels.url(address bytea)`. Pass that function an address from your query and your results table will contain a clickable link to for instance:

[https://duneanalytics.com/ethereum/address/0xD551234Ae421e3BCBA99A0Da6d736074f22192FF](https://duneanalytics.com/ethereum/address/0xD551234Ae421e3BCBA99A0Da6d736074f22192FF)

#### 📜 Usecase: I want to display labels for a list of addresses <a id="&#x1F4DC;-Usecase-I-want-to-display-labels-for-a-list-of-addresses"></a>

> We encourage you to run these queries in Dune while you read this

Say you’re looking at the top 10 traders of DAI across all dexes last 24 hours:

```text
SELECT trader_a, SUM(token_a_amount)
FROM dex.trades
WHERE token_a_symbol = 'DAI'
AND block_time > now() - interval '24 hours'
GROUP BY 1
ORDER BY 3 DESC
LIMIT 10;
```

If you want to have labels for these addresses simply alter the `trader_a` column to `labels.get(trader_a)`.

> Note: In the examples below `---` represents lines removed, and `+++` lines added.

```text

+++ SELECT labels.get(trader_a), SUM(token_a_amount)
    FROM dex.trades
    WHERE token_a_symbol = 'DAI'
    AND block_time > now() - interval '24 hours'
    GROUP BY 1
    ORDER BY 3 DESC
    LIMIT 10;
```

Now you’ve replaced the addresses with lists of all labels for trader\_a. Sometimes you’re only interested in a subset of labels: `labels.get` accepts an optional list of type names which filter the type of labels you get. Say you’re only interested in ‘activity’ labels:

```text

+++ SELECT labels.get(trader_a, 'activity'), SUM(token_a_amount)
    FROM dex.trades
    WHERE token_a_symbol = 'DAI'
    AND block_time > now() - interval '24 hours'
    GROUP BY 1
    ORDER BY 3 DESC
    LIMIT 10;
```

Of course you can also show the address, and filter for multiple label types

```text

+++ SELECT trader_a, labels.get(trader_a, 'activity', 'project', 'contract_name') as labels, SUM(token_a_amount)
    FROM dex.trades
    WHERE token_a_symbol = 'DAI'
    AND block_time > now() - interval '24 hours'

+++ GROUP BY 1, 2
    ORDER BY 3 DESC
    LIMIT 10;
```

You can also use `labels.url` to make the addresses clickable:

```text

+++ SELECT labels.url(trader_a), labels.get(trader_a, 'activity') as labels, SUM(token_a_amount)
    FROM dex.trades
    WHERE token_a_symbol = 'DAI'
    AND block_time > now() - interval '24 hours'

+++ GROUP BY 1, 2
    ORDER BY 3 DESC
    LIMIT 10;
```

This way people who look at your dashboard can easily contribute even better labels to it!

#### 🧼 Usecase: I want to filter my query by labels that exist. <a id="&#x1F9FC;-Usecase-I-want-to-filter-my-query-by-labels-that-exist"></a>

In this usecase you wouldn’t want to use `labels.get`, because it can be slow to operate with. Instead you’ll use the fantastic `EXISTS` function in SQL.

As an example: you’re querying _Uniswap_, but are interested in the behavior of users who have traded previously on _1inch_. Here’s how you’d go about that:

```text
SELECT "to"
FROM uniswap_v2."Pair_evt_Swap" 
WHERE EXISTS(
            SELECT *
            FROM labels.labels
            WHERE address="to"
            AND type='dapp usage'
            AND name='1inch user'
            )
LIMIT 10;
```

The above query will give you 10 address that has swapped on Uniswap and traded on 1inch.

Of course, you can use the two patterns in conjunction! If you _are_ interested for labels on those addresses, go ahead and use `labels.get` in addition to the `WHERE EXISTS` pattern:

```text

+++ SELECT "to", labels.get("to")
    FROM uniswap_v2."Pair_evt_Swap" 
    WHERE EXISTS(SELECT * FROM labels.labels WHERE address="to" AND type='dapp usage' AND name='1inch user')
    LIMIT 10;
```

There you have it: you see addresses that traded on both Uniswap and 1inch _and_ all associated address labels.

## 🧐 Understanding data decoding in Dune Analytics <a id="&#x1F9D0;-Understanding-data-decoding-in-Dune-Analytics"></a>

This section contains a quick primer on how you can explore what decoded data we have and the methods we use to decode the data.

In Dune, there are tables for each event and function defined in the smart contract ABI. Subsequently, every event or function call on that contract is decoded and inserted as rows into these tables.

The tables are named accordingly

events:`projectname."contractName_evt_eventName"`

function calls: `projectname."contractName_call_eventName"`

As an example, decoded data for the `AddLiquidity`-event and `addLiquidity`-function of the uniswap exchange contract are found in tables

`uniswap."Exchange_evt_AddLiquidity"` and `uniswap."Exchange_call_addLiquidity"`.

Using the event tables is usually sufficient, but in some cases you will want to use the `call` tables. For instance Maker DAO which don’t give you too many events you can use tables like `maker.SaiTub_call_draw`.

### What contracts have decoded data? <a id="What-contracts-have-decoded-data"></a>

#### Decoded data <a id="Decoded-data"></a>

By querying `ethereum.contracts`, you can get an overview over which contracts are tracked by the Dune backend. The columns are

```text
namespace 
name 
ABI 
address 
dynamic 
bytecode 
```

#### Abstractions and views <a id="Abstractions-and-views"></a>

On top of the decoded tables we have a growing number of views that make it even easier to work with the data.

Views are named `namespace.view_event` for instance. In general you can search for `view` in the table list to find the views we have.

#### A few handy queries to explore decoded tables <a id="A-few-handy-queries-to-explore-decoded-tables"></a>

**See all projects we have decoded data for**

```text
SELECT DISTINCT namespace FROM ethereum."contracts"; 
```

**Do we have decoded data for a specific contract?**

```text
SELECT * FROM ethereum."contracts"
WHERE address = '\xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2';
```

**Contracts that are “interface”-decoded**

```text
SELECT * FROM ethereum."contracts" WHERE address IS NULL;
```

If you are working with a an event or call table directly you can see if there are several instances of that contract with

```text
SELECT DISTINCT contract_address FROM projectname."contractName_evt_eventName"; 
```

### Scalable decoding across contracts <a id="Scalable-decoding-across-contracts"></a>

Many dApps have numerous smart contracts that are more or less similar, we have two main ways of handling this in a scalable way:

#### Contracts with the same bytecode <a id="Contracts-with-the-same-bytecode"></a>

Dune can dynamically add contracts to track by comparing the bytecode of deployed contracts to known bytecodes. If a known contract is “dynamic”, events and calls to a newly deployed contract with matching bytecode will find it’s way into the same tables as were defined by the base contract. Essentially this covers all factory-pattern contract architectures. As a result, `SELECT`-ing from a single table might yield data from multiple contracts. In decoded tables, the column `contract_address` tells you which smart contract the event or call is on. If you want to look at only a single contract you can filter by its address.

For example:

```text
SELECT DISTINCT contract_address FROM uniswap."Exchange_evt_TokenPurchase";
```

Will give you all the unique Uniswap exchanges with a Token Purchase event.

#### Interfaces <a id="Interfaces"></a>

When we’re interested in a subset of events fired regardless of the origin contract, Dune uses interface-decoding. Notable examples include erc20 and erc721 transfer events. This method is reserved for special cases.

### How Dune handles Proxy contracts <a id="How-Dune-handles-Proxy-contracts"></a>

Sometimes users interact with dApps through proxy contracts. The proxy contract throws the event, but there’s an underlying contract that contains and performs the action. In those cases, we apply the ABI of the proxied contract \(sometimes called “master copy”\) to the proxy contract address. We also usually apply the name of the proxied contract to the relevant table.

## 📬 Get any smart contract decoded <a id="&#x1F4EC;-Get-any-smart-contract-decoded"></a>

**We have decoded data for the most popular smart contract projects. Head to duneanalytics.com/decode if you have a request for decoding of data.**

## 👩‍🏭 Change log <a id="&#x1F469;&#x200D;&#x1F3ED;-Change-log"></a>

**March 2021 - Dune version 2 is live!**

**August 2020 - USD prices for more assets, token decimals on prices.usd table**

**March 2020 - block\_time denormalization, traces.success and more**

**January 2020 - ERC20 transfer table, Fallback decoding and more**

**October 2019 - New data structure**

## 👉 Some sample queries <a id="&#x1F449;-Some-sample-queries"></a>

### Growth rate <a id="Growth-rate"></a>

Assuming you have a query with a count of some event grouped by time \(month for instance\) you can add this snippet to you `select` statement to get growth rate.

```text
(count(distinct event) - lag(count(distinct event), 1)
over (order by date_trunc('month', evt_block_time))) / lag(count(distinct action), 1)
over (order by date_trunc('month', evt_block_time)) as "Growth rate"
```

Multiply the number by 100 to get percentage.

### Users and amount over a trailing period <a id="Users-and-amount-over-a-trailing-period"></a>

```text
SELECT  date_trunc('day', evt_block_time),
        COUNT (DISTINCT buyer),
        SUM(eth_bought / 1e18)
FROM uniswap."Exchange_evt_EthPurchase" p
WHERE evt_block_time > now() - interval '7 days'
GROUP BY 1
ORDER BY 1;
```

### Filter query by an address in the interface <a id="Filter-query-by-an-address-in-the-interface"></a>

If you use `{{}}` in a query an input field in the UI will appear and anyone looking at the query can easily input info in that field that will go into the query.

This is very useful when filtering for custom atributes like an Ethereum address or a token address.

When you query in Dune you use `\x...` while people commonly use `0x...` \(see more details [here](https://hackmd.io/k71ZUSTxQVKGqOcvR6OXnw?view#Using-Inline-Ethereum-addresses)\).

Using the below snippet will allow users to past addresses in the regular `0x...` format and then convert it to `\x...` that will work in a query.

```text
WHERE contract_address = CONCAT('\x', substring('{{Address}}' from 3))::bytea
```

[Here’s](https://explore.duneanalytics.com/queries/10505/source?p_Address=0x37236cd05b34cc79d3715af2383e96dd7443dcf1#20880) an example of this being applied in a query.

### Circulating supply over time of a token with mint/burn functions <a id="Circulating-supply-over-time-of-a-token-with-mintburn-functions"></a>

```text
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

### Circulating supply over time with mint/burn from `0x000...` address <a id="Circulating-supply-over-time-with-mintburn-from-0x000-address"></a>

```text

SELECT
week,
SUM(transfer) over (order by week)
FROM 
 (
    SELECT
    date_trunc('week', evt_block_time) as week,
    sum(value/1e8) as transfer 
    FROM erc20."ERC20_evt_Transfer"
    WHERE contract_address = '\x2260fac5e5542a773aa44fbcfedf7c193bc2c599' 
    AND "from" = '\x0000000000000000000000000000000000000000'
    GROUP BY 1
UNION
    SELECT
    date_trunc('week', evt_block_time) as week,
    sum(-value/1e8) as transfer 
    FROM erc20."ERC20_evt_Transfer"
    WHERE contract_address = '\x2260fac5e5542a773aa44fbcfedf7c193bc2c599' 
    AND "to" = '\x0000000000000000000000000000000000000000'
    GROUP BY 1
) as net;


```

### USD value of token utilised for an event <a id="USD-value-of-token-utilised-for-an-event"></a>

```text
SELECT
date_trunc('week', evt_block_time),
SUM(amount/1e18 * p.price) AS staked
FROM numerai."SimpleGriefing_evt_StakeAdded" s 
LEFT JOIN prices.usd p ON p.minute = date_trunc('minute', evt_block_time)
WHERE p.symbol = 'NMR' 

GROUP BY 1;
```

### USD trading volume per token over time <a id="USD-trading-volume-per-token-over-time"></a>

```text
SELECT    price.symbol,
          date_trunc('week', evt_block_time) AS time,
          SUM(["FilledAmount"] /10^(erc.decimals) * price.price) AS usd_value
   FROM [table].["fill_event"] filled
   LEFT JOIN prices.usd price ON date_trunc('minute', evt_block_time) = price.minute AND [tokenAddress] = price.contract_address
   LEFT JOIN erc20.tokens erc ON erc.contract_address = "takerAsset"
    WHERE evt_block_time < date_trunc('week', current_date)::date
   GROUP BY 1,
            2;
```

### USD price for a token from Uniswap <a id="USD-price-for-a-token-from-Uniswap"></a>

The most common and easiest way to get token USD prices on Dune Analytics is with the `prices.usd` table. However, this data is fetched from centralised exchanges so for a long tail of tokens the best approach is to get prices from Uniswap.

This query uses WETH pairs, which is used to map to USD price. The query can be modified to work with any token that has a price in `prices.usd`

You can find this query on Dune [here](https://explore.duneanalytics.com/queries/11050/source?p_Token%20address=0xeb4c2781e4eba804ce9a9803c67d0893436bb27d).

```text
WITH weth_pairs AS ( 
    SELECT cr."pair" AS contract, 
        CASE WHEN cr."token0" = '\xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2' then '0' ELSE '1' END  AS eth_token,
        CASE WHEN cr."token1" = '\xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2' then cr."token0" ELSE cr."token1" END  AS other_token 
    FROM uniswap_v2."Factory_evt_PairCreated" cr
    WHERE token0 = '\xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2' OR  token1 = '\xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2'
    )
    
, swap AS ( 
    SELECT
        CASE WHEN eth_token = '0' then sw."amount0In" + sw."amount0Out" ELSE sw."amount1In" + sw."amount1Out"
        END/1e18 AS eth_amt, 
        CASE WHEN eth_token = '1' then sw."amount0In" + sw."amount0Out" ELSE sw."amount1In" + sw."amount1Out"
        END/power(10, tok."decimals") AS other_amt, 
        tok."symbol",
        tok."contract_address",
        date_trunc('hour', sw."evt_block_time") AS hour
    FROM uniswap_v2."Pair_evt_Swap" sw
    JOIN weth_pairs ON sw."contract_address" = weth_pairs."contract"
    JOIN erc20."tokens" tok ON weth_pairs."other_token" = tok."contract_address"
    WHERE other_token = '\xeb4c2781e4eba804ce9a9803c67d0893436bb27d' 
    
    
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

### Token \(and USD value\) per token over time for an address <a id="Token-and-USD-value-per-token-over-time-for-an-address"></a>

Note that this query can get very heavy when there are many tokens and transfers over a long period of time.

```text
WITH transfers AS (
    
    SELECT  day,
            address, 
            token_address, 
            sum(amount) AS amount 
    FROM
    
    (
        SELECT  date_trunc('day', evt_block_time) AS day,
                "to" AS address,
                tr.contract_address AS token_address,
                value AS amount
        FROM erc20."ERC20_evt_Transfer" tr
        WHERE "to" = '\x70c730465dff5447a12bae37090446745c9edccc' 
        
        
        UNION ALL
        
        SELECT  date_trunc('day', evt_block_time) AS day,
                "from" AS address,
                tr.contract_address AS token_address,
                -value AS amount
        FROM erc20."ERC20_evt_Transfer" tr
        WHERE "from" = '\x70c730465dff5447a12bae37090446745c9edccc' 
        
    ) t
   GROUP BY 1, 2, 3
   )

, balances_with_gap_days AS (
    SELECT  t.day,
            address,
            t.token_address,
            SUM(amount) OVER (PARTITION BY token_address, address ORDER BY t.day) AS balance, 
            lead(day, 1, now()) OVER (PARTITION BY token_address, address ORDER BY t.day) AS next_day 
    FROM transfers t
    )
    
 , days AS (
    SELECT generate_series('2020-07-01'::timestamp, date_trunc('day', NOW()), '1 day') AS day 
    )
    
, balance_all_days AS (
    SELECT  d.day,
            address,
            erc.symbol,
            b.token_address,
            SUM(balance/10^decimals) AS balance
    FROM balances_with_gap_days b
    INNER JOIN days d ON b.day <= d.day AND d.day < b.next_day 
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

## 🤕 Known issues <a id="&#x1F915;-Known-issues"></a>

#### Function overloading <a id="Function-overloading"></a>

We have a known issue with _function overloading_. There are a few cases where smart contract developers use function overloading, i.e. specify two functions with the same name but different parameters. In these cases, we will currently only have _one_ of the implementations in our database. We’re working on a fix for this. One known case is the two approve implementations in the SAI contract.

