# Rewards

## Solana.rewards

This table contains data about rewards paid out on Solana. One block may contain zero or more rewards, and each row corresponds to one reward.

An example query can be found here: [Solana rewards fee per day](https://dune.xyz/queries/391421/747012)

| Column Name   | Column Type | Description                                                                                       |
| ------------- | ----------- | ------------------------------------------------------------------------------------------------- |
| block\_slot   | bigint      | This block’s slot index in the ledger                                                             |
| block\_hash   | string      | The hash of this block, base-58 encoded                                                           |
| block\_time   | timestamp   | The (estimated) time this block was produced                                                      |
| block\_date   | date        | Event date                                                                                        |
| commission    | string      | Vote account commission when the reward was credited, only present for voting and staking rewards |
| lamports      | bigint      | Number of reward lamports credited or debited by the account                                      |
| pre\_balance  | bigint      | Account balance in lamports before the reward was applied                                         |
| post\_balance | bigint      | Account balance in lamports after the reward was applied                                          |
| recipient     | string      | The public key, as base-58 encoded string, of the account that received the reward                |
| reward\_type  | string      | Type of reward: "fee", "rent", "voting", "staking"                                                |
