---
title: Decoded Tables
description: Instead of working with the transactions, logs, and traces in their raw states, on Dune we decode smart contract activity into nice human-readable tables.
---



**To make it easier to work with smart contracts and programs, Dune has decoded data from all transactions (all functions and logs) into human readable tables. This means you don't need to work with any of the raw data from the blockchain!**

!!! suggestion "Consider using spellbook tables first"
    We highly recommend you use spellbook tables first, as many decoded tables have been further abstracted into tables like [`nft.trades`](../spellbook/top-tables/nft.trades.md) and [`dex.trades`](../spellbook/top-tables/dex.trades.md)

## EVM decoded tables

We support [decoded tables for Ethereum based chains (EVM)](evm/index.md) like Ethereum, Optimism, Arbitrum.

There are two types of EVM decoded tables, one that decodes functions and one that decodes event logs. 
<div class="cards grid" markdown>

-   #### [Call Tables](evm/call-tables.md)

    ---

    These are decoded from traces, which contain every function call within a transaction (i.e. between contracts).
  
    [→ Call Tables](evm/call-tables.md)

-   #### [Event Log Tables](evm/event-logs.md)

    ---

    These are decoded from event logs, which are data points emitted during a function call.
  
    [→ Event Log Tables](evm/event-logs.md)

</div>


## Solana decoded tables

We also support [decoded tables on Solana](solana/idl-tables.md), for any program (Candy Machine, Whirlpool, Jupiter, SPL Token, System Program, Pyth, and many more).

<div class="cards grid" markdown>

-   #### [IDL Tables](solana/idl-tables.md)

    These are decoded from `instruction_calls`, so all function calls at the first instruction level (not inner instructions) are decoded.
  
    [→ IDL Tables](solana/idl-tables.md)
</div>