---
title: API Reference
description: Learn everything about how to use our Dune API here, including common errors
---

**The Dune API is flexible and powerful!** We can largely bucket Dune API features into these categories: 

1. 🪄 **Executing queries** - turning an existing query into an endpoint and execute it, or retrieve latest results associated 
2. 💫 **Editing queries** (**CRUD** [Create, Retrieve, Update, Delete/Archive] API) 
<!-- 3. 🪄 **Uploading data** (Write API)  -->

!!! abstract "ALL ENDPOINTS"

    === "Query Execution"

        POST [/api/v1/query/{{query_id}}/execute](../api-reference/execute-queries/execute-query-id.md)
        POST [/api/v1/execution/{{execution_id}}/cancel](../api-reference/execute-queries/cancel-execution.md)

    === "Query Results"

        GET [/api/v1/execution/{{execution_id}}/status](../api-reference/get-results/execution-status.md)
        GET [/api/v1/execution/{{execution_id}}/results](../api-reference/get-results/execution-status.md)
        GET [/api/v1/execution/{{execution_id}}/results/csv](../api-reference/get-results/execution-status.md)
        GET [/api/v1/query/{{query_id}}/results](../api-reference/get-results/execution-results.md)
        GET [/api/v1/query/{{query_id}}/results/csv](../api-reference/get-results/execution-results.md)

    === "CRUD Query Management"

        POST [/api/v1/query/](../api-reference/edit-queries/create-query.md)
        PATCH [/api/v1/query/{{query_id}}](../api-reference/edit-queries/update-query.md)
        GET [/api/v1/query/{{query_id}}](../api-reference/edit-queries/get-query.md)
        POST [/api/v1/query/{{query_id}}/archive](../api-reference/edit-queries/archive-query.md)
        POST [/api/v1/query/{{query_id}}/unarchive](../api-reference/edit-queries/archive-query.md)
        POST [/api/v1/query/{{query_id}}/private](../api-reference/edit-queries/private-query.md)
        POST [/api/v1/query/{{query_id}}/unprivate](../api-reference/edit-queries/private-query.md)

    === "Data Uploads"

        POST [https://api.dune.com/api/v1/table/upload/csv](../api-reference/upload-data/index.md)

!!! info end "Feature Availability"
    🪄 denotes features available to Community users whereas 💫 denotes features only available to Premium users. 

    For more information on features included in each plan, please refer to our [subscripiton page](https://dune.com/pricing).


<div class="grid cards" markdown>

-   #### Authentication

    ---

    Learn how to authenticate with our API.  
    
    [→ Authentication](authentication.md)

-   #### Errors Codes

    ---

    Get a comprehensive overview of the different error codes you may encounter while using our API, along with their meanings and potential solutions for troubleshooting.
    
    [→ Error Codes](errors.md)

-   #### Executing Queries

    ---

    Turn existing queries into endpoints and progmatically execute them.
    
    [→ Executing Queries](execute-queries/index.md)

    - [Execute Query Via Query ID](../api-reference/execute-queries/execute-query-id.md)
    - [Cancel Execution](../api-reference/execute-queries/cancel-execution.md)

-   #### Getting Results

    ---

    Get results of executed queries.
    
    [→ Executing Queries](get-results/index.md)

    - [Check Execution Status](../api-reference/get-results/execution-status.md)
    - [Get Execution Results](../api-reference/get-results/execution-results.md)
    - [Get Latest Query Results](../api-reference/get-results/latest-results.md)

-   #### Editing Queries (CRUD API)

    ---

    CRUD API endpoints enables users to create, read, update, or archive queries *beyond* the Dune IDE, enabling more flexible integration of Dune API into your workflow and freeing you from UI-exclusive query editing.

    [→ CRUD API](edit-queries/index.md)
    
    - [Create Query](../api-reference/edit-queries/create-query.md)
    - [Update Query](../api-reference/edit-queries/update-query.md)
    - [Retrieve or Get Query](../api-reference/edit-queries/get-query.md)
    - [Archive Query](../api-reference/edit-queries/archive-query.md)
    - [Make Query Private](../api-reference/edit-queries/private-query.md)
    - [How to Pass Parameters](../api-reference/edit-queries/parameter-passing.md)

<!-- -   #### Uploading Data (Write API)

    ---

    Use Dune's write API to upload CSV files to a specific table in the Dune database.

    [→ Write API](data-upload/write-api.md) -->
    
</div>
