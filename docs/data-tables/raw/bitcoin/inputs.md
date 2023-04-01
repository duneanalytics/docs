# Inputs

## `bitcoin.inputs`

|Column name        |Type  |Description                                                                                                                              |
|-------------------|------|-----------------------------------------------------------------------------------------------------------------------------------------|
|block_time         |timestamp|The block time                                                                                                                           |
|block_date         |date  |The block date                                                                                                                           |
|block_height       |bigint|The block number                                                                                                                         |
|index              |int   |The index of the input                                                                                                                   |
|block_hash         |bigint|The block hash of the output                                                                                                             |
|tx_id              |string|The transaction id that this input was used                                                                                              |
|spent_block_height |bigint|The block height of the output                                                                                                           |
|spent_tx_id        |string|The transaction id of the output                                                                                                         |
|spent_output_number|bigint|The output number                                                                                                                        |
|value              |double|The number of Satoshis attached to this input                                                                                            |
|address            |string|The address that owned/owns the output used as input                                                                                     |
|type               |string|The address type of the input                                                                                                            |
|coinbase           |string|This input was the coinbase input in the transaction                                                                                     |
|is_coinbase        |boolean|True if coinbase is not null, else false                                                                                                 |
|script_asm         |string|Symbolic representation of the bitcoin's script language op-codes                                                                        |
|script_hex         |string|Hexadecimal representation of the bitcoin's script language op-codes                                                                     |
|script_desc        |string|The description                                                                                                                          |
|script_signature_asm|string|Symbolic representation of the bitcoin's script language op-codes                                                                        |
|script_signature_hex|string|Hexadecimal representation of the bitcoin's script language op-codes                                                                     |
|sequence           |bigint|A number intended to allow unconfirmed time-locked transactions to be updated before being finalized; not currently used except to disable locktime in a transaction|
|witness_data       |array&lt;string&gt;|Witness data                                                                                                                             |
