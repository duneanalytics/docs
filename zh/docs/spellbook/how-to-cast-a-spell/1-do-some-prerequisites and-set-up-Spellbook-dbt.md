---
title: 1. 💻 Do Some Prerequisites and Set Up Spellbook dbt
description: Heres what you need to do to set up your computer to work on Spellbook.
---

To get started, you’ll need to install:

* [VSCode](https://code.visualstudio.com/) (any IDE will work but this is what we use)
* [Python 3.9](https://realpython.com/installing-python/) (you need this exact version of Python and distutils installed; if you have trouble ask for help in our [#spellbook Discord channel!](https://discord.com/channels/757637422384283659/999683200563564655))
* [pip](https://pip.pypa.io/en/stable/installation/)
* [pipenv](https://pypi.org/project/pipenv/)
* [git and GitHub](https://docs.github.com/en/get-started/quickstart/set-up-git) (including authentication)

After that, you’ll also need to:

* Make a [fork](https://docs.github.com/en/get-started/quickstart/fork-a-repo) of the [spellbook repo](https://github.com/duneanalytics/spellbook). Including cloning locally and adding an upstream. 
* Review Github’s [instructions](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/creating-a-pull-request-from-a-fork) on how to make a pull request from a fork. 

Here’s a quick video showing how to make a fork of the Spellbook repo:

![type:video](https://drive.google.com/file/d/1wGGhgwUsersdvqq4YpDWRMRSgqd8l8Qd/preview)

Essentially you:

1. Go to the Spellbook repository and click the fork button at the top.
2. Copy the HTTPS URL of your fork
3. Open the folder that you’d like to store Spellbook in inside of VS Code
4. Open a terminal in VS code and enter `git clone [paste your URL here]`

Once you hit enter, you’ll start downloading Spellbook, it’ll take a few minutes.

## Setting up Spellbook dbt

Once you have a local copy of your Spellbook fork, it’s time to set up Spellbook dbt!

If it isn’t already, open your local copy of your Spellbook fork in VSCode, then open a terminal and enter `pipenv install`.

This will install the packages necessary to run Spellbook on your computer.

Once that installation is complete, run `pipenv shell` to activate your virtual environment.

Then `dbt init` to initialize dbt.

Enter these values in each of the prompts that follow:

```

1. Enter a number: 2 [choose databricks]
2. host (yourorg.databricks.com): . [enter “.”]
3. http_path (HTTP Path): .
4. token (dapiXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX): [just hit enter at first]
    1. [1] use Unity Catalog
    2. [2] not use Unity Catalog
5. Desired unity catalog option (enter a number): 2
6. schema (default schema that dbt will build objects in): wizard
7. threads (1 or more) [1]: 2

```

Don’t run `dbt debug` this will fail as you don’t have (or need) the required credentials.

With this configuration saved, run `dbt deps` to install dependencies.

Here’s what this should roughly look like for you:

![type:video](https://drive.google.com/file/d/1V0SARSZ4RmjuroX0ysmFgDf7w7ImaYBT/preview)

Finally, run `dbt compile`.

If that runs correctly your terminal should end with “done” and you should see the “target” folder in your sidebar

![target folder success](images/target-folder-success.jpg)

Lastly, run `git checkout -b workshop` to create a new, locally stored branch called “workshop” for doing the practice work in this guide.

Finally, run `git push -u origin workshop` to add or “push” your local “workshop” branch to your remote GitHub repository so we can eventually make our Spellbook pull request.