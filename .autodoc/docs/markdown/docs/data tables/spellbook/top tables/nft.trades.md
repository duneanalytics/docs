[View code on GitHub](https://dune.com/blob/master/data tables\spellbook\top tables\nft.trades.md)

The `nft.trades` technical guide provides an overview of the effort to make NFT trading data easily available to everyone on Dune. The guide explains that the table aggregates and standardizes data between different data platforms and provides auxiliary information and metadata all in one table. The guide also lists the platforms that have been indexed so far, including OpenSea, Rarible, SuperRare, CryptoPunks, Foundation, and LooksRare.

The guide explains how single item trades work, including the exchange of an item between a buyer and a seller, the identification of the item through a combination of `nft_contract_address` and `token_id`, and the metadata associated with the trade. The guide also explains how bundle trades and aggregator trades work and provides recommendations for working with these types of trades.

The guide includes examples of SQL queries that can be used to retrieve data from the `nft.trades` table, including all trades for a given NFT, trades in the last 24 hours on a given platform, and platform volumes in the last year. The guide also includes examples of dashboards that utilize parameters and look across the entire ecosystem.

The guide provides a detailed list of column data, including the data type and description of each column. The guide also explains that the SQL code that processes the data for every marketplace is open source and available in the Dune Analytics GitHub repository, allowing anyone to review the code, make pull requests, and submit code to add more marketplaces.

Overall, the `nft.trades` technical guide provides a comprehensive overview of the effort to make NFT trading data easily available to everyone on Dune, including how the table works, how different types of trades work, examples of SQL queries and dashboards, and a detailed list of column data.
## Questions: 
 1. What platforms are currently indexed by nft.trades?
- OpenSea, Rarible, SuperRare, CryptoPunks, Foundation, and LooksRare are currently indexed by nft.trades.

2. What metadata is provided about the traded NFT?
- The metadata provided about the traded NFT includes nft_project_name and erc_standard.

3. What should be done if a platform is not indexed by nft.trades?
- If a platform is not indexed by nft.trades, the SQL code that processes the data for every marketplace is open source and available in their GitHub repository. Anyone can review the code, make pull requests, and submit code to add more marketplaces.