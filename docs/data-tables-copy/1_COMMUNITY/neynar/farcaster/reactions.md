# Reactions

### **dune.neynar.dataset_reactions**

This table contains data about likes and recast events on the Farcaster protocol.

| **Column name**       | **Type**                        | **Description**                                           |
| --------------------- | ------------------------------- | --------------------------------------------------------- |
| id                    | bigint                          | Row id                                                    |
| created\_at           | timestamp without timezone      | Timestamp of creation within database                     |
| updated\_at           | timestamp without timezone      | Timestamp of update within database                       |
| deleted\_at           | timestamp without timezone      | Timestamp of deletion on Farcaster protocol               |
| timestamp             | timestamp without timezone      | Timestamp of creation on Farcaster protocol               |
| fid                   | bigint                          | User ID of user on Farcaster protocol                     |
| reaction\_type        | smallint                        | Type of reaction: 1 = like, 2 = recast                    |
| hash                  | bytea                           | Reaction hash                                             |
| target\_hash          | bytea                           | Hash of the cast that the user is reacting to             |
| target\_fid           | bigint                          | FID of the user who wrote the target_hash                 |
| target\_url           | text                            | URL that the user is reacting to                          |

See more [here](https://github.com/farcasterxyz/protocol/discussions/71) for discussions on how Farcaster protocol handles flexible target URLs.
