---
title: Create a Dashboard
---

**Dashboards are where Dune's content lives and gets discovered.**

Dashboards on Dune consist of widgets. Widgets can either be Visualizations or Text. It is also possible to embed images or GIFs inside of the text widget.

You can freely resize every widget to match the layout you want to create.

## Creating a Dashboard



<div style="position: relative; padding-bottom: calc(66.66666666666666% + 41px); height: 0;"><iframe src="https://demo.arcade.software/xTAXmlo0nCL0FOn38hW9?embed" frameborder="0" loading="lazy" webkitallowfullscreen mozallowfullscreen allowfullscreen style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;color-scheme: light;" title="Creating a dashboard"></iframe></div>


**To create a dashboard on Dune:**

1. Use the create menu and pick "New Dashboard"
2. Give your Dashboard a name
3. Click on "Save and Open"
4. You are now inside of your Dashboard
5. Enter the edit mode by clicking on the "Edit" button in the top right corner
6. Add widgets by clicking on the "Add Widget" button in the top right corner
7. Pick the widget you want to add
8. You can now resize the widget by dragging the bottom right corner
9. You can also move the widget by dragging it around
10. Click on the "Save" button in the top right corner to save your changes

The initial name that you give to your Dashboard will also be the URL slug. You can't change the URL slug afterwards, so be mindful of the name you choose. Changing the Dashboards display name is always possible though.

## Add Widgets from the Query Editor

You can add widgets directly from the Query Editor.

<div style="position: relative; padding-bottom: calc(56.99999999999999% + 41px); height: 0;"><iframe src="https://demo.arcade.software/tcRqeUZ7qVNahQImdVsw?embed" frameborder="0" loading="lazy" webkitallowfullscreen mozallowfullscreen allowfullscreen style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;color-scheme: light;" title="Rocket Pool Minipools by ETH Bond vs. Time"></iframe></div>

1. Navigate to the query Editor
2. Pick the Visualization you want to add to your Dashboard
3. Click on the "Add to Dashboard" button
4. Choose the Dashboard you want to add the Visualization to
5. The Visualization is now added to your Dashboard

The widget will be added to the bottom of your Dashboard. You can move it around and resize it as you like.

## Adding Text Widget

You can add text widgets to your dashboard.

Text widgets support a subset of Markdown. You can manipulate text and embed images and GIFs.

### Text manipulation

This is a short list to Markdown syntax. A more advanced Markdown guide can be found [here](dashboards.md#dashboards-are-where-dunes-content-lives-and-gets-discovered.).

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

### Embedding Images and GIFs

Our text boxes can also be used to embed images or GIFs into your Dashboard.

The Syntax for embedding images is:

| [Image](https://www.markdownguide.org/basic-syntax/#images-1) | `![alt text](image url)` |
| ------------------------------------------------------------- | ------------------------ |

Since you can't store images locally on our servers, you need to upload your images somewhere else or find the raw file somewhere on the internet.

In practice this might look like this:

```markdown
![text](https://pbs.twimg.com/media/FEWVLQwWUAQcqLY?format=jpg&name=medium)
```

You can resize the image by simply resizing the widget it is contained in.

You can combine images and text in one widget.
