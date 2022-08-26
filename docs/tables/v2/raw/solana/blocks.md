# Blocks

## Solana.blocks

This table contains the block data within Solana’s blockchain. It can be used to identify block activity and transaction changes over time.

Query examples can be found here: [Solana blocks over time](https://dune.xyz/queries/389979) and [Transactions per day](https://dune.xyz/queries/390045)

| Column Name               | Column Type | Description                                         |
| ------------------------- | ----------- | --------------------------------------------------- |
| hash                      | string      | string The hash of this block, base-58 encoded      |
| height                    | bigint      | The number of blocks beneath this block             |
| slot                      | bigint      | This block’s slot index in the ledger               |
| time                      | timestamp   | The (estimated) time this block was produced        |
| date                      | date        | Used to partition by                                |
| parent\_slot              | bigint      | The slot index of this block's parent               |
| previous\_block\_\_\_hash | string      | The hash of this block's parent, base-58 encoded    |
| total\_transactions       | bigint      | The total number of transactions in this block      |
| successful\_transactions  | bigint      | The number of successful transactions in this block |
| failed\_transactions      | bigint      | The number of failed transactions in this block     |

##
