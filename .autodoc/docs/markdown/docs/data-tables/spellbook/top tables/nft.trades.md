[View code on GitHub](https://dune.com/docs/data-tables/spellbook/top tables/nft.trades.md)

The `nft.trades` technical guide is a documentation of the effort to make NFT trading data easily available to everyone on Dune. The guide provides an overview of the `nft.trades` table, which aggregates and standardizes the data between different data platforms and provides auxiliary information and metadata all in one table. The guide explains how the dataset makes it extremely easy to query for any NFT related trading data across all indexed platforms. 

The guide provides information on how the `nft.trades` table works, including Single Item Trade, Bundle Trade, and Aggregator Trade. The Single Item Trade occurs between a buyer and a seller, and they exchange an item that is uniquely identified by the combination of `nft_contract_address` and `token_id`. The Bundle Trade contains multiple items, and each of these items is uniquely identified through a combination of `nft_contract_address` and `token_id`. The Aggregator Trade is a trade in which a single trade transaction contains multiple items, and the approach is to unravel aggregator trades so that each row corresponds to a unique item that was traded, with its associated ID, price, collection, etc.

The guide also provides information on Platform and Royalty Fees. In the most recent version of `nft.trades`, information about the amount and percent of royalty fees in the original amount and in USD is available when this information was able to be retrieved. Royalty fees are going to the creator, and Platform fees are collected by the NFT platform. 

The guide provides examples of queries that can be run on the `nft.trades` table, including All trades for a given NFT, Trades in the last 24 hour on a given platform, and Platform volumes in the last year. The guide also provides examples of dashboards that utilize parameters and look across the entire ecosystem.

Finally, the guide provides a column data table that lists the column name, data type, and description of the `nft.trades` table. The guide also explains that the SQL code that processes the data for every marketplace is open source and available in their GitHub repository. Everyone can review the code, make pull requests, and submit code to add more marketplaces.
## Questions: 
 1. What platforms are currently indexed by nft.trades?
- OpenSea, Rarible, SuperRare, CryptoPunks, Foundation, and LooksRare are currently indexed by nft.trades.

2. What metadata is provided about the traded NFT?
- The metadata provided about the traded NFT includes nft_project_name and erc_standard.

3. Can a blockchain SQL analyst add their own aggregator platform to the nft.trades table?
- Yes, a blockchain SQL analyst can make a pull request to add their own aggregator platform to the nft.trades table.