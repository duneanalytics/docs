[View code on GitHub](https://dune.com/blob/master/app\queries\parameters.md)

# Parameters

This technical guide covers the use of parameters in the Dune app. Parameters are a feature that allows users to implement variables in certain parts of their Query code. This variable can be changed from dashboards, making it possible to create an interactive dashboard. 

The guide explains how parameters work, how to use them, and provides an example Query and several example dashboards. Parameters are defined in the Query code as `{{parametername}}` and will appear below the Query and in any dashboards in which a Query Visualization with parameters is used in. 

The guide explains how to add a parameter to a Query by writing `{{parametername}}` or using the button below the Query. Users can edit the properties of single parameters by clicking on the gear wheel next to the parameter in the Query editor. This allows users to set a default value, define a list of possible parameters, or change the type of the parameter. 

The guide provides an example Query that returns the running total of Gas Paid in USD. The Query Author has chosen to include a parameter for `wallet address`, `start date`, and `end date`. The guide also provides several example dashboards that use parameters. These dashboards allow users to find interesting stats on Ethereum wallets, drill down into the single pools of Barnbridge's Smart Yield Product, find out how many people are participating in Yearn Vaults, and find out how their investment in $KLIMA is doing. 

In summary, parameters allow users to make a certain part of their SQL query dynamic and thereby offer them to make Queries and dashboards interactive. That way, users can easily display detailed data on their dashboard since it allows the viewer to customize the dashboard for their needs. Parameters are like filters, but the possibilities of using this feature go beyond that.
## Questions: 
 1. What is the syntax for defining parameters in the Query code?
   
   Parameters are defined in the Query code as `{{parametername}}`.

2. How can parameters be shared between different Queries in a dashboard?
   
   Parameters in a Dashboard can be shared between different Queries, just make sure to use the same name, type and default value between all of them.

3. What is the purpose of using parameters in a Query or dashboard?
   
   Parameters allow you to make a certain part of your SQL query dynamic and thereby offer you to make Queries and dashboards interactive. That way you can easily display detailed data on your dashboard since it allows the viewer to customize the dashboard for his needs.