# 📙 Identify the required raw and decoded tables (henceforth sources) needed.

[ERC-20 ](https://ethereum.org/en/developers/docs/standards/tokens/erc-20/)tokens are fungible tokens that all follow a contract standard set by the Ethereum Foundation. To track daily balances, we need to first identify the transfers.

The main base Dune table we’ll use for this purpose is `erc20_ethereum.evt_Transfer` which you can find via the data explorer.a

![type:video](https://www.loom.com/embed/198148674ded4f5e944f65452852482b)

Then, in the Spellbook project, the source must be defined in a YAML file. We define this source in [base\_sources/ethereum\_base\_sources.yml.](https://github.com/duneanalytics/abstractions/blob/master/spellbook/models/base\_sources/ethereum\_base\_sources.yml) Once a source has been defined it does not need to be defined again.

Defining a source can be as simple as adding its schema and name. But to harness the full power of the tool, we’ll also want to define tests, freshness checks, and add column descriptions.

Define the table name and description under the schema.

```yaml
 sources:
  - name: erc20_ethereum
    description: "Transfers events for ERC20 tokens."
    tables:
      - name: evt_transfer
```

Add a freshness check. Freshness checks use a timestamp type field to validate when the last rows of data were loaded. Here we’ll use `evt_block_time` and use the DBT default warning and error checks.

```yaml
sources:
  - name: erc20_ethereum
    description: "Transfers events for ERC20 tokens."
    tables:
      - name: evt_transfer
        loaded_at_field: evt_block_time
        description: "Transfers events for ERC20 tokens."
        freshness:
          warn_after: { count: 12, period: hour }
          error_after: { count: 24, period: hour }
```

Add column descriptions and tests. Regarding tests, generally, you’ll want to make the primary key both unique and non\_null.

You can use an ampersand anchor `&` before a column name to reuse its description later in the same YAML file.

`*`column name will reuse the column description defined earlier.

```yaml
sources:
  - name: erc20_ethereum
    description: "Transfers events for ERC20 tokens."
    tables:
      - name: evt_transfer
        loaded_at_field: evt_block_time
        description: "Transfers events for ERC20 tokens."
        freshness:
          warn_after: { count: 12, period: hour }
          error_after: { count: 24, period: hour }
        columns:
        - name: contract_address
          description: "ERC20 token contract address"       
        - &evt_tx_hash
          name: evt_tx_hash
          description: "Transaction hash of the event"
        - &evt_index
          name: evt_index
          description: "Event index"   
        - &evt_block_time
          name: evt_block_time
          description: "Timestamp for block event time in UTC"
        - &evt_block_number
          name: evt_block_number
          description: "Event block number"  
        - *from
        - *to
        - name: value
          description: "Amount of ERC20 token transferred" 
```

These descriptions are rendered in the docs by dbt. Locally, you can open them by running `dbt docs generate` and `dbt docs serve` from your CLI in the spellbook directory. Soon they will be hosted on dune.com for all wizards to use.

![dbt documentation page](https://lh6.googleusercontent.com/vr9DleUs\_HcdzMZ6mWq81l-IRq1C\_utHCVB5WddOHy9Z1\_fSyz8GcB8Cyj877nKNHsXLh3K3-owFssNIl4ZaJS27clEeBppHBi8DlNjzVKGeGZdF\_AE8VxRj0pziR-2jGTA-MED7OtTq3GhuwQM)
