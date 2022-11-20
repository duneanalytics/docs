---
标题：魔法书（Spellbook）模型文档
描述：魔法书配有专门的dbt文档，以帮助您浏览其中的数据!
---

Spellbook配有专门的dbt文档，以帮助您浏览其中的数据! 可以在这里找到它：

<div class="grid cards" markdown>
- [魔法书模型文档](https://dune.com/spellbook)
</div>

这些内容和 [V2的表数据文档](../../tables/v2/raw/)很类似，不过有一些特殊的功能。

!!! 注意
  这些魔法书文档和魔法书数据湖（lake）是一项正在进行的工作。如果你无法找到一个特定的V2表/列，它很可能还没有准备好在魔法书中使用。如果你找到了它，但它在魔法书模型文档中还没有完整的标签，请查看我们的[V2数据表文档](../../tables/v2/raw/)。 。如果你仍然有问题，请在 [#data-tables Discord 频道](https://discord.com/channels/757637422384283659/757893948428517376)提出来。

![dune spellbook docs homepage](images/dune-spellbook-docs-homepage.png)

## 导航

![魔法书文档导航](images/spellbook-docs-navigation.png)

你可以使用窗口左侧的项目和数据库导航标签来探索魔法书模型，也可以使用顶部的搜索栏。

## 项目窗口

![project tab](images/project-tab.png)

项目标签是你可以找到数据源（sources）和魔法书模型的地方。

### 数据源模型

[数据源](../spellbook/getting-started/data-sources.md) 是由Dune V2数据湖中的数据表建立的dbt数据模型。

在使用魔法书之前，数据必须首先被拉入魔法书的数据源模型，所以通过这个列表，你可以了解哪些数据可以在你的魔法书中使用，以及哪些数据可能需要先作为数据源模型被添加。

比如， [Arbitrum blocks](../../tables/v2/raw/arbitrum/blocks/) 数据在魔法书中可用，但是 [Arbitrum event logs](../../tables/v2/raw/arbitrum/event-logs/) 则不行。

### 魔法书模型

在Sources下面，你会发现一个项目（Projects）目录，这里唯一重要的是Spellbook文件夹，它包含了与莫发表有关的各种代码和数据表的文档。

![spellbook models folder](images/spellbook-models-folder.png)

- **Macros** contains functions that make Spellbook work
- **Models** contains [Spells](../spellbook/getting-started/spells.md)
- **Seeds** contains static data used for testing
- **Tests** contains the [unit tests](../spellbook/getting-started/tests.md) that ensure Spells work as intended.

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
