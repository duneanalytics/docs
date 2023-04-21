---
title: 7. 🌈 Make a Pull Request, Get Merged, Become an Archwizard 🧙
description: With all this out of the way, it’s time to submit a PR to the official Spellbook!
---

With all this out of the way, it’s time to submit a PR to the official Spellbook!

To do that, make sure you Commit your local changes to your Spellbook GitHub fork.

Then, head over to your fork on Github, find the “Contribute” dropdown towards the top of the page, open that and smash the “Open pull request button.”

![open pull request button](images/open-pull-request-button.png)

Follow the PR template to make sure all of your checks and tests pass, and then add the `ready-for-review` label once it's all green! If you click into the ["dbt slim ci (in beta)"](https://github.com/duneanalytics/spellbook/actions/runs/4763996851/jobs/8468061865) action and go to "dbt run initial model(s)", you will see a test_schema model built for any schemas you changed that creates a temporary table like this `test_schema.git_5d780b2f_tokens_ethereum_erc20`. You can query this table in the Dune interface (only under Spark SQL for now).

None of us are perfect, so pretty much all of us get comments from the Team for things we need to fix or improve with our Spells before they’ll approve the pull request.

Once you’ve addressed all the comments, your Spell will be approved and you’ll be one of the select few Dune Archwizards! 🧙 You will earn a git POAP for your work.