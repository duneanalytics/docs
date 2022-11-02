---
title: Submissions
---

Here's how you can contribute your Spell on GitHub.

## Fork the Spellbook GitHub Repo and open a Pull Request.

When you’re happy with your Spell, from a fork of the [Spellbook GitHub Repo](https://github.com/duneanalytics/spellbook), open a Pull Request.

This step is non-specific to Spellbook. So I will farm out the explanation to Jake Jarvis who has an excellent [step by step guide](https://jarv.is/notes/how-to-pull-request-fork-github) to forking and committing a Pull Request to a public GitHub repository.

Once you’ve opened your pull request, fill out the [pull request template](https://github.com/duneanalytics/spellbook/blob/master/pull\_request\_template.md) and tag the duneanalytics/team-data-experience team-data-experience.

We will review your code and run your tests. Our goal is to eliminate this step and provide a sandbox where you can run your spells and tests directly. Unfortunately (fortunately?) GitHub rightfully blocks secrets from pull requests from forks which is why we can’t run DBT from your original pull requests.

## Dune will merge and deploy

If everything looks good, Dune will merge your changes and deploy them to production. Your Spells will be visible on [Dune V2 Data Explorer](../../getting-started/queries/data-explorer.md) under Spells.

And ta-da! You are a Spell casting wizard.

![](https://lh3.googleusercontent.com/sUXU5lD0NqGv9Xt2riyO\_WR2GUo74o9LaBWT5Kd\_a78A6CZ77ZvEiiCHLLOa-e8v\_Sqnmv3r2oBn6zvwZC1y3JX5HyFfhkYhJG59SWn-iefQ4-bKOAAXyaC1QS-umTHb73PYhZioaXYvP6QXP38)