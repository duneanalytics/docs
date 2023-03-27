[View code on GitHub](https://dune.com/blob/master/data tables\raw\solana\rewards.md)

# Rewards

This section of the app technical guide covers the `Solana.rewards` table, which contains data about rewards paid out on Solana. Each row in the table corresponds to one reward, and one block may contain zero or more rewards. The table has several columns, including `block_slot`, which indicates the block's slot index in the ledger, `block_hash`, which is the hash of the block, `block_time`, which is the estimated time the block was produced, and `block_date`, which is the date of the event. Other columns include `commission`, which indicates the vote account commission when the reward was credited (only present for voting and staking rewards), `lamports`, which is the number of reward lamports credited or debited by the account, `pre_balance`, which is the account balance in lamports before the reward was applied, `post_balance`, which is the account balance in lamports after the reward was applied, `recipient`, which is the public key of the account that received the reward, and `reward_type`, which indicates the type of reward (e.g., "fee", "rent", "voting", "staking").

An example query for this table is provided in the guide, which can be found at [Solana rewards fee per day](https://dune.xyz/queries/391421/747012). This query likely retrieves data from the `Solana.rewards` table to calculate the daily rewards paid out on Solana.

Overall, this section of the app technical guide provides information on the `Solana.rewards` table and its columns, which is useful for developers working on the rewards feature of the app.
## Questions: 
 1. What is the purpose of the Solana.rewards table?
    
    The Solana.rewards table contains data about rewards paid out on Solana, with each row corresponding to one reward.

2. What information does the commission column provide and when is it present?
    
    The commission column provides the vote account commission when the reward was credited, and it is only present for voting and staking rewards.

3. What are the different types of rewards listed in the reward_type column?
    
    The different types of rewards listed in the reward_type column are "fee", "rent", "voting", and "staking".