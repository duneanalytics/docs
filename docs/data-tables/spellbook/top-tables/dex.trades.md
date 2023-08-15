---
title: dex.trades
description: dex.trades aggregates data across multiple DEX platforms into one simple table.
---

Decentralized exchanges are the beating heart of the DeFi industry. You can swap any native (ETH) or ERC-20 token for any ERC-20 token through the magic of smart contracts.

The problem here: there are so many decentralized exchanges out there that it's hardly possible for any single person to work with the smart contract data for all of them.

That's why we created [dex.trades](https://dune.com/spellbook#!/model/model.spellbook.dex_trades).

This table standardizes and normalizes the trading data across virtually all relevant decentralized exchanges. This in turn allows you to easily query for trading data for your favorite tokens without having to deal with all of the different DEX smart contracts yourself.

The scripts that generate the table dex.trades can be found in this [public github](https://github.com/duneanalytics/spellbook/tree/main/models/dex) repo.

## Column Data

| Column Name             | Data Type         | Description                                                                              |
|-------------------------|-------------------|-----------------------------------------------------------------------                   |
| `amount_usd`            | _double_          | The USD value of this trade                                                              |
| `block_date`            | _timestamp_       | The truncated timestamp of the block including this transaction                          |
| `block_time`            | _timestamp_       | The timestamp of the block including this transaction                                    |
| `blockchain`            | _varchar_         | The blockchain where this transaction was broadcasted                                    |
| `evt_index`             | _int_             | This log's index position in the block (cumulative amount of logs ordered by execution)  |
| `maker`                 | _varbinary_       | In some special cases, the counterparty to transactions (if applicable)                  |
| `project`               | _varchar_         | The decentralized exchange (DEX) on which this trade was executed                        |
| `project_contract_address` | _varbinary_     | The contract address of the project or DEX                                              |
| `taker`                 | _varbinary_       | The contract that called the DEX contract                                                |
| `token_bought_address`  | _varbinary_       | The address of the token bought during this trade                                        |
| `token_bought_amount`   | _double_          | The amount of the token bought during this trade                                         |
| `token_bought_amount_raw` | _decimal(38,0)_  | The raw amount of the token bought during this trade                                    |
| `token_bought_symbol`   | _varchar_         | The symbol of the token bought                                                           |
| `token_pair`            | _varchar_         | The trading pair of tokens involved in this trade                                        |
| `token_sold_address`    | _varbinary_       | The address of the token sold during this trade                                          |
| `token_sold_amount`     | _double_          | The amount of the token sold during this trade                                           |
| `token_sold_amount_raw` | _decimal(38,0)_  | The raw amount of the token sold during this trade                                        |
| `token_sold_symbol`     | _varchar_         | The symbol of the token sold                                                             |
| `trace_address`         | _varchar_         | The position in the execution graph tree for this trade                                  |
| `tx_from`               | _varbinary_       | The address that initiated this transaction                                              |
| `tx_hash`               | _varbinary_       | The hash of the transaction containing this trade                                        |
| `tx_to`                 | _varbinary_       | The address of the first smart contract called during this transaction                   |
| `version`               | _varchar_         | The version of the DEX used for this trade                                               |

#### Get all transactions of USDC swaps in the past 24 hours

```sql
select * from dex.trades
where (token_bought_address = 0xa0b86991c6218b36c1d19d4a2e9eb0ce3606eb48 
OR     token_sold_address   = 0xa0b86991c6218b36c1d19d4a2e9eb0ce3606eb48)
AND blockchain = 'ethereum'
AND block_time >= NOW() - interval '24' hour
```

#### Get top 100 uniswap pairs' volume from uniswap in the past 3 days

```sql
select token_pair,
       SUM(amount_usd) as total_volume
from dex.trades
WHERE blockchain = 'ethereum'
AND project = 'uniswap'
AND block_time >= NOW() - interval '3' day
AND token_pair IS NOT NULL
GROUP BY 1
ORDER BY 2 DESC -- order by total_volume
limit 100 -- 100 rows
```


