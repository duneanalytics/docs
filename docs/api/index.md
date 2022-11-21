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

Dune API is currently in private beta with a closed set of users and will be open to the public in the coming months.

If you're a startup founder, researcher, or protocol who would like access now, [complete this form](https://docs.google.com/forms/d/e/1FAIpQLSfooxrP1RcDthQmXqN5K25wZDICYuhdF8WAUuWcqO3NzLaSbA/viewform) and we'll get back to you if we can meet your needs.

### Picking a Programming Language
While you can consume our API in the language of your choice - see the [API Reference](api-reference/authentication.md) section - we currently have quick start guides for [Python](quick-start/api-py.md) and [Node.js](quick-start/api-js.md).

### What can I build with the Dune API?
With Dune, you have access to almost all of the data from today's most popular blockchain ecosystems. There is no limit to what you can build on top of this data!

With so many possibilities, it can be challenging to figure out what to work on at times, so here are some ideas to help you ideate:

#### New Kinds of Interfaces for Blockchain Data

Our community champion [@0xBoxer](https://dune.com/0xBoxer) has this [tutorial](https://youtu.be/ez3VfcfNwvc) where he walks us through creating a [dashboard](https://dune.com/0xBoxer/gas-tracker-dashboard) for personalized metrics for any wallet.

With the Dune API it's possible to build a much nicer interface for this or any dashboard on Dune inside of your own super-smooth, super-cool app UX.

Or Excel, Google sheets, Notion Pages, Discord Bots, Telegram Bots, there are no limits.

With the API, the Data Can Flow anywhere!

#### Real World Examples from Cow Protocol

[@bh2smith](https://dune.com/bh2smith) from our community (and [Cow Protocol](https://dune.com/cowprotocol)), gave a talk Thursday at [DuneCon](https://dunecon.com) where he walked us through some real-world examples of how Cow Protocol has been using the API.

[Check out the replay here](https://youtu.be/VEvk-iqxXIM?t=404)!

## Important Links
 - API Documentation - you're already here, check out the sidebar to learn more!
 - [#dune-api Discord Channel](https://discord.com/channels/757637422384283659/1019910980634939433)
 - [API Client (Community Sourced)](https://dune.com/docs/api/quick-start/community-clients/)