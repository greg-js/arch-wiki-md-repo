MongoDB (from hu**mongo**us) is an open source document-oriented database system developed and supported by [MongoDB Inc. (formerly 10gen)](http://www.mongodb.com/). It is part of the NoSQL family of database systems. Instead of storing data in tables as is done in a "classical" relational database, MongoDB stores structured data as JSON-like documents with dynamic schemas (MongoDB calls the format [BSON](http://bsonspec.org/)), making the integration of data in certain types of applications easier and faster.

## Contents

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 MongoDB won't start](#MongoDB_won.27t_start)

## Installation

Install [mongodb](https://www.archlinux.org/packages/?name=mongodb) from [official repositories](/index.php/Official_repositories "Official repositories").

[Start/Enable](/index.php/Systemd#Using_units "Systemd") the `mongodb.service` daemon.

During the first startup of the mongodb service, it will pre-allocate space, by creating large files (for its journal and other data). These files may take up a total space of 3 GB.

Please note this step may take a while, during which the database shell is unavailable.

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

Check if the lock file exists:

```
# ls  -lisa /var/lib/mongodb

```

If it does, stop `mongodb.service`, and delete the file. Then start the service again.

```
# rm /var/lib/mongodb/mongod.lock

```

If it still won't start, run a repair on the database, specifying the dbpath (/var/lib/mongodb/ is the default --dbpath in Arch Linux):

```
# mongod --dbpath /var/lib/mongodb/ --repair

```

After running the repair as root, the files will be owned by the root user, whilst Arch Linux runs it under a different user. You will need to use chown to change the ownership of the files back to the correct user. See following link for further details: [Further reference](http://earlz.net/view/2011/03/11/0015/mongodb-and-arch-linux)

```
# chown -R mongodb: /var/{log,lib}/mongodb/

```

Check that the [boost-libs](https://www.archlinux.org/packages/?name=boost-libs) package is up to date. MongoDB requires a specific version, however, the package does not restrict the version of this dependency.