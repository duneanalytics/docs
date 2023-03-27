[View code on GitHub](https://dune.com/blob/master/data tables\spellbook\top tables\labels.md)

The Labels technical guide is a documentation for the Address Labels feature on Dune. The guide explains what labels are, how to add them, and how to use them. Labels are metadata about an address, in the form of a key-value pair, where the key is the label type and the value is the label name. The Labels feature allows users to add, update, and query labels for any address. 

The guide provides examples of what can be created with labels, such as labeling all addresses that used a certain dapp, all addresses that hold a certain amount of a token, or all addresses that use a dapp more than X times per month. Users can also come up with their own label types and names, as labels on Dune are open-ended and crowd-sourced. 

The Labels table stores labels in the `labels.labels` table, which has a schema that includes columns such as `id`, `address`, `name`, `blockchain`, `author`, `source`, `updated_at`, `label_type`, and `model_name`. 

The guide also provides a warning that the Using Labels section is currently under construction. 

Overall, the Labels technical guide provides a comprehensive explanation of the Address Labels feature on Dune, including what labels are, how to add them, and how to use them. It also provides examples of what can be done with labels and information on how labels are stored in the Labels table.
## Questions: 
 1. What is the purpose of the labels.labels table and what data is stored in it?
   
   The labels.labels table stores metadata about labeled addresses, including the label name, type, author, source, and last update time, as well as the address and blockchain it describes. It also includes the label model name.

2. How are labels added to addresses and what are some examples of labels that can be added?
   
   Labels can be added to addresses using Dune queries, which can be used to label addresses based on various criteria such as dapp usage, token holdings, and transaction history. Examples of labels that can be added include addresses that used a certain dapp, hold a certain amount of a token, or sent money to a specific address.

3. Are there any limitations or delays when querying labels in SQL on dune.com?
   
   There might be a few minutes delay from adding the label on dune.com until it can be queried in SQL.