# Blocks

## `bitcoin.blocks`

|Column name        |Column type  |Description                                                                                                                                 |
|-------------------|-------------|--------------------------------------------------------------------------------------------------------------------------------------------|
|time               |timestamp    |The block time                                                                                                                              |
|height             |bigint       |The block number                                                                                                                            |
|date               |date         |The block date                                                                                                                              |
|hash               |string       |The block hash                                                                                                                              |
|transaction_count  |             |The number of transactions in the block                                                                                                     |
|size               |bigint       |The size of the block                                                                                                                       |
|stripped_size      |bigint       |The size of the block excluding witness data                                                                                                |
|weight             |bigint       |The block weight as defined in BIP 141                                                                                                      |
|chainwork          |             |The expected number of hashes required to produce the current chain                                                                         |
|difficulty         |             |The estimated amount of work done to find this block relative to the estimated amount of work done to find block 0                          |
|merkle_root        |string       |The root node of a Merkle tree, where leaves are transaction hashes                                                                         |
|nonce              |             |The number of transactions made by the sender prior to this one                                                                             |
|coinbase           |             |The data specified in the coinbase transaction of the block                                                                                 |
|previous_block_hash|string       |The hash of the previous block                                                                                                              |
|bits               |             |The difficulty threshold specified in block header                                                                                          |
