---
title: 测试
---

如何为您的魔法编写单元测试？

在构筑魔法前先为其编写[测试](https://docs.getdbt.com/docs/building-a-dbt-project/tests)？这是什么软件工程？这种语言甚至是图灵完备的吗？！

我们正在努力实践测试驱动开发（[test-driven development](https://en.wikipedia.org/wiki/Test-driven_development)）。 这意味着，我们在编写魔法之前就需要考虑我们想要从魔法中得到什么结果。 之后，我们编写一个测试，如果这些结果与我们的输出匹配，则测试通过。 如果你无法想象你的魔法输出应该是什么样子，你需要重新回到数据建模。

编写一个好的单元测试需要创造力和一些勇气。 您需要找到一种方式来验证某些可能需要手动计算的输出。

举例来说, Etherscan 的[代币检查](https://etherscan.io/tokencheck-tool)可以查询出指定钱包地址、合约地址和日期的代币余额。 我们可以手动记录少数测试用例的结果，存储在 CSV 文件中作为 dbt [种子](https://docs.getdbt.com/docs/building-a-dbt-project/seeds)种子上传，或者作为单元测试本身的纯值。另一种方式可能是使用您的钱包来跟踪函数调用并计算该魔法对于该钱包的输出。

![Etherscan 代币余额检查](https://lh4.googleusercontent.com/EFymwYMt60l6zdbQHhmxV7c3FZ2RHSPjT0SIux1pdk0maghfXn1AyzfIT0b260VU-Hmol5Phm6QSWEROVP74fRqbcFYf2hZPjBDneyISwmjkpYF\_-DPYjAZXfKKQ2iVENYhJq3A6iGegSuggMf8)

这些测试不需要特别全面。 将来每当有人对该模型进行实质性更改时，都应该添加测试。 这里的主要目标是优先确保您的模型能正确运行并防止将来出现回退。

测试应该返回零行才能通过。 您可以发挥创造力，没有固定的方法来编写测试。 针对单个值编写测试的一种方法是使用`case when`语句来比较值。 我们在与模型进行比较值中可以进行一些硬编码。

“ref”栏里需要是您编写魔法的文件名，例如`{{ ref('balances_ethereum_erc20_day' )}}`。我们可以用 ref 在 DBT 项目中引用其他魔法或模型。

在编写测试时您不需要先编写模型，只需确定文件名即可。 您将在完成魔法后进行测试。 除非您想立即尝试运行测试以确认它会失败😉。

```sql
WITH unit_test1
    AS (SELECT CASE
                 WHEN amount == 100 THEN TRUE
                 ELSE FALSE
               END AS test
        FROM   {{ ref('balances_ethereum_erc20_day' )}}
        WHERE  wallet_address = '0x8de61aeacd24d2865a4fb471b8e746b02ef4e346'
               AND contract_address =
                   '0x00000000000045166c45af0fc6e4cf31d9e14b9a'
               AND DATE = '2022-06-27 00:00'),
    unit_test2
    AS (SELECT CASE
                 WHEN token == 'ONT'
                      AND amount == 7 THEN TRUE
                 ELSE FALSE
               END AS test
        FROM   {{ ref('balances_ethereum_erc20_day' )}}
        WHERE  wallet_address = '0x01bcb7117f00c4d3141ccab2432c7ae3bd5b00d3'
               AND contract_address =
                   '0x0000000000004946c0e9f43f4dee607b0ef1fa1c'
               AND DATE = '2022-06-27 00:00')
SELECT *
FROM   (SELECT *
       FROM   unit_test1
       UNION
       SELECT *
       FROM   unit_test2)
WHERE  test = FALSE
```
