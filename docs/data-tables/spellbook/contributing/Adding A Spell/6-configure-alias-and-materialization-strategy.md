---
title: 6. 🎨 Materiliazing Your Models and Naming/Aliasing them
description: With our Spell’s SQL defined, it’s time to configure our aliases.
---

With our Spell’s SQL defined, it’s time to configure our aliases so we can refer to these files in other Spells and Queries and how we want dbt to materialize our work.

## Materialize Your Model as a Table

In dbt, [materializations](https://docs.getdbt.com/docs/build/materializations) are strategies for persisting our data inside of our data lake house.

There are 4 materialization strategies in dbt:

* `table`
* `ephemeral`
* `view`
* `incremental`

For Spellbook, we just use `view` and `incremental`.

### Add Your Model as a View

`view` is the default materialization strategy in Spellbook - so we don’t need to specify it as our strategy in the Spells that use it.

These Spells are rebuilt each time they are run, meaning every time someone queries a `view` Spell, the SQL is run meaning fresh data is gathered according to our Spell’s SQL logic.

Basically, `view` Spells are just stored SQL logic, no additional data is stored as part of the Spell.

The Pro is that `view` Spells always have fresh data, the Con is that they can take a long time to run if there’s a lot of data involved.

### Add Your Model as an Incremental Materialized Table

`incremental` Spells allow dbt to insert or update records in a table according to the logic we define.

The benefit is that these Spells can run faster, though their data won’t be as fresh as `view` Spells.

To create an `incremental` Spell, in the Config section of our file we need to include

```sql

-- a statement of which column we should join new data to our existing data each time we increment; in this example, we use block_date and that’s often the best to use

partition_by = ['block_date'],

-- here we specify that this is an incremental Spell

materialized = 'incremental',

-- an instruction for how dbt should combine new/old data; use ‘merge’

incremental_strategy = 'merge',

```

We also need to add `if` statements to any `FROM` for which we want to increment data.

In this example, where we `partition_by = ['block_date']`, we’ve added ifs that will refresh data that’s more than a week old:

```sql
{% if is_incremental() %}

    WHERE evt_block_time >= date_trunc("day", now() - interval '1 week')

{% endif %}
```

## Configuring aliases and materialization

To configure your Spell’s alias and materialization, you’ll add this configuration to the top of each of your SQL files.

Note, this assumes we’re using a `view` materialization strategy; see above for how to implement `incremental` strategies.

```sql
{{ config (

    -- create an alias for your Spell file that will appear in the dune.com UI

    alias = 'job_log',

    -- this further defines how this file is stored and categorized in the UI, starting with what blockchain it’s associated with

    post_hook = '{{ expose_spells(\'["ethereum"]\',


         -- then we define whether this is a Spell for a specific project or a whole sector


        "project", 


         -- next, we name the project/sector


            "Keep3r",


         -- lastly, we name the contributors, including ourselves and in this case the creator of the V1 abstraction!


             \'["wei3erHase", "agaperste"]\') }}'

) }}
```

## Add new models to dbt_project.yml

Coming into the final stretch, we need to add our new models to the `dbt_project.yml` file in the Spellbook root folder.

First, find these lines:

```sls

# Configuring models

# Full documentation: https://docs.getdbt.com/docs/configuring-models

models:

	spellbook:

```

Underneath, we specify the project name, schema, and materialization strategy for the project as a whole as well as the specific blockchain(s) that we’ve created Spells for.

For Keep3r, our entry looks like this:

```sls

   keep3r_network:

      +schema: keep3r_network

      +materialized: view

      ethereum:

        +schema: keep3r_network_ethereum

        +materialized: view

```