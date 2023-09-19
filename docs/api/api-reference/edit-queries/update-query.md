---
title: Update queries
description: Here's how to update queries via Dune API
---

!!! abstract "ENDPOINTS"
    PATCH /api/alpha/v1/query/{{id}}

!!! success end "Note" 
    This endpoint is included only in our Premium subscription plans.

This endpoint updates the query with the ID from the URL. 

The request body should contain all fields that need to be updated. **Any omitted fields will be left untouched**. If the `tags` or `parameters` are provided as an empty array, they will be deleted from the query. If they are sent with some values, the existing ones will be overwritten by the new ones. And as with the other fields, if those keys aren’t set at all, they won’t be updated. 

The Update query endpoint does not allow setting a query as private or archived, please refer to [archive query](../archive-query) and [make query private](../private-query) pages respectively.

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

query_id = 62608
base_url = f"https://api.dune.com/api/v1/query/{query_id}"
params = {
	"name": "test query",
	"description": "this is the query description",
	"tags": ["any", "number", "of", "string", "tags"],
	"query_sql": "SELECT block_number, block_hash from ethereum.transactions limit {{limit}}",
	"parameters": [
    	{
        	"key": "limit",
        	"type": "number",
        	"value": "5"
    	}
	]
}
result_response = requests.request("PATCH", base_url, headers=headers, params=params)
```

### Standalone Request Body
```js
{
	"name": "test query",
	"description": "this is the query description",
	"tags": ["any", "number", "of", "string", "tags"],
	"query_sql": "SELECT block_number, block_hash from ethereum.transactions limit {{limit}}",
	"parameters": [
    	{
        	"key": "limit",
        	"type": "number",
        	"value": "5"
    	}
	]
}
```

## Example Return

```js
{"query_id":62608}
```

## Error Codes
- 400 - Invalid request (e.g. invalid query ID in URL, invalid JSON, params that don't match query, etc.)
- 402 - Reached maximum number of private queries
- 403 - Not allowed to update this query
- 409 - Query was updated in the meantime (this is currently never returned, but might be in the future if we add the version parameter or a nonce to the request)

