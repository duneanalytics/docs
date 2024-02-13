# Varchar Utility Functions

Dune SQL offers a series of functions designed to ease some common tasks when working with varchar data.

#### left()
**``left(varchar, bigint)``** → varchar

This function returns the leftmost `x` characters from a string, if `x` is less than or equal to 0 the result is an empty string. The first argument is the original string, and the second argument is `x`, the length of the resulting string.

```sql
SELECT 
    "left"('123456', 2)
```
will return `12`

#### right()
**``right(varchar, bigint)``** → varchar

This function returns the rightmost `x` characters from a string, if `x` is less than or equal to 0 the result is an empty string. The first argument is the original string, and the second argument is `x`, the length of the resulting string.

```sql
SELECT 
    "right"('123456', 2)
```
will return `56`

#### initcap()
**``initcap(varchar)``** → varchar

This function returns a string with the first letter of each word in uppercase and all other letters in lowercase. Words are delimited by white space or characters that are not alphanumeric. The only argument is the original string.

```sql
SELECT 
    "initcap"('hellO woRld')
```
will return `Hello World`

#### address_32_from_hex()
**``address_32_from_hex(varchar)``** → varbinary

This function converts a hexadecimal-formatted input string to varbinary, always producing an output of 32 bytes in length by left-padding with the 0x00 byte. The input string needs to be hexadecimal formatted, allowing characters from `[a-fA-F0-9]`; otherwise, an error is returned. While the input can be prefixed with '0x', this is not mandatory. The function accommodates the hexadecimal representation of any decimal number, provided it fits within 32 bytes.

This function proves useful in scenarios where addresses in the Aptos chain are utilized. In the Aptos chain, addresses serve as 32-byte identifiers for accounts or objects. All addresses in Aptos chain are represented as just that, using a 32-byte varbinary. However, it's quite common to represent addresses in their short-formed representation, having leading zeros trimmed. For example, a valid aptos account can have a 0x1 address. Additionally, it's typical to encounter the short format without the '0x' prefix. Therefore, this function serves to transform a short-form address into the internal representation format used for addresses
```sql
-- The following query will return: true, true, true
SELECT
    address_32_from_hex('0x1') = address_32_from_hex('0x01'),
    address_32_from_hex('0x1') = address_32_from_hex('1'),
    address_32_from_hex('0x1') = 0x0000000000000000000000000000000000000000000000000000000000000001
```

In the aptos context, we can use the function to find transactions with the entry function address being 0x1.
```sql
SELECT * FROM aptos.user_transactions WHERE entry_function_module_address = address_32_from_hex('0x1') LIMIT 10
```