# 🔧 How to Contribute a Spell



**On a high level, these are the steps you should take:**

1. Set up your local dev env as [per the instructions on the repo](https://github.com/duneanalytics/spellbook/blob/master/README.md)
2. Decide on what problem you’re trying to solve with a spell.
3. Identify the required raw and decoded tables (henceforth sources) needed. Define tests and freshness for your sources.
4. Define a unit test for your spell.
5. Write your spell as a select statement. Define your spell in a schema YAML file.
6. Run dbt compile to compile your spell.
7. Copy your spell from the target folder and try running it on dune.com in a new query window.
8. When you’re happy with your spell, from a fork of the abstractions Github Repo, open a Pull Request.
9. Tag duneanalytics/data-experience and write a short description of your spell.
10. Dune will open your pull request as an internal pull request which will trigger your spell to be created in the staging database and run tests.
11. If everything looks good, Dune will merge your changes and deploy them to production where they will be visible on Dune.com data explorer under abstractions.
