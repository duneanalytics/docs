---
title: Execute Query ID
description: Here's how to execute (run) a Query with or without parameters to retrieve data.
---
# [POST] Execute Query ID

Here's how to execute (run) a query for a specific query id. You can choose to include a `performance` parameter, by default it will use the "medium" performance tier which consumes 10 credits. "large" will use 20 credits. You cannot run API executions on the free tier.
## Example Request

```
POST v1/query/{{query_id}}/execute

https://api.dune.com/api/v1/query/{{query_id}}/execute
```
## Returns

Returns an `execution_id` for the specified request.
## Query Parameters

If the query has parameters and you don't add them in your API call, it will just run the default params. You may add query parameters as part of the POST params data: ([see this example](#curl-with-parameters)).
## Python
```
import dotenv
import os
import json
import requests
import pandas as pd
import time

# load .env file
dotenv.load_dotenv('/Users/zokum/Documents/Workspace/misc/.env')
# get API key
api_key = os.environ["DUNE_API_KEY"]
# authentiction with api key
headers = {"X-Dune-API-Key": api_key}

query_id = 1252207
base_url = f"https://api.dune.com/api/v1/query/{query_id}/execute"
params = {
    "performance": "large",
}
result_response = requests.request("POST", base_url, headers=headers, params=params)
```

This will give the response

```
{'execution_id': '01GXXWZSXR85GYT6K5EBRSYZ7C', 'state': 'QUERY_STATE_PENDING'}
```


### cURL

```
curl -X POST "https://api.dune.com/api/v1/query/{{query_id}}/execute"   \
  -H X-Dune-API-key: {{api_key}}
```

### cURL with Parameters

```
curl -X POST "https://api.dune.com/api/v1/query/{{query_id}}/execute"   \
  -H "X-Dune-API-Key: {{api_key}}                                       \
  -H "Content-Type: application/json"                                   \
  -d '{"query_parameters": {"param1":24}, "performance": "large"}'
```

## Example Response

!!! info "Dune API responses are delivered in JSON format."

```json
{
    "execution_id": "01GB1Y2MRA4C9PNQ0EQYVT4K6R",
    "state": "QUERY_STATE_PENDING"
}
```

 - *execution_id* : A unique ID that is generated every time this API is called. You might want to save it to later pass on to other API endpoints.
 - *state* : The current state of the query's execution. Check our `FAQ` section to see what different status codes mean.
