[View code on GitHub](https://dune.com/blob/master/data tables\spellbook\top tables\prices.md)

# Prices

This technical guide covers the `Prices` feature of the Dune Docs project. The `Prices` feature allows users to get the price of almost all relevant ERC20 tokens. The price data is pulled from the Coinpaprika API and is volume-weighted based on real-time market data, translated to USD.

The guide provides two tables for getting prices: `prices.usd` and `prices_from_dex_data`. The `prices.usd` table supports a range of ERC20 tokens. If the token you desire is not listed in this table, you can make a pull request to the GitHub repository or use the decentralized price feed `dex.view_token_prices` for V1 Engine.

The `prices_from_dex_data` table creates price feeds based on decentralized exchange trading data. This table covers much more assets than `prices.usd` since it covers all assets that are traded on any of the decentralized exchanges that are indexed in `dex.trades`. However, this table is very resource-intensive and can only be updated every few hours. The resolution is only hourly, so if you need minutely prices, you should refer to `prices.usd`.

The guide also explains how the `prices_from_dex_data` table works. The script generates median hourly prices based on data from decentralized exchanges found in `dex.trades`. It assigns asset prices based on a trading pair that has a price feed in `prices.usd`. For example, if the $SPELL/ETH pool is used, the script will dynamically calculate the price of $SPELL based on the price of $ETH that was exchanged for it.

The guide also highlights known issues with the `prices_from_dex_data` table. In rare cases, the script will generate price feeds that are based on illiquid pairs and therefore report wrong data. This happens when all liquid trading pools of this token do not have a price feed in `prices.usd`. In such cases, you have to manually construct a price feed.

Overall, this technical guide provides a comprehensive explanation of the `Prices` feature of the Dune Docs project. It explains how to use the two tables provided to get prices and highlights known issues with the `prices_from_dex_data` table.
## Questions: 
 1. What is the source of price data for this app?
- The price data is pulled from the coinpaprika API.

2. What is the difference between the `prices.usd` table and the table that creates price feeds based on decentralized exchange trading data?
- The `prices.usd` table supports a range of erc20.tokens and has a resolution by minute, while the table that creates price feeds based on decentralized exchange trading data covers much more assets than `prices.usd` and has a resolution only by hour.

3. What are the known issues with the script that generates median hourly prices based on data from decentralized exchanges found in `dex.trades`?
- In rare cases, the script will generate price feeds that are based on illiquid pairs and therefore report wrong data. This happens when all liquid trading pools of a token do not have a price feed in `prices.usd`. In cases like this, a manual price feed must be constructed.