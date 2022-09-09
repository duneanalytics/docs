---
title: Data Modelling
---

This is the most important part of spell building.

A spell should be a view (ideally) or table you or others can use to do great analysis.

The benefits of building a spell are:

* **Consistency and maintainability.** Forking and copying queries to remix for ad-hoc analysis is fantastic but ngmi for the long run. Imagine finding a bug in your query or something simply changing in a contract. You can update _your_ query but everyone who forked or copy pasta’d the query won’t get the update.

* **Improved clarity on metrics.** There are often a few ways a metric can be calculated. If everyone builds their version, it’s difficult to determine the source of truth, and time is wasted hunting down the inconsistencies. Spells are built in a completely transparent fashion on a public GitHub repo which means the community can work to agree upon implementations.

* **Simplicity and developer experience.** Who wants to write the same query over and over again? Automate the boring and focus on novel analysis. [DRY](https://www.softwareyoga.com/is-your-code-dry-or-wet) applies to SQL as much as it does to other programming languages.

Some signs it’s time to make a spell:

* When you have multiple queries that include the same subquery.
* You’re copying long(ish) lists of static values between queries.
* The query has been forked or copied many times.
* Your query contains complex logic that you’d like to use elsewhere or that others might benefit from.
