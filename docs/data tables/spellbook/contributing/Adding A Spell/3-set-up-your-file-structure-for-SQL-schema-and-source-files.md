---
title: 3. 🛣️ Set Up Your File Structure for SQL, Schema, and Source Files
description: Next, let’s check for an existing folder for our project and create one if it doesn’t exist.
---

Next, let’s check for an existing folder for our project and create one if it doesn’t exist.

All Spells are stored in the `/spellbook/models` directory by project name, then blockchain network.

Names are all lower case and words are separated by `_`

Eg `/spellbook/models/[project_name]/[blockchain_name]`

So in our Keep3r network example, the folder will be `/spellbook/models/keep3r_network/ethereum`

Since this folder already exists (because we’ve done this before :), in this case, we’ll just build in there.

If the project didn’t exist, we’d create that folder with the name of the blockchain it’s on; if the project folder exists but we’re creating a Spell for a new blockchain (e.g. that project just added Polygon support), then we’d create a folder for the new blockchain.

With our folder structure in place, we’ll need to create 3 files:

1. A `.sql` file where our Spell’s logic will go.
2. A `_schema.yml` where I define my spell’s purpose and add generic tests, descriptions, metadata, etc.
3. A `_sources.yml` with any project-specific table dependencies.

![spell folder file structure](images/spell-folder-file-structure.jpg)

Spells files are named like this:

* `[project_name]_[blockchain]_schema.yml` for schema files.
* `[project_name]_[blockchain]_sources.yml` for sources files.
* `[project_name]_[blockchain]_[spell_name].sql` for the Spell’s SQL files.

In this specific v1 migration example, we’ll also need to create 3 additional `.sql` files that `keep3r_network_ethereum_view_job_log.sql` depends on.

These are `keep3r_network_ethereum_view_job_liquidity_log.sql`,  `keep3r_network_ethereum_view_job_credits_log.sql`, and `keep3r_network_ethereum_view_job_migrations.sql`

How did we know we needed these?

Looking at the original `view_job_log.sql` V1 Abstraction, we see two `FROM` statements:

```sql

FROM

        keep3r_network.view_job_liquidity_log

```

```sql

FROM

        keep3r_network.view_job_credits_log

```

When we look at the V1 Keep3r network folder, we see that these two files are there - meaning they are also abstractions that need to be converted into Spells.

![keep3r other abstractions to translate](images/keep3r-other-abstractions-to-translate.png)

We also need to do a recursive check to see if those abstractions depend on any other abstractions that have yet to be migrated to Spells.

To do this, we open those two abstractions and search for `FROM` statements.

Here we find a couple of tables referenced that include “_evt_”, which is a naming convention for [Decoded Event tables](../../../decoded/event-logs.md).

You’ll find other Raw and Decoded data table naming conventions in our [Tables documentation here](../../../index.md). 

V1 abstractions are named like so:

`[project_name].[abstraction_name]`

And when we search both of the abstractions referenced in `view_job_log.sq` we also find a reference to `keep3r_network_ethereum_view_job_migrations` so that must also become a Spell.