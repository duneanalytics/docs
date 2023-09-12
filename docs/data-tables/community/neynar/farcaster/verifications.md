# Verifications

### **dune.neynar.dataset_verifications**

This table contains data about the Ethereum wallet addresses connected to Farcaster profiles.

| **Column name**       | **Type**                           | **Description**                                                          |
|-----------------------|------------------------------------|--------------------------------------------------------------------------|
| id                    | bigint                             | Row id                                                                   |
| created\_at            | timestamp without timezone         | Timestamp of creation within database                                     |
| updated\_at            | timestamp without timezone         | Timestamp of update within database                                       |
| deleted\_at            | timestamp without timezone         | Timestamp of deletion on Farcaster protocol                               |
| timestamp              | timestamp without timezone         | Timestamp of creation on Farcaster protocol                               |
| fid                    | bigint                             | User ID of user on Farcaster protocol                                     |
| hash                   | bytea                              | Hash of connecting address to profile on protocol                         |
| claim                  | jsonb                              | Connected wallet addresses and proof of connection                        |

