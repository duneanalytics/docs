# Transactions

## `bitcoin.transactions`

|Column name        |Type  |Description                                                                                                                              |
|-------------------|------|-----------------------------------------------------------------------------------------------------------------------------------------|
|block_time         |timestamp|The block time                                                                                                                           |
|block_date         |date  |The block date                                                                                                                           |
|block_height       |bigint|The block number                                                                                                                         |
|block_hash         |string|The hash of the block that contains this transaction                                                                                     |
|index              |int   |The number of the transaction in the block.                                                                                              |
|id                 |string|The id (hash) of this transaction                                                                                                        |
|input_value        |double|Total value of inputs in the transaction                                                                                                 |
|output_value       |double|Total value of outputs in the transaction                                                                                                |
|fee                |double|The transaction fee paid to the miner. = output_value - input_value                                                                      |
|input_count        |int   |The number of inputs in the transaction                                                                                                  |
|output_count       |int   |The number of outputs in the transaction                                                                                                 |
|size               |bigint|The size of this transaction in bytes                                                                                                    |
|virtual_size       |bigint|The virtual transaction size (differs from size for witness transactions)                                                                |
|is_coinbase        |boolean|The transaction is a coinbase transaction, which is the first transaction in a block                                                     |
|coinbase           |string|If the transaction is a coinbase transaction, contains the coinbase data. Otherwise, null.                                               |
|input              |struct|Transaction inputs                                                                                                                       |
|output             |struct|Transaction outputs. See outputs table.                                                                                                  |
|lock_time          |bigint|Earliest time that miners can include the transaction in their hashing of the Merkle root to attach it in the latest block of the blockchain|
|hex                |string|The transaction encoded as hexadecimal                                                                                                   |

### Struct definitions

Within several of these columns is a data type of STRUCT which allows for representing nested hierarchical data and has key-value pairs. It's similar to a dictionary in python and can be used to group fields together to make them more accessible.

**input**

| Field   | Data type | Description  |
|-------------------|------|-----------------------------------------------------------------------------------------------------------------------------------------|
|value        |double|The number of Satoshis attached to this output                                                                                           |
|height       |bigint|The height of the output                                                                                                                 |
|tx_id        |string|The transaction id of the output that is here used as input                                                                              |
|output_number|bigint|The number (index) of the output in transaction `tx_id`'s outputs                                                                        |
|coinbase     |string|The data specified in this transaction, if it was a coinbase transaction                                                                 |
|sequence     |bigint|Sequence number                                                                                                                          |
|witness_data |array<string>|Array of hex encoded witness data                                                                                                        |
|script_signature|struct|The script signature                                                                                                                     |
|script_pub_key|struct|The script public key                                                                                                                    |

***

**input.script_signature**
| Field   | Data type | Description  |
|---------|-----------|--------------|
|hex|string|The transaction's script operations, in hex                                                                                              |
|asm|string|The transaction's script operations, in symbolic representation                                                                          |

***

**input.script_pub_key**

| Field   | Data type | Description  |
|---------|-----------|--------------|
|asm|string|The transaction's script operations, in symbolic representation                                                                          |
|desc|string|The transaction's script operations, in symbolic representation                                                                          |
|address|string|The transaction's script operations, in symbolic representation                                                                          |
|hex|string|The transaction's script operations, in hex                                                                                              |
|type|string|The address type of the output                                                                                                           |

***

**output**

| Field   | Data type | Description  |
|-------------------|------|-----------------------------------------------------------------------------------------------------------------------------------------|
|index       |bigint|0-indexed number of an output within a transaction used by a later transaction to refer to that specific output                          |
|value       |double|The number of Satoshis attached to this output                                                                                           |
|script_pub_key|struct|The public key                                                                                                                           |

***

**output.script_pub_key**
| Field   | Data type | Description  |
| ------- | --------- | -------------|
|asm|string|The transaction's script operations, in symbolic representation                                                                          |
|hex|string|The transaction's script operations, in hex                                                                                              |
|address|string|The address the BTC came from                                                                                                            |
|type|string|The address type of the output                                                                                                           |
