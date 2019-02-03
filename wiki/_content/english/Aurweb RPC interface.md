Related articles

*   [Official repositories web interface](/index.php/Official_repositories_web_interface "Official repositories web interface")

The [Aurweb RPC interface](https://aur.archlinux.org/rpc.php) is a lightweight [RPC](https://en.wikipedia.org/wiki/Remote_procedure_call "wikipedia:Remote procedure call") interface for the [AUR](/index.php/AUR "AUR"). Queries are sent as HTTP GET requests and the server responds with [JSON](http://www.json.org/).

**Note:** This article describes v5 of the RPC Interface API, as updated with AUR v4.7.0 on July 7, 2018.

## Contents

*   [1 API usage](#API_usage)
    *   [1.1 Query types](#Query_types)
        *   [1.1.1 search](#search)
        *   [1.1.2 info](#info)
    *   [1.2 Return types](#Return_types)
        *   [1.2.1 error](#error)
        *   [1.2.2 search](#search_2)
        *   [1.2.3 info](#info_2)
    *   [1.3 jsonp](#jsonp)
*   [2 Limitations](#Limitations)
*   [3 Reference clients](#Reference_clients)

## API usage

### Query types

There are two query types:

*   search
*   info

#### search

Package searches can be performed by issuing requests of the form:

```
/rpc/?v=5&type=search&by=*field*&arg=*keywords*

```

where `*keywords*` is the search argument and `*field*` is one of the following values:

*   `name` (search by package name only)
*   `name-desc` (search by package name and description)
*   `maintainer` (search by package maintainer)
*   `depends` (search for packages that depend on keywords)
*   `makedepends` (search for packages that makedepend on keywords)
*   `optdepends` (search for packages that optdepend on keywords)
*   `checkdepends` (search for packages that checkdepend on keywords)

The `by` parameter can be skipped and defaults to `name-desc`. Possible return types are `search` and `error`.

If a maintainer search is performed and the search argument is left empty, a list of orphan packages is returned.

Examples:

Search for `foobar`:

```
https://aur.archlinux.org/rpc/?v=5&type=search&arg=foobar

```

Search for packages maintained by `john`:

```
https://aur.archlinux.org/rpc/?v=5&type=search&by=maintainer&arg=john

```

Search for packages that have `foobar` as `makedepends`:

```
https://aur.archlinux.org/rpc/?v=5&type=search&by=makedepends&arg=foobar

```

Search with callback:

```
https://aur.archlinux.org/rpc/?v=5&type=search&arg=foobar&callback=jsonp1192244621103

```

#### info

Package information can be performed by issuing requests of the form:

```
/rpc/?v=5&type=info&arg[]=*pkg1*&arg[]=*pkg2*&…

```

where `*pkg1*`, `*pkg2*`, … are the exact matches of names of packages to retrieve package details for.

Possible return types are `multiinfo` and `error`.

Examples:

Info for single `foobar` package:

```
https://aur.archlinux.org/rpc/?v=5&type=info&arg[]=foobar

```

Info for multiple `foobar` and `bar` packages:

```
https://aur.archlinux.org/rpc/?v=5&type=info&arg[]=foobar&arg[]=bar

```

### Return types

The return payload is of one format and currently has three main types. The response will always return a type so that the user can determine if the result of an operation was an error or not.

The format of the return payload is:

```
{"version":5,"type":*ReturnType*,"resultcount":0,"results":*ReturnData*}

```

`*ReturnType*` is a string, and the value is one of:

*   `search`
*   `multiinfo`
*   `error`

The type of `*ReturnData*` is an array of dictionary objects for the `search` and `multiinfo` `*ReturnType*`, and an empty array for `error` `*ReturnType*`.

#### error

The error type has an error response string as the return value. An error response can be returned from either a `search` or an `info` query type.

Example of `*ReturnType*` `error`:

```
{"version":5,"type":"error","resultcount":0,"results":[],"error":"Incorrect by field specified."}

```

#### search

The search type is the result returned from a search request operation. **The actual results of a search operation will be the same as an info request for each result. See the info section.**

Example of `*ReturnType*` `search`:

```
{"version":5,"type":"search","resultcount":2,"results":[{"ID":206807,"Name":"cower-git", ...}]}

```

#### info

The info type is the result returned from an info request operation.

Example of `*ReturnType*` `multiinfo`:

```
 {
    "version":5,
    "type":"multiinfo",
    "resultcount":1,
    "results":[{
        "ID":229417,
        "Name":"cower",
        "PackageBaseID":44921,
        "PackageBase":"cower",
        "Version":"14-2",
        "Description":"A simple AUR agent with a pretentious name",
        "URL":"http:\/\/github.com\/falconindy\/cower",
        "NumVotes":590,
        "Popularity":24.595536,
        "OutOfDate":null,
        "Maintainer":"falconindy",
        "FirstSubmitted":1293676237,
        "LastModified":1441804093,
        "URLPath":"\/cgit\/aur.git\/snapshot\/cower.tar.gz",
        "Depends":[
            "curl",
            "openssl",
            "pacman",
            "yajl"
        ],
        "MakeDepends":[
            "perl"
        ],
        "License":[
            "MIT"
        ],
        "Keywords":[]
    }]
 }

```

### jsonp

If you are working with a javascript page, and need a JSON callback mechanism, you can do it. You just need to provide an additional callback variable. This callback is usually handled via the javascript library, but here is an example.

Example Query:

```
https://aur.archlinux.org/rpc/?v=5&type=search&arg=foobar&callback=jsonp1192244621103

```

Example Result:

```
/**/jsonp1192244621103({"version":5,"type":"search","resultcount":1,"results":[{"ID":250608,"Name":"foobar2000","PackageBaseID":37068,"PackageBase":"foobar2000","Version":"1.3.9-1","Description":"An advanced freeware audio player (uses Wine).","URL":"http:\/\/www.foobar2000.org\/","NumVotes":39,"Popularity":0.425966,"OutOfDate":null,"Maintainer":"supermario","FirstSubmitted":1273255356,"LastModified":1448326415,"URLPath":"\/cgit\/aur.git\/snapshot\/foobar2000.tar.gz"}]})

```

This would automatically call the JavaScript function `jsonp1192244621103` with the parameter set to the results of the RPC call.

## Limitations

*   HTTP GET requests are limited to URI of 8190 bytes maximum length. However, the official AUR instance running on a nginx server with HTTP/2 uses the [default URI maximum length](https://nginx.org/en/docs/http/ngx_http_v2_module.html#http2_max_field_size) limit of 4443 bytes. Info requests with more than about 200 packages as an argument will need to be split.
*   The API rate is limited to a maximum of 4000 requests per day per IP.

## Reference clients

Sometimes things are easier to understand with examples. A few reference implementations (jQuery, python, ruby) are available at the following URL: [https://github.com/cactus/random/tree/2b72a1723bfc8ae64eed6a3c40cb154accae3974/aurjson_examples](https://github.com/cactus/random/tree/2b72a1723bfc8ae64eed6a3c40cb154accae3974/aurjson_examples)