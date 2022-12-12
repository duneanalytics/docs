---
description: >-
  更改日志包含在测试版中对 Solana 表进行的更新。
---

# 更改日志

### 2022-03-25

`solana.account_activity`表已更新为新版本。该表的新版本包含有关代币活动的附加信息。新增了以下列到表中：

* `pre_token_balances`
  * 交易处理前的代币余额
* `post_token_balances`
  * 交易处理后的代币余额
* `token_balance_changes`
  * 作为交易的一部分发生的余额变化

### 2022-03-18

发布了`solana.account_activity`表，其中包含有关交易中帐户使用情况的所有信息。

该表经过优化以更好地运行“WHERE address = ...”查询。

### 2022-03-01

`solana.transactions`表现已升级到新版本。新版本的表使用更简洁的数组结构，以便更容易地提取有用信息。

投票交易也被拆分到自己的表`solana.vote_transactions`中，因此使用`solana.transactions`的查询将具有更好的性能。不幸的是，此表的修改也意味着一些现有查询现在将会中断并需要更新。


这对使用`solana.transactions`的现有查询有什么影响：

* 您无需再检查交易是否为投票交易，这通常使用`WHERE ARRAY_CONTAINS(account_keys, "Vote111111111111111111111111111111111111111") = false`来完成。
* `error_index`和`error_message`列已被删除，并已合并到`error`列（这是一个结构）。所以现在查询应该用`WHERE error is not null`而不是用`WHERE error_index is not null`。
* 包含`account_keys`索引的结构现在直接包含帐户地址，因此无需再使用`account_keys`列来查找帐户地址：

```
之前                                             	->  现在
account_keys[instructions[i]['program_id_index']]  	->  instructions[i].executing_account
account_keys[pre_token_balances[i]['account_index']]   ->  pre_token_balances[i].account
account_keys[post_token_balances[i]['account_index']]  ->  post_token_balances[i].account
```

* `pre_token_balances`和`post_token_balances`列已更改。代币余额现在包含在`amount`字段中。并且如上所述，数组中的结构现在有一个字段`account`，它是代币余额归属的帐户。
* `instructions`列已更改。如上所述，数组中的结构现在有一个字段`executing_account`，它是执行指令的帐户。
* `inner_instructions`列被删除，内部指令已移至`instructions`列中。
