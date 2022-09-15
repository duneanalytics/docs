---
title: API
description: Welcome to the Dune API
---

# Welcome to the Dune API

![dune API Cover](images/dune_api_cover.jpg)

The Dune API gives you full access to the queries and data you can see on the Dune website. This means you can execute and read results from any public query, as well as any personal private queries your Dune account has access to.

This documentation describes all of the available API calls and properties of the returned objects. If you have any questions or feedback, please reach out to [api-feedback@dune.com](mailto:api-feedback@dune.com) or our #[dune-api](https://discord.com/channels/757637422384283659/1019910980634939433) Discord channel!

!!! warning 
    At this time, the Dune API is in private beta. This means that the way it works and the data it returns may change with advanced notice. 

## How does the API work?

The API currently lets users:

1. Execute a query
2. Check the status of an execution
3. Get the results of an execution

These results are currently stored separately from anything you see on the Dune.com website. This means the only way to get query results from the Dune API is to execute a query using the Dune API.

Similarly, results from API executions are not currently reflected on Dune’s website.

## API Getting Started

### Obtaining an API Key

Currently we have rolled out the API in a private beta to a closed set of users.

You can fill out our [API Interest form here](https://docs.google.com/forms/d/e/1FAIpQLSdoF4_LC1BdPumRq1TJguxAsKC-g5i6u2f7-sac5v14EubLsw/viewform).
And we will notify you when we do a wider launch.

### How do I find a query id?

When navigating to a query, it’s the first number after “/queries/” in the URL.

![query-id-example](images/query-id-example.jpg)