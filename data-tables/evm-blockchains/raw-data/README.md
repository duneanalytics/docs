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

{% content-ref url="chains/arbitrum/" %}
[arbitrum](chains/arbitrum/)
{% endcontent-ref %}

{% content-ref url="chains/avalanche-c-chain/" %}
[avalanche-c-chain](chains/avalanche-c-chain/)
{% endcontent-ref %}

{% content-ref url="chains/bnb-chain-bsc/" %}
[bnb-chain-bsc](chains/bnb-chain-bsc/)
{% endcontent-ref %}

{% content-ref url="chains/ethereum-mainnet/" %}
[ethereum-mainnet](chains/ethereum-mainnet/)
{% endcontent-ref %}

{% content-ref url="chains/gnosis-chain-xdai/" %}
[gnosis-chain-xdai](chains/gnosis-chain-xdai/)
{% endcontent-ref %}

{% content-ref url="chains/optimism/" %}
[optimism](chains/optimism/)
{% endcontent-ref %}

{% content-ref url="chains/polygon/" %}
[polygon](chains/polygon/)
{% endcontent-ref %}

