---
title: 4. 🧪 Define Schema/Test
description: Next, we define what success means for our Spell in two ways.
---

Next, we define what success means for our Spell in two ways:

1. A schema of columns to output.
2. A unit test to ensure accurate data is being outputted to those columns.

## Defining schema

First, we start by defining our model’s schema - what columns should be outputted for each of the .sql files in our Spell.

Our `_schema.yml` files are structured like this:

```sls

version: 2

models:

  - name: [model_name]

    meta:

      blockchain: [blockchain_name]

      project: [project_name]

      contributors: [your_name]

    config:

      tags: ["[blockchain]", "[project_name]", "[other_relevant_tags]"]

    description: [description]

    columns:

      - &[column_name]

        name: [column_name]

        description: "[description]"

        tests:

          - [generic_test_criteria]

  - name: [model_name_2]

    meta:

      blockchain: [blockchain_name]

      project: [project_name]

      contributors: [your_name]

    config:

      tags: ["[blockchain]", "[project_name]", "[other_relevant_tags]"]

    description: [description]

    columns:

      - *[previously_definied_column]

```

!!! note
    “&” is used for the first definition of a column and “*” thereafter will lead to a column with the same name in a different model inheriting the same name, description, and generic tests.

Each of the SQL files we created in our fourth step is a model here, with each of the columns we want to output named and described along with a mention of any generic tests that they should be checked against.

[Check out the Keep3r Spell schema here for what that looks like when finished in our example](https://github.com/duneanalytics/spellbook/blob/b9260a03351e562448c5c9e62529da7b2d94ca59/models/keep3r_network/ethereum/keep3r_network_ethereum_schema.yml).

## Set up unit test seed file structure

With our schema set up, we’re ready to define our [Unit Tests](https://en.wikipedia.org/wiki/Unit_testing) - which will help us ensure our Spells work as intended.

This starts with setting up a seed file structure.

In dbt, [seed files are CSVs](https://docs.getdbt.com/docs/build/seeds) that we use to store reference data we can use in our Spells and unit tests; in this case, we’ll use it to store some data we can use to validate our Spell is WAI.

Navigating to the `/seeds` folder, just like we do for new projects, we’ll create a `/[project_name]/[blockchain]` subfolder.

So in our Keep3r example `/seeds/keep3r_network/ethereum`

With that in place, we need to create a CSV file with a descriptive name using this format:

`[project_name]_[blockchain]_[spell_name]_test_data.csv`

So in our example:

`keep3r_network_ethereum_view_job_log_test_data.csv`

## Finding expected values for unit tests

Our unit tests will be run against a list of expected values, essentially we want to check to make sure our Spell delivers the results it should.

What results should we expect?

To figure that out we’ll need to learn a bit more about Keep3r network by reading through their website, docs, Medium blog, asking in their discord, etc.

For our example, the important thing to know is that Keep3r network is a marketplace for posting and accepting jobs to help run decentralized infrastructure.

Jobs on the Keep3r network are smart contracts that need Keepers to do something outside of their internal logic. Doing these tasks results in the Keeper being rewarded.

Based on this understanding we can write a test where, given a transaction hash, we can see the amount that was awarded for the job, the keeper who received it, and which token they were paid in.

So in our CSV file, we start by defining the columns we’ll have test data to validate against, in this case: `tx_hash`, `amount`, ` keeper`, and `token`.

Next, we’ll find a few specific transactions, 3 is enough, and add the actual data that should be in each of those columns.

The result is something like this:

```csv

tx_hash,amount,keeper,token

0xca1ee6de6d2a776afda7d6ab6bc489d4554f69777725db58591a7ac0ef533c96,0.11,0x9429cd74a3984396f3117d51cde46ea8e0e21487,0x1cEB5cB57C4D4E2b2433641b95Dd330A33185A44

0xdd59724ee9a1f151706bc182be810483a35b36c2a82485469245887742996313,0.13,0xfb20864791b7dd70542dae2f4907ef0535a68cdc,0x1cEB5cB57C4D4E2b2433641b95Dd330A33185A44

0xa8c8383254bd4cda949de1e847f8ae0d7f765053ddeeca11a159ad8191d8cc85,0.35,0xfb20864791b7dd70542dae2f4907ef0535a68cdc,0x1cEB5cB57C4D4E2b2433641b95Dd330A33185A44

```

## Writing unit tests

Now that we have expected results to test against, we can write our unit test!

First, as you might expect, we create a folder structure in the `/tests` folder, as well as a SQL file for our test.

Same naming conventions as before for the folders, for our SQL file we’ll name it `[project_name]_[spell_name]_test.sql`

So:

`/keep3r_network/ethereum/keep3r_network_view_job_log_test.sql`

![keep3r test file](images/keep3r-test-file.jpg)

To write our unit test, we’re going to check to ensure the results from the Spell we’ll (finally) define in the next step matches the real-world results we added to our expected values seed file.

To do this, we’ll define a [Common Table Expression](https://learnsql.com/blog/cte-with-examples/) (CTE) called `unit_test`, joining our test and actual results data, and comparing that data returning errors if they don’t match.

Here’s what the unit test for this example looks like, with comments explaining what’s going on:

```sql

-- CTEs are created using WITH statements

WITH unit_test AS (

    -- Here we compare test data to actual data, returning TRUE if it matches and FALSE if not; ROUND and LOWER ensure we don’t get false errors due to formatting differences.

    SELECT

        CASE

            WHEN test.amount = ROUND(

                actual.amount,

                2

            ) THEN TRUE

            ELSE FALSE

        END AS amount_test,

        CASE

            WHEN LOWER(

                test.keeper

            ) = LOWER(

                actual.keeper

            ) THEN TRUE

            ELSE FALSE

        END AS keeper_test,

        CASE

            WHEN LOWER(

                test.token

            ) = LOWER(

                actual.token

            ) THEN TRUE

            ELSE FALSE

        END AS token_test

   /* Here we JOIN our actual and test data on tx_hash. Note for “actual” we reference our actual Spell model file, and our test data file for “test.” The {{}} is JINJA templating we’ll cover later. */

    FROM

        {{ ref('keep3r_network_ethereum_view_job_log') }} AS actual

        INNER JOIN {{ ref('keep3r_network_ethereum_view_job_log_test_data') }} AS test

        ON LOWER(

            actual.tx_hash

        ) = LOWER(

            test.tx_hash

        )

)

-- Loading all columns from unit_test, we return any FALSE results

SELECT

    *

FROM

    unit_test

WHERE

    amount_test = FALSE

    OR keeper_test = FALSE

    OR token_test = FALSE

```