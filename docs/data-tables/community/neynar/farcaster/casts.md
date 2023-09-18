# Casts

## **dune.neynar.dataset_farcaster_casts**

This table contains all casts on the Farcaster protocol

| **Column name**          | **Type**                        | **Description**                                                  |
| ------------------------ | ------------------------------- | --------------------------------------------------------------   |
| id                       | bigint                          | Row id                                                           |
| created\_at              | timestamp without timezone      | Timestamp of creation within database                            |
| updated\_at              | timestamp without timezone      | Timestamp of update within database                              |
| deleted\_at              | timestamp without timezone      | Timestamp of deletion on Farcaster protocol                      |
| timestamp                | timestamp without timezone      | Timestamp of creation on Farcaster protocol                      |
| fid                      | bigint                          | User ID of user on Farcaster protocol                            |
| hash                     | bytea                           | Hash of the cast                                                 |
| parent\_hash             | bytea                           | Hash of the cast that this cast is a reply to                    |
| parent\_fid              | bigint                          | FID of author or parent_hash                                     |
| text                     | text                            | Text of the cast                                                 |
| embeds                   | jsonb                           | Attachments inside the cast e.g. images, links, etc.             |
| mentions                 | bigint[]                        | Array of FIDs for the users that were mentioned in the cast text |
| mentions\_positions      | smallint[]                      | Positions in the cast text where the users were mentioned        |
