# Signers

### **dune.neynar.dataset_signers**

This table contains data about signers associated with users on the Farcaster protocol.

| **Column name**       | **Type**                        | **Description**                                           |
| --------------------- | ------------------------------- | --------------------------------------------------------- |
| id                    | bigint                          | Row id                                                    |
| created\_at           | timestamp without timezone      | Timestamp of creation within database                     |
| updated\_at           | timestamp without timezone      | Timestamp of update within database                       |
| deleted\_at           | timestamp without timezone      | Timestamp of deletion on Farcaster protocol               |
| timestamp             | timestamp without timezone      | Timestamp of creation on Farcaster protocol               |
| fid                   | bigint                          | User ID of user on Farcaster protocol                     |
| hash                  | bytea                           | Hash of creating signer on the protocol                   |
| signer                | bytea                           | Signer created by user                                    |
