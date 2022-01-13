# Token standards

## Interfaces

When we’re interested in a subset of events fired regardless of the origin contract, Dune uses interface-decoding. Notable examples include erc20, erc721 and erc1155 transfer events. This method is reserved for special cases. These tables make it easy to keep track of ERC20 tokens and NFT's flowing in and out of contracts and wallets and are widely used across dune.

**erc20."ERC20\_evt\_Transfer"**

| column name        | **data type** | **description**                                                                                                |
| ------------------ | ------------- | -------------------------------------------------------------------------------------------------------------- |
| from               | bytea         | the transactions sender                                                                                        |
| to                 | bytea         | the transaction receiver                                                                                       |
| value              | numeric       | the amount of erc20 tokens sent. Notice that you have divide this by the relevant decimals of the erc20 token. |
| contract\_address  | bytea         | the contract\_address of the erc20 token                                                                       |
| evt\_tx\_hash      | bytea         | the transaction hash                                                                                           |
| evt\_index         | numeric       | the transaction index                                                                                          |
| evt\_block\_time   | timestamptz   | the time at which the transaction occurred                                                                     |
| evt\_block\_number | int8          | the length of the blockchain                                                                                   |

[See this table in action](https://dune.xyz/queries/39012)

**erc721."ERC721\_evt\_Transfer"**

| **c**olumn name    | **data type** | **description**                                 |
| ------------------ | ------------- | ----------------------------------------------- |
| from               | bytea         | the transactions sender                         |
| to                 | bytea         | the transaction receiver                        |
| tokenID            | numeric       | The Token ID which uniquely identifies this NFT |
| contract\_address  | bytea         | the contract\_address of the erc20 token        |
| evt\_tx\_hash      | bytea         | the transaction hash                            |
| evt\_index         | numeric       | the transaction index                           |
| evt\_block\_time   | timestamptz   | the time at which the transaction occurred      |
| evt\_block\_number | int8          | the length of the blockchain                    |

[See this table in action](https://dune.xyz/queries/38974)

You can query for special tables using this query:

**Contracts that are “interface”-decoded**

```sql
SELECT * FROM ethereum."contracts" WHERE address IS NULL;
```
