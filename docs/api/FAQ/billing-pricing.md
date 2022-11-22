---
title: Dune API Billing & Pricing
description: Information about Dune's API billing and pricing.
---
# FAQ: Billing & Pricing

## Is the API free?
    
We currently only offer paid tiers of the API but will be launching a free tier in early 2023!
    
## How will API Billing work with the new Team plans?
We'll be supporting API keys on a team level. So any usage associated with those keys will be billed to their respective team.

## What’s a datapoint?

A datapoint can in most cases be thought of rows * columns with an additional limit of 50 avg bytes per cell in a set of results. This can be expressed as:

Datapoints = max(rows*columns, ceil(totalbytes/50))

## Do I get charged datapoints for every execution?

We charge the data points in the result for the 1st read result of every distinct query execution and every subsequent 100th read per billing cycle.
