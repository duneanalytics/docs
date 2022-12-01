# Blocks

## Solana.blocks

This table contains the block data within Solana’s blockchain. It can be used to identify block activity and transaction changes over time.

![type:video](https://dune.com/embeds/1582515/2634478/fae7d1bb-b0c0-46b6-abc3-3da1c918233e)

| Column Name               | Data Type     | Description                                         |
| :-----------------------: | :-----------: | --------------------------------------------------- |
| `hash`                    | _string_      | string The hash of this block, base-58 encoded      |
| `height`                  | _bigint_      | The number of blocks beneath this block             |
| `slot`                    | _bigint_      | This block’s slot index in the ledger               |
| `time`                    | _timestamp_   | The (estimated) time this block was produced        |
| `date`                    | _date_        | Used to partition by                                |
| `parent_slot`             | _bigint_      | The slot index of this block's parent               |
| `previous_block___hash`   | _string_      | The hash of this block's parent, base-58 encoded    |
| `total_transactions`      | _bigint_      | The total number of transactions in this block      |
| `successful_transactions` | _bigint_      | The number of successful transactions in this block |
| `failed_transactions`     | _bigint_      | The number of failed transactions in this block     |

Solana Query examples can be found here: [Solana blocks over time](https://dune.xyz/queries/389979) and [Transactions per day](https://dune.xyz/queries/390045)