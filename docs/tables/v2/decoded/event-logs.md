# Event logs

### Event logs

Smart Contracts emit **event logs** when certain predefined actions are completed. The structure published in these logs is predefined by the developer of the smart contract, the content is dynamically created during the transaction.

Logs are useful for monitoring, alerting and in general keeping track of what happens inside of a smart contract. Logs are your best friend as a data analyst since they reliably present you with data that is intended to be analysed post factum. If you ever want to see which logs _can_ be emitted by a smart contract, you can simply search for the keyword `emit` in the source code of the smart contract.

We will decode all event logs for smart contracts into tables named accordingly to this schema: `projectname_blockchain.contractName_evt_eventName`.

Let's stay in the context of the [uniswap v3 factory](https://etherscan.io/address/0x1f98431c8ad98523631ae4a59f267346ea31f984#code) and look at the event that gets emitted upon the creation of a new pool. The event is called `PoolCreated` and gets emitted every time somebody successfully deployed a new Uniswap V3 pool by calling the function `createPool`. The event will readily give us information like the tokens in the pool, the fee tier of this pool and the tick spacing. In Etherscan, you can easily look at the event logs of transaction by opening the [logs tab](https://etherscan.io/tx/0xdeb368592f3de0f2840754bce61d2c3f29cdb3407c63c699052e68a854c71eaa#eventlog). In Dune, this particular event will be stored in the table [`uniswap_v3_ethereum.Factory_evt_PoolCreated`](https://dune.com/queries/757381).

**Multiple Instances**

If there is multiple instances of a contract we will collect all event logs across all instances of this smart contract in one table. For example, all uniswap v3 pool `swap` events (on ethereum) are stored in the table \`\` [`uniswap_v3_ethereum.Pair_evt_Swap`](https://dune.com/queries/742037). The column `contract_address` indicates as to which smart contract emitted this event.

**Further Reading:**

[Understanding event logs on the Ethereum blockchain](https://medium.com/mycrypto/understanding-event-logs-on-the-ethereum-blockchain-f4ae7ba50378)

[Everything You Ever Wanted to Know About Events and Logs on Ethereum](https://medium.com/linum-labs/everything-you-ever-wanted-to-know-about-events-and-logs-on-ethereum-fec84ea7d0a5)
