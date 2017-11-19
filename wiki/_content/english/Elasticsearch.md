From [Wikipedia:Elasticsearch](https://en.wikipedia.org/wiki/Elasticsearch "wikipedia:Elasticsearch"):

	*[Elasticsearch](https://www.elastic.co/products/elasticsearch) is a search engine based on [Lucene](http://lucene.apache.org/). It provides a distributed, multitenant-capable full-text search engine with an HTTP web interface and schema-free JSON documents. Elasticsearch is developed in Java and is released as open source under the terms of the Apache License.*

## Contents

*   [1 Installation](#Installation)
*   [2 Running](#Running)
*   [3 Configuration](#Configuration)
*   [4 Usage](#Usage)

## Installation

Elasticsearch requires at least OpenJDK 7, see [Java](/index.php/Java "Java").

[Install](/index.php/Install "Install") the [elasticsearch](https://www.archlinux.org/packages/?name=elasticsearch) package.

## Running

[Start/enable](/index.php/Start/enable "Start/enable") `elasticsearch.service`.

Ensure Elasticsearch is running and accessible by using [curl](https://www.archlinux.org/packages/?name=curl), `curl '<protocol>://<host>:<port>'`:

 `curl [http://127.0.0.1:9200](http://127.0.0.1:9200)` 
```
{
  "name" : "Sunder",
  "cluster_name" : "elasticsearch",
  "cluster_uuid" : "*cluster-uuid*",
  "version" : {
    "number" : "2.4.1",
    "build_hash" : "c67dc32e24162035d18d6fe1e952c4cbcbe79d16",
    "build_timestamp" : "2016-09-27T18:57:55Z",
    "build_snapshot" : false,
    "lucene_version" : "5.5.2"
  },
  "tagline" : "You Know, for Search"
}

```

## Configuration

The main Elasticsearch configuration file is well-documented and located at `/etc/elasticsearch/elasticsearch.yml`.

*   By default Elasticsearch is public accessible, it may be preferred to allow only access on the host instead:

```
network.host: 127.0.0.1

```

*   It is possible to use a custom port instead of the default `9200`:

```
http.port: 9200

```

You may want to change the default initial and maximum allowed memory usage:

 `/etc/elasticsearch/jvm.options` 
```
# Xms represents the initial size of total heap space
# Xmx represents the maximum size of total heap space

-Xms128m # e.g. 256m, 1g, 2g, ..
-Xmx512m # e.g. 256m, 1g, 2g, ..

```

**Note:** Installing [elasticsearch](https://www.archlinux.org/packages/?name=elasticsearch) provides already an increased `vm.max_map_count` as in `/usr/lib/sysctl.d/elasticsearch.conf`.

You might need to update the [vm.max_map_count](https://www.elastic.co/guide/en/elasticsearch/reference/5.2/vm-max-map-count.html) system limit:

```
# sysctl -w vm.max_map_count=262144

```

## Usage

Elasticsearch uses a REST API, see [Wikipedia:RESTful API](https://en.wikipedia.org/wiki/RESTful_API "wikipedia:RESTful API") for more information.

[Talking to Elasticsearch](https://www.elastic.co/guide/en/elasticsearch/guide/current/_talking_to_elasticsearch.html) and the [Getting started](https://www.elastic.co/guide/en/elasticsearch/guide/current/getting-started.html) guide should provide you with basic and detailed usage information.

The Elasticsearch server management (document maintenance, performing search, etc.) is usually done by [clients](https://www.elastic.co/guide/en/elasticsearch/client/index.html), that should provide a seamless integration with the preferred programming language.

Useful tools to manage ElasticSearch instances and clusters like [ElasticHQ](http://www.elastichq.org), [Elasticsearch GUI](https://github.com/jettro/elasticsearch-gui), [Kibana](https://www.elastic.co/products/kibana) and [Adminer](/index.php/Adminer "Adminer") are also available to simplify management.