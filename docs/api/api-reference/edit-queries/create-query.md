---
title: Create queries
description: Here's how to create new queries via Dune API
---

!!! abstract "ENDPOINTS"
	```
    POST /api/v1/query/
	```

!!! success end "Note" 
    This endpoint is included only in our Premium subscription plans.

This endpoint accepts a JSON body to create a new query. It returns just the new query ID. **The `name` and `query_sql` parameters are mandatory, the rest are optional.** All newly created queries are only created on our [DuneSQL](../../../query/index.md) query engine.

## Example Request in Python

```python
import dotenv
import os
import json
import requests
import pandas as pd
import time

# load .env file
dotenv.load_dotenv('/Users/abc/Documents/Workspace/misc/.env')
# get API key
api_key = os.environ["DUNE_API_KEY"]
# authentiction with api key
headers = {"X-Dune-API-Key": api_key}

base_url = f"https://api.dune.com/api/v1/query/"
params = {
	"name": "test query",
	"query_sql": "SELECT block_number, block_hash from ethereum.transactions limit {{limit}}",
	"parameters": [
    	{
        	"key": "limit",
        	"type": "number",
        	"value": "5"
    	}
	],
	"is_private": false
}
result_response = requests.request("POST", base_url, headers=headers, params=params)
```

### Standalone Request Body
```js
{
	"name": "test query",
	"query_sql": "SELECT block_number, block_hash from ethereum.transactions limit {{limit}}",
	"parameters": [
    	{
        	"key": "limit",
        	"type": "number",
        	"value": "5"
    	}
	],
	"is_private": false
}
```

## Example Return

```js
{"query_id":62608}
```

## Error Codes
- 400 - Invalid request (e.g. invalid JSON, missing `name` or `query_sql` fields, params that don't match query, etc.)
- 402 - Reached maximum number of private queries
- 403 - Not allowed to create this query
