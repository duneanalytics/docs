# Extrinsics

## **{chain}.extrinsics**

This table contains historical extrinsics information:

| **Column name**       | **Type**                        | **Description**                                          |
| --------------------- | ------------------------------- | -------------------------------------------------------- |
| block_time       | timestamp |  |
| block_number     | long      |  |
| extrinsic_id     | string    |  |
| hash             | binary    |  |
| block_hash       | binary    |  |
| lifetime         | string    |  |
| params           | string    |  |
| fee              | double    |  |
| weight           | long      |  |
| signed           | boolean   |  |
| signer_ss58      | string    |  |
| signer_pub_key   | binary    |  |
| fee_usd          | double    |  |


Extrinsics are included if the extrinsic  _successful_ or _failed_.
