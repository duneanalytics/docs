---
title: Sunsetting SparkSQL
description: Dune is sunsetting SparkSQL. Support for SparkSQL will be removed on 2023-07-31. Please migrate your queries to DuneSQL.
---



Dune is progressively ceasing to support SparkSQL. SparkSQL has turned out to be a poor fit for our use case and we are moving to a new query engine called [DuneSQL](../query/index.md). 

SparkSQL queries will be depreceated on 2023/07/31.

## What does this mean for you?

Once SparkSQL is decomissioned, queries referencing SparkSQL won't be editable anymore until you select DuneV2 from the data explorer drop down to re-run them as V2 queries.  
You will need to either manually adjust the Syntax or use the [DuneSQL Migration Tool](../query/migration-tool.md) to migrate your queries to DuneSQL.

Please also note:

- No new contracts that are submitted for decoding (on all blockchains) will be decoded on V1, they will only be decoded on V2 (already decoded contracts will continue to work as normal) 
- No new Abstraction PRs will be merged on V1 (please use Spellbook on V2)
 
_special cases can be individually reviewed_ 

## Decommissioning Schedule for Dune V1 Databases

| 1. Step  (Kickoff)            | 2. Step    | 3. Step    | 4. Step (Decommission Completed)|
|-------------------------------|------------|------------|---------------------------------|
| 2023/04/07                    | 2023/07/01 | 2023/07/15 | 2023/07/31                      |

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

