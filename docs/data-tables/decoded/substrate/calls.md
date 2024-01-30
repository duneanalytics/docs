# Calls

## **{chain}.calls**

This table contains historical calls information:



| **Column name**       | **Type**                        | **Description**                                          |
| --------------------- | ------------------------------- | -------------------------------------------------------- |
| block_number      | bigint              |                       |
| block_time        | timestamp           |                       |
| extrinsic_id      | string              |                       |
| relay_chain       | string              |                       |
| para_id           | bigint              |                       |
| id                | string              |                       |
| block_hash        | binary              |                       |
| extrinsic_hash    | binary              |                       |
| extrinsic_section | string              |                       |
| extrinsic_method  | string              |                       |
| call_id           | string              |                       |
| call_index        | binary              |                       |
| call_args         | string              |                       |
| call_args_def     | string              |                       |
| root              | boolean             |                       |
| leaf              | boolean             |                       |
| fee               | double              |                       |
| fee_usd           | double              |                       |
| weight            | bigint              |                       |
| signed            | boolean             |                       |
| signer_ss58       | string              |                       |
| signer_pub_key    | binary              |                       |
| lifetime          | string              |                       |


Calls are only included if the extrinsic is _successful_.
