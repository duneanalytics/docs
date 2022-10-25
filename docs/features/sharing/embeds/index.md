---
title: Embeds
description: Embeds allow you to enjoy beautiful, updating dune charts across the web!
---

**Screenshots are boring and tech of the past.**

Instead of using static screenshots in varying forms of quality, Dune has a native embed function that works across most platforms.

You can generate embed links by clicking on any query title and selecting the embed function in the top right corner.

!!! note
    The embed button works as a stand alone link and as a way to embed your live graphs into websites/apps. If your Query has no Visualizations, the link will be to the Query Results table. If you have multiple Visualizations, the link will be for whichever Visualization you've selected when you clicked the Embed button.

![generating an embed link](images/embed-link.gif)

## Parameterized embeds

Embed links also work with parameterized queries, but it is a bit tricky to get them to work:

The embed link that gets generated does not include the necessary parameters yet, even if you have ran the query with it. We are already working on automating the link generation, but for now the way described below is the only thing to make this to work:

You need to manually prefix the parameter link with the parameters.

The syntax for this is:

`link?name_of_parameter1=xxxx&?name_of_parameter2=yyyy&...` \_\_

An example of this would be:

`>https://dune.com/embeds/118220/238460/aa002dd3-f9e2-4d63-86c8-b765569306c6NFT?address=0xff9c1b15b16263c61d017ee9f65c50e4ae0113d7&rolling_n_trades=500`

\`\`

## Embeds across different platforms

Here are a couple of exemplary use cases for Dune embeds:

<div class="cards grid" markdown>
- [Discord](discord.md)
- [Twitter](twitter.md)
- [Mirror.xyz](mirror.xyz.md)
- [Webpages](webpages.md)
</div>

## Known Issues

Unfortunately, embeds do not work in a couple of fairly popular sites, including:

* Substack
* Medium
* GitBook
