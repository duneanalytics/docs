---
title: 嵌入第三方平台
description: 嵌入后，您可以在整个网络上享受漂亮的、更新的 dune 图片!
---

**截图是无趣和过时的。**

Dune自带可以跨平台使用的嵌入功能，而不必使用形式不一的截图功能。

你可以通过点击任何查询标题并选择右上角的嵌入功能来生成嵌入链接。

!生成一个嵌入链接](images/embed-link.gif)

## 参数化嵌入

嵌入链接也可用于参数化查询，但是需要一些技巧：

生成的嵌入链接并不包含必要的参数，尽管查询已经被执行过。我们正在致力于实现自动化的生成链接，但是目前仅有这一条途径能够做到。

现在你需要在链接前手动输入参数。

输入参数的写法是这样的：

`link?name_of_parameter1=xxxx&?name_of_parameter2=yyyy&...` \_\_

一个示例：

`>https://dune.com/embeds/118220/238460/aa002dd3-f9e2-4d63-86c8-b765569306c6NFT?address=0xff9c1b15b16263c61d017ee9f65c50e4ae0113d7&rolling_n_trades=500`

\`\`

## 在不同平台上嵌入

以下是几个使用Dune嵌入的示例：

<div class="cards grid" markdown>
- [Discord](discord.md)
- [Twitter](twitter.md)
- [Mirror.xyz](mirror.xyz.md)
- [Webpages](webpages.md)
</div>

## 已知问题

不幸的是，嵌入在几个相当流行的网站中不起作用，包括：

* Substack
* Medium
* GitBook
