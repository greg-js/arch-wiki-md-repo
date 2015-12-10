# RethinkDB

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

RethinkDB is a document-oriented database similar to [MongoDB](/index.php/MongoDB "MongoDB") but aims to overcome scalability and practical limitation of the latter. [[1]](http://www.rethinkdb.com/docs/comparisons/mongodb/) [[2]](http://www.rethinkdb.com/blog/mongodb-biased-comparison/) RethinkDB is built to store JSON documents, and scale to multiple machines with very little effort. It has a pleasant query language that supports really useful queries like table joins and group by, and is easy to setup and learn.

## Installing RethinkDB

Install [rethinkdb](https://www.archlinux.org/packages/?name=rethinkdb) from official repository.

Now you can start rethinkdb from command-line:

```
# rethinkdb

```

Or instead you can run it as systemd service. Enable default rethinkdb instance as

```
# systemctl enable rethinkdb@default

```

and start it:

```
# systemctl start rethinkdb@default

```

Admin UI will be available at [8080](http://localhost:8080) port.

## Configuring RethinkDB

RethinkDB has multi-instance support, which means you can run several independent database instances at the same machine. Systemd service also supports multi-instance configuration.

To create a new RethinkDB instance create its configuration file:

```
# cd /etc/rethinkdb
# cp default.conf.sample instances.d/<NAME>.conf

```

where <NAME> is the name of you configuration that you'll going to use later. Change configuration options in the new config file. Then start the service:

```
# systectl enable rethinkdb@<NAME>
# systectl start rethinkdb@<NAME>

```

'default' instance is created at installation time for your convinence. Its data is stored in /var/lib/rethinkdb/default

Retrieved from "[https://wiki.archlinux.org/index.php?title=RethinkDB&oldid=409772](https://wiki.archlinux.org/index.php?title=RethinkDB&oldid=409772)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Database management systems](/index.php/Category:Database_management_systems "Category:Database management systems")