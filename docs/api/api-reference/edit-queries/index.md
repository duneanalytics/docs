---
title: Editing (CRUD) Queries
description: Learn how to CRUD queries via Dune API
---

CRUD API endpoints enables users to create, read, update, or archive queries *beyond* the Dune IDE, enabling more flexible integration of Dune API into your workflow and freeing you from UI-exclusive query editing. Learn more about our CRUD queries feature:

!!! success end "Note" 
    CRUD queries is an advanced feature included only in our Premium subscription plans. Please upgrade your plan to use it.
    
!!! info end "What is CRUD"
    1. CRUD operations, standing for Create, Read, Update, and Delete, are the four basic functions that a software application needs to interact with data. They are essential because they allow you to add new data (Create), view existing data (Read), modify existing data (Update), and remove data (Delete) in your database or other storage systems.
    2. In Dune context, `delete` aciton is replaced by `archive` as deletion of queries is not possible.


<div class="cards grid" markdown>
- [Create Query](../edit-queries/create-query.md)
- [Update Query](../edit-queries/update-query.md)
- [Retrieve or Get Query](../edit-queries/get-query.md)
- [Archive Query](../edit-queries/archive-query.md)
- [Make Query Private](../edit-queries/private-query.md)
- [How to Pass Parameters](../edit-queries/parameter-passing.md)
</div>

!!! tip 
    Unlike endpoints in [query execution](../execute-queries) group, endpoints in CRUD queries API *cannot* be cancelled, i.e. it is a sync call and there is no intermediary status.