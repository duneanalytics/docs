# Balances

## **{chain}.balances**

This table contains historical balances information:

| **Column name**       | **Type**                        | **Description**                                          |
| --------------------- | ------------------------------- | -------------------------------------------------------- |
| ts           | timestamp without timezone      | Timestamp of balance                              |
| symbol       | string                          | Token Symbol                   |
| address_ss58     | string          | SS58 Address of Asset holder                                 |
| address_pubkey   | binary          | Pubkey of holder        |
| id               | string          | Chain ID (e.g. "polkadot")              |
| chain_name       | string          | Chain Name (e.g. "KILT Spirit")     |
| asset            | string          |                  |
| para_id          | long            |                  |
| free             | double          |                  |
| free_usd         | double          |                  |
| reserved         | double          |                  |
| reserved_usd     | double          |                  |
| misc_frozen      | double          |                  |
| misc_frozen_usd  | double          |                  |
| frozen           | double          |                  |
| frozen_usd       | double          |                  |
| price_usd        | double          |                  |
| nonce            | long            |                  |
| free_raw         | string          |                  |
| reserved_raw     | string          |                  |
| misc_frozen_raw  | string          |                  |
| frozen_raw       | string          |                  |
| flags_raw        | string          |                  |

Balances are taken at the end of each day.  
