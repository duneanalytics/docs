---
title: 2. 🤔 Decide on a Spell to Cast 
description: Next, you’ll need to decide on a Spell to cast.
---

Next, you’ll need to decide on a Spell to cast.

There are a few ways to do this:

1. You might already have an idea if you’ve used Dune enough to know where you’ve wanted more abstract data than you’ve been able to find.
2. [You can also take a look at our Spellbook bounties in Dework](https://app.dework.xyz/dune/spellbook-86233/overview).
3. Feel free to ask in our [#spellbook Discord channel](https://discord.com/channels/757637422384283659/999683200563564655) to see what people need help with/suggest you work on!

For this guide, we’re going to make a migration Spell - translating the Keep3r network `view_job_log` abstraction from Dune’s v1 database into a V2 Spell.

Inside VSCode, find the “deprecated-dune-v1-abstractions” folder then dig down to find the “view_job_log.sql” file.

!!! note
    [Dune V1 Abstractions have been moved to this repository](https://github.com/duneanalytics/dune-v1-abstractions), which you'll now need to clone in order to access the code for migrating a V1 Abstraction to a Spell.

This should be the full path: 

`[folder you cloned spellbook to]/deprecated-dune-v1-abstractions/ethereum/keep3r_network/view_job_log.sql`

![keep34 v1 abstraction location](images/keep3r-v1-abstraction-location.jpg)

Now we’re ready to set up the file structure for our Spell’s SQL schema and source files.