---
title: labels
description: Address labels is a feature on Dune where you as a user can add, update and query labels for any address.
---

Because of all the open data on blockchain, we can enhance our understanding of any given address by tagging it with different labels. This immediately give any analysis enhanced context. 

**labels.addresses** is a spell in Dune that allows you to add static or query labels to enhance your analysis.

## What is a label?

A label is **a piece of metadata about an address**, a tag or metadata if you will. It comes in the form of a key-value pair. The key is the label _type_, and the value the label _name_.

Browse addresses and and labels at the [**labels page**](https://dune.com/dune/dune-v2-labels) or contribute to the spell [starting with the readme](https://github.com/duneanalytics/spellbook/tree/main/models/labels/addresses).

Here’s a list of label types:

- **Identifiers**: Most static labels should be this label type, as well as common usernames such as Farcaster, ENS, and Lens names. As a rule of thumb, identifiers should usually specify a unique entity name.
- **Usage**: These are the existing top volume and frequency (or some other percentile-able metric) within a domain and the usage of specific protocols. There must be some sort of ranking/percentile involved!
- **Personas**: These are for on-chain curated behaviors (like common CT memes) or protocol user tagging. They should be easily understood to non-analysts, though the underlying calculation methods may be more subjective.

To give a sense of examples, for the "social" category you would expect these labels:

- Identifier: Lens username (.lens) ENS reverse resolver (.eth), farcaster (_farcaster)
- Usage: top holders from ENS
- Usage: top posters from lens
- Persona: Lens User, ENS User
- Persona: Squatter (sitting on dozens of ENS names)

## What labels look like

Check out [this dashboard](https://dune.com/dune/dune-v2-labels) for examples on what can be created with labels.

The address `0xD551234Ae421e3BCBA99A0Da6d736074f22192FF` can be labeled like this:

| Type | Name |
| ----------- | -------- |
| `cex` | binance |

The address is controlled by the exchange Binance.

The address `0xe65040f61701940b62e18da7a53126a58525588b` can be labeled like this:

| label_type | Name |
| ---------- | ------------ |
| `persona` | uniswap user |
| `persona` | dex trader |

The address in the past interacted with Uniswap.

You are free to come up with both new types and label names, as labels on Dune are open ended and **crowd sourced**.

## Adding labels

Use Dune queries to label addresses. A very powerful and scalable way to add labels like “all these addresses used Uniswap”, and much much more.

Please see our [GitHub](https://github.com/duneanalytics/spellbook/tree/main/models/labels) for examples of labels created with queries and PR in your own!

Examples of what you can do:

- Label all addresses that used a certain dapp
- Label all addresses that hold a certain amount of a token
- Label all addresses that use a dapp more than X times per month
- Label all addresses that sent money to Binance

You could also do more novel and involved things around user patterns like who did arbitrage trades or profited from flash loans and so much more.

Note that there might be a few minutes delay from adding the label on [dune.com](http://dune.com) until you can query it in SQL.

## The labels table

Labels are stored in the new `labels.all` table which has the following schema:

| Column name   | Data type     | Description                                           |
|---------------|---------------|-------------------------------------------------------|
| `address`     | _varbinary_   | The address of a contract or wallet this label describes |
| `category`    | _varchar_     | The category of the label (e.g., dex/contracts/institution) |
| `blockchain`  | _varchar_     | The blockchain of the address where the label is given |
| `contributor` | _varchar_     | The name of the contributor that created the label    |
| `name`        | _varchar_     | The name of the label                                |
| `source`      | _varchar_     | The source reference of the label                    |
| `label_type`  | _varchar_     | The type of label (e.g., persona/usage/identifier)   |
| `model_name`  | _varchar_     | The name of the model used to create the label       |
| `created_at`  | _timestamp_   | The time when the label was created                  |
| `updated_at`  | _timestamp_   | The time when the label was last updated             |

## Using labels

#### Using label to identify top token holders

Using labels to identify top CRV holders

```sql
SELECT address,
       ens,
       ARRAY_AGG(DISTINCT name) as label_list,
       symbol,
       contract_address,
       balance
FROM (
SELECT address,
       symbol,
       name as ens,
       contract_address,
       SUM(amount) as balance
FROM (
SELECT tr."from" AS address,
       symbol,
       contract_address,
       -(tr.value/POW(10,decimals)) AS amount
FROM erc20_ethereum.evt_transfer tr JOIN tokens.erc20 USING (contract_address)
WHERE "from" != 0x0000000000000000000000000000000000000000 -- exclude mint/burn addresses
AND contract_address = 0xD533a949740bb3306d119CC777fa900bA034cd52 -- contract_address of the erc20 token 
UNION ALL
SELECT tr."to" AS address,
       symbol,
       contract_address,
       (tr.value/POW(10,decimals)) AS amount
FROM erc20_ethereum.evt_transfer tr JOIN tokens.erc20 USING (contract_address)
 WHERE "to" != 0x0000000000000000000000000000000000000000 -- exclude mint/burn addresses
 AND contract_address = 0xD533a949740bb3306d119CC777fa900bA034cd52 -- contract_address of the erc20 token
 ) x LEFT JOIN ens.reverse_latest USING (address)
 GROUP BY 1,2,3,4
 HAVING SUM(amount) > 0.1 --  having more than 0.1 balance
 ) p LEFT JOIN labels.all USING (address)
 GROUP BY 1,2,4,5,6
 ORDER BY 6 DESC
```

#### Using addresses of labels.contract_deployers_ethereum to find the top 100 deployers

```sql
SELECT "from" as deployer,
       COUNT(*) as contracts_deployed
from ethereum.creation_traces
WHERE "from" IN (SELECT distinct address FROM labels.contract_deployers_ethereum)
AND block_time >= NOW() - interval '7' day
GROUP BY 1
ORDER BY 2 DESC
LIMIT 100
```

#### Using smart_dex_traders label to find tokens traded by traders

```sql
SELECT tx_from as address,
       COALESCE(token_bought_symbol,CAST(token_bought_address AS VARCHAR)) as token_amount,
       SUM(amount_usd) as total_volume,
       SUM(SUM(amount_usd)) OVER (PARTITION BY COALESCE(token_bought_symbol,CAST(token_bought_address AS VARCHAR))) as total_token_volume
FROM dex.trades
WHERE tx_from IN (select from_hex(address) from labels.smart_dex_traders)
AND block_time >= NOW() - interval '14' day
GROUP BY 1,2
HAVING SUM(amount_usd) >= 100000
ORDER BY 4 DESC,3 DESC
```