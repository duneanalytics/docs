# Blocks

## `bitcoin.blocks`

|Column name        |Column type  |Description                                                                                                                          |
|-------------------|---------|-----------------------------------------------------------------------------------------------------------------------------------------|
|time               |timestamp|The block time                                                                                                                           |
|height             |bigint   |The block number                                                                                                                         |
|date               |date     |The block date                                                                                                                           |
|hash               |string   |The block hash                                                                                                                           |
|transaction_count  |int      |The number of transactions in the block                                                                                                  |
|size               |bigint   |The size of the block                                                                                                                    |
|mint_reward        |double   |The output paid out to the miner for minting the block                                                                                   |
|total_fees         |double   |The fees paid out to the miner from transaction users. Each transaction's fee is what's left of output after input is subtracted from it.|
|total_reward       |double   |The static reward given to the miner. It is the sum of the outputs in the coinbase transaction (the first transaction).                  |
|stripped_size      |bigint   |The size of the block excluding witness data                                                                                             |
|weight             |bigint   |The block weight as defined in BIP 141                                                                                                   |
|chainwork          |string   |The expected number of hashes required to produce the current chain                                                                      |
|difficulty         |string   |The estimated amount of work done to find this block relative to the estimated amount of work done to find block 0                       |
|merkle_root        |string   |The root node of a Merkle tree, where leaves are transaction hashes                                                                      |
|nonce              |string   |The number of transactions made by the sender prior to this one                                                                          |
|coinbase           |string   |The data specified in the coinbase transaction of the block                                                                              |
|previous_block_hash|string   |The hash of the previous block                                                                                                           |
|bits               |string   |The difficulty threshold specified in block header                                                                                       |
