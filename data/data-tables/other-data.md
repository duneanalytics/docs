# 3rd Party Data Feeds

#### Centralised exchanges trading data <a id="Centralised-exchanges-trading-data"></a>

Token volume is great, but more often than not you want to know the USD value of smart contract activity.

You can easily get and join that information with onchain data using the data we pull from the coincap API. See how to use it below.

* `prices.usd` - assets on Ethereum
  * contract\_address
  * price
  * minute
  * symbol \(ticker\)

Note that `WETH` can be used for ETH price.

* `prices.layer_1usd` - native layer 1 assets
  * price
  * minute
  * symbol \(ticker\)

Price is the volume-weighted price based on real-time market data every minute, translated to USD.

