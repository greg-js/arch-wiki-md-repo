*"Apache CouchDB is a document-oriented database that can be queried and indexed in a MapReduce fashion using JavaScript."* - [CouchDB homepage](http://couchdb.apache.org/)

## Contents

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
    *   [2.1 Using Fauxton admin interface](#Using_Fauxton_admin_interface)
*   [3 Configuration](#Configuration)
    *   [3.1 Creating a self-signed certificate](#Creating_a_self-signed_certificate)
*   [4 Single node setup & Security](#Single_node_setup_.26_Security)
*   [5 See also](#See_also)

## Installation

Install the [couchdb](https://www.archlinux.org/packages/?name=couchdb) package.

## Usage

[Start/Enable](/index.php/Systemd#Using_units "Systemd") the `couchdb.service` daemon.

Test to see if the service is running by running `curl http://127.0.0.1:5984/`. Note that in order to access this instance of CouchDB from another system you’ll need to configure it (see below).

### Using Fauxton admin interface

You can now access the Fauxton admin interface by going to [http://localhost:5984/_utils](http://localhost:5984/_utils).

## Configuration

You can do this through Fauxton or using command line.

To setup the database and create an admin account through Fauxton, visit [http://127.0.0.1:5984/_utils/#setup](http://127.0.0.1:5984/_utils/#setup).

To setup a single node from the command line (where `<adminuser>` and `<password>` are to be replaced).

```
   curl -X POST -H "Content-Type: application/json" [http://127.0.0.1:5984/_cluster_setup](http://127.0.0.1:5984/_cluster_setup) -d '{"action": "enable_single_node", "bind_address":"127.0.0.1", "username": "<adminuser>", "password": "<password>"}'
   curl -X PUT http://<adminuser>:<password>@127.0.0.1:5984/_users
   curl -X PUT http://<adminuser>:<password>@127.0.0.1:5984/_replicator

```

Also, you might want to take a look at [#Single node setup & Security](#Single_node_setup_.26_Security).

**Tip:** If you are doing a cluster setup, you might want to set `bind_address` to `0.0.0.0` to access CouchDB from other nodes.

Note that you can also do all this as well as changing the default port, bind address, log-level and other useful nuggets in `/etc/couchdb/local.ini`.

**Note:** Do not modify `/etc/couchdb/default.ini` as it gets overwritten whenever couchdb is updated, copy any values you would like to change and put them in `/etc/couchdb/local.ini`. Also be sure to restart `couchdb.service` after changes to this file.

If you want to run CouchDB on port 80 you will have to run the daemon as root, use a reverse proxy or set an iptables rule such as:

```
$ iptables -t nat -A PREROUTING -p tcp --dport 80 -j REDIRECT --to-ports 5984

```

### Creating a self-signed certificate

If you would like to use ssl with a self-signed certificate you can create one like this:

```
# cd /etc/couchdb
# openssl req -new -x509 -nodes -newkey rsa:4096 -keyout server.key -out server.crt

```

Then uncomment httpsd and update the paths in `[daemons]` and `[ssl]` sections:

 `/etc/couchdb/local.ini` 
```
[daemons]
httpsd = {couch_httpd, start_link, [https]}

[ssl]
cert_file = /etc/couchdb/server.crt
key_file = /etc/couchdb/server.key
```

Fauxton can then be accessed over SSL on port 6984 via [https://localhost:6984/_utils/](https://localhost:6984/_utils/).

## Single node setup & Security

If you run CouchDB in a single node setup, you might want to increase security by not binding unnecessarily on public network interfaces. Two process are actually doing so: `epmd` and `beam.smp`. The first one is quite easy to work around, you can simply add the following systemd drop-in addition to `couchdb.service`:

 `/etc/systemd/system/couchdb.service.d/10-bind-locally.conf` 
```
[Service]
Environment=ERL_EPMD_ADDRESS=127.0.0.1
```

The second one needs an edit in `vm.args`

 `/etc/couchdb/vm.args`  `-kernel inet_dist_use_interface {127,0,0,1}` 

## See also

*   [Official CouchDB page](http://couchdb.apache.org/)
*   [CouchDB Wiki](http://wiki.apache.org/couchdb/FrontPage)
*   [CouchDB - The Definitive Guide](http://guide.couchdb.org/)
*   [create a read-only database](http://lizconlan.github.com/sandbox/securing-couchdb.html)