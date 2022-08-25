# sandwiches

## **sandwiches**

This table contains detailed information about executed sandwiches

| **Column name**                   | **Type**  | **Description**                                                 |
| --------------------------------- | --------- | --------------------------------------------------------------- |
| created\_at                       | datetime  | Time of the records creation                                    |
| block\_number                     | bigint    | Block number                                                    |
| backrun\_swap\_trace\_address     | string    | address of the swap in the backrun transaction                  |
| backrun\_swap\_transaction\_hash  | string    | transaction\_hash of backrun transaction of specified sandwich  |
| frontrun\_swap\_trace\_address    | string    | address of the swap in the frontrun transaction                 |
| frontrun\_swap\_transaction\_hash | string    | transaction\_hash of frontrun transaction of specified sandwich |
| id                                | string    | Internal id of the sandwich                                     |
| profit\_amount                    | bigint    | Profit amount after the arbitrage                               |
| profit\_token\_address            | string    | Address of the profit asset                                     |
| sandwicher\_address               | string    | Address of the sandwicher                                       |
| timestamp                         | timestamp | Timestamp of the latest update of the file                      |

## \*\*\*\*
