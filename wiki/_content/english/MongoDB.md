MongoDB (from hu**mongo**us) is an open source document-oriented database system developed and supported by [MongoDB Inc. (formerly 10gen)](http://www.mongodb.com/). It is part of the NoSQL family of database systems. Instead of storing data in tables as is done in a "classical" relational database, MongoDB stores structured data as JSON-like documents with dynamic schemas (MongoDB calls the format [BSON](http://bsonspec.org/)), making the integration of data in certain types of applications easier and faster.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 MongoDB won't start](#MongoDB_won't_start)
    *   [3.2 Warning about Transparent Huge Pages (THP)](#Warning_about_Transparent_Huge_Pages_(THP))

## Installation

MongoDB has been removed from the [official repositories](/index.php/Official_repositories "Official repositories") due to its re-licensing issues [[1]](https://lists.archlinux.org/pipermail/arch-dev-public/2019-January/029430.html).

[PKGBUILDs](/index.php/PKGBUILD "PKGBUILD") are provided in [AUR](/index.php/AUR "AUR") to build MongoDB from source instead:

*   [mongodb](https://aur.archlinux.org/packages/mongodb/) - requires around 160GB free disk space and may take several hours to build.
*   [mongodb-bin](https://aur.archlinux.org/packages/mongodb-bin/) - prebuilt MongoDB binary.

[Install](/index.php/Install "Install") [mongodb-tools](https://www.archlinux.org/packages/?name=mongodb-tools) or [mongodb-tools-bin](https://aur.archlinux.org/packages/mongodb-tools-bin/), which provides tools such as `mongoimport`, `mongoexport`, `mongodump`, `mongorestore`, among others.

## Usage

[Start](/index.php/Start "Start")/[Enable](/index.php/Enable "Enable") the `mongodb.service` daemon.

**Note:** During the first startup of the mongodb service, it will [pre-allocate space](https://docs.mongodb.com/manual/faq/storage/#preallocated-data-files), by creating large files (for its journal and other data). This step may take a while, during which the MongoDB shell is unavailable.

Use `mongo` to access the MongoDB shell [[2]](https://docs.mongodb.com/manual/mongo/):

```
$ mongo

```

## Troubleshooting

### MongoDB won't start

Check that the systemctl service is configured to use the correct database location:

```
$ vi /usr/lib/systemd/system/mongodb.service

```

Add "--dbpath /var/lib/mongodb" to the "ExecStart" line:

```
ExecStart=/usr/bin/numactl --interleave=all mongod --quiet --config /etc/mongodb.conf --dbpath /var/lib/mongodb

```

Check that there is at least 3GB space available for its journal files, otherwise mongodb can fail to start (without issuing a message to the user):

```
$ df -h /var/lib/mongodb/

```

Check if the mongod.lock lock file is empty or not:

```
# ls  -lisa /var/lib/mongodb

```

If it is, stop `mongodb.service`. Run a repair on the database, specifying the dbpath (/var/lib/mongodb/ is the default --dbpath in Arch Linux):

```
# mongod --dbpath /var/lib/mongodb/ --repair

```

Upon completion, the dbpath should contain the repaired data files and an empty mongod.lock file.

**Warning:** In dire situations, you can remove the file, start the database using the possibly corrupt files, and attempt to recover data from the database. However, it is impossible to predict the state of the database in these situations. See [upstream document for detail](https://docs.mongodb.com/manual/tutorial/recover-data-following-unexpected-shutdown/).

After running the repair as root, the files will be owned by the root user, whilst Arch Linux runs it under a different user. You will need to use chown to change the ownership of the files back to the correct user. See following link for further details: [Further reference](http://earlz.net/view/2011/03/11/0015/mongodb-and-arch-linux)

```
# chown -R mongodb: /var/{log,lib}/mongodb/

```

Finally, if you copied the configuration file from mongodb [documentation](https://docs.mongodb.com/manual/reference/configuration-options/), remove these two lines and [restart](/index.php/Restart "Restart") mongodb.service:

 `/etc/mongodb.conf` 
```
processManagement:
   fork: true

```

### Warning about Transparent Huge Pages (THP)

One may want to permanently disable this feature by using a [tmpfile](/index.php/Tmpfile "Tmpfile"):

 `/etc/tmpfiles.d/mongodb.conf` 
```
w /sys/kernel/mm/transparent_hugepage/enabled - - - - never
w /sys/kernel/mm/transparent_hugepage/defrag - - - - never

```

Use [sysctl](/index.php/Sysctl "Sysctl") to disable THP at runtime:

```
# echo never > /sys/kernel/mm/transparent_hugepage/enabled
# echo never > /sys/kernel/mm/transparent_hugepage/defrag

```