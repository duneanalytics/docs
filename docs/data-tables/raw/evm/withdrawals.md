---
title: Withdrawls
description: The withdrawal table stores information about withdrawals made on the Ethereum beacon chain, including the block time, block number, index, validator index, amount, address, withdrawals root, and block hash.
---

!!!note
    Dune does not have beacon chain data yet. This table introduces the action of withdrawing from the beacon chain only.  

The Ethereum Improvement Proposal (EIP) 4895 introduces a system-level "operation" to support validator withdrawals that are "pushed" from the beacon chain to the EVM.

 Withdrawals are represented as a new type of object in the execution payload, called an "operation", that cleanly separates this "system-level" operation from regular transactions. Withdrawals provide key information from the consensus layer such as a monotonically increasing index, validator index, recipient address, and the amount of ether given in Gwei. This table allows you to query the withdrawal data.


## Column Data

### Example

![type:video](https://dune.com/embeds/2363408/3873540)

### Description

| Column Name       | Datatype | Description                                                             |
|-------------------|----------|-------------------------------------------------------------------------|
| block_time        | timestamp | The time the block was created                                          |
| block_number      | bigint    | The number of the block in the blockchain                               |
| index             | bigint    | a monotonically increasing index, starting from 0, as a value that increments by 1 per withdrawal to uniquely identify each withdrawal|
| validator_index   | bigint    | the validator_index of the validator, as a uint64 value, on the consensus layer the withdrawal corresponds to|
| amount            | bigint    | a nonzero amount of ether given in Gwei (1e9 wei)                        |
| address           | varbinary | a recipient for the withdrawn ether. Note that depositor and recipient address are not neccesarily the same|
| withdrawals_root  | varbinary | the 32 byte root of the trie committing to the list of withdrawals provided in a given execution payload|
| block_hash        | varbinary | The hash of the block                                                    |