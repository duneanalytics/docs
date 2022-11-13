---
title: 查询引擎
---

## 欢迎来到 DuneV2

DuneV2 改变了我们整个数据库的架构。 我们正在从 PostgreSQL 数据库向托管在 Databricks 上的 [Apache Spark](https://www.databricks.com/glossary/what-is-apache-spark) hosted on [Databricks](https://docs.databricks.com/getting-started/introduction/index.html)实例。 两种系统的却别可以总结如下:

* 我们现在使用 Databricks SQL，而不是 PostgresQL。SQL 关键字的变化很小，但可能与你的某些查询书写习惯有关。
* 与 PostgresQL 的面向行的方法相反，Spark 是一个面向列的数据库。
* 传统的索引被列块级别的 最小/最大 值替换。

!!! 注意
    下面是关于V2给构建查询带来的变化的详细介绍。 您可以从这里开始练习 [@springzhang](https://dune.com/springzhang/)'s [Tips and Tricks for Dune V2 Queries and Visualizations](https://dune.com/springzhang/tips-and-tricks-for-query-and-visualization-in-v2-engine)

## Databricks SQL 与 PostgresSQL 操作符的变化

两种编码语码愈发和关键字运算符之前的变化非常小，但是你应该注意下面这些差异:

| 描述                                     | DuneV1                                                                                                                                                                    | DuneV2                                                                                                                  |
|----------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------|
| **Spark 中不存在 bytea2numeric**           | bytea2numeric(bytea)                                                                                                                                                      | bytea2numeric_v2(string)                                                                                                |
| **基于 0 与基于 1 的索引**                     | 基于1                                                                                                                                                                       | 基于0                                                                                                                     |
| **bytea 与 string 字符串（地址、tx哈希等…）**      | <p><code>\x2a7d..</code><br>(bytea)</p>                                                                                                                                   | <p><code>0x2a7d...</code><br>(string)</p>                                                                               |
| **地址（string）在Dune v2 中是小写的**           | <p><code>\x2A7D...</code>(bytea)<br>Works in Postgres</p>                                                                                                                 | <p><code>0x2a7d...</code> (string)<br>在 Spark 中必须小写。<br>可以通过 <code>lower('0x2A7D...')</code>完成。</p>                     |
| **选择关键字列的方法不同**                        | `"from"`                                                                                                                                                                  | `` `from` ``                                                                                                            |
| **别名的命名方式不同**                          | `as "daily active users`"                                                                                                                                                 | ``as `daily active user``\`                                                                                             |
| **指数符号**                               | `x/10^y`                                                                                                                                                                  | `x*power(10,y)` or `x*1e*y`                                                                                             |
| **时间间隔参数在数字和时间单位之间需要一个空格**             | `Interval '1day'`                                                                                                                                                         | `Interval '1 day'`                                                                                                      |
| **Generate_series() 现在变成了 sequence()** | `generate_series('2022-05-15', CURRENT_DATE, '1 day')`                                                                                                                    | `explode(sequence(to_date('2022-01-01'), to_date('2022-02-01'), interval 1 day))`                                       |
| **prices.usd 表不再包含 Decimals 字段**       | <p>不要使用<br><code>prices.usd</code>的 decimals字段</p>                                                                                                                        | 用 `blockchain.erc20_tokens.decimals` 替换                                                                                 |
| **定义 NULL 数组**                         | `NULL::integer[]`                                                                                                                                                         | `CAST(NULL AS ARRAY<int>))`                                                                                             |
| **对字符串进行十六进制编码**                       | `encode(string, 'hex')`                                                                                                                                                   | `hex(string)`                                                                                                           |
| **获取json对象的差异**                        | <p><code>("takerOutputUpdate"-></code><br><code>'deltaWei'->'value'</code>)<br><br><br><code>decode(substring(("addressSet"->'baseAsset')::TEXT, 4,40), 'hex')</code></p> | <p><code>get_json_object(get_json_object(takerOutputUpdate,'$.deltaWei'),'$.value')</code><br><br><code>'0x'</code></p> |

在 DuneV2 中不建议使用双引号，即使引擎可以运行查询并且没有返回错误。

这是因为解析器有时将双引号中的词作为一个字符串处理，有时将其作为一个对象（例如列名）处理。

例如，在 where 子句中使用双引号引用一个列名，可以正常运行。然而，在 CTE 中的同一查询将列名视为一个字符串。[就想这里一样](https://dune.com/queries/1199604).

如果你发现有任何其他需要注意的变化， 请随时向我们的文档提交一份 PR，或在 [Discord](https://discord.com/dunecom)中向我们反馈!

在搜索 SQL 问题时，你现在应该搜索  `Databricks SQL median` 而不是搜索 `PGSQL median`. Databricks 在其网站上有一个有据可查的内置函数索引。

<div class="cards grid" markdown>
- [Databricks - Databricks SQL Language Reference](https://docs.databricks.com/sql/language-manual/sql-ref-functions-builtin.html)
</div>

## 数据库工作方式的变化

### 数据库是如何工作的？

在非常高的层次上，数据库将数据从存储读取到内存中，以返回你的查询结果。数据库通常会受到其将数据读入内存的速度的限制。这是一个经典的计算机科学问题，通常被称为[ I/O bound](https://en.wikipedia.org/wiki/I/O\_bound).

### **面向行的数据库**

数据库将其数据存储在页（pages）中。页通常包含多行信息。 多页将组成一个数据文件。数据库中的一个表有时会包含多个数据文件。


![面向行的数据库(PostgreSQL)](images/row-oriented.png)

当从数据库检索数据时，数据库将以页的大小将数据读入内存/缓存。 这是数据库一次性读取的最小数据量，也是从任何数据库读取数据时的一个常见瓶颈。在将数据读入内存后，数据库数据库要么创建临时文件，要么能够再次从内存中读取数据，最终到达所需的查询输出。

在任何数据库系统中，我们都希望在从数据库中检索任意数量的数据时减少读取的页的数量。 由于传统数据库将多行数据存储在一页中，因此它们最适合在一个查询中检索一行的所有列的情况。数据库将始终必须读取存储特定行的整个页，因此数据库返回也存储在同一页中的其他数据非常简单。查询在数据库中紧密存储在一起的其他行也是如此。因此查询第 500-600 行是非常高效的，查询第 5、87、789 和 1050 行并不是那么高效，但仍然没问题。

相比之下，查询存储在许多不同逻辑行中的数据，从而查询不同的页面，是一个非常昂贵的操作。今天我们在Dune上运行的大多数查询都是对数千甚至数百万行的某一列的数据点进行聚合。 在这些情况下，数据库将读取存储此列数据的整个页，即使它只需要其中一列的数据。  这意味着平均而言，我们正在读取大量返回查询结果并不需要用到的数据，只是因为它也包含在同一个页上，，并且数据库不能“仅”读取一列，而是必须读取包含该列的整行。

在 Postgres 中，我们可以使用索引来避免强制数据库读取整个表（因此读取了很多页），而只查看其中一个结构化的子集。这将使查询更加快速和高效, 但仅限于被索引的列。 由于为一个特定的表创建的每一个新索引都将是数据库中的一个新文件，并使更新和维护该表变得更加困难，因此这并不是一个可持续的数据库扩展方法。

我们不可能在数据库中的每一列或每一列的组合上都创建一个索引，而不至于在下一步遇到麻烦。因此，Dune V2不会在面向行的数据库上运行，而是在面向列的数据库上运行。

### **面向列的数据库**

我们不在页中存储行，而在页中存储列。通过这种方式，我们减少了数据库在聚合或读取特定列时需要读取的页数量。


![面向列的数据库 (Spark)](images/column-oriented.png)

具体来说，在 Dune V2 中，我们将 [parquet 文件格式](https://github.com/apache/parquet-format) 用于我们的新数据库。Parquet 有时被描述为面向行的数据库和面向列的数据库之间的混合方法，因为数据库中的表仍然由多个 Parquet 文件组成，这些文件由数据集的行分区。在 parquet 文件中，实际包含数据的页将包含列而不是行，但仍存储在行组中，这些行组进一步按行划分数据。数据库仍然粗略地以面向行的格式存储，但各个值以列方向存储在页上。

![parquet 文件示意图](images/parquet.png)

这意味着，即使整个数据库在某种程度上是以面向行的方式定向的，但如果我们真的想要读取数据，我们总是会从面向列的页中读取。通过这种方式，我们可以轻松地将大量逻辑行中的数据聚合到一列中，因为在这种布局中，我们必须加载到内存中以实际读取数据的页的数量被最小化了。

相反，如果我们尝试查询特定逻辑行的所有列，我们必须访问许多不同的页，因为一个逻辑行的数据不再存储在一个页中，而是分布在许多不同的页中。

这个视频很好地向我们解释了面向行和面向列的数据库系统的差异。

![type:video](https://www.youtube.com/embed/Vw1fCeD06YI)

**本质上**，将列而不是行存储在页中可以最大限度地减少数据库在从大量逻辑行中检索一列的数据时读取的不需要的数据量。我们有时能够在 Postgres 中通过以索引的形式创建大量结构化的子集数据来模仿这一点，但这并不能扩展。

### 索引或者说没有索引

在基于 parquet 的系统中，传统意义上的索引并不存在。但是，它们基本上是动态创建的，每个 parquet 文件都有一个页脚，其中包含存储在该 parquet 文件中的每一列的 `最小/最大` 。 然后在列块级别上重复此模式，它为 parquet 文件中特定行组内的不同列存储此元数据。

![最小/最大值示意图](images/minmax-schema.jpg)

在文件级别和列块级别同时使用这些 `最小/最大` 值, 允许数据库在扫描表时高效地跳过整个 parquet 文件或 parquet 文件中的列块。

不幸的是，字符串的 `最小/最大` 值通常不是很有用。特别是区块链系统中的 `tx_hash` 字符串 `地址` 字符串不适合这种 `最小/最大` 数据收集，因为它们是随机生成的。 这意味着数据库将无法基于这些字符串跳过文件或列块，因此查询将非常低效，因为它需要数据库实际将所有页加载到内存中。

也就是说，由于查询引擎总体上仍然能够非常有效地读取存储这些字符串的各个列，因此在大多数情况下，这不会对你的查询执行速度产生很大影响。

这主要与 `ethereum.transactions`, `bnb.logs`, `erc20_ethereum.erc20_evt_transfer`等基表相关，这些基表包含未经预过滤的非常大的数据集。

一个值得注意的例外是 solana 数据集 `account_activity` 它不像我们的其他数据集那样按 `block_time` 排序，而是按 `account_keys`排序。 这使我们能够实际合理地利用所使用的帐户密钥的 `最小/最大` 值，从而基于 `account_keys` 值运行有效的查询。

### 查询示例

有了这些知识，我们再来看看新版 Dune V2 引擎的一些查询。

**查询交易哈希**

```sql
Select * from ethereum.transactions
where hash = '0xce1f1a2dd0c10fcf9385d14bc92c686c210e4accf00a3fe7ec2b5db7a5499cff'
```

如果你用我们之前学到的所有知识来思考一下这个问题，你就会明白这个查询的效率非常低。 我们这里唯一的过滤条件是 `hash` 字符串，因此我们基本上强制查询引擎读取所有存储在 `tx_hash` 列数据的页。 我们可能可以跳过那些存储在每个 parquet 文件的页脚中的最小/最大值是 `0xa0 - 0xcd`的部分列块，但这些只是一个罕见的例外。

鉴于我们为了查询一个 `hash` 基本上要在对以太坊主网的整个历史进行全面扫描  (在撰写本报告时有16亿条记录)，这个查询在大约 6 分钟内运行完成是相当令人印象深刻的。

鉴于查询 `hash` 是Dune上的分析师的工作流程中是非常常见的，让我们考虑一下如何才能更快地完成这项工作吧。

我们只需要使用一个实际上包含有用的 `最小/最大` 值的列，以便能够不必完整读取所有页，而是能够跳过大量文件和列块。 Both `block_time` 和  `block_number` 都可用于此目的。

```sql
Select * from ethereum.transactions
where block_number = 14854616
and hash = '0xce1f1a2dd0c10fcf9385d14bc92c686c210e4accf00a3fe7ec2b5db7a5499cff'
```

这个查询仍然不如在 Postgres 中那么快,（在Postgres中我们可以使用  B-tree 索引），但运行时间为 13 秒，我们已经非常接近了。

在这种情况下，在查询执行过程中发生的事情是，数据库引擎能够读取parquet文件的页脚，能够确定很多parquet文件的`最小/最大`值不符合定义的标准，并有效地跳过它们。一旦我们找到了一个真正满足我们条件的 parquet 文件，我们可以简单地深入到列块的`最小/最大`值，找到合适的列块，并将剩下的几页列数据加载到内存中，也可以找到符合`hash`条件的列块。由于我们在这个查询中选择的是逻辑行的所有条目，实际上我们还需要访问其他几页，但是如果我们只对几行进行这样的操作，这就是一个合理有效的操作。

**经验：** 以一种数据库能够合理处理文件和列块的 `最小/最大` 值的方式来定义你的条件，以便它能够有效地找到你需要的逻辑行。

**在大量逻辑行上聚合数据**

下面是一个案例研究，以说明DuneV2在聚集大量逻辑行的数据方面有多高效。

```sql
Select avg(gas_used) from ethereum.transactions
```

此查询在 **惊人的** 7 秒内运行完成。 这主要是因为我们现在不必从字面上读取整个表。 我们现在能够极大地减少我们必须阅读的页的数量，因为所有这些数据都存储在多个 parquet 文件中的页中。 在 Postgres 中，我们必须读取的每个页都包含大量不需要的数据，在 Dune V2 中，我们只读取我们实际需要的数据。

**经验：** 跨大量逻辑行查询数据现在更加高效，并且许多以前由于超时而完全不可能的查询现在已经可以正常执行。

 [hildobby's](https://twitter.com/hildobby\_) [Ethereum Overview](https://dune.com/hildobby/Ethereum-Overview) 仪表盘就是这一点的很好的例子， 这是一个以前不可能实现的数据处理水平。

### 结束语

一些在我们的V1数据库上有大量索引的查询在DuneV2中可能会感到有点尴尬。对于erc20事件转移表(event transfer)、`ethereum.transactions` 和 `ethereum.logs`以及它们在其他区块链上的对应物，情况尤其如此。这是我们为了在大规模基础上实现区块链分析而采取的一种权衡。我们将继续对这些数据集和我们的数据库架构进行创新，以使每个查询在DuneV2上尽可能快地运行，但像对 `tx_hash` 的查询很慢只是这个新数据库系统的本质。尽管如此，我们认为我们已经在实现很多新的使用场景，以及加快大量现有查询的速度的方面做得非常好了，。

如果你对新系统有任何反馈或遇到问题，我们都会倾听并等待你在 [Canny](https://feedback.dune.com) and [Discord](https://discord.com/dunecom)上的反馈。
