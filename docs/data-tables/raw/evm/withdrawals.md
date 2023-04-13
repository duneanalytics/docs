---
title: Withdrawals
description: The withdrawal table stores information about withdrawals made on the Ethereum beacon chain, including the block time, block number, index, validator index, amount, address, withdrawals root, and block hash.
---

!!!note
    Dune does not have beacon chain data yet. This table introduces the action of withdrawing from the beacon chain only.  


The [Ethereum Improvement Proposal (EIP) 4895](https://eips.ethereum.org/EIPS/eip-4895) introduces a system-level "operation" to support validator withdrawals that are "pushed" from the beacon chain to the EVM.

 Withdrawals are represented as a new type of object in the execution payload, called an "operation", that cleanly separates this "system-level" operation from regular transactions. Withdrawals provide key information from the consensus layer such as a monotonically increasing index, validator index, recipient address, and the amount of ether given in Gwei.

 Using this table you can observe beacon chain withdrawls.

### How to work with this table

In order to connect deposits and withdrawals, we must identify the ``validator_index`` of unique depositors. Since Dune doesn't have beacon chain data yet, we have to rely on a workaround using a query to obtain a list of valid and active deposits from the Ethereum deposit contract.

This [query](https://dune.com/queries/2364548) returns a list of valid and active deposits, which we can use to identify the ``validator_index`` of unique depositors. We can then use this list to filter out invalid and inactive deposits from the ``withdrawals`` table. 

The Query is manually maintained and therefore may not always be up to date, but most historical data is available.


We hope to integrate beacon chain data in the future, which will streamline the process of connecting deposits and withdrawals, and eliminate the need for manual exclusions of invalid and inactive deposits.


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