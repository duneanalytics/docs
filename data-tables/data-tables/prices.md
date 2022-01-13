# Prices

#### Centralized exchanges trading data <a href="#centralised-exchanges-trading-data" id="centralised-exchanges-trading-data"></a>

Token volume is great, but more often than not you want to know the USD value of smart contract activity.\
You can easily get and combine that information with on-chain data using the data we pull from the coinpaprika API.

The Price is the volume-weighted price based on real-time market data, translated to USD.

**prices.usd**

This table support a range of erc20.tokens. \
If the token you desire is not listed in here, please make a pull request to our [github repository](https://github.com/duneanalytics/abstractions/tree/master/prices) **** or use the decentralized price feed **dex.view\_token\_prices.**

| <p></p><p>column name</p> | description                                   |
| ------------------------- | --------------------------------------------- |
| contract\_address         | the contract address of the erc20 token       |
| symbol                    | the identifier of the asset (ticker, cashtag) |
| price                     | the price of the asset in any given minute    |
| minute                    | the resolution for this table is by minute    |

Note that `WETH` can be used for ETH price.

**prices.layer\_1usd**

This table also supports layer 1 assets on other blockchains.

| column name       | description                                   |
| ----------------- | --------------------------------------------- |
| contract\_address | the contract address of the erc20 token       |
| symbol            | the identifier of the asset (ticker, cashtag) |
| price             | the price of the asset in any given minute    |
| minute            | the resolution for this table is by minute    |

****

**dex.view\_token\_prices**

We created a decentralized price feed that calculates prices based on decentralized exchange trading data. **This table covers much more assets than prices.usd.** This table is very resource intensive and can therefore only be updated every few hours, please keep that in mind when utilizing it.

This table currently only exists for Ethereum data.

| column name       | description                                                                                                                                                                     |
| ----------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| contract\_address | the contract address of the erc20 token                                                                                                                                         |
| sample\_size      | the number of trades that occurred for this asset on all decentralized exchanges (If the number is very small you might want to exclude the data, it can lead to inaccuracies). |
| median\_price     | the median price of the asset in any given hour                                                                                                                                 |
| hour              | the resolution for this table is hourly                                                                                                                                         |



