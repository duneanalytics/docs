---
title: Understand and Add a Spell
description: Learn how to add a Data Model to the Spellbook
---

## Understanding Spell Models

If you are just looking to understand the basic models [from the Github Repo](https://github.com/duneanalytics/spellbook), read through the [example model walkthroughs of transfers and balances of ERC20 tokens](Example%20Spell%20Models/index.md)

## 7 Steps to adding a Spell

Let’s learn how to add a Spell!   
By the end of this guide, you’ll have your local environment set up and the knowledge you need to add Spells.

**7 steps to go:**

<div class="cards grid" markdown>
- [1. 💻 Set Up Spellbook dbt locally](1-do-some-prerequisites%20and-set-up-Spellbook-dbt.md)
- [2. 🛣️ Set Up Your File Structure for SQL, Schema, and Source Files](2-set-up-your-file-structure-for-SQL-schema-and-source-files.md)
- [3. 📙 Identify and Define Sources](3-identify-and-define-sources.md)
- [4. 🧪 Define Schema and Tests](4-define-expectations-with-schema-and-tests.md)
- [5. 🖋️ Write Your Spell](5-write-your-spell-as-SELECT-statement.md)
- [6. 🎨 Configure Alias and Materialization](6-configure-alias-and-materialization-strategy.md)
- [7. 🧙 Make a Pull Request, Become an Archwizard](7-make-a-pull-request-get-merged-become-an-archwizard.md)
</div>

!!! note "Spellbook Model Creation Runs on Spark SQL"
       Spellbook Spells are available on Dune V2, queryable from both Spark SQL and Dune SQL [V2 Query Engines](../query/index.md). For now, Spells will continue to be written in Spark SQL and querying them with Dune SQL will require small syntax changes. While the changes needed to make Spells Dune SQL native are small, we want to make sure Dune SQL is rock solid before we implement them!
## Video Guides

If you’re more of a watcher, check out these video workshops.

In collaboration with [MetricsDAO](https://metricsdao.xyz/), [@agaperste](https://dune.com/agaperste) showed us how to add a Spell from scratch!

![type:video](https://www.youtube.com/embed/VdTYRxg96-E)

In this [DuneCon workshop](https://www.youtube.com/playlist?list=PLK3b5d4iK10eVQejE7O1JEwcBMA4uwdSC), Dune Team member Megan Heintz (who came up with the name "Spellbook") walks us through Spellbook's infrastructure and how to migrate data to a Spell:

![type:video](https://www.youtube.com/embed/r9pcL7dgaWs)

In this tutorial, [@ilemi](https://dune.com/ilemi) aka Andrew Hong shows us the main protocol interactions (creating a pair, managing liquidity, swapping through pairs) and how to pull and transform data on Ethereum using.

[Read his guide here](https://ath.mirror.xyz/K-S_Mwhj7osTBqN-AOWbCmfNn9TZViEkzICCmK-oObM) or watch the video below:

![type:video](https://www.youtube.com/embed/7zReSzVdV2s)
