---
title: Dashboards
---

**Dashboards are where Dune's content lives and gets discovered.**

Dashboards on Dune consist of widgets. Widgets can either be Visualizations or a text box. It is also possible to embed images/GIFs inside of the text box.

You can freely resize every widget to match the layout you want to create.

## Creating a Dashboard

You can create a new Dashboard by navigating to our "Discover" page and clicking on the "new Dashboard" button on the right.

The initial name that you give to your Dashboard will also be the URL slug. You can't change the URL slug afterwards, so be mindful of the name you choose. Changing the Dashboards display name is always possible though.

![create Dashboard](images/create-dashboard.gif)

## Adding Visualizations

You can simply add Visualizations to your Dashboard by going into the editor mode and clicking on the corresponding button. To go into editor mode first open one of your own Dashboards and click on the edit button on the top right.

![Add Visualizations](images/dashboard-visualizations.gif)

## Adding text boxes

To add text boxes to your Dashboard you have to go into editor mode first and can afterwards click on "add text widget". This will open a simple text editor window.

![Text widget](images/dashboard-text-widget.gif)

Text boxes support a subset of markdown. You can manipulate text and embed images and GIFs.

### Text manipulation

This is a short list to markdown syntax. A more advanced markdown guide can be found [here](dashboards.md#dashboards-are-where-dunes-content-lives-and-gets-discovered.).

| Element                                                                         | Markdown Syntax                                                                                    |
| ------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------- |
| [Heading](https://www.markdownguide.org/basic-syntax/#headings)                 | <p><code># H1</code><br><code>## H2</code><br><code>### H3</code></p>                              |
| [Bold](https://www.markdownguide.org/basic-syntax/#bold)                        | `**bold text**`                                                                                    |
| [Italic](https://www.markdownguide.org/basic-syntax/#italic)                    | `*italicized text`                                                                                 |
| [Ordered List](https://www.markdownguide.org/basic-syntax/#ordered-lists)       | <p><code>1. First item</code><br><code>2. Second item</code><br><code>3. Third item</code><br></p> |
| [Unordered List](https://www.markdownguide.org/basic-syntax/#unordered-lists)   | <p><code>- First item</code><br><code>- Second item</code><br><code>- Third item</code><br></p>    |
| [Code](https://www.markdownguide.org/basic-syntax/#code)                        | `` `code` ``                                                                                       |
| [Horizontal Rule](https://www.markdownguide.org/basic-syntax/#horizontal-rules) | `---`                                                                                              |
| [Link](https://www.markdownguide.org/basic-syntax/#links)                       | `[title](https://www.example.com)`                                                                 |

## Embedding Images and GIFs

Our text boxes can also be used to embed images or GIFs into your Dashboard.

The Syntax for embedding images is:

| [Image](https://www.markdownguide.org/basic-syntax/#images-1) | `![alt text](image url)` |
| ------------------------------------------------------------- | ------------------------ |

Since you can't store images locally on our servers, you need to upload your images somewhere else or find the raw file somewhere on the internet.

In practice this might look like this:

```
![text](https://pbs.twimg.com/media/FEWVLQwWUAQcqLY?format=jpg&name=medium)
--this is an image stored on twitters servers
```

You can resize the image by simply resizing the widget it is contained in.

You can combine images and text in one widget.

![embedding an image and resizing it](images/dashboard-image.gif)

## Arranging the layout of the Dashboard

You can arrange the different widgets on the Dashboard in whatever way you like.

Widgets will always try to move upwards, so if you want to create a visual divider section in your Dashboard it is advised to create a big text box as a divider.

![Dashboard layout](images/dashboard-layout.gif)
