---
description: Data Tables are what makes Dune work.
---

# Data tables



{% embed url="https://www.youtube.com/watch?v=UDu23Eyvo_Y" %}

This video covers all important topics around data tables.

## Dune's Table Structure

Dune aggregates blockchain data into an accessilbe PostgreSQL database. The schema can be understood in the following way:

1\) Low-level data (raw transaction data) provides detailed records of all activities on the blockchain&#x20;

2\) Project-level data tables are created tables that return pre-processed, clean data on specific projects.

3\) Abstractions are higher-level created tables that return aggregated data on sectors/topics. [See a list of all abstractions here](https://github.com/duneanalytics/abstractions)

You can currently query data from **Ethereum, Polygon** and **xDai**.

## How do I find the data I need?

This section aims to guide you in the process of finding the right data tables to work on your project.\
Different Use Cases of Dune require different data tables to pull data from, study these carefully and you'll recognize what significance each of the data table types has for your Queries and Dashboards.

Most of the tables on Dune are populated by Dune and are just a translation of the blockchain data to SQL tables, but in the case of [abstractions ](abstractions.md)and dune\_user\_generated tables you can actually create your own tables that aggregate or modify the dataset to your need.

{% content-ref url="raw-data/" %}
[raw-data](raw-data/)
{% endcontent-ref %}

{% content-ref url="decoded-data.md" %}
[decoded-data.md](decoded-data.md)
{% endcontent-ref %}

{% content-ref url="abstractions.md" %}
[abstractions.md](abstractions.md)
{% endcontent-ref %}

{% content-ref url="prices.md" %}
[prices.md](prices.md)
{% endcontent-ref %}

{% content-ref url="labels.md" %}
[labels.md](labels.md)
{% endcontent-ref %}
