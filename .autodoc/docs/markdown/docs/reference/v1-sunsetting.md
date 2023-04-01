[View code on GitHub](https://dune.com/docs/reference/v1-sunsetting.md)

# Sunsetting Dune V1

This technical guide covers the decommissioning of Dune Engine V1 and the transition to V2 as the primary platform. The guide provides details on the decommissioning process, including the timeline for each blockchain, and what users can expect during each step. 

The guide starts by announcing that with the release of the Polygon decoded tables on Dune Engine V2, all Raw and Decoded data that was on V1 is now on V2. As a result, the decommissioning process has started, and blockchains on V1 are being decommissioned as the transition to V2 is made. 

The guide then provides details on the decommissioning process, which is the same for all blockchains. The process has four steps, starting with a fair warning that the blockchain will be decommissioned in the future, followed by the removal of the blockchain from the blockchain selection dropdown, making existing queries still editable on V1, but no new queries can be created on V1 dataset. The third step is where V1 queries for the given blockchain become read-only, and forking and updating to DuneSQL is required. Queries can still be run, but no changes can be made. The final step is where no new data will be ingested, and no new query executions on V1 databases, decommission complete. Queries have to be forked and adjusted to V2.

The guide also provides a schedule for the decommissioning of each blockchain, including the kickoff date and the completion date for each step. 

Finally, the guide provides links to resources where users can learn more about DuneSQL, how searching in V2 works, and general insights from Dune Arcana videos. Users can also join live office hours or ask questions in the #query-questions Discord channel.

Overall, this guide provides a clear and detailed explanation of the decommissioning process for Dune Engine V1 and what users can expect during each step. It also provides helpful resources for users to learn more about the transition to V2 and ask questions.
## Questions: 
 1. What is the reason for sunsetting Dune V1 and transitioning to V2 as the primary platform?
   
   Answer: The reason for sunsetting Dune V1 and transitioning to V2 as the primary platform is due to the release of the Polygon decoded tables on Dune Engine V2, which now has all Raw and Decoded data that was on V1 on V2.

2. What are the implications for existing and new contracts that are submitted for decoding on all blockchains?
   
   Answer: No new contracts that are submitted for decoding (on all blockchains) will be decoded on V1, they will only be decoded on V2 (already decoded contracts will continue to work as normal).

3. What is the decommissioning schedule for Dune V1 databases and what are the steps involved in the decommissioning process?
   
   Answer: The decommissioning schedule for Dune V1 databases is provided in the table in the technical guide. The steps involved in the decommissioning process include: (1) kicking off the decommissioning, (2) removal of the blockchain from the blockchain selection dropdown, (3) V1 queries for the given blockchain will become read only, and (4) no new data will be ingested and no new query executions on V1 databases, decommission complete. Queries have to be forked and adjusted to V2.