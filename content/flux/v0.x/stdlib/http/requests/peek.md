---
title: requests.peek() function
description: >
  `requests.peek()` converts an HTTP response into a table for easy inspection.
menu:
  flux_0_x_ref:
    name: requests.peek
    parent: http/requests
    identifier: http/requests/peek
weight: 201
---

<!------------------------------------------------------------------------------

IMPORTANT: This page was generated from comments in the Flux source code. Any
edits made directly to this page will be overwritten the next time the
documentation is generated. 

To make updates to this documentation, update the function comments above the
function definition in the Flux source code:

https://github.com/influxdata/flux/blob/master/stdlib/http/requests/requests.flux#L307-L317

Contributing to Flux: https://github.com/influxdata/flux#contributing
Fluxdoc syntax: https://github.com/influxdata/flux/blob/master/docs/fluxdoc.md

------------------------------------------------------------------------------->

`requests.peek()` converts an HTTP response into a table for easy inspection.

The output table includes the following columns:
 - **body** with the response body as a string
 - **statusCode** with the returned status code as an integer
 - **headers** with a string representation of the headers
 - **duration** the duration of the request as a number of nanoseconds

To customize how the response data is structured in a table, use `array.from()`
with a function like `json.parse()`. Parse the response body into a set of values
and then use `array.from()` to construct a table from those values.

##### Function type signature

```js
(
    response: {A with statusCode: E, headers: D, duration: C, body: B},
) => stream[{statusCode: E, headers: string, duration: int, body: string}]
```

{{% caption %}}For more information, see [Function type signatures](/flux/v0.x/function-type-signatures/).{{% /caption %}}

## Parameters

### response
({{< req >}})
Response data from an HTTP request.




## Examples

### Inspect the response of an HTTP request

```js
import "http/requests"

requests.peek(response: requests.get(url: "https://api.agify.io", params: ["name": ["natalie"]]))

```

{{< expand-wrapper >}}
{{% expand "View example output" %}}

#### Output data

| body                                      | duration  | headers                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   | statusCode  |
| ----------------------------------------- | --------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------- |
| {"name":"natalie","age":34,"count":20959} | 100000000 | [
    Access-Control-Allow-Headers: Content-Type, X-Genderize-Source, 
    Access-Control-Allow-Methods: GET, 
    Access-Control-Allow-Origin: *, 
    Connection: keep-alive, 
    Content-Length: 41, 
    Content-Type: application/json; charset=utf-8, 
    Date: Wed, 29 Jun 2022 20:19:40 GMT, 
    Etag: W/"29-klDahUESBLxHyQ7NiaetCn2CvCI", 
    Server: nginx/1.16.1, 
    X-Rate-Limit-Limit: 1000, 
    X-Rate-Limit-Remaining: 996, 
    X-Rate-Reset: 13219
]                           | 200         |

{{% /expand %}}
{{< /expand-wrapper >}}