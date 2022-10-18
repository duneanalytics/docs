## Abstractions (V1)

You can check for existing abstractions in our [public github repository](https://github.com/duneanalytics/spellbook/index.md), under `deprecated-dune-v1-abstractions`.

You can generally divide them into 2 distinct categories:

### Sector Abstractions

Sector Abstractions are tables like dex.trades, erc20.stablecoins, lending.borrow etc.

These abstractions take in data from multiple contracts and projects, standardize the data across them and therefore make it very easy to query for this data and compare the metrics of different projects with each other.

Most of the [sector](../../../getting-started/use-cases/sector-dashboards.md) Dashboards depend on sector abstractions. This introduces an interesting dynamic in which projects can easily get their data into these dashboards by making a pull request to our public [github repo](https://github.com/duneanalytics/spellbook/index.md).

Team Dune and the community are always improving on these sector abstractions, all new additions to existing ones are always welcome.

### Project Abstractions

Projects can assemble their data into one neat table that has all the data they need in one place. To do this, you can construct views or tables in our abstractions.

The main advantage here over just constructing a view is that you are able to deal with bigger amounts of data in our abstractions since we can run them automatically in the background every few hours.

## Contributing to abstractions

Our abstractions for v1 are no longer open for contributions.

If you'd like to contribute to Dune abstractions, take a look at [Spellbook](../../../spellbook/index.md).