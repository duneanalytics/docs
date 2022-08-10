---
description: Raw data tables are the basic building blocks of our database.
---

# BNB Chain

BNB Chain(formerly Binance Smart Chain, BSC) is an instance of the Ethereum Virtual Machine built and maintained by a team from the popular Crypto Exchange [Binance](https://binance.com/).
BNB Chain follows most of the rules of Ethereum Mainnet, but has not implemented EIP1559. Instead it relies on [BEP-95](https://github.com/bnb-chain/BEPs/blob/master/BEP95.md) to burn fees that accrue during usage of the platform. Furthermore, the gas limit per block is set to 100 mio, enabling more transactions to be processed in a given block. Transactions fees are paid in \$BNB instead of \$ETH. 

You can read more about BNB Chain in [the documentation](https://docs.bnbchain.org/docs/bnbIntro).

On Dune, that means that the gas fields for EIP1559 transactions stay empty, everything else is the same.


### Raw data tables

{% content-ref url="blocks.md" %}
[blocks.md](blocks.md)
{% endcontent-ref %}

{% content-ref url="transactions.md" %}
[transactions.md](transactions.md)
{% endcontent-ref %}

{% content-ref url="event-logs.md" %}
[event-logs.md](event-logs.md)
{% endcontent-ref %}

{% content-ref url="traces.md" %}
[traces.md](traces.md)
{% endcontent-ref %}
