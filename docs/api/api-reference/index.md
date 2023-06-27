---
title: API Reference
description: Learn everything about how to use our Dune API here, including common errors
---

**The Dune API is flexible and powerful!** We can largely bucket Dune API features into three categories: 

1. 🪄 **Executing queries** - turning an existing query into an endpoint and execute it, or retrieve latest results associated 
2. 💫 **Editing queries** (**CRUD** [Create, Retrieve, Update, Delete/Archive] API) 
3. 🪄 **Uploading data** (Write API) 


!!! info end "Feature Availability"
    🪄 denotes features available to Community users whereas 💫 denotes features only available to Premium users. 

    For more information on features included in each plan, please refer to our [subscripiton page](https://dune.com/pricing).


<div class="grid cards" markdown>

-   #### Authentication

    ---

    Learn how to authenticate with our API.  
    
    [:octicons-arrow-right-24: Authentication](authentication.md)

-   #### Errors Codes

    ---

    Get a comprehensive overview of the different error codes you may encounter while using our API, along with their meanings and potential solutions for troubleshooting.
    
    [:octicons-arrow-right-24: Error Codes](errors.md)

-   #### Executing Queries

    ---

    Turn existing queries into endpoints and progmatically execute them.
    
    [:octicons-arrow-right-24: Executing Queries](execute-queries/index.md)

    - [Execute Query Via Query ID](../api-reference/execute-queries/execute-query-id.md)
    - [Cancel Execution](../api-reference/execute-queries/cancel-execution.md)

-   #### Getting Results

    ---

    Get results of executed queries.
    
    [:octicons-arrow-right-24: Executing Queries](get-results/index.md)

    - [Check Execution Status](../api-reference/get-results/execution-status.md)
    - [Get Execution Results](../api-reference/get-results/execution-results.md)
    - [Get Latest Query Results](../api-reference/get-results/latest-results.md)

-   #### Uploading Data (Write API)

    ---

    Use Dune's write API to upload CSV files to a specific table in the Dune database.

    [:octicons-arrow-right-24: Write API](data-upload/write-api.md)

-   #### Editing Queries (CRUD API)

    ---

    CRUD API endpoints enables users to create, read, update, or archive queries *beyond* the Dune IDE, enabling more flexible integration of Dune API into your workflow and freeing you from UI-exclusive query editing.

    [:octicons-arrow-right-24: CRUD API](edit-queries/index.md)
    
    - [Create Query](../api-reference/edit-queries/create-query.md)
    - [Update Query](../api-reference/edit-queries/update-query.md)
    - [Retrieve or Get Query](../api-reference/edit-queries/get-query.md)
    - [Archive Query](../api-reference/edit-queries/archive-query.md)
    - [Make Query Private](../api-reference/edit-queries/private-query.md)
    - [How to Pass Parameters](../api-reference/edit-queries/parameter-passing.md)

</div>
