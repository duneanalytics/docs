---
title: The Query Window
description: The Query window is where you work your Dune 🪄 by inputting SQL code and running it.
---

The Query window is where you work your Dune 🪄 by inputting SQL code and running it.

![Query window](images/query-window.png)

## Autocomplete

You can enable/disable the autocomplete function of the Query editor using the gear wheel in the top right corner:

![turn on autocomplete example](images/turn-on-autocomplete-example.png)

The autocomplete feature will bring up PostgreSQL keywords, as well as tables and aliases you've already included in your Query.

![query editor autocomplete example](images/query-editor-autocomplete-example.gif)

## Run Selection

To save yourself time while testing and debugging your Queries, you can run just a part of your Query.

To do this, highlight a part of your Query. You'll then see the <span class="fk-btn-1">Run</span> button turn into a <span class="fk-btn-1">Run selection</span> button.

Click and 🪄

![run selection example gif](images/run-selection.gif)

You'll need to highlight a syntactically complete and correct piece of SQL otherwise you'll get an error:

![run selection syntax error](images/run-selection-syntax-error.gif)

## Shortcuts

Here are a handful of shortcuts to make crafting Queries a 💨

| Shortcut      | Action                         |
| ------------- | ------------------------------ |
| ctrl + enter  | execute the Query              |
| ctrl + # or / | comments out the selected code |
| ctrl + space  | brings up a list of keywords   |
| crtl + z      | undoes your last changes       |
| ctrl + y      | redoes your last changes       |
| ctrl + f      | search for keywords            |
| ctrl + h      | search and replace keywords    |

_These shortcuts work on US/UK Keyboards and might vary based on the language setting on your machine._