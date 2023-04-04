[View code on GitHub](https://dune.com/docs/data-tables/raw/solana/rewards.md)

# Rewards

This section of the app technical guide covers the `Solana.rewards` table, which contains data about rewards paid out on Solana. The table is structured such that each row corresponds to one reward, and one block may contain zero or more rewards. The purpose of this table is to provide information about rewards paid out on the Solana blockchain, which can be useful for analyzing trends and patterns in reward distribution.

The table contains several columns, each with a specific purpose. The `block_slot` column contains the block's slot index in the ledger, while the `block_hash` column contains the hash of the block, base-58 encoded. The `block_time` column contains the estimated time the block was produced, and the `block_date` column contains the date of the event. The `commission` column contains the vote account commission when the reward was credited, only present for voting and staking rewards. The `lamports` column contains the number of reward lamports credited or debited by the account, while the `pre_balance` column contains the account balance in lamports before the reward was applied. The `post_balance` column contains the account balance in lamports after the reward was applied, and the `recipient` column contains the public key, as a base-58 encoded string, of the account that received the reward. Finally, the `reward_type` column contains the type of reward, which can be "fee", "rent", "voting", or "staking".

An example query for this table is provided in the guide, which shows how to retrieve the Solana rewards fee per day. This query can be useful for analyzing the distribution of rewards over time and identifying any trends or patterns in reward distribution.

Overall, this section of the app technical guide provides a detailed overview of the `Solana.rewards` table, including its purpose, structure, and columns. It also provides an example query to demonstrate how the table can be used to analyze reward distribution on the Solana blockchain.
## Questions: 
 1. What is the purpose of the Solana.rewards table?
    
    The Solana.rewards table contains data about rewards paid out on Solana, with each row corresponding to one reward. It includes information such as the block slot, block hash, block time, commission, lamports, pre and post balance, recipient, and reward type.

2. What types of rewards are included in the reward_type column?
    
    The reward_type column includes four types of rewards: "fee", "rent", "voting", and "staking". The commission column is also present for voting and staking rewards.

3. Are there any limitations or restrictions on the data included in the Solana.rewards table?
    
    The app technical guide does not provide information on any limitations or restrictions on the data included in the Solana.rewards table. It is possible that a blockchain SQL analyst may have additional questions or concerns about the accuracy or completeness of the data.