---
title: Decoding Contracts
description: Here's everything you need to know about Decoded contracts and how to submit them!
---

**Dune contains an extensive catalog of Decoded Contracts, brought into the platform through Wizard submissions!**

Instead of working with raw transaction, log, and trace data, contracts are decoded into human-readable tables for each event and function defined in the smart contract's ABI ([Application Binary Interface](https://www.alchemy.com/overviews/what-is-an-abi-of-a-smart-contract-examples-and-usage)).

Learn more about how Decoding works and what Decoded tables are available in the [data tables section](../../data-tables/decoded/).

## Submitting a new contract for decoding

![type:video](https://www.youtube.com/embed/4v9zEYZvv34)

Contracts can be submitted for decoding through:

- [The New contract form](https://dune.com/contracts/new)
- The [My Creations > Contracts Tab](https://dune.com/browse/contracts/authored)

### 1. Blockchain and address

We first ask for the contract's address and blockchain. Requesting this data first has two purposes:

1. To enable us to review for potential duplicate contracts and pending submissions.
2. To automate parts of the submission process where we can.

The latter is usually accomplished by fetching potentially useful metadata from Dune and other third party sources where relevant.

For instance, below here's an example of submitting the USDT contract (`0x94b008aA00579c1307B0EF2c499aD98a8ce58e58`) in Optimism:

![Submit smart contract](images/decoding-contracts/submit-smart-contract.png)

If we can find the contract through a third party source, we will show a green check mark next to the address field.

This means we were able to fetch information such as the contract's name and ABI (Application Binary Interface).

### 2. Contract details

After pressing Next, we ask for other information about the contract that we need in order to decode it:

![Submit smart contract 2](images/decoding-contracts/submit-smart-contract-2.png)

If we found the contract through other third party sources, you will only have to fill in the project name.

We have some naming conventions on that, partly due to our technical setup and also to make finding data more predictable.

**Project Names Rules**

- All lowercase
- No spaces (underscore "_" if needed)
- Added "_v2" or other version names at the end if applicable


Although we try to fetch contract information such as the ABI, sometimes this information might not be available through our sources.

In those instances, you will need to manually input the contract's name and its ABI.

If the contract has been verified by the chain's block explorer, you should be able to find this information there.

#### How do I submit a Proxy contract?

In order to properly decode transactions towards contracts that fit the [Proxy pattern](https://blog.openzeppelin.com/proxy-patterns/), Dune needs to map the Proxy contract's address with the implementation contract's ABI.

We avoid monitoring the implementation contract's address because its logic is accessed in transactions via the [`DelegateCall` function](https://medium.com/coinmonks/delegatecall-calling-another-contract-function-in-solidity-b579f804178c).

If we did monitor the implementation contract's address directly, we would miss out on any event logs in its logic since these are actually fired by the caller (the Proxy in this case) when calling a function through `DelegateCall`.

!!! warning
    When submitting Proxy-patterned contracts to Dune, you should input the Proxy contract's address and, if you have it, the Implementation contract's ABI.

When you submit the Proxy contract's address, we'll attempt to fetch the proxy's contract name and the implementation address it's pointing towards to source the Implementation contract's ABI.

If we can't find the Implementation contract's ABI, you'll need to find it using the relevant chain's blockchain explorer and input it manually.


#### How do I re-submit a contract?

Dune assumes each address in the blockchain can map to at most 1 contract. For this reason, submitting a contract with an address that already exists in `[blockchain].contracts` will override it for Decoding purposes.

This has a couple potential dangerous side effects:

- If the project or contract name has changed, we will generate new tables for all of the contract's methods and events. In turn, previous tables will stop updating, data will be fragmented, and Queries will stop working.
- If the ABI has changed in a way that modifies an existing table's parameters, Queries that depend on such table might break or become inaccurate.

If you attempt to submit a contract that already exists, we'll first present a warning note and ask you to confirm you want to proceed:

![new contract resubmission warning](images/decoding-contracts/new-contract-resubmission-warning.png)

Then, at the bottom of the Details page, we'll ask you to explain why you're resubmitting the contract so we can assess whether it's worth overriding the contract's data:

![new contract resubmission reason](images/decoding-contracts/new-contract-resubmission-reason.png)

If we believe the risk of accepting a re-submission is higher than the added value, we'll reject your resubmission.

If you think we're wrong (we're only human!), feel free to reach out in our [#decoding Discord channel](https://discord.com/channels/757637422384283659/850326962152538122) and we'll discuss it further with you!

#### How do I submit Diamond Proxy contracts?

Similar to vanilla Proxy contracts, [EIP-2535](https://eips.ethereum.org/EIPS/eip-2535) contracts can be supported by passing in the address of the Diamond Proxy as well as **a single ABI representing the totality of all the facets interfaces**.

#### My submission got rejected, why?

In the interest of data quality, we reject duplicative, incorrect or low quality submissions. To avoid rejection, be sure to submit accurate contract information! 🙏

#### Why am I missing historical data for my contract?

It may take up to six hours from the time of contract approval for the contract to be fully decoded along with its historical data. If you still can't see the data after this period, please reach out to us through our [#decoding Discord channel](https://discord.com/channels/757637422384283659/850326962152538122).

#### For all other questions:

Head over to the [#decoding Discord channel](https://discord.com/channels/757637422384283659/850326962152538122) and we'll be happy to help!
