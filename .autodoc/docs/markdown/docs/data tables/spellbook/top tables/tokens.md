[View code on GitHub](https://dune.com/blob/master/data tables\spellbook\top tables\tokens.md)

The Tokens section of the app technical guide for the Dune Docs project covers token transfers and metadata. The guide is aimed at analysts who will be working with both fungible (erc20) and non-fungible (erc721 and erc1155) tokens. The guide provides information on several tables that are essential for working with tokens.

The Metadata tables section of the guide covers two tables: tokens.erc20 and tokens.nft. The tokens.erc20 table contains useful information such as the token symbol and the decimals for any given contract_address. The latter is needed to get the actual amount from raw amounts in on-chain data. The tokens.nft table contains the collection name and symbol for any given contract_address. These tables are usually joined on contract_address at the end of a query to make everything more human-readable.

The Transfer tables section of the guide covers two tables: erc20_ethereum.evt_Transfer and nft.transfers. The erc20_ethereum.evt_Transfer table contains all transfer events for every erc20 token. Analysts can find how to get erc20 balances, mints, and burns using a provided guide. The nft.transfers table contains all transfer events for every erc721 or erc1155 token. Analysts can learn how to leverage this to find nft balances, transfers, and mints in a provided guide.

Finally, the guide provides a link to a guide on how to calculate native token balances like ethereum (ETH) balances. This guide is useful for analysts who need to calculate balances for native tokens.

Overall, the Tokens section of the app technical guide provides essential information for analysts working with tokens. The guide covers metadata and transfer tables for both fungible and non-fungible tokens, as well as a guide on how to calculate native token balances.
## Questions: 
 1. What types of tokens does this app support?
   - The app supports both fungible (erc20) and nonfungible (erc721 and erc1155) tokens.
2. What information can be found in the metadata tables?
   - The metadata tables contain information such as the token symbol, decimals, collection name, and symbol for a given contract address.
3. What transfer events can be found in the transfer tables?
   - The transfer tables contain all transfer events for erc20, erc721, and erc1155 tokens, which can be used to find balances, transfers, mints, and burns.