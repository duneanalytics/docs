---
title: URL functions
---

## Extraction functions

The URL extraction functions extract components from HTTP URLs (or any
valid URIs conforming to `2396`{.interpreted-text role="rfc"}). The
following syntax is supported:

``` text
[protocol:][//host[:port]][path][?query][#fragment]
```

The extracted components do not contain URI syntax separators such as
`:` or `?`.

#### url_extract_fragment()
**url_extract_fragment(url)** → varchar

Returns the fragment identifier from `url`.

#### url_extract_host()
**url_extract_host(url)** → varchar

Returns the host from `url`.

#### url_extract_parameter()
**url_extract_parameter(url, name)** → varchar

Returns the value of the f query string parameter named `name` from `url`. Parameter extraction is handled in the typical manner as specified by RFC 1866#section-8.2.1.

#### url_extract_path()
**url_extract_path(url)** → varchar

Returns the path from `url`.

#### url_extract_port()
**url_extract_port(url)** → bigint

Returns the port number from `url`.

#### url_extract_protocol()
**url_extract_protocol(url)** → varchar

Returns the protocol from `url`.

#### url_extract_query()
**url_extract_query(url)** → varchar

Returns the query string from `url`.

## Encoding functions

#### url_encode()
**url_encode(value)** → varchar

Escapes `value` by encoding it so that it can be safely included in URL query parameter names and values.

#### url_decode()
**url_decode(value)** → varchar

Unescapes the URL encoded `value`. This function is the inverse of `url_encode`.
