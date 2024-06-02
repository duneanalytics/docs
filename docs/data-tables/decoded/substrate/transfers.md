# Transfers

## **{chain}.transfers**

This table contains historical transfers

| **Column name**       | **Type**                        | **Description**                                          |
| --------------------- | ------------------------------- | -------------------------------------------------------- |
| block_time        | timestamp       |           |
| block_number      | long            |           |
| event_id          | string          |           |
| extrinsic_id      | string          |           |
| section           | string          |           |
| method            | string          |           |
| extrinsic_hash    | binary          |           |
| block_hash        | binary          |           |
| from_ss58         | string          |           |
| from_pub_key      | binary          |           |
| to_ss58           | string          |           |
| to_pub_key        | binary          |           |
| asset             | string          |           |
| price_usd         | double          |           |
| amount_usd        | double          |           |
| symbol            | string          |           |
| decimals          | long            |           |
| amount            | double          |           |
| raw_amount        | decimal(38,9)   |           |
