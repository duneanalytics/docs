[View code on GitHub](https://dune.com/docs/data-tables/spellbook/top tables/prices.md)

# Prices

This technical guide covers the `Prices` feature of the Dune Docs project. The `Prices` feature allows users to get the price of almost all relevant ERC20 tokens. The data is pulled from the Coinpaprika API and the price is the volume-weighted price based on real-time market data, translated to USD.

The guide provides two tables for getting prices: `prices.usd` and `prices_from_dex_data`. The `prices.usd` table supports a range of ERC20 tokens. If the token you desire is not listed in this table, you can make a pull request to the GitHub repository. The `prices_from_dex_data` table creates price feeds based on decentralized exchange trading data. This table covers much more assets than `prices.usd`, since it covers all assets that are traded on any of the decentralized exchanges that are indexed in `dex.trades`. However, this table is very resource-intensive and can only be updated every few hours. Also, the resolution is only hourly, so if you need minutely prices, you should refer to `prices.usd`.

The guide provides a detailed explanation of how the `prices_from_dex_data` table works. The script generates median hourly prices based on data from decentralized exchanges found in `dex.trades`. It assigns asset prices based on a trading pair which has a price feed in `prices.usd`. For example, if the $SPELL/ETH pool is used, the $ETH price is contained in `prices.usd`, but the $SPELL price is not. In order to get the $SPELL price, the script will dynamically calculate the price of $SPELL based on the price of $ETH that was exchanged for it. The guide provides an example of how this calculation is done.

The guide also highlights known issues with the `prices_from_dex_data` table. In rare cases, the script will generate price feeds that are based on illiquid pairs and therefore report wrong data. This happens when all liquid trading pools of this token do not have a price feed in `prices.usd`. The guide provides an example of how this issue can occur and how to manually construct a price feed in such cases.

Overall, this technical guide provides a comprehensive explanation of the `Prices` feature of the Dune Docs project, including how to use the `prices.usd` and `prices_from_dex_data` tables, how the `prices_from_dex_data` table works, and known issues with the table.
## Questions: 
 1. What is the source of the price data for the decentralized exchange trading data table?
- The source of the price data for the decentralized exchange trading data table is the trading data from decentralized exchanges found in `dex.trades`.

2. What is the resolution for the `prices.usd` table?
- The resolution for the `prices.usd` table is by minute.

3. What are the known issues with the script that generates median hourly prices based on data from decentralized exchanges found in `dex.trades`?
- In rare cases, the script will generate price feeds that are based on illiquid pairs and therefore report wrong data. This happens when all liquid trading pools of a token do not have a price feed in `prices.usd`. In cases like this, a manual price feed construction is required.