# Blocks

## **{chain}.blocks**

This table contains historical blocks information:

| **Column name**       | **Type**                        | **Description**                                          |
| --------------------- | ------------------------------- | -------------------------------------------------------- |
| block_time           | timestamp          |                      |
| number               | long               |                      |
| spec_version         | long               |                      |
| relay_block_number   | long               |                      |
| hash                 | binary             |                      |
| parent_hash          | binary             |                      |
| state_root           | binary             |                      |
| extrinsics_root      | binary             |                      |
| author_ss58          | string             |                      |
| author_pub_key       | binary             |                      |
| relay_state_root     | binary             |                      |
| extrinsic_count      | long               |                      |
| event_count          | long               |                      |
| transfer_count       | long               |                      |
| trace_count          | long               |                      |
