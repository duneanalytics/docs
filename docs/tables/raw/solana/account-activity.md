# Account activity

## Solana.account\_activity

This table contains information from the transactions table focused on account usage. Each row contains all information about an account's usage in a transaction.

| Column Name                | Column Type | Description                                                      |
| -------------------------- | ----------- | ---------------------------------------------------------------- |
| block\_slot                | bigint      | The slot of the block this transaction was in.                   |
| block\_hash                | string      | The hash of the block this transaction was in                    |
| block\_time                | timestamp   | The timestamp that this account usage occurred                   |
| block\_date                | date        | The date this account usage occurred                             |
| address                    | string      | The address of the account, also referred to as public key       |
| tx\_index                  | int         | The index of this transaction in the block                       |
| tx\_id                     | string      | The ID of the transaction in which this account usage occurred   |
| tx\_success                | boolean     | The transaction succeeded and was committed                      |
| signed                     | boolean     | This account signed this transaction                             |
| writeable                  | boolean     | This account was granted read-write access in this transaction   |
| pre\_balance               | bigint      | The balance of this account before the transaction was processed |
| pre\_token\_balance    | decimal     | The token balance before the transaction was processed           |
| post\_balance              | bigint      | The balance of this account after the transaction was processed  |
| post\_token\_balance   | decimal     | The token balance after the transaction was processed            |
| balance\_change            | bigint      | The balance change that occurred as part of the transaction      |
| token\_balance\_change | decimal     | The balance change that occurred as part of the transaction      |
