---
title: Types of Spellbook Contribution
description: There are two main types of Spellbook contributions, learn more about them here!
---

Spellbook consists of two primary data structures, each of which has different guidelines for contribution.

## Static Views

Static views are our way of maintaining reference datasets in Spellbook. We currently have two major types.

### Token Metadata

Token Metadata views store basic metadata such as symbol, decimals, etc.

They have slightly different schemas depending on the token standard (e.g. ERC20, ERC721).

### Token Prices

Token Prices views are configuration files to our internal pricing jobs that fetch prices for our prices table.

Learn more about the [guidelines for contributing Static Views here](../contribution-guidelines/contributing-static-views.md)!

## Spells

Spells are the abstracted datasets our community and team build on top of raw blockchain data - they're a core part of what makes Dune the best source for blockchain data and tool for analysis!

Each Spell is a dbt model on the Spellbook repository ([browse our list of existing Spells here](https://dune.com/spellbook#!/overview)).

All Spells have the same general structure with slight differences depending on the type of materialization.

In general, every time you build an entirely new spell, it's going to be as a view. In case you are extending an existing sector Spell with new projects (e.g. adding a new dex to dex.trades) you'll be following that spell's materialization strategy (usually incremental).

If you know what you're doing, you can use the type that best matches your application.

### Views

Views are the most common and default type of Spell. They're executed every time they're queried.

### Incremental Tables

Used for large tables like `dex.trades`, Spells materialized as Incremental Tables are stored on disk, records from new blocks are appended regularly every hour.

### Tables

Tables are relatively rare as the data is stored on disk and the Spell is executed on the whole blockchain - making them computationally intensive and naturally slower to run.

Learn more about the [guidelines for contributing Spells here](../contribution-guidelines/contributing-spells.md)!
