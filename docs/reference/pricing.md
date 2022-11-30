---
title: Pricing
description: Dune Premium accounts let you access a host of additional features, learn more on our Pricing page!
---

![dune pricing plans](images/dune-pricing-plans.png)

Whether you're a basement degen or Blackrock VP, Dune has you covered with our Premium plans!

Dune Premium accounts let you access a host of additional features including:

- Private Queries and Dashboards
- CSV Exports
- [Up to 64x faster executions](#whats-the-performance-difference-between-tiers)
- No Dune watermarks
- Processing for up to 6 Queries at once

[Learn more and get started on our Pricing page](https://dune.com/pricing)!

!!! note
    Premium Team and API plans coming soon, stay tuned! 📺

## FAQ

### General Questions

#### Where can I see my billing history?

To view your billing history, follow these steps:

- [Sign in to your Dune account](https://dune.com/auth/login)
- Click your avatar in the top right corner
- Click “Settings” then “Subscription”

Your billing history can be found under “Billing”.

#### How do I upgrade, downgrade, or cancel my subscription?

Individuals with paid plans or [Team](../getting-started/teams.md) admins can upgrade, downgrade, or cancel subscriptions.

To upgrade or downgrade, follow these steps:

- [Sign in to your Dune account](https://dune.com/auth/login)
- Click your avatar in the top right corner
- Click “Settings” then “Subscription”
- Select the plan you want to up- or downgrade to

To cancel your subscription, follow these steps:

- [Sign in to your Dune account](https://dune.com/auth/login)
- Click “Settings” then “Subscription”
- Select the Community plan

Your current subscription will remain active for a full 30 days after your last payment.

E.g. if you decide to cancel 15 days after your last payment, your current plan will remain active for an additional 15 days.

#### How does billing work when I upgrade or downgrade?

Upgrading immediately resets your billing cycle to the day you upgrade. You'll be charged the full price for your new plan and be refunded pro rata for the unused days of your current plan.

Downgrades are applied at the end of your billing cycle, so you'll keep your current tier benefits until the end of your current cycle.

#### Which query engine will I be billed on?

Queries and CSV downloads on both Dune Engine V2 and other datasets will be billed.

#### What if I have more questions?
For any questions or issues regarding premium plans, please ask in our [#paid-plans Discord channel](https://discord.com/channels/757637422384283659/1041694148530548776) or email us at [support@dune.com](mailto:support@dune.com).

### Query Execution

#### Which query engine do the performance tiers support?

The performance tiers are only supported on Dune Engine V2 as we are phasing out our V1 datasets. Until then, you will still be billed for any query executions or CSV downloads using other datasets.

#### What's the performance difference between tiers?

Roughly speaking, each tier has 2-4x the amount of computational power of the previous tier. This will be more or less noticeable depending on query complexity and cluster load at any point in time.

Overall, the higher the tier, the faster your queries will run!

#### When does the rate for additional executions kick in?

When your monthly execution quota drops to 0, additional queries will be charged at your plan's Additional Execution rate and charged the next time you're billed.

#### Can I limit premium Query usage when I've reached my limit to avoid paying extra fees?

You can limit premium Query usage once you reach your monthly limit!

[Head to Settings -> Subscription](https://dune.com/settings/subscription) while logged in and turn on the "Limit extra query executions" toggle.

When turned on, extra query executions will run on the Community tier and you will not be charged additional fees.

![limit extra query executions toggle](images/limit-extra-query-executions-toggle.png)

### Features

#### What if I add a private query to a public dashboard?

Other Dune users will be able to see the Visualization in the public dashboard, but won't see anything when they click the query. The results table, other Visualizations you might have, and the underlying query, all remain private.

#### Can I embed private queries on other websites?

Yes! Anyone visiting a website with your Dune embed [can see the Visualization you chose](../getting-started/embeds.md) and nothing else.

#### As an Elite user, what will happen to watermarks?

When logged in, you will never see watermarks, and chart embeds you’ve created won’t have watermarks.

However, public Dashboards URLs will always be watermarked.