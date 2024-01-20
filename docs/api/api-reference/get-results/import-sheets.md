---
title: Import to Google Sheets
description: Here's how to import your results into a google sheet without any coding.
---
!!! warning
    Our API docs have moved to [here](https://dune.mintlify.app/api-reference/overview/introduction), this reference page will be deprecated soon.

Import your query results easily into a google sheet without any coding. Empower your finance, operations, and business teams to work with blockchain data in Google sheets.

1. Use "Import Data" to import your CSV results into a google sheet using "api_key" as a param. (We advise against doing this any public document where your API key can be viewed and compromised.)<br>
```=importData("https://api.dune.com/api/v1/query/{{query_id}}/results/csv?api_key={{api_key}}")```
    
2. [Schedule a query execution](https://dune.com/docs/app/query-editor/query-scheduler/?h=scheduling) to have your results regularly updated on a set schedule. 
![image (7)](https://user-images.githubusercontent.com/105652677/220012986-aaf6f372-8f4c-4e30-8da3-25e87a5271ab.png)
