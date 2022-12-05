---
title: Prerequisites
description: Here's the local environment setup you'll need to do before casting a Spell.
---

Before you can start casting Spells, you'll need to set up your local environment.

- Have [Python 3.9](https://realpython.com/installing-python/) installed on your computer. Our recommendation is to follow the [Hitchhiker's Guide to Python](https://docs.python-guide.org/starting/installation/)

- Install an IDE to edit your code. [VSCode](https://code.visualstudio.com/) is a nice free one.

- Ensure that [pip](https://pip.pypa.io/en/stable/installation/) is installed.

- Install [pipenv](https://pypi.org/project/pipenv/), this will allow us to create a virtualenv with dbt.

- Set up [git and github](https://docs.github.com/en/get-started/quickstart/set-up-git) including authentication.

- Make a [fork](https://docs.github.com/en/get-started/quickstart/fork-a-repo) of the [spellbook repo](https://github.com/duneanalytics/spellbook). Including cloning locally and adding an upstream.

- Review Github’s [instructions](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/creating-a-pull-request-from-a-fork) on how to make a pull request from a fork.

P.S. If you have trouble with these prerequisites, please reach out for help in the [#📜spellbook Discord Channel](https://discord.com/channels/757637422384283659/999683200563564655) channel!


## Initial Installation

You can watch the video version of this if you scroll down a bit.

Navigate to the abstraction repo within your CLI (Command line interface).

```console
cd user\directory\github\spellbook
# Change this to wherever spellbooks are stored locally on your machine.
```

Use the pipfile to create a pipenv.

```console
pipenv install
```

If the env is created successfully, skip ahead to `pipenv shell`.

Our script is looking for a static python version, the likelihood of an error for a wrong python version is pretty high. If that error occurs, check your python version with:

```console
py --version
```

Now use any text editor program to change the python version in the pipfile within the spellbook directory to your python version. You need to have at least python 3.9.
If you have changed the python version in the pipfile, run `pipenv install` again.

You are now ready to activate this project's virtual environment.
Use:

```console
pipenv shell
```

You have now created a virtual environment for this project. You can read more about virtual environments [here](https://realpython.com/pipenv-guide/).

To initiate the dbt project run:

```console
dbt init
```

Enter the values as shown below:

```console
Which database would you like to use?
[1] databricks
[2] spark

(Don't see the one you want? https://docs.getdbt.com/docs/available-adapters)

Enter a number: 1
host (yourorg.databricks.com): .
http_path (HTTP Path): .
token (dapiXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX):
[1] use Unity Catalog
[2] not use Unity Catalog
Desired unity catalog option (enter a number): 2
schema (default schema that dbt will build objects in): wizard
threads (1 or more) [1]: 2
```

This will not connect to the database but you have access to some dbt actions.
**When you are prompted to choose a schema, please enter `wizard` so we know you are an external contributor.**
Should you make an error during this process (not entering `wizard` being the only one you can make), simply quit the CLI and start over.

To pull the dbt project dependencies run:

```console
dbt deps
```

Then, run the following command:

```console
dbt compile
```

dbt compile will compile the JINJA and SQL templated SQL into plain SQL which can be executed in the Dune UI. Your spellbook directory now has a folder named `target` containing plain SQL versions of all models in Dune. If you have made changes to the repo before completing all these actions, you can now be certain that at least the compile process works correctly, if there is big errors the compile process will not complete.
If you haven't made changes to the directory beforehand, you can now start adding, editing or deleting files within the repository.
Afterwards simply run `dbt compile` again once you are finished with your work in the directory and test the plain language sql queries on dune.com.

## Coming back after Initial Installation

If you have done this installation on your machine once, to get back into dbt, simply navigate to the spellbook repo, run `pipenv shell`, and you can run `dbt compile` again.

## What did I just do?

You now have the ability to compile your dbt model statements and test statements into plain SQL. This allows you to test those queries on the usual dune.com environment and should therefore lead to a better experience while developing spells. Running the queries will immediately give you feedback on typos, logical errors or mismatches.
This in turn will help us deploy these spells faster and avoid any potential mistakes.

We are thinking about better solutions to make more dbt actions available directly but we also have to consider security.
