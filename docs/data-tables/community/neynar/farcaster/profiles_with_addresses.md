# Profiles with addresses

## **dune.neynar.dataset_farcaster_profiles_with_addresses**

This table contains farcaster user's profile data and their connected addresses

| Column name | type | description |
| --- | --- | --- |
| fid | bigint | User ID of farcaster user |
| fname | text | Username |
| display_name | text | Display name of user |
| avatar_url | text | Link to profile picture |
| bio | text | User profile bio |
| verified_addresses | jsonb | EVM wallet addresses connected to Farcaster profile  |