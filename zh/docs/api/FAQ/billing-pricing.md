---
title: Dune API Billing & Pricing
description: Information about Dune's API billing and pricing.
---
# FAQ: Billing & Pricing

## Is the API free?
    
We are offering limited-time free trials for select users. The API will be a paid service after any trial period.
    
## How will API Billing work with the new Team plans?
    
Over the next several months we’ll be rolling out new “Team Plans” which will have their own credit card associated with that billing method.
    
API calls that come from a user who is a member of Team [X] for a query made by Team [X] are automatically billed to Team [X].

API calls that come from a user and do not belong to their team are billed to their personal accounts.

We therefore recommend any individual users who recieved API keys during their trial consolidate their keys and usage into a single account at the end of their trial, 

This helps streamline Team API usage easier and avoids the need for every API key holder to keep their credit card information on file.

## How will the API be priced?

The API will be priced based on # of executions and # of data points returned. More details on this will be shared in the coming weeks!

## What’s a datapoint?

A datapoint can in most cases be thought of rows * columns with an additional limit of 50 avg bytes per cell in a set of results. This can be expressed as:

Datapoints = max(rows*columns, ceil(totalbytes/50))

## Do I get charged datapoints for every execution?

We charge the data points in the result for the 1st read result of every distinct query execution and every subsequent 100th read.
