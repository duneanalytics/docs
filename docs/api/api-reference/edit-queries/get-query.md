---
title: Get queries
description: Here's how to get or retrieve query info via Dune API
---

!!! abstract "ENDPOINTS"
	```
	GET /api/v1/query/{{query_id}}	
	```

!!! success end "Note"
    This endpoint is included only in our Premium subscription plans.

This endpoint will get details about a query (public, owned by the user, or a team the user belongs to), given the query ID. In the future we will likely also support getting a specific version, but for now, it returns data for the latest version.

User will be permissioned to get any public queries, private queries user owns, and private queries owned by teams user belongs to.

## Example Request

### cURL
```cURL
curl -X GET "https://api.dune.com/api/v1/query/{{query_id}}"   \
  -H X-Dune-API-key: {{api_key}}
```

### Python
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

query_id = 60066
base_url = f"https://api.dune.com/api/v1/query/{query_id}"
result_response = requests.request("GET", base_url, headers=headers)
```
## Example Return

```js
{
	"query_id": 60066,
	"name": "Ethereum transactions",
	"description": "Returns ethereum transactions starting from the oldest by block time",
	"tags": [
    	"ethereum",
    	"transactions"
	],
	"version": 15,
	"parameters": [
    	{
        	"key": "limit",
        	"value": "5",
        	"type": "number"
    	}
	],
	"query_engine": "v2 Dune SQL",
	"query_sql": "select block_number, block_hash, value from ethereum.transactions order by block_time asc limit {{limit}};",
	"is_private": false,
	"is_archived": false,
	"is_unsaved": false,
	"owner": "dzebedaje"
}
```

## Error Codes
- 400 - Invalid query ID passed in URL (e.g. not a number)
- 404 - Query not found, or it’s private and belongs to somebody else
