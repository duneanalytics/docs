[View code on GitHub](https://dune.com/docs/api/quick-start/api-ready-queries.md)

# API Ready Queries

This technical guide provides a list of queries that are ready for API use in the Dune Docs project. The guide contains four queries, each with a unique query ID that can be used in any of the API guides or can be forked and modified to create a new query ID for use in the API. 

## Get the ERC20 balances for a given address

This query provides the ERC20 token balances for a given address. The query ID is 1616880, and it requires the following parameters:

- `address`: The address that you would like to get balances for. It must be a valid EVM address.
- `blocknumber`: The cutoff block for checking balances. Use 0 if you want the most recent block, otherwise any block number that has been processed will work (~3 minute/15 block delay).
- `chain`: The EVM chain you'd like to check balances for. Valid choices include `ethereum`, `polygon`, `bnb`, `optimism`, `arbitrum`, `avalanche_c`, and `gnosis`.
- `dust`: Keep or remove dust tokens (worth less than $0.01). Valid choices are `keep` or `remove`.

The output columns include:

- `symbol`: The token symbol, if available.
- `notional_value`: The notional amount of tokens held, rounded to 5 decimals.
- `total_value`: The $USD value of tokens held, rounded to 3 decimals.
- `token_price`: The $USD price of the token.

## Get all the holders and their balances for a given ERC20 address

This query provides all the holders and their balances for a given ERC20 address. The query ID is 1618116, and it requires the following parameters:

- `address`: The ERC20 token address you would like to get holders of. It must be a valid EVM address.
- `blocknumber`: The cutoff block for checking balances. Use 0 if you want the most recent block, otherwise any block number that has been processed will work (~3 minute/15 block delay).
- `chain`: The EVM chain you'd like to check balances for. Valid choices include `ethereum`, `polygon`, `bnb`, `optimism`, `arbitrum`, `avalanche_c`, and `gnosis`.

The output columns include:

- `holder`: The address of the holder.
- `holder_ens`: The ENS of the holder address, if any.
- `notional_value`: The notional amount of tokens held, rounded to 5 decimals.
- `total_value`: The $USD value of tokens held, rounded to 3 decimals.
- `token_price`: The $USD price of the token.

## Get the NFT balances for a given address

This query provides the NFT balances for a given address. The query ID is 1617158, and it requires the following parameters:

- `address`: The address that you would like to get balances for. It must be a valid EVM address.
- `blocknumber`: The cutoff block for checking balances. Use 0 if you want the most recent block, otherwise any block number that has been processed will work (~3 minute/15 block delay).
- `chain`: The EVM chain you'd like to check balances for. Valid choices include `ethereum`, `polygon`, `bnb`, `optimism`, `arbitrum`, `avalanche_c`, and `gnosis`.

The output columns include:

- `symbol`: The symbol of the NFT, if available.
- `name`: The name of the NFT, if available.
- `category`: The category of the NFT, if available.
- `token_id`: The token ID of the NFT.
- `contract_address`: The contract address of the NFT.
- `acquired_how`: Whether the NFT was `minted` or `transferred/bought`.
- `acquired_on_block_number`: The block number that the NFT was received on.

## Get all the holders and their balances for a given NFT address

This query provides all the holders and their balances for a given NFT address. The query ID is 1618122, and it requires the following parameters:

- `address`: The NFT address that you would like to get holders of. It must be a valid EVM address.
- `blocknumber`: The cutoff block for checking balances. Use 0 if you want the most recent block, otherwise any block number that has been processed will work (~3 minute/15 block delay).
- `chain`: The EVM chain you'd like to check balances for. Valid choices include `ethereum`, `polygon`, `bnb`, `optimism`, `arbitrum`, `avalanche_c`, and `gnosis`.

The output columns include:

- `holder`: The address of the holder.
- `holder_ens`: The ENS of the holder address, if any.
- `tokens_held`: The number of NFTs from this contract held.
- `token_ids`: An array of all the token IDs held.
## Questions: 
 1. What are the valid choices for the `chain` parameter in each of the queries?
- Valid choices for the `chain` parameter in each of the queries are `ethereum`, `polygon`, `bnb`, `optimism`, `arbitrum`, `avalanche_c`, and `gnosis`.

2. What is the delay between block processing and when the `blocknumber` parameter can be used in each of the queries?
- The delay between block processing and when the `blocknumber` parameter can be used in each of the queries is approximately 3 minutes or 15 blocks.

3. What is the difference between the `notional_value` and `total_value` output columns in each of the queries?
- The `notional_value` output column in each of the queries represents the notional amount of tokens or NFTs held, rounded to 5 decimals. The `total_value` output column represents the $USD value of tokens or NFTs held, rounded to 3 decimals.