---
title: Execute Query ID
description: Here's how to execute (run) a Query with or without parameters to retrieve data.
---

!!! abstract "ENDPOINTS"
    ```
    POST /api/v1/query/{{query_id}}/execute
    ```

This endpoint allows you to execute, or run a query for the specified query id. 

If the query has parameters and you don't add them in your API call, it will just run the default params. You may add query parameters as part of the POST params data.

You can choose to include a `performance` parameter, by default it will use the "medium" performance tier which consumes 10 credits. "large" will use 20 credits. You cannot run API executions on the free tier. Result returns an `execution_id` for the specified request.

!!!tip "Careful of Credit Limits"
    Make sure you check the query in the app interface to see how many rows and columns of data are being returned, so that you don't spend all of your credits in one query read. The free tier gets 2.5k credits, which at 1000 datapoints a credit allows you to return 2.5 million rows and 1 column (or 1.25m rows and 2 columns, 250k rows and 10 columns, etc.). There won't be overage charges (unless you've changed this setting), but still be sure to double check.

## Example Request

### cURL

```cURL

curl -X POST "https://api.dune.com/api/v1/query/{{query_id}}/execute"   \
  -H "X-Dune-API-Key: {{api_key}}                                       \
  -H "Content-Type: application/json"                                   \
  -d '{"query_parameters": {"param1":24}, "performance": "large"}'

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

query_id = 1252207
base_url = f"https://api.dune.com/api/v1/query/{query_id}/execute"
params = {
    "performance": "large",
}
result_response = requests.request("POST", base_url, headers=headers, params=params)
```


## Example Response

```json
{
    "execution_id": "01GB1Y2MRA4C9PNQ0EQYVT4K6R",
    "state": "QUERY_STATE_PENDING"
}
```

 - *execution_id* : A unique ID that is generated every time this API is called. You might want to save it to later pass on to other API endpoints.
 - *state* : The current state of the query's execution. Check our [`FAQ` section](../../FAQ/functionality.md#what-is-the-difference-between-the-states-executing-and-pending) to see what different status codes mean.
