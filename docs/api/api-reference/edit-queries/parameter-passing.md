---
title: Note on parameters
description: Here's how to pass in parameters while using CRUD API
---

!!! warning "Docs Migration"
    Our API docs have moved to [here](https://dune.mintlify.app/api-reference/overview/introduction), this reference page will be deprecated soon.

The parameters have to be passed in a specific format laid out here:  

- The `type` field can be one of `number`, `text`, `datetime`, `enum` 
- The `key` and `type` fields are always mandatory, while the `value` and `enumOptions` fields can be omitted for some types. 
- The `value` represents the default value used by this parameter during execution and should *always* be passed in as a JSON string.

Here are details about the four different type options:

1. `number` - numeric parameters, value is mandatory and must be a number wrapped in `“`
2. `text` - string parameters, including hex 0x-prefixed values. `value` can be empty and will use an empty string by default in that case
3. `datetime` - date and time parameters. `value` must be provided in the following format `YYYY-MM-DD hh:mm:ss`
4. `enum` - used when there’s a specific list of values that can be provided to the parameter. The `enumOptions` field is used only for this type and is mandatory. It must be a JSON list of strings that represent all the valid options for the enumeration. The value field is also mandatory and must be one of the values provided in the `enumOptions`


## Example parameters with different types

```js

[
	{
    	"key": "block_time_start",
    	"type": "datetime",
    	"value": "2017-01-01 00:00:00"
	},
	{
    	"key": "from",
    	"type": "text",
    	"value": "0xae2fc483527b8ef99eb5d9b44875f005ba1fae13"
	},
	{
    	"key": "limit",
    	"type": "number",
    	"value": "20"
	},
	{
    	"key": "type",
    	"type": "enum",
    	"value": "DynamicFee",
    	"enumOptions": [
        	"DynamicFee",
        	"Legacy"
    	]
	}
]

```
