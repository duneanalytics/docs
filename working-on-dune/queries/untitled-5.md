# Filter query by an address in the interface

###  <a id="Filter-query-by-an-address-in-the-interface"></a>

If you use `{{}}` in a query an input field in the UI will appear and anyone looking at the query can easily input info in that field that will go into the query.

This is very useful when filtering for custom atributes like an Ethereum address or a token address.

When you query in Dune you use `\x...` while people commonly use `0x...` \(see more details [here](https://hackmd.io/k71ZUSTxQVKGqOcvR6OXnw?view#Using-Inline-Ethereum-addresses)\).

Using the below snippet will allow users to past addresses in the regular `0x...` format and then convert it to `\x...` that will work in a query.

```sql
WHERE contract_address = CONCAT('\x', substring('{{Address}}' from 3))::bytea
```

[Here’s](https://explore.duneanalytics.com/queries/10505/source?p_Address=0x37236cd05b34cc79d3715af2383e96dd7443dcf1#20880) an example of this being applied in a query.

