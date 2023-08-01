---
title: 3. 📙 Define Sources.yml
description: With our file structure setup, let’s complete our `_sources.yml` file.
---

With our file structure setup, let’s complete our `_sources.yml` file.

Here’s how these files are formatted:

```sls

version: 2 # Spells all have “version: 2” as that’s the version of our engine they use.

sources:

  - name: [project_name]_[blockchain]

    description: [one line description] # right arrow > allows us to make a multi-line description

    tables:

      - name: [source_table_1]

      - name: [source_table_2]

      - name: [source_table_3]

```

What sources do we need to name?

To find this, we again go through each of the V1 abstractions that we’re migrating, search for `FROM` statements, and this time we’re looking for all tables mentioned that *are not* abstractions.

In our Keep3r example, doing that for our main abstraction and its dependencies:

* `keep3r_network.view_job_log`
* `keep3r_network.view_job_liquidity_log`
* `keep3r_network.view_job_credits_log`
* `keep3r_network_ethereum_view_job_migrations`

We end up with a `keep3r_network_ethereum_sources.yml` file that looks like this:

```sls

version: 2

sources:

  - name: keep3r_network_ethereum

    description: >

      Decoded events for [keep3r.network](https://keep3r.network/), a marketplace for posting and accepting jobs to help run decentralized infrastructure.

      The scope of Keep3r Network is not to manage the jobs themselves, but to allow contracts to register as jobs for keepers, and keepers to register themselves as available to perform jobs. A "keeper" is a term used to refer to an external person and/or team that executes a job.

      See their [docs](https://docs.keep3r.network/) for more.

    tables:

      - name: Keep3r_evt_LiquidityAddition

      - name: Keep3r_v2_evt_LiquidityAddition

      - name: Keep3r_evt_LiquidityWithdrawal

      - name: Keep3r_v2_evt_LiquidityWithdrawal

      - name: Keep3r_evt_JobMigrationSuccessful

      - name: Keep3r_v2_evt_JobMigrationSuccessful

      - name: Keep3r_evt_KeeperWork

      - name: Keep3r_v2_evt_KeeperWork

      - name: Keep3r_evt_LiquidityCreditsReward

      - name: Keep3r_v2_evt_LiquidityCreditsReward

```