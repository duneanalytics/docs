---
title: Dune API Billing & Pricing
description: Information about Dune's API billing and pricing.
---
# FAQ: Billing & Pricing
    
## How will API Billing work with the new Team plans?
We'll be shortly supporting API keys on a team level in first few months of 2023. Any usage associated with a team api key will be billed to their respective team.

## What’s a datapoint?

A datapoint can in most cases be thought of rows * columns with an additional limit of 50 avg bytes per cell in a set of results. This can be expressed as:

Datapoints = max(rows*columns, ceil(totalbytes/50))

## Do I get charged datapoints for every execution?

We charge the data points in the result for the 1st read result of every distinct query execution and every subsequent 100th read per billing cycle.
