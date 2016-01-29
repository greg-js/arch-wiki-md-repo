# Couchdb

_"Apache CouchDB is a document-oriented database that can be queried and indexed in a MapReduce fashion using JavaScript."_ - [CouchDB homepage](http://couchdb.apache.org/)

## Contents

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
    *   [2.1 Using Futon admin interface](#Using_Futon_admin_interface)
*   [3 Configuration](#Configuration)
    *   [3.1 Creating a self-signed certificate](#Creating_a_self-signed_certificate)
    *   [3.2 Creating administrator users](#Creating_administrator_users)
*   [4 See also](#See_also)

## Installation

Install the [couchdb](https://www.archlinux.org/packages/?name=couchdb) package.

By default, the package depends on [erlang-nox](https://www.archlinux.org/packages/?name=erlang-nox) without GTK, for headless servers. You can also install the standard version, [erlang](https://www.archlinux.org/packages/?name=erlang), that does require GTK.

## Usage

[Start/Enable](/index.php/Systemd#Using_units "Systemd") the `couchdb.service` daemon.

Test to see if the service is running by running `curl -XGET http://127.0.0.1:5984/`. Ping will not work (it's not supposed to unlike on other systems where it does). Note that in order to access this instance of CouchDB from another system you'll need to configure it (see below).

### Using Futon admin interface

You can now access the Futon admin interface by going to [http://localhost:5984/_utils](http://localhost:5984/_utils).

## Configuration

Change the default port, bind address, log-level and other useful nuggets in `/etc/couchdb/local.ini`.

**Tip:** Set `bind_address` to `0.0.0.0` to access CouchDB from any computer other than local.

If you want to run CouchDB on port 80 you will have to run the daemon as root or use an iptables rule such as:

```
$ iptables -t nat -A PREROUTING -p tcp --dport 80 -j REDIRECT --to-ports 5984

```

**Note:** Do not modify `/etc/couchdb/default.ini` as it gets overwritten whenever couchdb is updated, copy any values you would like to change and put them in `/etc/couchdb/local.ini`. Also be sure to restart `couchdb.service` after changes to this file.

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

Futon can be accessed over SSL on port 6984 via [https://localhost:6984/_utils/](https://localhost:6984/_utils/).

### Creating administrator users

Before a server admin is configured, all clients have admin privileges. To create an admin user, click on "Fix this" link at bottom right of Futon interface.

See [create a read-only database](http://lizconlan.github.com/sandbox/securing-couchdb.html) for locking down databases and further security.

## See also

*   [Official CouchDB page](http://couchdb.apache.org/)
*   [CouchDB Wiki](http://wiki.apache.org/couchdb/FrontPage)
*   [CouchDB - The Definitive Guide](http://guide.couchdb.org/)
*   [create a read-only database](http://lizconlan.github.com/sandbox/securing-couchdb.html)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Couchdb&oldid=409775](https://wiki.archlinux.org/index.php?title=Couchdb&oldid=409775)"