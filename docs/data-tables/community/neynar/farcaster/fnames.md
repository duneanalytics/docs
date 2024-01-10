# Fnames

### **dune.neynar.dataset_farcaster_fnames**

This table contains usernames associated with FIDs on the Farcaster protocol.

| **Column name**       | **Type**                        | **Description**                                           |
| --------------------- | ------------------------------- | --------------------------------------------------------- |
| fname                 | varchar                          | Fname of the given user                                  |
| created\_at           | timestamp without timezone      | Timestamp of creation within database                     |
| updated\_at           | timestamp without timezone      | Timestamp of update within database                       |
| fid                   | bigint                          | User ID of user on Farcaster protocol                     |
| custody\_address      | varbinary                       | Address that stores the FC profile for the user           |
| expires\_at           | timestamp without timezone      | Timestamp when username expires for the user              |
