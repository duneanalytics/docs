---
title: API Reference
description: Learn everything about how to use our Dune API here, including common errors
---

Here are all endpoints: 

!!! abstract "ALL ENDPOINTS"

    === "Executing Queries"

        POST [/api/v1/query/{{query_id}}/execute](../api-reference/execute-queries/execute-query-id.md)<br>
        POST [/api/v1/execution/{{execution_id}}/cancel](../api-reference/execute-queries/cancel-execution.md)

    === "Getting Results"

        GET [/api/v1/execution/{{execution_id}}/status](../api-reference/get-results/execution-status.md)<br>
        GET [/api/v1/execution/{{execution_id}}/results](../api-reference/get-results/execution-status.md)<br>
        GET [/api/v1/execution/{{execution_id}}/results/csv](../api-reference/get-results/execution-status.md)<br>
        GET [/api/v1/query/{{query_id}}/results](../api-reference/get-results/execution-results.md)<br>
        GET [/api/v1/query/{{query_id}}/results/csv](../api-reference/get-results/execution-results.md)

    === "Editing Queries (CRUD API)"

        POST [/api/v1/query/](../api-reference/edit-queries/create-query.md)<br>
        PATCH [/api/v1/query/{{query_id}}](../api-reference/edit-queries/update-query.md)<br>
        GET [/api/v1/query/{{query_id}}](../api-reference/edit-queries/get-query.md)<br>
        POST [/api/v1/query/{{query_id}}/archive](../api-reference/edit-queries/archive-query.md)<br>
        POST [/api/v1/query/{{query_id}}/unarchive](../api-reference/edit-queries/archive-query.md)<br>
        POST [/api/v1/query/{{query_id}}/private](../api-reference/edit-queries/private-query.md)<br>
        POST [/api/v1/query/{{query_id}}/unprivate](../api-reference/edit-queries/private-query.md)

    === "Data Uploads"

        POST [https://api.dune.com/api/v1/table/upload/csv](../api-reference/upload-data/index.md)

<div class="grid cards" markdown>

-   #### Authentication
-   
    Learn how to authenticate with our API.  

-   #### Errors Codes

    Get a comprehensive overview of the different error codes you may encounter while using our API, along with their meanings and potential solutions for troubleshooting.

-   #### Executing Queries

    Turn existing queries into endpoints and progmatically execute them.

-   #### Getting Results

    Get results of executed queries.

-   #### Editing Queries (CRUD API)

    CRUD API endpoints enables users to create, read, update, or archive queries *beyond* the Dune IDE, enabling more flexible integration of Dune API into your workflow and freeing you from UI-exclusive query editing.

-   #### Uploading Data (Write API)

    Use Dune's write API to upload CSV files to a specific table in the Dune database.
    
</div>
