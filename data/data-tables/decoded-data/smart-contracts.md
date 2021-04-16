# Decoding Smart Contracts

## 🧐 Understanding data decoding in Dune Analytics <a id="&#x1F9D0;-Understanding-data-decoding-in-Dune-Analytics"></a>

This section contains a quick primer on how you can explore what decoded data we have and the methods we use to decode the data.

In Dune, there are tables for each event and function defined in the smart contract ABI. Subsequently, every event or function call on that contract is decoded and inserted as rows into these tables.

The tables are named accordingly

events:`projectname."contractName_evt_eventName"`

function calls: `projectname."contractName_call_eventName"`

As an example, decoded data for the `AddLiquidity`-event and `addLiquidity`-function of the uniswap exchange contract are found in tables

`uniswap."Exchange_evt_AddLiquidity"` and `uniswap."Exchange_call_addLiquidity"`.

Using the event tables is usually sufficient, but in some cases you will want to use the `call` tables. For instance Maker DAO which don’t give you too many events you can use tables like `maker.SaiTub_call_draw`.

### What contracts have decoded data? <a id="What-contracts-have-decoded-data"></a>

#### Decoded data <a id="Decoded-data"></a>

By querying `ethereum.contracts`, you can get an overview over which contracts are tracked by the Dune backend. The columns are

```text
namespace -- Project/product name
name -- Contract name
ABI -- The ABI that will populate the relevant tables
address -- The contract address
dynamic -- True if all contracts with the same bytecode are decoded automatically
bytecode -- The bytecode for the decoded contract
```

#### Abstractions and views <a id="Abstractions-and-views"></a>

On top of the decoded tables we have a growing number of views that make it even easier to work with the data.

Views are named `namespace.view_event` for instance. In general you can search for `view` in the table list to find the views we have.

#### A few handy queries to explore decoded tables <a id="A-few-handy-queries-to-explore-decoded-tables"></a>

**See all projects we have decoded data for**

```text
SELECT DISTINCT namespace FROM ethereum."contracts"; 
```

**Do we have decoded data for a specific contract?**

```text
SELECT * FROM ethereum."contracts"
WHERE address = '\xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2';
```

**Contracts that are “interface”-decoded**

```text
SELECT * FROM ethereum."contracts" WHERE address IS NULL;
```

If you are working with a an event or call table directly you can see if there are several instances of that contract with

```text
SELECT DISTINCT contract_address FROM projectname."contractName_evt_eventName"; 
```

### Scalable decoding across contracts <a id="Scalable-decoding-across-contracts"></a>

Many dApps have numerous smart contracts that are more or less similar, we have two main ways of handling this in a scalable way:

#### Contracts with the same bytecode <a id="Contracts-with-the-same-bytecode"></a>

Dune can dynamically add contracts to track by comparing the bytecode of deployed contracts to known bytecodes. If a known contract is “dynamic”, events and calls to a newly deployed contract with matching bytecode will find it’s way into the same tables as were defined by the base contract. Essentially this covers all factory-pattern contract architectures. As a result, `SELECT`-ing from a single table might yield data from multiple contracts. In decoded tables, the column `contract_address` tells you which smart contract the event or call is on. If you want to look at only a single contract you can filter by its address.

For example:

```text
SELECT DISTINCT contract_address FROM uniswap."Exchange_evt_TokenPurchase";
```

Will give you all the unique Uniswap exchanges with a Token Purchase event.

#### Interfaces <a id="Interfaces"></a>

When we’re interested in a subset of events fired regardless of the origin contract, Dune uses interface-decoding. Notable examples include erc20 and erc721 transfer events. This method is reserved for special cases.

