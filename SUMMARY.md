# Table of contents

* [Introduction to Dune](README.md)

## About Dune <a href="#about" id="about"></a>

* [Use Cases](about/usecases/README.md)
  * [Project Dashboards](about/usecases/project-dashboards.md)
  * [Sector Dashboards](about/usecases/sector-dashboards.md)
  * [Ecosystem Dashboards](about/usecases/ecosystem-dashboards.md)
* [Tutorials](about/tutorials/README.md)
  * [Our Network course](about/tutorials/our-network-course.md)
  * [Dune Guides](about/tutorials/dune-guides/README.md)
    * [Tips for querying](about/tutorials/dune-guides/tips.md)
  * [SQL guides](about/tutorials/sql-guides.md)
  * [Video Series](about/tutorials/video-series.md)
  * [Query templates](about/tutorials/queries/README.md)
    * [ETH Balance of a wallet](about/tutorials/queries/eth-balance-of-a-wallet.md)
    * [raw transactions per wallet](about/tutorials/queries/tx-wallet.md)
    * [gas metrics per wallet](about/tutorials/queries/gas-metrics-per-wallet.md)
    * [price queries](about/tutorials/queries/price-queries.md)
    * [total supply over time of a token](about/tutorials/queries/supply.md)
    * [Users and amount over a trailing period](about/tutorials/queries/untitled-6.md)
    * [USD value of token utilised for an event](about/tutorials/queries/untitled-3.md)
    * [USD price for a token from Uniswap](about/tutorials/queries/untitled-2.md)
    * [Token (and USD value) per token over time for an address](about/tutorials/queries/untitled-1.md)

## Data Tables

* [Data tables](data-tables/data-tables/README.md)
  * [nft.trades](data-tables/data-tables/nft.trading.md)
  * [Raw Data](data-tables/data-tables/raw-data/README.md)
    * [Ethereum data](data-tables/data-tables/raw-data/ethereum-data.md)
    * [xDai Data](data-tables/data-tables/raw-data/xdai-data.md)
  * [Decoded Data](data-tables/data-tables/decoded-data.md)
  * [Token standards](data-tables/data-tables/special-tables.md)
  * [ERC-20 balances](data-tables/data-tables/erc-20-balances.md)
  * [Abstractions](data-tables/data-tables/abstractions.md)
  * [User Generated](data-tables/data-tables/user-generated.md)
  * [Prices](data-tables/data-tables/prices.md)
  * [Labels](data-tables/data-tables/labels.md)
  * [Solana Data](data-tables/data-tables/solana-data/README.md)
    * [Changelog](data-tables/data-tables/solana-data/changelog.md)
  * [Third Party Data](data-tables/data-tables/community-data/README.md)
    * [Flashbots](data-tables/data-tables/community-data/flashbots.md)

## Dune Engine V2 (beta)

* [Dune V2 Intro](dune-engine-v2-beta/dunes-new-query-engine.md)
* [Query Engine](dune-engine-v2-beta/query-engine.md)
* [Abstractions/Spells in Dune V2](dune-engine-v2-beta/abstractions-in-dunev2/README.md)
  * [🪄 Introducing Spellbook](dune-engine-v2-beta/abstractions-in-dunev2/introducing-spellbook.md)
  * [🔧 How to Contribute a Spell](dune-engine-v2-beta/abstractions-in-dunev2/how-to-contribute-a-spell/README.md)
    * [🤔 Decide on what problem you’re trying to solve with a spell.](dune-engine-v2-beta/abstractions-in-dunev2/how-to-contribute-a-spell/decide-on-what-problem-youre-trying-to-solve-with-a-spell..md)
    * [📙 Identify the required raw and decoded tables (henceforth sources) needed.](dune-engine-v2-beta/abstractions-in-dunev2/how-to-contribute-a-spell/identify-the-required-raw-and-decoded-tables-henceforth-sources-needed..md)
    * [🧪 Define a unit test for your spell.](dune-engine-v2-beta/abstractions-in-dunev2/how-to-contribute-a-spell/define-a-unit-test-for-your-spell..md)
    * [⛏ Write your spell as a select statement.](dune-engine-v2-beta/abstractions-in-dunev2/how-to-contribute-a-spell/write-your-spell-as-a-select-statement./README.md)
      * [A reformatted transfers table.](dune-engine-v2-beta/abstractions-in-dunev2/how-to-contribute-a-spell/write-your-spell-as-a-select-statement./a-reformatted-transfers-table..md)
      * [A daily aggregation of transfers.](dune-engine-v2-beta/abstractions-in-dunev2/how-to-contribute-a-spell/write-your-spell-as-a-select-statement./a-daily-aggregation-of-transfers..md)
      * [Rolling sum of daily transfers](dune-engine-v2-beta/abstractions-in-dunev2/how-to-contribute-a-spell/write-your-spell-as-a-select-statement./rolling-sum-of-daily-transfers.md)
      * [Final daily Ethereum ERC20 token balances spell](dune-engine-v2-beta/abstractions-in-dunev2/how-to-contribute-a-spell/write-your-spell-as-a-select-statement./final-daily-ethereum-erc20-token-balances-spell.md)
    * [🏃♀ Run your spell on dune.com](dune-engine-v2-beta/abstractions-in-dunev2/how-to-contribute-a-spell/run-your-spell-on-dune.com.md)
    * [🍴 Fork of the abstractions Github Repo, open a Pull Request.](dune-engine-v2-beta/abstractions-in-dunev2/how-to-contribute-a-spell/fork-of-the-abstractions-github-repo-open-a-pull-request..md)
    * [🎯 Dune will merge and deploy](dune-engine-v2-beta/abstractions-in-dunev2/how-to-contribute-a-spell/dune-will-merge-and-deploy.md)
  * [Spellbook Docs](https://spellbook-docs.dune.com/#!/overview)

## Dune App <a href="#duneapp" id="duneapp"></a>

* [Query Editor](duneapp/query-editor.md)
* [Visualizations](duneapp/visualizations/README.md)
  * [Graphs](duneapp/visualizations/graphs.md)
  * [Counters](duneapp/visualizations/counters.md)
  * [Pie Charts](duneapp/visualizations/pie-charts.md)
* [Dashboards](duneapp/dashboards.md)
* [Parameters](duneapp/parameters.md)
* [Adding new contracts](duneapp/adding-new-contracts.md)
* [Teams](duneapp/teams.md)

## Onboarding

* [Onboarding to Dune](onboarding/onboarding-to-dune.md)

## Bounties

* [Wizard Request Program](bounties/wizard-request-program.md)

## Dune Charts across the web <a href="#sharing" id="sharing"></a>

* [Attribution](sharing/attribution.md)
* [Embeds](sharing/embeds/README.md)
  * [Discord](sharing/embeds/discord.md)
  * [Twitter](sharing/embeds/twitter.md)
  * [Webpages](sharing/embeds/webpages.md)
  * [Mirror.xyz](sharing/embeds/mirror.xyz.md)
  * [Known Issues](sharing/embeds/known-issues.md)

## Resources

* [Press Kit](resources/press-kit.md)

## FAQ

* [How does Dune get it's data ?](faq/how-does-dune-get-its-data.md)
* [Does Dune have an API?](faq/does-dune-have-an-api.md)
* [Does Dune have a Token?](faq/does-dune-have-a-token.md)
* [How are results refreshing?](faq/how-are-results-refreshing.md)

## Changelog

* [Changes to Dune](changelog/dune-changes/README.md)
  * [March 2021](changelog/dune-changes/march-2021.md)
  * [August 2020](changelog/dune-changes/august-2020.md)
  * [March 2020](changelog/dune-changes/march-2020.md)
  * [January 2020](changelog/dune-changes/january-2020.md)
  * [October 2019](changelog/dune-changes/october-2019.md)
