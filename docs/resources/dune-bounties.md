---
title: Dune Bounties
---

# Wizard Request Program

Over the past 3 years, Dune has become the go-to solution for on-demand crypto analytics. 
How many Holders does BAYC have? Wanna do some whale watching? How is the UST depeg going? How many users are using Uniswap V3 in a day?

Dune has it all and can do it all, but there is still lots of things that are left unexplored. Dune only works because of the countless Wizards out there who surface this data for the greater space. Many of the dashboards and queries you see on Dune today were made out of sheer curiosity and enjoyment, but fundamentally, Wizards should and want to be paid.  
Wizards will work for clout, carrots and stars, but they also do like money.

![type:video](https://www.youtube.com/embed/MRfC9cqAUKw)

## The problem

Projects need data, Wizards want jobs. It's hard for one to find the other. Tasks are spread out between Twitter, Discord, Gitcoin, Layer3, Notion boards and a few other places. 

It's hard for **Wizards** to keep track of all these places and creates unncessary friction in the application and work process. 

For **Projects** on the other hand, it makes it exceedingly hard to find the right Wizard for the job and also introduces unnecessary friciton and overhead.

Fundamentally, what solves this problem is the emergence of one marketplace which helps the data flow.
This one solution should be able to handle task creation, the application process, communication, reputation, payments and additionally be web3 native.

Thankfully, such solutions exist!

## The solution

Going forward, we will leverage [dework.xyz](https://www.dework.xyz) to manage and operate our bounty program. Additionally, we encourage other organisation to make use of the same infrastrucutre, so that the data can flow more efficiently. 
Dework describes itself as a “web3 native trello with payments and credentialing". What that exactly means, you can find out from Lonis, co-founder of Dework, in this video:

![type:video](https://www.youtube.com/embed/hyOLRGurjDc)

Dework offers infrastructure for us to write out tasks on our own [board](https://app.dework.xyz/dune/board) and allows other organisations to seamlessly connect with Dune Wizards by simply specifying “Dune Analytics” as Skill.   
All open tasks that have the Dune Analytics Skill attached will appear in the [Dune hub](https://app.dework.xyz/hubs/dune), allowing for tasks to be easily found by our Wizard Community.

## Some notes about working on Dune

Dune can rougly be seperated into two parts: the **app layer** and the **data layer**. 

In the **app layer**, you can find queries, visualisations and dashboards. Everything in the App Layer is public by default and can be utilized by other Wizards, but the work produced in the app layer is not very persistent and most importantly doesn't easily allow other analysts to build on top of this work.

The **data Layer** of Dune allows you to produce scaleable and persistent work. DuneÄs data layer is called [Spellbook](https://dune.com/docs/spellbook/) and allows wizards to standardize and normalize data.  

A good example of ultilizing the **data layer** is Opensea standardizing and normalizing [all trades across all chains](https://dune.com/spellbook#!/model/model.spellbook.opensea_trades) and versions into the `opensea.trades` table. In this way, 2 things can happen:

1) all Wizards on Dune can easily work with Opensea's data as the data is already cleaned and standardized
2) The data can furthermore be used in the `nft.trades` table in Dune's data layer, further making it easier for analysts to work with NFT data at large. The `nft.trades` table contains data from all marketplaces across all chains.

There really isn't an optimal way to work on Dune since many ways can lead you to your desired results, but in principle, getting your data normalized, standardized and possibly inserted into one of our sector level tables like `nft.trades` is a good starting point. Once that is done, people working in the **App layer** will have a much easier time building good queries, visualizations and dashboards since the hardest data engineering parts are already taken care of.  
If this all sounds confusing to you, don't worry we can advise you in this process!

**TL;DR**
We suggest to do things in this order so the data flows efficiently:

1. Build Spells in Data Layer to take care of data engineering
2. Build cool stuff in App Layer to surface findings

## For projects looking for Wizards

**If you are an organisation in need of web3 analytics, it’s now easier than ever before to connect with Dune Wizards!**





=== "Self Serve"

    1. **Create an organisation**

        If you don’t have a Dework organisation yet, the first step is creating one. For a basic setup, we recommend setting up at least a description, an icon and link to your socials so Wizards know who they are working with.
        
    2. **Define tasks**

        After completing the initial setup, you can start creating tasks for anything really, but in our case, we want to define tasks with the "Dune Analytics" Skill. Once you have created a task, the task will be 1) in your board and 2) in the Dune hub. From there on out, people can find your open task and apply.

    ![dework skills](images/dework-skills.jpeg)

    3.  **Choose an applicant**

        If you have defined a task that needs to be assigned to someone, you will get notifications within Dework and can vet the contributor using their work history, github profile and any other attached information on their profile. It is strongly recommended to spend some effort looking at the contributor to have a smooth bounty process.

    4.  **Review the work**

        Once the Wizard you have chosen has submitted their work for review, you can start reviewing the completed task. If it is satisfactory, you can mark the task as done and initiate the payment process.

    5.  **Pay your contributor**

        Dework integrates with Metamask, Gnosis Safes, Utopia Labs and even phantom wallet for Solana based payments. You can choose whatever works best for you here.


=== "Supported approach"

    1. **Create an organisation**

        If you don’t have a Dework organisation yet, the first step is creating one. For a basic setup, we recommend setting up at least a description, an icon and link to your socials so Wizards know who they are working with.
        
    2. **Define tasks**

        After completing the initial setup, you can reach out to the Dune team via this form provided 

    3.  **Choose an applicant**

        If you have defined a task that needs to be assigned to someone, you will get notifications within Dework and can vet the contributor using their work history, github profile and any other attached information on their profile. It is strongly recommended to spend some effort looking at the contributor to have a smooth bounty process.

    4.  **Review the work**

        Once the Wizard you have chosen has submitted their work for review, you can start reviewing the completed task. If it is satisfactory, you can mark the task as done and initiate the payment process.

    5.  **Pay your contributor**

        Dework integrates with Metamask, Gnosis Safes, Utopia Labs and even phantom wallet for Solana based payments. You can choose whatever works best for you here.

=== "bruv, help"

    Just reach out to us via this 

## For Wizards looking for :moneybag::moneybag::moneybag:

If you are a Wizard or an aspiring Wizard, join the Dune Analytics organisation on Dework and start looking for tasks on our [board](https://app.dework.xyz/dune/board) or on the [Dune hub](https://app.dework.xyz/hubs/dune). Joining our organisation is highly recommended so other organisation on Dework can see the roles we have assigned to you. Make sure to properly define your profile with relevant links to socials, github and dune profile so organisations trying to assess your skills can make sure to judge you properly.


## FAQs about the program

### I want to create a requests but I don’t know how much should I pay/offer for it

Well, that really depends on how much work/complexity your request entails but to the extent that you can, we encourage you to be generous. If you ain’t sure you can always ask on our Discord!

### Does Dune take a cut?

No we don’t. In fact, Dune does not take part in closing the deal or following up over time, this is strictly between the wizard and the project.


<div data-tf-widget="DtX4jqkd" data-tf-opacity="100" style="width:100%;height:100%;"></div><script src="//embed.typeform.com/next/embed.js"></script>
