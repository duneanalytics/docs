# Decoded Data

#### Decoded smart contract data <a id="Decoded-smart-contract-data"></a>

Instead of working with the traces, logs, and receipts, Dune decodes smart contract activity into nice human-readable tables.  


In Dune, there are tables for each event and function defined in the smart contract ABI. Subsequently, every event or function call on that contract is decoded and inserted as rows into these tables.

The tables are named accordingly

events:`projectname."contractName_evt_eventName"`

function calls: `projectname."contractName_call_eventName"`

As an example, decoded data for the `AddLiquidity`-event and `addLiquidity`-function of the uniswap exchange contract are found in tables

`uniswap."Exchange_evt_AddLiquidity"` and `uniswap."Exchange_call_addLiquidity"`.

Using the event tables is usually sufficient, but in some cases you will want to use the `call` tables. For instance Maker DAO which don’t give you too many events you can use tables like `maker.SaiTub_call_draw`.

Submit contracts for decoding at [dune.xyz/decode](https://hackmd.io/k71ZUSTxQVKGqOcvR6OXnw).



### What contracts have decoded data? <a id="What-contracts-have-decoded-data"></a>

By querying `ethereum.contracts`, you can get an overview over which contracts are tracked by the Dune backend. The columns are

```text
namespace -- Project/product name
name -- Contract name
ABI -- The ABI that will populate the relevant tables
address -- The contract address
dynamic -- True if all contracts with the same bytecode are decoded automatically
bytecode -- The bytecode for the decoded contract
```

