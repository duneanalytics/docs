@R1971---
title: Authentication
description: Here's how to authenticate your API requests.
---

The Dune API uses API keys to authenticate requests. Your API key is used to determine the permissions of private queries you may call, as well as which account to bill for the requests, so be sure to keep them secure!

**Do not share your secret API keys in publicly accessible areas such as GitHub, client-side code, and so forth.**

## Header

Authentication with the API can be performed by adding an “x-dune-api-key” property to the request header.

Here's one example of doing this with an Execute POST API request:

```
curl -X POST -H x-dune-api-key:{{api_key}} "https://api.dune.com/api/v1/query/{{query_id}}/execute"
```

## Query Parameter

Authentication with the API can also be performed by adding an `api_key` query paramater.

Here's one example of doing this with an Execute POST API request:

```
curl -X POST "https://api.dune.com/api/v1/query/{{query_id}}/execute?api_key={{api_key}}"
```
