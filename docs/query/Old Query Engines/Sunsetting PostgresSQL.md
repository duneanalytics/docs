---
title: Sunsetting PostgresSQL
description: Dune is sunsetting PostgreSQL. Support for PostgreSQL will be removed on 2023-07-31. Please migrate your queries to DuneSQL.
---

Dune is progressively ceasing to support PostgreSQL instances. All Chains are their own instance of PostgreSQL, which makes it difficult to scale and maintain. We are sunsetting PostgreSQL in favor of [DuneSQL](../query/index.md), which is a more scalable and flexible solution. 

We have started decommissioning blockchains on V1 as we transition to V2 as our primary platform.

Once a chain is commissioned, queries referncing the V1 version won't be editable anymore until you log in and select DuneV2 from the data explorer drop down to re-run them as V2 queries.

Please also note:

- No new contracts that are submitted for decoding (on all blockchains) will be decoded on V1, they will only be decoded on V2 (already decoded contracts will continue to work as normal) 
- No new Abstraction PRs will be merged on V1 (please use Spellbook on V2)
 
_special cases can be individually reviewed_ 

## Decommissioning Schedule for Dune V1 Databases

| Blockchain | 1. Step  (Kickoff)            | 2. Step    | 3. Step    | 4. Step (Decommission Completed)|
|------------|-------------------------------|------------|------------|---------------------------------|
| BNB        | 02/11/2022                    | 23/11/2022 | 19/01/2023 | 31/01/2023                      |
| Polygon    | 02/11/2022                    | 23/11/2022 | 19/01/2023 | 31/01/2023                      |
| xDAI       | 19/01/2023                    | 09/02/2023 | 02/03/2023 | 31/03/2023                      |
| Optimism   | 19/01/2023                    | 09/02/2023 | 02/03/2023 | 31/03/2023                      |
| Ethereum   | 07/04/2023                    | 01/05/2023 | TBD        | 31/07/2023                      |

## Decommissioning details:

The process below is the same for all blockchains based on when the kickoff date is announced for decommissioning. 

**1. Step (Start)**  
Kicking of the decommissioning, no changes to V1 queries.   
A fair warning that the blockchain will be decommissioned in the future.    

**2. Step**    
Removal of the blockchain from the blockchain selection dropdown.  
Existing queries are still editable on V1.  
No new queries can be created on V1 dataset.  

**3. Step**    
V1 queries for the given blockchain will become read only, forking and updating to DuneSQL is required.  
Queries can still be run, but no changes can be made.

**4. Step(End)**    
No new data will be ingested and no new query executions on V1 databases, decommission complete. 
Queries have to be forked and adjusted to V2.



## To learn more and ask questions

- Check out our [DuneSQL](../query/index.md) to learn more about how V2 works.
- Check out our [Data Explorer guide](../app/queries/data-explorer.md) to learn more about how searching in V2 works.
- Watch our [Dune Arcana](https://dune.com/watch) videos for general insights - they all use DuneSQL
- ask in our [#query-questions Discord channel](https://discord.gg/dunecom)

