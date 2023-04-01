[View code on GitHub](https://dune.com/docs/data-tables/spellbook/top tables/tokens.md)

# Tokens

This section of the app technical guide for the Dune Docs project covers token transfers and metadata. The guide is aimed at individuals who will be working with fungible (ERC20) and non-fungible (ERC721 and ERC1155) tokens in their analysis. The guide provides information on two metadata tables and two transfer tables that are essential for working with tokens.

The metadata tables include:

1. `tokens.erc20`: This table contains useful information such as the token `symbol` and the `decimals` for any given `contract_address`. The `decimals` information is needed to get the actual amount from raw amounts in on-chain data.

2. `tokens.nft`: This table contains the collection `name` and `symbol` for any given `contract_address`.

These tables are usually joined on `contract_address` at the end of a query to make everything more human-readable.

The transfer tables include:

1. `erc20_ethereum.evt_Transfer`: This table contains all transfer events for every ERC20 token. The guide provides a link to a video guide that explains how to get ERC20 balances, mints, and burns.

2. `nft.transfers`: This table contains all transfer events for every ERC721 or ERC1155 token. The guide provides a link to a guide that explains how to leverage this table to find NFT balances, transfers, and mints.

If you're looking for information on how to calculate native token balances like Ethereum (ETH) balances, the guide provides a link to another guide that covers this topic.

Overall, this section of the app technical guide provides essential information for individuals working with tokens in their analysis. The metadata and transfer tables are crucial for understanding token transfers and metadata, and the guide provides links to additional resources for further learning.
## Questions: 
 1. What types of tokens does this app support?
- The app supports both fungible (erc20) and nonfungible (erc721 and erc1155) tokens.

2. What information can be found in the metadata tables?
- The metadata tables contain information such as the token symbol, decimals, collection name, and symbol for a given contract address.

3. What transfer events can be found in the transfer tables?
- The transfer tables contain all transfer events for erc20, erc721, and erc1155 tokens, and can be used to find balances, transfers, mints, and burns.