---
title: Import to Google Sheets
description: Here's how to import your results into a google sheet without any coding.
---

1. In order to get the latest results in CSV format, append "/csv": ``` GET /api/v1/query/{{query_id}}/results/csv ```
 The results will be returned in CSV format without additional metadata details like the JSON response.
2. Use "Import Data" to import your CSV results into a google sheet using "api_key" as a param  ```=importData("https://api.dune.com/api/v1/query/{{query_id}}/results/csv?api_key={{api_key}}")```
(We advise against doing this any public document where your API key can be viewed and compromised.)
    
3. [Schedule a query execution](https://dune.com/docs/app/query-editor/query-scheduler/?h=scheduling) to have your results updated on a set schedule. 
![image (7)](https://user-images.githubusercontent.com/105652677/220012986-aaf6f372-8f4c-4e30-8da3-25e87a5271ab.png)
