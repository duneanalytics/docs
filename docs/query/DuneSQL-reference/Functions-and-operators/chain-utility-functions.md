# Chain Utility Functions

Dune SQL offers a series of functions designed for interacting with all the chains available on Dune.

#### get_chain_explorer(varchar)
**``get_chain_explorer(varchar)``** → varchar

This function returns the URL of the explorer for a specified chain (provided as a varchar).

#### all_evm_chains()
**``all_evm_chains()``** → array(varchar)

This function returns an array listing all the EVM chains available on Dune.

#### get_href(varchar, varchar)
**``get_href(varchar, varchar)``** → varchar

This function converts a link and associated text into a clickable hyperlink.

#### get_chain_explorer_address(varchar, varchar)
**``get_chain_explorer_address(varchar, varchar)``** → varchar

This function generates a URL for the explorer of a specified chain (provided as a varchar) for a given address (also provided as a varchar).

#### get_chain_explorer_address(varchar, varbinary)
**``get_chain_explorer_address(varchar, varbinary)``** → varchar

This function generates a URL for the explorer of a specified chain (provided as a varchar) for a given address (provided as a varbinary).

#### get_chain_explorer_tx_hash(varchar, varchar)
**``get_chain_explorer_tx_hash(varchar, varchar)``** → varchar

This function generates a URL for the explorer of a specified chain (provided as a varchar) for a given transaction hash (also provided as a varchar).

#### get_chain_explorer_tx_hash(varchar, varbinary)
**``get_chain_explorer_tx_hash(varchar, varbinary)``** → varchar

This function generates a URL for the explorer of a specified chain (provided as a varchar) for a given transaction hash (provided as a varbinary).
