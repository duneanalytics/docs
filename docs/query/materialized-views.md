---
title: Materialized Views
description: This feature in DuneSQL allows you to schedule a query and save it's results as a table, to be used in another query. This powerful functionality enables you to take the query view feature even further.
---

!!! warning
    THIS FEATURE IS CURRENTLY IN ALPHA. There may still be breaking changes, we welcome your feedback anytime. Thank you for helping us test the feature!

## Overview

The "Materialized View" feature in DuneSQL allows you to use an existing query's results in another query. This powerful functionality enables you to break down bigger queries so that the complex/high compute logic only has to run a few times a day, and the queries you build on top run much faster.

You have full control over this view, you can think of it as a simplified Spellbook table. You should think of using this feature any time you run into:

1. Query timeouts (running longer than 30 mintes)
2. Stage limits (exceeding stage limits in the planning stage, normally happens when you join too many tables)
3. Memory limits (exceeding the memory limits, normally happens when you use too many large tables like `solana.transactions` or `ethereum.traces`)

## To create a materialized view
Write a new query or go to an existing query. (We suggest creating via team context on a plan with sufficient credits)

1. Make sure all columns are explicitly named
2. Save the query
3. After saving a “materialize” button will appear below the run button.
4. Click the materialize button, and set a refresh schedule. Each refresh uses up credits based on cluster used.

<div style="position: relative; padding-bottom: calc(66.66666666666666% + 41px); height: 0;"><iframe src="https://demo.arcade.software/NWga8JMv0LWkB7toRngC?embed" frameborder="0" loading="lazy" webkitallowfullscreen mozallowfullscreen allowfullscreen style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;color-scheme: light;" title="wallet all chain activity summary"></iframe></div>

You can find the example query [here](https://dune.com/queries/2858381), and it can be queried with just:

```
SELECT 
*
FROM dune.dune.result_2858381
```

Some key things to keep in mind: 

1. A query result has a 200MB limit in the editor but a materialized view doesn’t have storage limits. Even though the results will look truncated in the editor.
2. This materialized view refresh schedule is DIFFERENT from the query scheduler. Results from running the query or the normal query scheduler will NOT update the materialized view. 
3. Plans have total monthly storage limits (for premium plans, it’s 50GB, plus it’s 15GB, free is 10MB). These limits will soon be implemented, so keep that in mind.
4. You can delete your materialized view at any time. By going to the settings "gear" icon in the query.
   
## To query a materialized view

Wait for materialized view to finish creation first. It should be roughly similar to time the query normally takes to execute - maybe a bit longer due to time it takes to write the new table.

Query the materialized view via `dune.<username>.result_<queryId>` (displayed in modal)
If your username starts with a number, you’ll need to wrap the <username> in quotes i.e. `dune.”123co”.result567`

Eventually, you’ll be able to query by the materialized view name specified during the materialized view creation flow but that doesn’t work yet.

!!! info
    When you query a materialized view in another query, it does not rerun the materialized view (unlike query views).  

## Missing functionality
We still have several more things to work on. Things we know that aren’t working include:

1. Hiding/showing a materialized view in the right context based on the context switcher might not work perfectly.
3. Currently there is no way to force refresh a materialized view outside the normally set schedule (we are looking to add this later).
3. Marking a materialized view as private does not work yet. Private materialized views will be available on premium tier plans and above in late August.
4. All materialized views can be seen by other alpha testers currently (and later the public)

**Matviews are marked separately in your query list and can also be filtered on.**

Feedback:
Feel free to message in Discord/Twitter any feedback you might have! 
