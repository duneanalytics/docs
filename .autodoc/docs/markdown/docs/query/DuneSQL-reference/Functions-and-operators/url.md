[View code on GitHub](https://dune.com/docs/query/DuneSQL-reference/Functions-and-operators/url.md)

# URL Functions

This technical guide is focused on the URL functions in the Dune Docs project. The URL extraction functions extract components from HTTP URLs or any valid URIs conforming to `2396`. The syntax supported includes `[protocol:][//host[:port]][path][?query][#fragment]`. The extracted components do not contain URI syntax separators such as `:` or `?`.

## Extraction Functions

The following are the extraction functions available in the Dune Docs project:

### url_extract_fragment()

**`url_extract_fragment(url)`** → varchar

This function returns the fragment identifier from `url`.

### url_extract_host()

**`url_extract_host(url)`** → varchar

This function returns the host from `url`.

### url_extract_parameter()

**`url_extract_parameter(url, name)`** → varchar

This function returns the value of the f query string parameter named `name` from `url`. Parameter extraction is handled in the typical manner as specified by RFC 1866#section-8.2.1.

### url_extract_path()

**`url_extract_path(url)`** → varchar

This function returns the path from `url`.

### url_extract_port()

**`url_extract_port(url)`** → bigint

This function returns the port number from `url`.

### url_extract_protocol()

**`url_extract_protocol(url)`** → varchar

This function returns the protocol from `url`.

### url_extract_query()

**`url_extract_query(url)`** → varchar

This function returns the query string from `url`.

## Encoding Functions

The following are the encoding functions available in the Dune Docs project:

### url_encode()

**`url_encode(value)`** → varchar

This function escapes `value` by encoding it so that it can be safely included in URL query parameter names and values.

### url_decode()

**`url_decode(value)`** → varchar

This function unescapes the URL encoded `value`. This function is the inverse of `url_encode`.

The guide provides a clear explanation of the URL functions available in the Dune Docs project. The extraction functions extract components from HTTP URLs or any valid URIs conforming to `2396`. The encoding functions escape and unescape URL encoded values. The guide also provides examples of how to use each function.
## Questions: 
 1. What is the purpose of the dune docs app and how does it relate to blockchain technology?
- The app technical guide does not provide information on the purpose of the dune docs app or its relation to blockchain technology.

2. Are there any security measures in place for the URL encoding and decoding functions?
- The app technical guide does not mention any security measures for the URL encoding and decoding functions.

3. Can the URL extraction functions be used to extract components from blockchain transactions or blocks?
- The app technical guide does not provide information on whether the URL extraction functions can be used to extract components from blockchain transactions or blocks.