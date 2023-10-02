# Fnames

### **dune.neynar.dataset_farcaster_fnames**

This table contains usernames associated with FIDs on the Farcaster protocol.

| **Column name**       | **Type**                        | **Description**                                           |
| --------------------- | ------------------------------- | --------------------------------------------------------- |
| id                    | bigint                          | Row id                                                    |
| created\_at           | timestamp without timezone      | Timestamp of creation within database                     |
| updated\_at           | timestamp without timezone      | Timestamp of update within database                       |
| deleted\_at           | timestamp without timezone      | Timestamp of deletion on Farcaster protocol               |
| timestamp             | timestamp without timezone      | Timestamp of creation on Farcaster protocol               |
| fid                   | bigint                          | User ID of user on Farcaster protocol                     |
| custody\_address      | bytea                           | Address that stores the FC profile for the user           |
| expires\_at           | timestamp without timezone      | Timestamp when username expires for the user              |
