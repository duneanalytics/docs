# Token standards

## Interfaces

When we’re interested in a subset of events logs fired regardless of the origin contract, Dune uses interface-decoding. Notable examples include `ERC20`, `ERC721` and `ERC1155` transfer events. This method is reserved for special cases. These tables make it easy to keep track of fungible and non fungible tokens flowing in and out of contracts and wallets and are widely used across Dune.

You can read more about the individual token standards and the tables here:

{% content-ref url="erc20.md" %}
[erc20.md](erc20.md)
{% endcontent-ref %}

{% content-ref url="erc721.md" %}
[erc721.md](erc721.md)
{% endcontent-ref %}

{% content-ref url="erc1155.md" %}
[erc1155.md](erc1155.md)
{% endcontent-ref %}
