The **AurJson** interface is a lightweight remote interface for the [AUR](/index.php/AUR "AUR"). It utilizes http GET queries as the request format, and [json](http://www.json.org/) as the response data exchange format.

## Contents

*   [1 API usage](#API_usage)
    *   [1.1 Query types](#Query_types)
        *   [1.1.1 search](#search)
        *   [1.1.2 msearch](#msearch)
        *   [1.1.3 info](#info)
        *   [1.1.4 multiinfo](#multiinfo)
    *   [1.2 Return types](#Return_types)
        *   [1.2.1 error](#error)
        *   [1.2.2 search](#search_2)
        *   [1.2.3 msearch](#msearch_2)
        *   [1.2.4 info](#info_2)
        *   [1.2.5 multiinfo](#multiinfo_2)
    *   [1.3 jsonp](#jsonp)
*   [2 More examples](#More_examples)
*   [3 Reference clients](#Reference_clients)
*   [4 Associated code](#Associated_code)

## API usage

The [RPC interface](https://aur.archlinux.org/rpc.php) has four major query types:

*   search
*   msearch
*   info
*   multiinfo

Each method requires the following HTTP GET syntax:

```
type=methodname&arg=data

```

Where _**methodname**_ is the name of an allowed method, and _**data**_ is the argument to the call.

Data is returned in json encapsulated format.

### Query types

As noted above, there are four query types:

*   search
*   msearch
*   info
*   multiinfo

#### search

A _**search**_ type query takes an argument of a string with which to perform a package search. Possible return types are _**error**_ and _**search**_.

Example:

```
https://aur.archlinux.org/rpc.php?type=search&arg=foobar

```

The above is a query of type _**search**_ and the search argument is "foobar".

#### msearch

A _**msearch**_ type query takes an argument of a string with which to perform a search by maintainer name. Possible return types are _**error**_ and _**msearch**_.

Example:

```
https://aur.archlinux.org/rpc.php?type=msearch&arg=cactus

```

The above is a query of type _**msearch**_ and the search argument is "cactus".

#### info

An _**info**_ type query takes an argument of a string _**or**_ an integer. If an integer, the integer must be an exact match to an existing packageID, or an _**error**_ type is returned. If a string, the string must be an exact match to an existing packageName, or an _**error**_ type is returned.

Examples:

```
https://aur.archlinux.org/rpc.php?type=info&arg=1123
https://aur.archlinux.org/rpc.php?type=info&arg=foobar

```

The two examples above are both queries of type _**info**_. The first query is using an integer type argument, and the second is using a packageName argument. If packageID 1123 corresponded to packageName foobar, then both of the above queries would return the details of the foobar package.

#### multiinfo

The majority of "real world" info requests come in hefty batches. AUR can handle these in one request rather than multiple by allowing AUR clients to send multiple arguments.

Examples:

```
https://aur.archlinux.org/rpc.php?type=multiinfo&arg[]=cups-xerox&arg[]=cups-mc2430dl&arg[]=10673

```

### Return types

The return payload is of one format, and currently has five main types. The response will always return a type so that the user can determine if the result of an operation was an error or not.

The format of the return payload is:

```
{"type":ReturnType,"results":ReturnData}

```

ReturnType is a string, and the value is one of:

```
* error
* search
* msearch
* info
* multiinfo

```

The type of ReturnData is dependent on the query type:

*   If ReturnType is _**error**_ then ReturnData is a string.
*   If ReturnType is _**search**_ then ReturnData is an array of dictionary objects.
*   If ReturnType is _**msearch**_ then ReturnData is an array of dictionary objects.
*   If ReturnType is _**info**_ then ReturnData is a single dictionary object.
*   If ReturnType is _**multiinfo**_ then ReturnData is an array of dictionary objects.

#### error

The error type has an error response string as the return value. An error response can be returned from either a _**search**_ or an _**info**_ query type.

Example of ReturnType _**error**_:

```
{"type":"error","results":"No results found"}

```

#### search

The search type is the result returned from a search request operation. **The actual results of a search operation will be the same as an info request for each result. See the info section.**

Example of ReturnType _**search**_:

```
{"type":"search","results":[{"Name":"pam_abl","ID":1995, ...}]}

```

#### msearch

The msearch type is the result returned from an msearch request operation. **The actual results of an msearch operation will be the same as an info request for each result. See the info section.**

Example of ReturnType _**msearch**_:

```
{"type":"msearch","results":[{"Name":"pam_abl","ID":1995, ...}]}

```

#### info

The info type is the result returned from an info request operation. Returning the type as search is useful for detecting whether the response to a search operation is search data or an error.

Example of ReturnType _**info**_:

```
 {
    "type": "info",
    "results": {
        "URL": "http://pam-abl.deksai.com/"
        "Description": "Automated blacklisting on repeated failed authentication attempts"
        "Version": "0.4.3-1"
        "Name": "pam_abl"
        "FirstSubmitted": 1125707839
        "License": "BSD GPL"
        "ID": 1995
        "OutOfDate": 0
        "LastModified": 1336659370
        "Maintainer": "redden0t8"
        "CategoryID": 16
        "URLPath": "/packages/pa/pam_abl/pam_abl.tar.gz"
        "NumVotes": 10
    }

 }

```

#### multiinfo

The multiinfo type is the result returned from a multiinfo request operation. **The actual results of a multiinfo operation will be the same as an info request for each result. See the info section.**

Example of ReturnType _**multiinfo**_:

```
{"type":"multiinfo","results":[{"Name":"pam_abl","ID":1995, ...}]}

```

### jsonp

If you are working with a javascript page, and need a json callback mechanism, you can do it. You just need to provide an additional callback variable. This callback is usually handled via the javascript library, but here is an example.

Example Query:

```
https://aur.archlinux.org/rpc.php?type=search&arg=foobar&callback=jsonp1192244621103

```

Example Result:

```
jsonp1192244621103({"type":"error","results":"No results found"})

```

This would automatically call the JavaScript function `jsonp1192244621103` with the parameter set to the results of the RPC call. (In this case, `{"type":"error","results":"No results found"}`)

## More examples

Example Query and Result:

```
 https://aur-url/rpc.php?type=search&arg=foobar
 {"type":"error","results":"No results found"}

```

Example Query and Result:

```
 https://aur-url/rpc.php?type=search&arg=pam_abl
 {"type":"search","results":[{"Name":"pam_abl","ID":1995}]}

```

Example Query and Result:

```
 https://aur-url/rpc.php?type=info&arg=pam_abl
 {
    "type": "info",
    "results": {       
        "Description": "Provides auto blacklisting of hosts and users responsible for repeated failed authentication attempts", 
        "ID": 1995, 
        "License": "", 
        "Name": "pam_abl", 
        "NumVotes": 4,
        "OutOfDate": 0,
        "URL": "http://www.hexten.net/pam_abl",
        "URLPath": "/packages/pam_abl/pam_abl.tar.gz",
        "Version": "0.2.3-1"
    }
 }

```

## Reference clients

Sometimes things are easier to understand with examples. A few reference implementations (jQuery, python, ruby) are available at the following url: [https://github.com/cactus/random/tree/master/aurjson_examples](https://github.com/cactus/random/tree/master/aurjson_examples)

## Associated code

*   The [python3-aur](https://aur.archlinux.org/packages/python3-aur/) package provides [python](/index.php/Python "Python") modules for interacting with the remote AUR JSON interface, among other AUR services. See [python3-aur](http://xyne.archlinux.ca/projects/python3-aur/) for details.
*   [jshon](https://www.archlinux.org/packages/?name=jshon) parses, reads and creates JSON from the command-line. See [jshon](http://kmkeen.com/jshon/) for details.