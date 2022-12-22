# Outputs

## `bitcoin.outputs`

|Column name        |Column type  |Description                                                                                                                                 |
|-------------------|-------------|--------------------------------------------------------------------------------------------------------------------------------------------|
|block_time         |timestamp    |The block time                                                                                                                              |
|block_date         |date         |The block date                                                                                                                              |
|block_height       |bigint       |The block number                                                                                                                            |
|block_hash         |string       |The block hash                                                                                                                              |
|tx_id            |string         |The id of the transaction this output was produced in                                                                                            |
|index              |int          |0-indexed number of an input within a transaction. Used by inputs to identify outputs.                                                      |
|value              |double       |The number of Satoshis attached to this output                                                                                              |
|type               |string       |The address type of the output                                                                                                              |
|script_asm         |string       |Symbolic representation of the bitcoin's script language op-codes                                                                           |
|script_hex         |string       |Hexadecimal representation of the bitcoin's script language op-codes                                                                        |
|required_signatures|bigint       |The number of signatures required to authorize spending of this output                                                                      |
|addresses          |array\<string\>|Addresses that own this output                                                                                                            |
