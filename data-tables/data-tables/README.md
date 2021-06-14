---
description: Data Tables are what makes Dune work.
---

# Data tables



{% embed url="https://www.youtube.com/watch?v=UDu23Eyvo\_Y" %}

This video covers all important topics around data tables.

## Dune's Table Structure

Dune aggregates blockchain data into an accessilbe PostgreSQL database. The schema can be understood in the following way:

1\) Low-level data \(raw transaction data\) provides detailed records of all activities on the blockchain 

2\) Project-level data tables are created tables that return pre-processed, clean data on specific projects. [Submit projects for decoding here](https://github.com/duneanalytics/docs/tree/0be360c3f482abe12012f17a6d2195d16d5fc863/data-tables/data-tables/duneanalytics.com/decode/README.md) 

3\) Abstractions are higher-level created tables that return aggregated data on sectors/topics. [See a list of all abstractions here](https://github.com/duneanalytics/abstractions)

You can currently query data from **Ethereum** and **xDai**. We are already working on expanding our offer to other chains in the future. Dune also makes it possible to query price data from 3rd party sources.

## How do I find the data I need?

This section aims to guide you in the process of finding the right data tables to work on your project.  
Different Use Cases of Dune require different data tables to pull data from, study these carefully and you'll recognize what significance each of the data table types has for your Queries and Dashboards.

Most of the tables on Dune are populated by Dune and are just a translation of the blockchain data to SQL tables, but in the case of [abstractions ](abstractions.md)and dune\_user\_generated tables you can actually create your own tables that aggregate or modify the dataset to your need.

{% page-ref page="raw-data/" %}

{% page-ref page="decoded-data.md" %}

{% page-ref page="abstractions.md" %}

{% page-ref page="prices.md" %}

{% page-ref page="labels.md" %}

