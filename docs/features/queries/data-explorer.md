---
title: The Data Explorer
description: The Data Explorer allows you to search for blockchain and other data to use in your Queries. Here's how it works.
---

The Data Explorer empowers you to search for blockchain and other data to use in your Queries (learn about all the data Dune offers in the [Tables section](../../tables/index.md)).

![the dune data explorer](images/dune-data-explorer-close-up.png)

To find the data you're looking for, first select which database you want to search in:

![data explorer dropdown example](images/data-explorer-dropdown.gif)

Then simply enter any keywords, protocol names, contract names, or event names into the search bar at the top.

This will bring up a list of [Tables](../../tables/index.md) containing blockchain data you can use to your Queries! 🧙

## Searching by Keyword

Searching for just `uniswap` will bring up all tables that contain the keyword `uniswap` in some form.

![data explorer keyword search example](images/keyword-search-example.gif)

Use spaces to create multi-keyword searches.

![multi keyword search](images/multi-keyword-search.gif)

## Finding Specific Schemas

!!! warning
    This is a Dune V1 exclusive feature.

Searching for `uniswap_v2.` will bring up all tables related to the `uniswap_v2` schema specifically.

In Dune's V1 Engine, adding "." at the end specifies you're looking for data in this exact schema of tables. Without the "." at the end you'll also find a lot of data that includes references to, in this example, `uniswap_v2.`.     

![data explorer specific schema example](images/data-explorer-search-example-1.gif)

## Finding Events, Calls, or Contracts

Searching for `uniswap_v2. evt` will bring up only event tables related to the `uniswap_v2` schema. 

Likewise `call` will bring up calls, and searching for a specific `{{contractName}}` will bring up all the data for that contract.

![events calls contracts search example](images/events-calls-contracts-search-example.gif)

## Finding Specific Contract Data

Click a Table name to see a list of all the columns inside that contract's table:

![how to find contract data in tables](images/how-to-find-contract-data-in-tables.gif)

## Adding References to the Query Window

To add references to the contract tables, click the `>>` next to the Table name:

![adding table name reference](images/adding-table-name-reference.gif)

To reference specific data within a Table, click its name:

![adding data from table example](images/add-data-from-table-example.gif)