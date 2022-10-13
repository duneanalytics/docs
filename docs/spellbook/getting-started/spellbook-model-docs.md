---
title: Spellbook Model Docs
description: Spellbook comes with dedicated dbt documentation to help you navigate the data within!
---

![dune spellbook docs homepage](images/dune-spellbook-docs-homepage.png)

Spellbook comes with dedicated dbt documentation to help you navigate the data within! Find it here:

<div class="grid cards" markdown>
- [Spellbook Table Docs](https://spellbook-docs.dune.com/)
</div>

These work similarly to the [V2 table documentation you can find here](../../tables/v2/raw/), with a couple of special features.

!!! warning
    These Spellbook Table Docs and the Spellbook data lake are a work in progress. If you're not able to find  a specific V2 table/column, it likely isn't ready for use in Spells yet. If you do find it but it's not yet fully labeled in the Spellbook Model docs, please check our [V2 table documentation here](../../tables/v2/raw/). If you still have questions drop them in the [#data-tables Discord channel](https://discord.com/channels/757637422384283659/757893948428517376)!

## General Navigation

![spellbook docs navigation](images/spellbook-docs-navigation.png)

You can use the Project and Database navigation tabs on the left side of the window to explore Spellbook models, as well as the search bar up top.

## Project Tab

![project tab](images/project-tab.png)

The Project tab is where you'll find the Sources and Spellbook models.

### Sources models

[Sources](../getting-started/data-sources.md) are dbt data models built from data tables contained in the main Dune V2 data lake.

Data must first be pulled into Spellbook Source models before it can be used in Spells, so using this list you can get an idea of what data is ready for use in your Spells, as well as what data might need to be added first as a Source model.

For example, [Arbitrum blocks](../../tables/v2/raw/arbitrum/blocks/) data is available for Spells, but [Arbitrum event logs](../../tables/v2/raw/arbitrum/event-logs/) are not.

### Spellbook models

Below Sources you'll find a "Projects" heading, the only important thing here is the Spellbook folder which contains documentation on the various Spell-related code and data tables.

![spellbook models folder](images/spellbook-models-folder.png)

- **Macros** contains functions that make Spellbook work
- **Models** contains [Spells](../getting-started/spells.md)
- **Seeds** contains static data used for testing
- **Tests** contains the [unit tests](../getting-started/tests.md) that ensure Spells work as intended.

## The Lineage Graph
You can click the blue icon on the bottom-right corner of a page to view the lineage graph of the model you're looking at:

![lineage graph button](images/lineage-graph-button.png)

In the lineage graph, you'll see the immediate parents and children of the model you're exploring. 

![lineage graph example](images/lineage-graph-example.png)

Click the Expand button at the top-right of this lineage pane to see all of the models that are used to build, or are built from, the model you're exploring.

![expand lineage graph](images/expand-lineage-graph.gif)

Once expanded, click on any model name to highlight its related parent/child models:

![highlight parent child models](images/highlight-parent-child-models.gif)

You can also right-click on models to interactively explore and filter the graph:

![right click lineage menu](images/right-click-lineage-menu.png)

Lastly, there are a variety of options for filtering the graph at the bottom:

![lineage graph filters](images/lineage-graph-filters.png)