RethinkDB is a document-oriented database similar to [MongoDB](/index.php/MongoDB "MongoDB") but aims to overcome scalability and practical limitation of the latter. [[1]](http://www.rethinkdb.com/docs/comparisons/mongodb/) [[2]](http://www.rethinkdb.com/blog/mongodb-biased-comparison/) RethinkDB is built to store JSON documents, and scale to multiple machines with very little effort. It has a pleasant query language that supports queries such as table joins and group by. It is easy to setup and learn. For more detailed information, see the [official homepage](https://www.rethinkdb.com/).

## Installation

[Install](/index.php/Install "Install") [rethinkdb](https://www.archlinux.org/packages/?name=rethinkdb) from the official repositories.

Create and set user rights for RethinkDB folder:

```
# mkdir /var/lib/rethinkdb/default
# chown -R rethinkdb:rethinkdb /var/lib/rethinkdb/

```

Now you can start `rethinkdb` from the command-line:

```
# rethinkdb

```

Or instead you can run it as a `systemd` service. Enable the default `rethinkdb` instance as

```
# systemctl enable rethinkdb@default

```

and start it:

```
# systemctl start rethinkdb@default

```

RethinkDB's admin UI is now available on port [8080](http://localhost:8080).

## Configuration

RethinkDB has multi-instance support, which means you can run several independent database instances on the same machine. The `systemd` service also supports multi-instance configuration.

To create a new RethinkDB instance, create its configuration file:

```
# cd /etc/rethinkdb
# cp default.conf.sample instances.d/<NAME>.conf

```

where <NAME> represents the configuration you'll be using later. Change the configuration options in the new config file. Then start the service:

```
# systemctl enable rethinkdb@<NAME>
# systemctl start rethinkdb@<NAME>

```

The 'default' instance is created at installation time for your convenience. Its data is stored in `/var/lib/rethinkdb/default`.