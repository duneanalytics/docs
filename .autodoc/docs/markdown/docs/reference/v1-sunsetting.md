[View code on GitHub](https://dune.com/blob/master/reference\v1-sunsetting.md)

The technical guide titled "Sunsetting Dune V1" provides information on the decommissioning of the V1 platform of the Dune Engine. The guide explains that with the release of the Polygon decoded tables on Dune Engine V2, all raw and decoded data that was on V1 is now available on V2. As a result, the V1 platform is being decommissioned, and the guide provides details on the decommissioning process.

The guide explains that once a chain is commissioned, queries referencing the V1 version won't be editable anymore until the user logs in and selects DuneV2 from the data explorer drop-down to re-run them as V2 queries. The guide also notes that no new contracts submitted for decoding on all blockchains will be decoded on V1, and no new Abstraction PRs will be merged on V1.

The guide provides a decommissioning schedule for Dune V1 databases, which includes the kickoff date for each blockchain, the date when the blockchain will be removed from the blockchain selection dropdown, the date when V1 queries for the given blockchain will become read-only, and the date when no new data will be ingested, and no new query executions on V1 databases will be allowed.

The guide also provides links to resources where users can learn more about how V2 works, how searching in V2 works, and general insights on Dune V2. Users can check out the DuneSQL to learn more about how V2 works, the Data Explorer guide to learn more about how searching in V2 works, and watch Dune Arcana videos for general insights. Additionally, users can join live Office Hours or ask in the #query-questions Discord channel to ask questions.

Overall, the guide provides a comprehensive overview of the decommissioning process of the V1 platform of the Dune Engine and provides users with the necessary information to transition to the V2 platform.
## Questions: 
 1. What is the reason for sunsetting Dune V1 and transitioning to V2 as the primary platform?
- The reason for sunsetting Dune V1 and transitioning to V2 as the primary platform is due to the release of the Polygon decoded tables on Dune Engine V2, which now has all Raw and Decoded data that was on V1 on V2.

2. What are the implications for existing and new contracts submitted for decoding on all blockchains?
- No new contracts that are submitted for decoding (on all blockchains) will be decoded on V1, they will only be decoded on V2 (already decoded contracts will continue to work as normal).

3. What is the timeline for decommissioning each blockchain on Dune V1?
- The timeline for decommissioning each blockchain on Dune V1 is provided in the Decommissioning Schedule for Dune V1 Databases table, which includes the kickoff date for decommissioning, removal of the blockchain from the blockchain selection dropdown, read-only access to V1 queries, and the end of decommissioning.