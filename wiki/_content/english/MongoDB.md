MongoDB (from hu**mongo**us) is an open source document-oriented database system developed and supported by [MongoDB Inc. (formerly 10gen)](http://www.mongodb.com/). It is part of the NoSQL family of database systems. Instead of storing data in tables as is done in a "classical" relational database, MongoDB stores structured data as JSON-like documents with dynamic schemas (MongoDB calls the format [BSON](http://bsonspec.org/)), making the integration of data in certain types of applications easier and faster.

## Contents

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 MongoDB won't start](#MongoDB_won.27t_start)
    *   [3.2 MongoDB complains about transparent_hugepage Kernel Setting](#MongoDB_complains_about_transparent_hugepage_Kernel_Setting)

## Installation

Install [mongodb](https://www.archlinux.org/packages/?name=mongodb) from [official repositories](/index.php/Official_repositories "Official repositories"). You may also wish to still [mongodb-tools](https://www.archlinux.org/packages/?name=mongodb-tools), which provides tools such as `mongoimport`, `mongoexport`, `mongodump`, `mongorestore`, among others.

[Start/Enable](/index.php/Systemd#Using_units "Systemd") the `mongodb.service` daemon.

During the first startup of the mongodb service, it will [pre-allocate space](https://docs.mongodb.com/manual/faq/storage/#preallocated-data-files), by creating large files (for its journal and other data). This step may take a while, during which the database shell is unavailable.

## Usage

To access the Database shell type in the terminal:

```
$ mongo

```

## Troubleshooting

### MongoDB won't start

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

### MongoDB complains about transparent_hugepage Kernel Setting

After starting the mongoDB, if you see some warnings about the transparent_hugepage you can permanently disable this System Setting by editing the following file (see [FreeDesktop tmpfiles.d Manual](https://www.freedesktop.org/software/systemd/man/tmpfiles.d.html)):

 `/etc/tmpfiles.d/local.conf` 
```
w /sys/kernel/mm/transparent_hugepage/enabled - - - - never
w /sys/kernel/mm/transparent_hugepage/defrag - - - - never

```

If you want to disable only for this boot, you can use SysCtl or by simply echoing in the files like below:

```
# echo never > /sys/kernel/mm/transparent_hugepage/enabled
# echo never > /sys/kernel/mm/transparent_hugepage/defrag

```