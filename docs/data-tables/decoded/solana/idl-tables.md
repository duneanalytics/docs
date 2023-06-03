---
title: IDL Decoded Tables
description: Table Schemas
---

!!! info "Submissions"
    You can submit any program for decoding that has a public IDL or github repo (anchor and native are both supported) like [this one](https://solscan.io/account/JUP4Fb2cqiRUcaTHdrPC8h2gNsA2ETXiPDD33WcGuJB#anchorProgramIDL). You can submit to [this form](https://forms.gle/tbHZ6ZeEke5qwVjcA).

Decoded tables inherit all of the columns from [`instruction_calls`](../../raw/solana/instruction-calls.md), so you can refer there for most of the types. We only add columns for each argument in the function call `data` and each account that was required to be in `account_arguments`. **These only decode from instructions, and not inner instructions.**

## Example IDL Decoded Walkthrough

Using an IDL, we decode the function data arguments and the required account arguments. Let's look at an example using Whirlpool - normally you can find the IDL [on Solscan](https://solscan.io/account/whirLbMiicVdio4qvUfM5KAg6Ct8VwpYzGff3uctyCc#anchorProgramIDL), but this time we had to dig [into the project repo](https://github.com/orca-so/whirlpools/blob/main/sdk/src/artifacts/whirlpool.json). IDLs are like ABIs on Ethereum, except they are created from the [Anchor lang](https://www.anchor-lang.com/) project instead of natively from every program.

[Here's a transaction](https://solscan.io/tx/TGDKvM2E8mWYcsG2JBnb9axFcyEcKqs7yZLyayCmrV8p8SSdA8r9SLEC7EHQ4mcXQXpczEyaCBXvnmEi9yoKVJ9) of a pool (a trading pair) being initialzed.

You can see that the instruction data is decoded in "Bumps", "TickSpacing", and "InitialSqrtPrice" on the explorer. We have the same thing in a SQL table! You can also see all the account names are labelled clearly as well with an `account_` prefix. Raw table inherited columns like `tx_id`, `block_time`, `tx_index` get a `call_` prefix.

The main thing to note is that we've exploded outer and inner instructions, where the index will match what you see on explorers. This example call is at the outer instruction level, so the inner instruction index is null. For Whirlpool swaps, often times it will happen in inner_instructions so then the top level outer instruction is inherited into the `call_outer_instruction_index` and the inner index is `call_inner_instruction_index` (same idea with the `call_outer_executing_account` and `call_inner_executing_acount`)

![type:video](https://dune.com/embeds/2352049/3851391)

Try it out for yourself in [this query](https://dune.com/embeds/2352049/3851391) below:

```
SELECT * FROM whirlpool_solana.whirlpool_call_initializePool
WHERE call_tx_id = 'TGDKvM2E8mWYcsG2JBnb9axFcyEcKqs7yZLyayCmrV8p8SSdA8r9SLEC7EHQ4mcXQXpczEyaCBXvnmEi9yoKVJ9'
```

The table name follows the pattern `<namespace>_solana.<programName>_call_<instructionName>`. We already have many of the top projects decoded, so go play around!
