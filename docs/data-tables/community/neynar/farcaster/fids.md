# fids

## **farcaster.fids**

This table contains all User IDs for Farcaster users

| **Column name**       | **Type**                        | **Description**                                          |
| --------------------- | ------------------------------- | -------------------------------------------------------- |
| fid                   | bigint                          | User ID of user on Farcaster protocol                    |
| created\_at           | timestamp without timezone      | Timestamp of row creation                                |
| updated\_at           | timestamp without timezone      | Timestamp of last update                                 |
| custody\_address      | bytea                           | Address that stores user profile on the protocol         |
