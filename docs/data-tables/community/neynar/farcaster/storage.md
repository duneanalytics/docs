# Storage

### **dune.neynar.dataset_farcaster_storage**

This table contains data about the storage units available for users on the Farcaster protocol.

| **Column name**        | **Type**                           | **Description**                                          |
|------------------------|------------------------------------|----------------------------------------------------------|
| id                     | bigint                             | Row id                                                   |
| created\_at            | timestamp without timezone         | Timestamp of creation within database                    |
| updated\_at            | timestamp without timezone         | Timestamp of update within database                      |
| deleted\_at            | timestamp without timezone         | Timestamp of deletion on Farcaster protocol              |
| timestamp              | timestamp without timezone         | Timestamp of creation on Farcaster protocol              |
| fid                    | bigint                             | User ID of user on Farcaster protocol                    |
| units                  | bigint                             | Units of storage available for the user on the protocol  |
| expiry                 | timestamp without timezone         | Time when storage expires for user                       |

