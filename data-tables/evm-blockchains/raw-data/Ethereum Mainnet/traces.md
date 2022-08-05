# Traces

## ethereum.traces

Transactions can trigger smaller atomic actions that modify the internal state of an Ethereum Virtual Machine. Information about the execution of these actions is logged and can be found stored as an EVM execution trace, or just a _trace_. In Etherscan these are referred to as "internal transactions".

Read more [here](https://medium.com/chainalysis/ethereum-traces-not-transactions-3f0533d26aa).

| **Column Name** | **datatype** | **Description**                                                                                                                                                                                                                                |
| --------------- | ------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| block\_time     | timestamptz  | the time when the block was mined                                                                                                                                                                                                              |
| tx\_success     | boolean      | a true/false value that indicates if the transaction succeeded                                                                                                                                                                                 |
| success         | boolean      | a true/false value that shows if the trace action succeeded                                                                                                                                                                                    |
| block\_hash     | bytea        | a unique identifier for that block                                                                                                                                                                                                             |
| block\_number   | int8         | the length of the blockchain in blocks                                                                                                                                                                                                         |
| tx\_hash        | bytea        | the transaction hash of the event                                                                                                                                                                                                              |
| from            | bytea        | address of the sender                                                                                                                                                                                                                          |
| to              | bytea        | address of the receiver. `Null` when its a contract creation transaction                                                                                                                                                                       |
| value           | numeric      | the amount of ether sent in this transaction in `wei`.                                                                                                                                                                                         |
| gas             | numeric      | Gas provided with the message call                                                                                                                                                                                                             |
| gas\_used       | numeric      | the gas consumed by the transaction in wei                                                                                                                                                                                                     |
| tx\_index       | numeric      | The position of the transaction in a block.                                                                                                                                                                                                    |
| trace\_address  | array        | address of the trace within the call graph forest. E.g., \[0, 2, 1] is the parent of \[0, 2, 1, 0].                                                                                                                                            |
| sub\_traces     | numeric      | number of children of a trace                                                                                                                                                                                                                  |
| type            | text         | can be `reward`, `create`, `call` or `suicide`. Describes the type of action taken in this trace.                                                                                                                                              |
| address         | bytea        | the contract that is called when the type is `suicide` or `create`                                                                                                                                                                             |
| code            | bytea        | the bytecode to deploy a new contract, only contains data when type is `create`.                                                                                                                                                               |
| call\_type      | bytea        | <p>can be <code>staticcall</code>, <code>delegatecall</code> or <code>call</code>.<br>For more information refer <a href="https://medium.com/coinmonks/delegatecall-calling-another-contract-function-in-solidity-b579f804178c">here</a>. </p> |
| input           | bytea        | the bytecode of the call that is made to another smart contract                                                                                                                                                                                |
| output          | bytea        | the bytecode answer the smart contract that was called gives back                                                                                                                                                                              |
| refund\_address | bytea        | only contains data if `type` was `suicide`. Specifies where to send the outstanding ether balance.                                                                                                                                             |




### Gas used in traces

The `gas_used` column in the ethereum.traces table is a bit hard to understand, so here is some pointers:

* the `gas_used` of a trace will always include the gas consumed by the trace and all it's subtraces.
* the `gas_used` of the inital call will not contain the cost of making the call in the first place
  * you need to add 21000 gas units + the cost of sending zero + non zero bytes to the `gas_used` value of the top trace to arrive at the "true" `gas_used` value.
  * for more reading on this please refer to this [stackexchange entry](https://ethereum.stackexchange.com/questions/31443/what-do-the-response-values-of-a-parity-trace-transaction-call-actually-repres)
  * a query doing this in dune: [https://dune.com/queries/895857](https://dune.com/queries/895857)

