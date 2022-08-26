---
description: Spells transform blockchain data into easy to use tables for all analysts!
---

# 🪄 Introducing Spellbook

## New level unlocked.

We’ve updated our database and now it’s time to update our contribution tools.

On January 31, 2020, we launched the abstractions repo as a place for wizards to create views and later tables. Since then, we’ve had over three hundred contributors and nearly 1k commits.

![Mats inaugural comment](https://lh3.googleusercontent.com/meUyvFUduwOIY8pm1I0Ce2HTTSndb5rgGycrWEWzcIeMCNsluARtfEP980iyJ0oiURs-KI6S8iF5vRiemNol7nEZn4UZjFUqhADOPlxXkdimu7T5jA-gisFoEzkoGszWTuXNoZpbj5rRU3EWPk8)

Abstractions are some of the most queried tables on Dune. That makes creating them one of the highest leverage things a wizard can do. We want to make that experience better by launching the **Spellbook**, a retooling of our existing [abstractions](https://github.com/duneanalytics/abstractions) repo + a first-in-class open-source analytics engineering tool called dbt.

[dbt-core](https://docs.getdbt.com/docs/introduction) (data build tool) is an open-source framework that injects more classical software engineering practices into writing SQL by mixing SQL with JINJA templating.

![Succinct description of why we are appropriately hyped on dbt ](https://lh5.googleusercontent.com/qloTvFTbRUeDcK3L5jecL7DbRzxhx8LrMf20RP6U3Wd4EWPKRQSgkctH8a9KpUPfUW6PdosA6uAxOiscz0tfCHifZNtanIiTyLhfCtQmCv159iHHerUEo4SAF\_Os\_s3BMEPj99\_J1Qendyi\_W00)

Abstractions, henceforth **models** in dbt-speak or **spells** in dune-speak, can be materialized into views and tables, but there are many possible refinements, including incrementally-loaded tables, date-partitioned tables, and more. These can all be compiled into SQL and run on dune.com. No more contributing code that you can’t test without our help.

dbt allows us to write and manage unit tests to spot and prevent any issues in our abstractions.

Data integrity tests can easily be added with a single line in a YAML file. Models can be checked for unique primary keys, non-null values, accepted values, and relational integrity with minimal effort.

dbt natively understands the dependencies between all models. In our old abstractions logic we were managing dependencies manually, which made deploying and maintaining them a mess. With dependency management, we can guarantee that all models are deployed in the correct order.

![Dependency graph created by dbt showing erc20 daily balances dependency tree](https://lh5.googleusercontent.com/0WikhWy2j\_jonRdBkuf0S2Z9f2ZJegTnM4WQjKZpO0T-biYx\_JNzBceEuM10AevnCeSE077ikWSFGicf90XBvCxa1XGOVYxi4hVCsP6HRwLFjugV6gTQSn15aviuQ1VQ0nYb0ir4pmRqKR3DV9g)

We hope you are as excited as we are about this new tool. Spellbook is now live in prod and we welcome new contributors.

#### Continue reading here to learn how to cast a spell into our github repo:

<div class="cards grid" markdown>
- [How to contribute a spell](how-to-contribute-a-spell/)
</div>

#### Visit the spellbook models documentation to see the current models

<div class="cards grid" markdown>
- [Spellbook Docs](https://spellbook-docs.dune.com/#!/overview/spellbook)
</div>


