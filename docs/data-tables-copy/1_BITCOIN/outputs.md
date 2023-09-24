# Outputs

## `bitcoin.outputs`

|Column name        |Type  |Description                                                                                                                              |
|-------------------|------|-----------------------------------------------------------------------------------------------------------------------------------------|
|block_time         |timestamp|The block time                                                                                                                           |
|block_date         |date  |The block date                                                                                                                           |
|block_height       |bigint|The block number                                                                                                                         |
|block_hash         |string|The block hash                                                                                                                           |
|tx_id              |string|The id (hash) of the transaction this is from                                                                                            |
|index              |int   |0-indexed number of an output within a transaction. Used by inputs to identify outputs.                                                  |
|value              |double|The number of Satoshis attached to this output                                                                                           |
|script_asm         |string|Symbolic representation of the bitcoin's script language op-codes                                                                        |
|script_hex         |string|Hexadecimal representation of the bitcoin's script language op-codes                                                                     |
|address            |string|The address that owns this output                                                                                                        |
|type               |string|The address type of the output                                                                                                           |
