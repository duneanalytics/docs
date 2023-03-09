---
title: Spellbook Contribution Guidelines
description: To adhere to those best practices, dbt's requirements, and facilitate contribution and collaboration across our community, we have a few requirements we'll ask you to follow when contributing to Spellbook.
---

Spellbook is a powerful tool for creating well-organized and accurate data abstractions at scale.

Built using [dbt-core](https://docs.getdbt.com/docs/introduction) (data build tool), Spellbook mixes SQL with JINJA templating to enable us to build as a team and community using data engineering best practices.

To adhere to those best practices, dbt's requirements, and facilitate contribution and collaboration across our community, we have a few requirements we'll ask you to follow.

We've created these docs to help you understand those conventions and structures as well as some of the why behind them in order to help you successfully build Spells and get your PRs approved faster!

Read on to learn about the different types of Spellbook contributions and General Guidelines.

If you're looking for guidelines on a specific type of Spellbook contribution, see these pages:

<div class="cards grid" markdown>

- [Contributing Static Views](contributing-static-views.md)

- [Contributing Spells](contributing-spells.md)

</div>

And as always, if you have questions reach out in the [#spellbook Discord Channel](https://discord.com/channels/757637422384283659/999683200563564655) - someone from the community or team is always happy to help!


## General Spellbook contribution guidelines

In order to best facilitate community contributions while adhering to dbt's requirements and keeping Spellbook manageable for our team, we have a few guidelines that we'll ask you to follow.

### Directory format and naming conventions

Spellbook is a repository where many people contribute and collaborate, so to keep it easily understandable for everyone, we have some rather strict naming and directory organization conventions.

Spells are organized under `models` (all Spells are just dbt models) using the following structure:

- Sectors (DEX, NFT, etc.) have their own Spells under `/models/[sector]`
- Project Spells `/models/[project]/[blockchain]`
- Most Spells are built bottom-up, starting from a single project version in a single chain and merging all the way up to a sector, with there being four total levels of the hierarchy
  - Project version on one blockchain
  - Project on one blockchain
  - Project on all blockchains
  - Sector on all blockchains

We have a few special cases for storing static datasets, they are:

- Token metadata views live under `/models/tokens/[blockchain]>`
  - Files follow the convention `tokens_[blockchain]_[subset].sql` and contain metadata for tokens of a subset of tokens (e.g. erc20, NFTs, Rebasing tokens)
- Price feeds metadata live on `/models/prices/prices_tokens.sql`