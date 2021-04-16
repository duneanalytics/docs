---
description: Data Tables are what makes Dune work.
---

# Data

You can currently query data from **Ethereum mainnet** and **xDai**. We are working on expanding our offer to  other chains in the future.



The most commonly used tables are:

* \*\*\*\*[**Event and call data**](decoded-data/) for each project where you typically get the action that occurred in the smart contract. Simply search for project name to find the relevant tables.
* \*\*\*\*[**Abstractions/view tables**](abstractions.md) containing abstractions that makes various data very straight forward to query. Examples
  * `dex.trades`
  * `lending.borrow`, `lending.collateral_change`, `lending.repay`
  * `stablecoin.transfer`, `stablecoin.mint`, `stablecoin.burn`
  * See the full list and add your own via our [Github](https://github.com/duneanalytics/abstractions)
* \*\*\*\*[**prices.usd**](other-data.md) which gives you USD price of various assets per minute. Typically joined on minute with the event data and multiplied by the on-chain value \(trade, transfer etc\).
* \*\*\*\*[**erc20.tokens**](abstractions.md) gives you contract address, symbol and number of decimals for popular tokens. Token value transfers are then divided by `10` to the power of `decimals` from this table.
* \*\*\*\*[**Ethereum transactions**](raw-data.md) to get ETH transfers. Typically join with event on `ethereum.transactions.hash = evt_tx_hash`.

####  <a id="Decoded-smart-contract-data"></a>

