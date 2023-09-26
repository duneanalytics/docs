# Links

### **dune.neynar.dataset_farcaster_links**

This table contains data about follower and following relationships on the Farcaster protocol.

| **Column name**       | **Type**                        | **Description**                                           |
| --------------------- | ------------------------------- | --------------------------------------------------------- |
| id                    | bigint                          | Row id                                                    |
| created\_at           | timestamp without timezone      | Timestamp of creation within database                     |
| updated\_at           | timestamp without timezone      | Timestamp of update within database                       |
| deleted\_at           | timestamp without timezone      | Timestamp of deletion on Farcaster protocol               |
| timestamp             | timestamp without timezone      | Timestamp of creation on Farcaster protocol               |
| fid                   | bigint                          | User ID of user on Farcaster protocol                     |
| target\_fid           | bigint                          | FID of the user who is link target                        |
| hash                  | bytea                           | Link hash on the protocol                                 |
| type                  | text                            | Link type, usually this is a “follow”                     |
