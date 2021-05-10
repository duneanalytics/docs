---
description: >-
  The Schema dune_user_generated is an easy way to construct your own view,
  function or table inside of our database.
---

# User Generated

## Usecases

There is several ways in which you can utilize your own views and tables inside of Dune to make working with your data on Dune even easier.  
Your own tables, views and function all have an important part to play in creating content on Dune and make maintenance of your dashboards and queries easier if used correctly.

If you are unfamiliar with tables, views, materialized views and functions please consult the [pgSQL documentation](https://www.postgresqltutorial.com/postgresql-views/) or check out our [Tutorials](../../about/tutorials/).

### Storing Information

Sometimes certain references or information that you do need for your data extraction are not properly stored in available tables or stored in many different tables, which would makes the query quite hard to work with. In these cases, you are best off storing the necessary information in a view and referencing that view.

An example of this would be the mapping of certain vault or lending tokens to their respective underlying tokens.

```sql
CREATE OR REPLACE VIEW dune_user_generated.view_test (symbol, contract_address, decimals, underlying_token_address) AS VALUES
('iETH'::text, '\x9Dde7cdd09dbed542fC422d18d89A589fA9fD4C0'::bytea, 18::numeric, '\xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2'::bytea),
('yDAI'::text, '\x9D25057e62939D3408406975aD75Ffe834DA4cDd'::bytea, 18::numeric, '\x6B175474E89094C44Da98b954EedeAC495271d0F'::bytea),
('yUSDC'::text, '\xa2609b2b43ac0f5ebe27deb944d2a399c201e3da'::bytea, 6::numeric, '\xA0b86991c6218b36c1d19D4a2e9Eb0cE3606eB48'::bytea),
('ySUSD'::text, '\x36324b8168f960A12a8fD01406C9C78143d41380'::bytea, 18::numeric, '\x57Ab1ec28D129707052df4dF418D58a2D46d5f51'::bytea),
('yUSDT'::text,'\xa1787206d5b1bE0f432C4c4f96Dc4D1257A1Dd14'::bytea, 6::numeric, '\xdAC17F958D2ee523a2206206994597C13D831ec7'::bytea),
('yCRV'::text,'\x9Ce551A9D2B1A4Ec0cc6eB0E0CC12977F6ED306C'::bytea, 18::numeric, '\x6B175474E89094C44Da98b954EedeAC495271d0F'::bytea),
('yBTC'::text, '\x04EF8121aD039ff41d10029c91EA1694432514e9'::bytea, 8::numeric, '\x2260FAC5E5542a773Aa44fBCfeDf7C193bc2C599'::bytea)
```

This table generates a view that you can use to join on your query.

[Look at the table](https://duneanalytics.com/queries/41577).

### Aggregating Data

Views can also be used to aggregate the actions of multiple smart contracts into one view that contains all the necessary data.

This is especially useful if you are working with the same dataset over and over and only change the way you display or aggregate the data. That way, instead of having to query for your dataset again and again, you just put it into a view once and then can start referencing that view.   
This will allow you to change the base query that constructs your dataset without having to go through multiple different instances of your query. Think about it like splitting your data collection and the actual work/display you do with that data into two different parts that function independently of each other. 

Utilizing this will make the maintenance of your dashboards much easier since you can just change the **dune\_user\_generated** view instead of having to go through all queries individually.

A great example of this in action is almost all queries on [this dashboard](https://duneanalytics.com/keeganead/cryptoart_1). The Creator made one base dataset in the **dune\_user\_generated** schema and uses that to base all of his queries on.



Please do note that while this approach works for most cases, views can get very computationally expensive and you might be better off constructing a materialized view or table in our [abstractions](abstractions.md).

### Testing Abstractions

Another great usecase of utilizing the "create" function is to test out if the Pull Request you are making to our abstractions github actually produce the intended results. Simply try running the query with the schema **dune\_user\_generated** instead of the actual schema that you want in Github.

If the test succeeds, you can proceed in making the Pull Request. If you can please attach the "Test Table/View" into the Pull Request.

