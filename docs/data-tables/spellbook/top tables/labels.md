---
title: Labels
description: Address labels is a feature on Dune where you as a user can add, update and query labels for any address.
---

Have you ever made a query on Dune where you get a list of addresses, only to stop and wonder what’s behind these beautiful, random hexadecimal encoded strings? So have we.

**Address labels** is a spell in Dune that allows you to add static or query labels to enhance your analysis.

## What is a label?

A label is **a piece of metadata about an address**, a tag or metadata if you will. It comes in the form of a key-value pair. The key is the label _type_, and the value the label _name_.

Browse addresses and and labels at the [**labels page**](https://dune.com/dune/dune-v2-labels).

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

Labels are stored in the new `labels.labels` table which has the following schema:

| Column name | Data type | Description |
| - | :-: | - |
| `id` | _int_ | incrementing integer |
| `address` | _varbinary_ | The address of a contract or wallet this label describes |
| `name` | _varchar_ | label name |
| `blockchain` | _varchar_ | the blockchain the label is meant for |
| `author` | _varchar_ | The username of the user who created this label |
| `source` | _varchar_ | The source of this label, autopopulated by Dune |
| `updated_at` | _timestamptz_ | The last time this label was changed |
| `label_type` | _varchar_ | The type of label, defined in the readme |
| `model_name` | _varchar_ | The name of the label model (filename) |

## Using labels

!!! warning
    this section is currently under construction, stay tuned!