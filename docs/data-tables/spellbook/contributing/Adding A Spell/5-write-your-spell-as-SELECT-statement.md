---
title: 5. 🖋️ Write Your Spell as a SELECT Statement
description: Now we’re ready to *officially* start casting our Spell!
---

Now we’re ready to *officially* start casting our Spell!

While our endpoint is `_view_job_log.sql`, we need to start with `_view_job_migrations.sql`.

## `_view_job_migrations.sql`

Why start here? Because it’s our lowest-level dependency!

Remember `keep3r_network_ethereum_view_job_log.sql` depends on `keep3r_network_ethereum_view_job_liquidity_log.sql` and `keep3r_network_ethereum_view_job_credits_log.sql` - both of which rely on `keep3r_network_ethereum_view_job_migrations.sql`

So by starting with `_migrations.sql`, we’ll be able to test as we cast our Spell without having anything break because the dependencies aren’t built.

To migrate from our V1 abstraction, we’ll start by copying the contents of the V1 file (`/spellbook/deprecated-dune-v1-abstractions/ethereum/keep3r_network/view_job_migrations.sql`) to our `keep3r_network_ethereum_view_job_migrations.sql` file:

```sql

CREATE OR REPLACE VIEW keep3r_network.view_job_migrations AS (

    SELECT

        evt_block_time AS timestamp,

        '0x' || encode(evt_tx_hash, 'hex') AS tx_hash,

        evt_index + s.step AS evt_index,

        CASE s.step

        WHEN (0) THEN

            'JobMigrationOut'

        WHEN (1) THEN

            'JobMigrationIn'

        END AS event,

        '0x' || encode(contract_address, 'hex') keep3r,

        '0x' || encode(

            CASE s.step

            WHEN (0) THEN

                m. "_fromJob"

            WHEN (1) THEN

                m. "_toJob"

            END, 'hex') AS job

    FROM (

        SELECT

            *

        FROM

            keep3r_network. "Keep3r_evt_JobMigrationSuccessful"

        UNION

        SELECT

            *

        FROM

            keep3r_network. "Keep3r_v2_evt_JobMigrationSuccessful") AS m

        INNER JOIN (

            SELECT

                generate_series(0, 1) AS step) AS s ON TRUE);

```

We don’t need the `CREATE` or `REPLACE` definition statement, so we’ll just need everything from the first `SELECT` to the last `TRUE`

Then for our FROM statements, we need to replace the old references with the new syntax and double check we mention these in our  `_sources.yml` file.

```sql

-- Removed CREATE/REPLACE statement

SELECT

    evt_block_time AS timestamp,

    '0x' || encode(evt_tx_hash, 'hex') AS tx_hash,

    evt_index + s.step AS evt_index,

    CASE s.step

    WHEN (0) THEN

        'JobMigrationOut'

    WHEN (1) THEN

        'JobMigrationIn'

    END AS event,

    '0x' || encode(contract_address, 'hex') keep3r,

    '0x' || encode(

        CASE s.step

        WHEN (0) THEN

            m. "_fromJob"

        WHEN (1) THEN

            m. "_toJob"

        END, 'hex') AS job

FROM (

    SELECT *

    -- Updated the two tables we reference with our new syntax, confirming they’re both in our sources file.

    FROM

            keep3r_network_ethereum.Keep3r_evt_JobMigrationSuccessful

    UNION

    SELECT *

    FROM

        'keep3r_network_ethereum.Keep3r_v2_evt_JobMigrationSuccessful) AS m

    INNER JOIN (

        SELECT

            generate_series(0, 1) AS step) AS s ON TRUE

```

Notice how the old abstraction had a `SELECT *` statement; it’s best practice to only `SELECT` the actual columns we need when performing a `UNION` so that our Spell doesn’t break should one of our reference tables be updated.

Looking above our first `SELECT *` statement we’ll find the specific columns we need, both of our final statements look like this:

```sql

SELECT

    evt_block_time,

    evt_tx_hash,

    evt_index,

    contract_address,

    _fromJob,

    _toJob

```

Next, we need to change our syntax from V1 abstraction style to V2 Spell style, which means a couple of things in this case:

1. We don’t need to `encode` contract addresses (in V1 they were `bytea` format and in V2 they’re `string`)
2. Column references no longer need double quotes so `m. "_fromJob"` -> `m._fromJob`

After we’ve done that, let’s copy our SQL to a new Query in dune.com to see if it works.

If you get any errors, fix them with the help of the error code; while building this example, we got an Undefined function error as `generate_series`, a function used in the V1 abstraction that does not exist in V2.

Knowing that Dune V1 is PostgreSQL and V2 is Spark SQL, in this case by googling “generate series Spark SQL” we were able to find this [StackExchange answer](https://stackoverflow.com/questions/43141671/sparksql-on-pyspark-how-to-generate-time-series) to perform the same transformation using Spark functionality.

If you’re not so lucky with Google, then ask for help in our [#spellbook Discord channel](https://discord.com/channels/757637422384283659/999683200563564655)!

## `_liquidity_log.sql`, `_credit_log.sql`, and `_log.sql`

The process is essentially just the same for our other files (modifying the syntax to V2/Spark SQL).

Since `_liquidity_log.sql` and `_credits_log.sql` both depend on `_migrations.sql`, which we just created and haven’t added to the in-production Spellbook yet, we need to copy/paste the logic that we just created as a `WITH` statement.

So in `_liquidity_log.sql`, we have this reference: `keep3r_network.view_job_migrations migs`

Let’s update that to `keep3r_network.view_job_migrations_temp migs`

Then define `_temp` at the top of our SQL file:

```sql

WITH 

keep3r_network.view_job_migrations_temp as (

-- [insert the _migrations code we just created here]

)

```

Then we can copy/paste our new SQL into dune.com and fix errors just like we did above.

## Replace hard-coded references with JINJA templating

With our SQL translated from PostgreSQL to Spark and tested individually, we need to add our JINJA templating so that this will all work in production!

First, let’s clarify a couple of terms:

* **Sources** are data that’s been added by the Dune team - raw blockchain data, Decoded data, prices, and Community tables - basically anything that’s not a Spell.
    * With JINJA, references to models are formatted as `{{ source() }}`
* **Models **are the `SELECT` statements the community have defined in the `.sql` files stored inside of our `spellbook/models` directory.
    * With JINJA, references models are formatted as `{{ ref() }}`

For `sources()` references, we first need to pass the name of our `_sources.yml` file, then the name of the source.

So our V1 abstraction reference `keep3r_network. "Keep3r_evt_JobMigrationSuccessful"` becomes `{{ source('keep3r_network_ethereum','Keep3r_evt_JobMigrationSuccessful') }}` where:

* `keep3r_network_ethereum` is the name of our `_sources.yml` *without* the `_sources.yml` part, and
* 'Keep3r_evt_JobMigrationSuccessful' is the name of a Decoded table that we included in `keep3r_network_ethereum_sources.yml`

For our `ref()` references, we just need to name the SQL files we created without `.sql`.

So our V1 abstraction reference `keep3r_network.view_job_liquidity_log` becomes `{{ ref('keep3r_network_ethereum_view_job_liquidity_log') }}`.

Once you’ve added the JINJA formatting to your references, run `dbt compile` and fix any errors!

Again, googling “xxx error dbt” or “JINJA” or “Spark SQL” can help with a lot; if our Google overlords fail you hit up the community in our [#spellbook Discord channel](https://discord.com/channels/757637422384283659/999683200563564655)!