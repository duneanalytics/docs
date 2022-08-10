# Raw Data

**Raw data tables allow you to query for any transaction, block, event log or trace across the blockchains Dune supports. These tables provide you raw, unfiltered and unedited data.**

### Introduction

**Raw data tables allow you to query for any transaction, block, event log or trace across the blockchains Dune supports. These tables provide you raw, unfiltered and unedited data.**

Raw data tables are very useful to get meta information about the blockchain, a transaction, traces or certain events.

Additionally, with a few tricks and a few tricks, you can actually gain substantial insights into systems of smart contracts using the encoded data. [Alex Kroeger](https://twitter.com/alex\_kroeger) wrote [a great article](https://alexkroeger.mirror.xyz/0C3EQBtFqAK4k2TAGPZhg0JMY-upfTAxuTD-o91vBPc) about this exact topic. We have a several [SQL functions](https://github.com/duneanalytics/abstractions/tree/master/ethereum/public) in our database that allow you to more easily work with encoded data.

However, queries that have been written using raw data tables are notoriously hard to understand and audit due to the nature of the the encoded data commonly found in these tables. Furthermore, the raw data tables have a very large number of rows and hence can be slow to query.

Most of the time you are better off [submitting contracts for decoding](../../../duneapp/adding-new-contracts.md) and working with [decoded data](../decoded-data/).



### Differences in EVM chains

EVM chains at large follow the same execution model, however there is sometimes is differences in the consensus algorithm, the gas costs or even the calculation of gas costs.

You can find out about the individual chains in the specific sections of the documentation:

{% content-ref url="Chains/Arbitrum/" %}
[Arbitrum](Chains/Arbitrum/)
{% endcontent-ref %}

{% content-ref url="Chains/Avalanche-C-Chain/" %}
[Avalanche-C-Chain](Chains/Avalanche-C-Chain/)
{% endcontent-ref %}

{% content-ref url="Chains/BNB-Chain-(BSC)/" %}
[BNB-Chain-(BSC)](Chains/BNB-Chain-\(BSC\)/)
{% endcontent-ref %}

{% content-ref url="Chains/Ethereum-Mainnet/" %}
[Ethereum-Mainnet](Chains/Ethereum-Mainnet/)
{% endcontent-ref %}

{% content-ref url="Chains/Gnosis-Chain-(xDai)/" %}
[Gnosis-Chain-(xDai)](Chains/Gnosis-Chain-\(xDai\)/)
{% endcontent-ref %}

{% content-ref url="Chains/Optimism/" %}
[Optimism](Chains/Optimism/)
{% endcontent-ref %}

{% content-ref url="Chains/Polygon/" %}
[Polygon](Chains/Polygon/)
{% endcontent-ref %}

