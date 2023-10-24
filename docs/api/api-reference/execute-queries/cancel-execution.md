---
title: Cancel Execution
description: Here's how to cancel your Dune API execution requests.
---

!!! abstract "ENDPOINTS"
    ```
    POST /api/v1/execution/{{execution_id}}/cancel
    ```

This endpoint allows you to cancel an triggered execution request. You must pass the **`execution_id`** obtained from making a [Execute Query ID POST](execute-query-id.md) request. Result returns a boolean for whether the execution is successfully canceled.

## Example Request 

### cURL

```cURL
curl -X POST -H x-dune-api-key:{{api_key}} "https://api.dune.com/api/v1/execution/{{execution_id}}/cancel"
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
base_url = f"https://api.dune.com/api/v1/execution/{query_id}/cancel"
result_response = requests.request("POST", base_url, headers=headers)

```

## Example Return

```json
{
    "success": true
}
```