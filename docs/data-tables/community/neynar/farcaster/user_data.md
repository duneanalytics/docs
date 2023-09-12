# User Data

## **User information for Farcaster users**

### **farcaster.user_data**

This table contains data about the user information on the Farcaster protocol. It can be joined with `fname` or `fid` for additional details.

| **Column name**       | **Type**                           | **Description**                                                                                                      |
|-----------------------|------------------------------------|--------------------------------------------------------                                                              |
| id                    | bigint                             | Row id                                                                                                               |
| created\_at            | timestamp without timezone         | Timestamp of creation within database                                                                               |
| updated\_at            | timestamp without timezone         | Timestamp of update within database                                                                                 |
| deleted\_at            | timestamp without timezone         | Timestamp of deletion on Farcaster protocol                                                                         |
| timestamp              | timestamp without timezone         | Timestamp of creation on Farcaster protocol                                                                         |
| fid                    | bigint                             | User ID of user on Farcaster protocol                                                                               |
| hash                   | bytea                              | Hash of user data                                                                                                   |
| type                   | smallint                           | Type of user data: (1 = Avatar URL, 2 = Display name, 3 = Profile bio, 5 = URL of the user, 6 = Preferred fname)    |
