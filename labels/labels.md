# Labels

Have you ever made a query on Dune where you get a list of addresses, only to stop and wonder what’s behind these beautiful, random hexadecimal encoded strings? So have we.

**Address labels** is a new feature on Dune where you as a user can _add_, _update_ and _query_ labels for any address. All for free!

#### 🪧 What is a label? <a id="&#x1FAA7;-What-is-a-label"></a>

A label is **a piece of metadata about an address**, a tag or metadata if you will. It comes in the form of a key-value pair. The key is the label _type_, and the value the label _name_.

Browse addresses and and labels at the [**labels page**](https://dune.xyz/labels).

#### 🖼 What labels looks like <a id="&#x1F5BC;-What-labels-looks-like"></a>

Check out [this dashboard](https://dune.xyz/hagaetc/labels) for examples on what can be created with labels.

**Address label examples**

The address [0xD551234Ae421e3BCBA99A0Da6d736074f22192FF](https://dune.xyz/ethereum/address/0xD551234Ae421e3BCBA99A0Da6d736074f22192FF) can be labeled

| type | name |
| :--- | :--- |
| owner | binance |
| wallet type | exchange |

Because the address is controlled by the exchange Binance.

The address [0xe65040f61701940b62e18da7a53126a58525588b](https://dune.xyz/ethereum/address/0xe65040f61701940b62e18da7a53126a58525588b) can be labeled

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

Note that there might be a few minutes delay from adding the label on [dune.xyz](http://dune.xyz/) until you can query it in SQL.

#### 🗄 The labels table <a id="&#x1F5C4;-The-labels-table"></a>

Labels are stored in the new `labels.labels` table which has the following schema:

```text
CREATE TABLE IF NOT EXISTS labels.labels (
    -- the id of the label is just an incrementing integer (not useful for querying)
    id integer PRIMARY KEY,               
    -- the address this label describes
    address bytea NOT NULL,            
    -- the actual label
    name text NOT NULL, 
    -- the label type
    type text NOT NULL,
    -- the username of the Dune user who created this label
    author text NOT NULL,                 
    -- the source of this label, autopopulated by dune
    source text NOT NULL,                 
    -- the last time this label was changed
    updated_at timestamptz NOT NULL       
);                                        
```

#### 🧑‍🔧 Using labels <a id="&#x1F9D1;&#x200D;&#x1F527;-Using-labels"></a>

Note that this table holds multiple rows per address, and therefore joins against it can be tricky to get right. For that reason we’ve made the convenient function:

`labels.get(address bytea, type text default null) RETURNS text[]`

which we anticipate will be the primary way to use labels. See examples below.

Typically if you do a query that returns `address` you can use `labels.get(address)` to get all labels for that address independent of label type. If you want to see labels of the type `owner` you can do `labels.get(address, 'owner')`. You can also pass this function several label types you want included like: `labels.get(address, 'owner', 'project')`.

We’ve also added the function `labels.url(address bytea)`. Pass that function an address from your query and your results table will contain a clickable link to for instance:

[https://dune.xyz/ethereum/address/0xD551234Ae421e3BCBA99A0Da6d736074f22192FF](https://dune.xyz/ethereum/address/0xD551234Ae421e3BCBA99A0Da6d736074f22192FF)

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
--- SELECT trader_a, SUM(token_a_amount)
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
--- SELECT labels.get(trader_a), SUM(token_a_amount)
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
--- SELECT labels.get(trader_a, 'activity'), SUM(token_a_amount)
+++ SELECT trader_a, labels.get(trader_a, 'activity', 'project', 'contract_name') as labels, SUM(token_a_amount)
    FROM dex.trades
    WHERE token_a_symbol = 'DAI'
    AND block_time > now() - interval '24 hours'
--- GROUP BY 1
+++ GROUP BY 1, 2
    ORDER BY 3 DESC
    LIMIT 10;
```

You can also use `labels.url` to make the addresses clickable:

```text
--- SELECT trader_a, labels.get(trader_a, 'activity') as labels, SUM(token_a_amount)
+++ SELECT labels.url(trader_a), labels.get(trader_a, 'activity') as labels, SUM(token_a_amount)
    FROM dex.trades
    WHERE token_a_symbol = 'DAI'
    AND block_time > now() - interval '24 hours'
--- GROUP BY 1
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
--- SELECT "to"
+++ SELECT "to", labels.get("to")
    FROM uniswap_v2."Pair_evt_Swap" 
    WHERE EXISTS(SELECT * FROM labels.labels WHERE address="to" AND type='dapp usage' AND name='1inch user')
    LIMIT 10;
```

There you have it: you see addresses that traded on both Uniswap and 1inch _and_ all associated address labels.

