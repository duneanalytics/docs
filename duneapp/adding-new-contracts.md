---
description: >-
  Everything you should know about the submission process to successfully decode
  new contracts
---

# Adding new contracts

The Dune App contains an extensive catalog of decoded contracts in the form of [call and event tables](../data-tables/data-tables/decoded-data.md#decoded-smart-contract-data). These contracts are brought into Dune by wizards through a process commonly referred to as [Decoding](../data-tables/data-tables/decoded-data.md).

## Quick tour

{% embed url="https://www.youtube.com/watch?v=4v9zEYZvv34" %}

## Submitting a new contract

Contracts can be submitted for decoding through the New contract form, which can be accessed via [My Creations > Contracts](https://dune.xyz/browse/contracts/authored) or within the dataset explorer in the query editor's sidebar:

![](<../.gitbook/assets/Screen Shot 2022-01-03 at 15.46.22.png>)

Clicking there will pop up a new browser tab with the contract submission form, which consists of 2 steps:

### 1. Blockchain and address

We first ask for the contract's address and blockchain. Requesting this data first has two purposes: to anticipate potential duplicate contracts and pending submissions, and to automate parts of the submission process where we can. The latter is usually accomplished by fetching potentially useful metadata from Dune and other third party sources where relevant.

For instance, below we submit the USDT contract (`0x94b008aA00579c1307B0EF2c499aD98a8ce58e58`) in Optimism:

![](<../.gitbook/assets/Screen Shot 2022-01-03 at 16.02.19.png>)

If we can find the contract through a third party source, we will show a green check mark next to the address field. This means we were able to fetch information such as the contract's name and ABI.&#x20;

### 2. Contract details

Then, after pressing Next, you will be prompted for other information about the contract that we need in order to decode it:

![](<../.gitbook/assets/Screen Shot 2022-01-03 at 16.05.07.png>)

If we found the contract through other third party sources, you will only have to fill in the project name. We have some naming conventions on that, partly due to our technical setup and also to make finding data more predictable.

Once you submit it, you are done! The contract will be stored in our queue, which we manually review for quality assurance purposes. Your submission might take a few days to get processed.

### Advanced options

In some instances, Dune can automatically detect and index multiple contract addresses under the same submission. This is useful for examples such as AMM pools where there often exists one contract instance per pair.&#x20;

We have two strategies for detecting other contracts for decoding:

1. **Bytecode match.** We use the bytecode of the contract address in the submission to find other matches in the whole chain history.
2. **Factory instances.** We find all other contracts created by the same address as the one responsible for creating the submitted contract.

In both cases, we assume that all the contracts found through either method correspond to the same blockchain, project name, contract name and ABI.

If you want us to index more than one contract, toggle on Advanced options and select "Yes" to the first question. Then, to the question of "Is it created by a factory contract?" select "No" to index all other contracts with the same bytecode or "Yes" to index all other contracts originating from the same creator.

{% hint style="warning" %}
Only use these options if you know what you're doing and are extremely familiar with the project's architecture and deployment hierarchy.&#x20;

Incorrectly applying these settings may lead to a rejected submission.
{% endhint %}

## Tracking your submissions

You can view your submissions and their processing status at any time by navigating to [My Creations > Contracts](https://dune.xyz/browse/contracts/authored):

![](<../.gitbook/assets/Screen Shot 2022-01-03 at 14.43.07.png>)

## Frequently Asked Questions

### Submitting contract information manually

Although we try to fetch contract information such as the ABI, sometimes this information might not be available through our sources.&#x20;

In those instances, you will need to manually input the contract's name and its ABI. This information should be available in block explorers such as [Etherscan](http://etherscan.io/) or [Blockscout](https://blockscout.com/) if the contract is verified in any of those sites.

{% hint style="info" %}
If the contract being manually submitted is a Proxy contract, we recommend you to move on to the next section.
{% endhint %}

### Submitting a Proxy contract

In order to properly decode transactions towards contracts that fit the Proxy pattern, Dune needs to map the Proxy contract's address with the implementation contract's ABI.&#x20;

We avoid monitoring the implementation contract's address because its logic is accessed via usage of Delegatecall in transactions. This would cause us to miss out on any event logs in the implementation contract's logic, since these are actually fired by the caller (the Proxy in this case) when calling a function through Delegatecall.

**When submitting proxy contracts to Dune, you should input the address of the Proxy contract.** We then will attempt to fetch the proxy's contract name and the implementation address it's pointing towards. After, we will attempt to source the implementation contract's ABI.

{% hint style="info" %}
For correctly decoding a Proxy contract, Dune needs the **Proxy address** and the **Implementation ABI**.
{% endhint %}

### Re-submitting a contract

Dune assumes each address in the blockchain can map to at most 1 contract. For this reason, submitting a contract with an address that already exists in `ethereum.contracts` will override it for Decoding purposes. This has a couple potential dangerous side effects:

* If the project or contract name has changed, we will generate new tables for all of the contract's methods and events. In turn, previous tables will stop updating, data will be fragmented, and queries will stop working.
* If the ABI has changed in a way that modifies an existing table's parameters, queries that depend on such table might break or become inaccurate.

If you attempt to submit an already existent contract, make sure to include extra context as part of the submission so we can assess whether it's worth overriding the contract's data.&#x20;

Sometimes, the risk of accepting a re-submission is higher than the perceived value by us, and my result in a rejection. If you disagree, feel free to reach out to us at #decoding in the Dune Discord and we'll see what we can do.

### Decoding of Diamond Proxy contracts

Similar to vanilla Proxy contracts, [EIP-2535](https://eips.ethereum.org/EIPS/eip-2535) contracts can be supported by passing in the address of the Diamond Proxy as well as **a single ABI representing the totality of all the facets interfaces**.

### My submission got rejected, why?

In the interest of data quality, we reject duplicative, incorrect or low quality submissions. To avoid that, make sure to submit accurate contract information.

### Other questions

Head over to #decoding on our [Discord](https://discord.gg/ErrzwBz) and we'll be happy to help!
