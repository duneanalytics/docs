---
title: Materialized Views
description: The "Materialized View" feature in DuneSQL allows you to schedule a query and save it's results as a table, to be used in another query. This powerful functionality enables you to take the query view feature even further.
---

!!! warning
    THIS FEATURE IS CURRENTLY IN ALPHA. There may still be breaking changes, we welcome your feedback anytime. Thank you for helping us test the feature!

## Overview

The "Materialized View" feature in DuneSQL allows you to use an existing query as a view in another query. This powerful functionality enables you to break down bigger queries so that the complex/high compute logic only has to run a few times a day, and the queries you build on top run much faster.

You have full control over this view, you can think of it as a simplified Spellbook table. You should think of using this feature any time you run into:
1. Query timeouts (running longer than 30 mintes)
2. Stage limits (exceeding stage limits in the planning stage, normally happens when you join too many tables)
3. Memory limits (exceeding the memory limits, normally happens when you use too many large tables like `solana.transactions` or `ethereum.traces`)

Here are some examples: 

| Description | Original | Example Materialized View |
|---|---|---|
| Query which bumps into cluster capacity issue | https://dune.com/queries/2698624/4490178 | https://dune.com/queries/2744461 |
| A large view used within the above query (to be materialized) | https://dune.com/queries/268877 | https://dune.com/queries/2744412

## To create a materialized view
Write a new query or go to an existing query. (We suggest creating via team context on a plan with sufficient credits.)
1. Make sure all columns are explicitly named
2. Save the query
3. After saving a “materialize” button will appear below the run button.
4. Click the materialize button, and set a refresh schedule. Each refresh uses up credits based on cluster used.

(add arcade example walkthrough later)

Some key things to keep in mind: 
1. A query result has a 200MB limit in the editor but a materialized view doesn’t have storage limits. Even though the results will look truncated in the editor.
2. This materialized view refresh schedule is DIFFERENT from the query scheduler. Results from running the query or the normal query scheduler will NOT update the materialized view. 
3. Plans have total monthly storage limits (for premium plans, it’s 50GB, plus it’s 15GB, free is 10MB). These limits will soon be implemented, so keep that in mind.

## To query a materialized view

Wait X minutes after initiating for materialized view to finish creation. (Should be roughly similar to time the query normally takes to execute.)

Query a materialized view via `dune.<username>.result_<queryId>` (displayed in modal)
If your username starts with a number, you’ll need to wrap the <username> in quotes i.e. `dune.”123co”.result567`

Eventually, you’ll be able to query by the materialized view name specified during the materialized view creation flow but that doesn’t work yet.

!!! info
    When you query a materialized view in another query, it does not rerun the materialized view (unlike query views).  

## Missing functionality
We still have several more things to work on. Things we know that aren’t working include:
1. Deleting a materialized view (although you can turn off the schedule for now)
2. Hiding/showing a materialized view in the right context based on the context switcher might not work perfectly.
3. Currently there is no way to force refresh a materialized view outside the normally set schedule (we are looking to add this later).
4. Marking a materialized view as private does not work yet. Private materialized views will be available on premium tier plans and above in late August.
5. All materialized views can be seen by other alpha testers currently (and later the public)

**Matviews are marked separately in your query list and can also be filtered on.**

Feedback:
Feel free to message in Discord/Twitter any feedback you might have! 
