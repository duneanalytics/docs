---
description: >-
  The changelog contains the updates being made to the Solana tables while in
  beta.
---

# Changelog

### 2022-03-25

the `solana.account_activity` table has been updated to a new version. The new version of the table contains additional information around token activity. The following columns were added to the table:

* `pre_token_balances`
  * The token balance before the transaction was processed
* `post_token_balances`
  * The token balance after the transaction was processed
* `token_balance_changes`
  * The balance change that occurred as part of the transaction

### 2022-03-18

Released the `solana.account_activity` table that contains all of the information about an account’s usage in a transaction.

The table is optimized to run with ‘WHERE address = …’ queries

### 2022-03-01

The `solana.transactions` table has now been upgraded to a new version. The new version of the table uses cleaner array structs to make it easier to extract useful information.

The vote transactions have also been split into their own table `solana.vote_transactions`, so queries using `solana.transactions` will have better performance. Unfortunately, the table change also means that some existing queries will now break and need to be changed.

What this means for your existing queries using `solana.transactions`:

* You won't need to check if a transaction is a vote transaction, which has typically been done with `WHERE ARRAY_CONTAINS(account_keys, "Vote111111111111111111111111111111111111111") = false`
* The `error_index` and `error_message` columns have been removed, and have been merged into the `error` column (which is a struct). So now instead of `WHERE error_index is not null`, a query should do `WHERE error is not null`.
* Structs containing indexes to `account_keys` now include the account address directly, so there is no need to use the `account_keys` column to look up the account addresses:

```
before                                             	->  now
account_keys[instructions[i]['program_id_index']]  	->  instructions[i].executing_account
account_keys[pre_token_balances[i]['account_index']]   ->  pre_token_balances[i].account
account_keys[post_token_balances[i]['account_index']]  ->  post_token_balances[i].account
```

* The `pre_token_balances` and `post_token_balances` columns have changed. The token balance is now included in the field `amount`. And as mentioned above, the struct in the array now has a field `account`, which is the account of the token balance.
* The `instructions` column has changed. As mentioned above, the struct in the array now has a field `executing_account`, which is the account executing the instruction.
* The `inner_instructions` column is removed, and inner instructions have been moved into the `instructions` column.
