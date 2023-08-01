---
title: Share your work
description: Embeds allow you to enjoy beautiful, updating Dune charts across the web!
---

**Create embeds to display your Dune widgets across the web!**

To save you from having to take screenshots that might not look so great but will definitely be out of date a few minutes after you take them, we've built a native embed function that works across most web platforms.

You can generate embed links by clicking on any query title and selecting the embed function in the top right corner.

!!! note
    The embed button works as a stand alone link and as a way to embed your live graphs into websites/apps. If a Query has no Visualizations, the link will be to the Query Results table. If you have multiple Visualizations, the link will be for whichever Visualization you've selected when you clicked the Embed button.

![generating an embed link](images/embed-link.gif)

## Using Embeds on different platforms

Here are a few examples of how you can use Dune embeds on different platforms.

### Twitter

Twitter renders and updates Dune Visualizations automatically!

Simply paste your embed link and let the magic happen.

![Twitter automatically renders the embed link correctly](images/twitter.gif)

### Discord

Dune embeds work very well in Discord, simply drop the embed link in the chat and the corresponding Visualization will be displayed.

This also lends itself very well to programming a bot to return the corresponding charts on command.

![Discord](images/discord.gif)

### Web Pages

You can use Dune's embed links to add live Visualizations to any web page using an `iframe`

Here is a code snippet example:
```html
<iframe src="[your-query's-embed-link]" height="500" width="500" title="[name-of-your-query]"></iframe>`
```
A great showcase for this is the [cryptoart.io](https://cryptoart.io/data) website.

### Mirror.xyz

Dune Visualizations can easily be embedded into articles on mirror.xyz. Simply generate an embed link and postfix it with `?display=iframe`

```html

https://dune.com/embeds/208941/391702/34ee3319-1cac-40e1-a08d-160bd93693cc?display=iframe`
```
### Known Issues

Unfortunately, embeds do not work in a couple of fairly popular web platforms, including:

* Substack
* Medium
* GitBook

## Creating Embeds with Parameters

Embed links also work with parameterized Queries, but it is a bit tricky to get them to work:

The embed link you generate won't include the necessary parameters yet, even if you ran the query with them.

We are working on automating this, but for now you'll need to manually prefix the parameter link with the parameters:

`link?[name_of_parameter_1]=[xxxx]&?[name_of_parameter_2]=[yyyy]&[...]`

Here is a working example:
```
https://dune.com/embeds/118220/238460/aa002dd3-f9e2-4d63-86c8-b765569306c6NFT?address=0xff9c1b15b16263c61d017ee9f65c50e4ae0113d7&rolling_n_trades=500
```