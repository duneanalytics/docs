---
标题: V2 数据库
描述: 了解更多关于我们V2数据库结构背后的差异和思考。
---

高度概括地来说，数据库从存储中读取数据到内存中，以便对该数据进行操作，在Dune中，就是根据你的Dune查询的逻辑，转换和返回区块链数据。

读取速度，即把数据从存储空间加载到内存所需的时间，是数据库的一个基本制约因素。在计算机科学中，这被称为 [I/O 约束](https://en.wikipedia.org/wiki/I/O_bound), 这也是我们在Dune V2中过渡到数据湖并将存储和计算分离的主要挑战之一。

让我们看看这是如何发生的。

## 面向行的数据库

数据库将数据存储在页面中，传统上，这些页面包含信息的行。

多个页面组成一个数据文件，一个表将由一个或多个数据文件组成。

![面向行的数据库 (PostgreSQL)](images/row-oriented.png)

当从存储器中检索数据以对数据进行操作时，数据库将按页将数据读入内存。页面大小和加载的页面数量是查询速度的关键瓶颈，因为加载的页面数量和大小意味着更长的读取时间和等待查询结果的时间。

由于传统的数据库按行存储页面，它们最适合于检索一行的所有列或多个连续行的数据。

无论我们是想检索第10行的所有列还是第11-25行的第3列，我们的查询都会很快，因为只需要将一个页面读入内存。

相比之下，查询存储在许多不同逻辑行中的数据，也就是不同的物理页，是一个昂贵的操作，因为所有的页面都必须从磁盘中读取。

今天，我们在Dune上运行的大多数查询都是对数千甚至数百万行的某一列的数据点进行聚合。

这是因为我们的每一行都是基于我们所查询的区块链的一个交易或跟踪。

所以例如我们想看到上个月ETH和USDC之间的所有互换，交易将分布在成千上万的交易中，因此有成千上万的行 - 但数据将全部在这些行的一个列中。

因此，在面向行的数据库中，我们最终会用不需要的数据加载许多页面，因为我们在数千或数百万行中查询一个列。

在PostgreSQL中，我们使用索引来寻找特定的数据子集，而不是读取充满不相干数据的整个页面/表。

这使得查询非常快速和高效，但仅限于有索引的列。

由于为一个表创建的每一个新的索引都是一个新的数据库文件，所以在规模上更难更新和维护该表。

因此，Dune V2运行于面向列的表，而不是面向行的表。


## 面向列的数据库

![面向列的数据库 (Spark)](images/column-oriented.png)

在Dune V2中, 我们用 [parquet 文件格式](https://github.com/apache/parquet-format)在AWS S3上存储我们的数据。

Parquet有时被描述为面向行的数据库和面向列的数据库之间的一种混合方法，因为一个表仍然由多个parquet文件组成，而这些文件本身是按行划分的。

不过，在parquet文件内部，页面本身包含列而不是行。

页面被存储在行组中，而行组在parquet文件中是按行来划分数据的。

因此，数据库仍然大致以面向行的格式存储，但各个数值是以列的方式存储在页面内。

![parquet示意图](images/parquet.png)

尽管整个数据库在某种程度上是面向行的，但当我们真正想要读取数据时，我们是从面向列的页面读取的，因此是按列将页面读入内存。


相反，如果我们试图查询特定逻辑行的所有列，我们必须访问很多不同的页面，因为一个逻辑行的数据不再存储在一个页面中，而是分布在很多不同的页面中。

为了更好地理解行与列的区别，请看这个视频。

![type:video]([https://youtu.be/Vw1fCeD06YI](https://youtu.be/Vw1fCeD06YI))


### 索引，还是不索引？

我们有时能够模仿V1的PostgreSQL中基于列的数据的效率，以索引的形式创建大量的结构化子集数据，但目前这还不能扩展。

每个parquet文件都有一个页脚，包含存储在其中的每一列的 `最小/最大` 值。

这种模式在列块层面上重复，它为parquet文件中特定行组内的列存储这种元数据。

![混合 最大/最小值的示意图](images/minmax-schema.jpg)

在文件层面和列块层面使用这些 `最小/最大` 值，允许数据库在扫描表时有效地跳过整个parquet文件或parquet文件中的列块。为了使最小/最大值发挥作用，并使列块跳过发挥作用，列必须与文件的排序相关联。

不幸的是，字符串的 `最小/最大` 值往往不是很有用。

例如，区块链系统中的 `tx_hash` 字符串和 `address` 字符串不适合这种 `min/max` 数据收集，因为它们是随机生成的。

因此，如果我们按 `block_time` 对表进行排序（几乎在所有情况下都是这样做的），我们就不能有效地按 `tx_hash` 或 `address` 字符串进行 `min/max` ，因为这些数据不会按顺序排列。

这意味着数据库无法根据这些字符串跳过文件或列块，因此引用这些字符串的查询将是相当低效的，因为所有相关的页面都需要被读入内存。

也就是说，由于查询引擎仍然能够非常有效地读取存储这些字符串的各个列，因此在大多数情况下，这不会对查询的执行速度产生很大影响

性能成本主要与基础表有关，如`ethereum.transactions`，`bnb.logs`，`erc20_ethereum.erc20_evt_transfer`，等等，这些表包含非常大的数据集，没有预先过滤。

一个明显的例外是Solana数据集`account_activity`_，_ 它是按`account_keys`而不是像基于EVM的数据集那样按`block_time`排序。

这使得我们在建立基于 [raw Solana data](../tables/raw/solana/index.md)的查询时，可以利用`account_keys`的`min/max`值。



## Dune V2 查询示例

Equipped with the above knowledge, let's look at how some Queries on Dune V2 work.

!!! note
    These examples are written in Spark SQL.

### Querying for transaction hashes

```sql

Select * from ethereum.transactions

where hash = '0xce1f1a2dd0c10fcf9385d14bc92c686c210e4accf00a3fe7ec2b5db7a5499cff'

```

Based on the way our parquet file system works, this Query is very inefficient.

Our only filter condition here is a `hash` string so we’re asking the query engine to read all pages that store `tx_hash` column data.

The engine can skip a few column chunks where the `min/max` value stored in the parquet file footer is `0xa0 - 0xcd`, but those will be a rare exception.

Given we’re doing a full scan over the entire history of Ethereum Mainnet (billions of rows) to search for one `hash`, it's pretty impressive that this Query only takes about 6 minutes to run.

Since querying for ‘hash’ is a very common part of a Wizard’s workflow, let's think about how we can make this faster.

To do that, we just have to search based on a column that has sequential ‘min/max’ values so our query engine can skip over most pages/column chunks.

Both ‘block_time’ and ‘block_number’ are useful for this purpose.

```sql

Select * from ethereum.transactions

where block_number = 14854616

and hash = '0xce1f1a2dd0c10fcf9385d14bc92c686c210e4accf00a3fe7ec2b5db7a5499cff'

```

This Query is still not as fast as in PostgreSQL, where we can make use of [B-tree indexes](https://en.wikipedia.org/wiki/B-tree), but with a runtime of 13 seconds, we’re pretty close.

Again, by using our `where` clause to filter by block number, we’re leveraging the V2 engine’s ability to read the parquet file footers’ ‘min/max’ values and skip those that are out of bounds.

Once a parquet file that meets our condition is found, the engine simply loads into memory the relatively few pages from the column chunk with a `min` lower and a `max` greater than our specified `block_number` before finding a match to our ‘hash’ condition.

Since we are selecting all entries from the logical row in this Query, we actually need to access a few other pages as well, but this is a reasonably efficient operation if we only do this for a few rows.

**Lesson:** Define your conditions in a way in which the database is able to work with ‘min/max’ values of files and columns chunks so it can efficiently find the logical row(s) you need.


### Aggregating data over a large amount of logical rows

This is mainly a case study to illustrate how efficient DuneV2 is in aggregating data over a large set of logical rows.

```sql

Select avg(gas_used) from ethereum.transactions

```

This Query runs in an **amazing** 7 seconds.

This is mainly due to the fact that V2 doesn’t have to read the entire table since all this data is stored together in column-oriented pages across parquet files.

In V1’s PostgreSQL, each page we read into memory would have contained a lot of unneeded data.

In Dune V2, we can just read the data that we actually need.

**Lesson:** Querying for data across a large amount of logical rows is now much more efficient and a lot of Queries that were formerly sheer impossible due to timing out are now able to be executed.

Another good example to illustrate this is [@hildobby's](https://twitter.com/hildobby_) [Ethereum Overview](https://dune.com/hildobby/Ethereum-Overview) Dashboard.


## We’ll keep innovating

Some Queries that were heavily indexed on our V1 database might feel a bit awkward in Dune V2.

This is especially the case for `erc20` event transfer tables, `ethereum.transactions`, `ethereum.logs` and their counterparts on other blockchains.

This is a tradeoff we made to enable blockchain analytics on a large scale basis.

We will continue to keep innovating on these datasets and our database architecture to make every Query run as fast as possible on V2. Hopefully now you understand why Queries for data like `tx_hash` will be slow due to the tradeoffs we’ve made.

If you have any feedback or run into trouble with the new system, our #dune-sql Discord channel is the best place to get help from our team and Wizard community when Google fails you.

As you come across issues or identify areas of improvement, please send us an email at [dunesql-feedback@dune.com](mailto:dunesql-feedback@dune.com) and we’ll work with you to update and optimize!
