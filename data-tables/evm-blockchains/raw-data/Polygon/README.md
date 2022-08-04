---
description: Raw data tables are the basic building blocks of our database.
---

# Raw Data

## Introduction

**Raw data tables allow you to query for any transaction, block, event log or trace across the blockchains Dune supports. These tables provide you raw, unfiltered and unedited data.**

Raw data tables are very useful to get meta information about the blockchain, a transaction, traces or certain events.

Additionally, with a few tricks and a bit of patience, you can actually gain substantial insights into systems of smart contracts using the encoded data. [Alex Kroeger](https://twitter.com/alex\_kroeger) wrote [a great article](https://alexkroeger.mirror.xyz/0C3EQBtFqAK4k2TAGPZhg0JMY-upfTAxuTD-o91vBPc) about this exact topic. We have a several [SQL functions](https://github.com/duneanalytics/abstractions/tree/master/ethereum/public) in our database that allow you to more easily work with encoded data.

However, queries that have been written using raw data tables are notoriously hard to understand and audit due to the nature of the the encoded data commonly found in these tables. Furthermore, the raw data tables have a very large number of rows and hence can be slow to query.&#x20;

Most of the time you are better off submitting contracts for [decoding](../../../duneapp/adding-new-contracts.md) and working with [decoded data](../decoded-data/).

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
