MongoDB (from hu**mongo**us) is an open source document-oriented database system developed and supported by [MongoDB Inc. (formerly 10gen)](http://www.mongodb.com/). It is part of the NoSQL family of database systems. Instead of storing data in tables as is done in a "classical" relational database, MongoDB stores structured data as JSON-like documents with dynamic schemas (MongoDB calls the format [BSON](http://bsonspec.org/)), making the integration of data in certain types of applications easier and faster.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
*   [3 Configuration](#Configuration)
    *   [3.1 File Format](#File_Format)
    *   [3.2 Requiring Authentication](#Requiring_Authentication)
    *   [3.3 NUMA](#NUMA)
    *   [3.4 Clean Start and Stop](#Clean_Start_and_Stop)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 MongoDB won't start](#MongoDB_won't_start)
    *   [4.2 Warning about Transparent Huge Pages (THP)](#Warning_about_Transparent_Huge_Pages_(THP))

## Installation

MongoDB has been removed from the [official repositories](/index.php/Official_repositories "Official repositories") due to its re-licensing issues [[1]](https://lists.archlinux.org/pipermail/arch-dev-public/2019-January/029430.html).

[PKGBUILDs](/index.php/PKGBUILD "PKGBUILD") are provided in [AUR](/index.php/AUR "AUR"):

*   [mongodb](https://aur.archlinux.org/packages/mongodb/) - builds from source, requiring 180GB+ free disk space, and may take several hours to build (i.e. 6.5 hours on Intel i7, 1 hour on 32 Xeon cores with high-end NVMe.)
*   [mongodb-bin](https://aur.archlinux.org/packages/mongodb-bin/) - prebuilt MongoDB binary extracted from [official MongoDB Ubuntu repository](https://repo.mongodb.org/apt/ubuntu/) packages. Compilation options used are unknown.

[Install](/index.php/Install "Install") tools (`mongoimport`, `mongoexport`, `mongodump`, `mongorestore`, among others) using the [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") from the [AUR](/index.php/AUR "AUR") corresponding to the main [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") you chose:

*   [mongodb-tools](https://aur.archlinux.org/packages/mongodb-tools/)
*   [mongodb-tools-bin](https://aur.archlinux.org/packages/mongodb-tools-bin/)

## Usage

[Start](/index.php/Start "Start")/[Enable](/index.php/Enable "Enable") the `mongodb.service` daemon.

**Note:** During the first startup of the mongodb service, it will [pre-allocate space](https://docs.mongodb.com/manual/faq/storage/#preallocated-data-files), by creating large files (for its journal and other data). This step may take a while, during which the MongoDB shell is unavailable.

To access the MongoDB shell [[2]](https://docs.mongodb.com/manual/mongo/):

```
$ mongo

```

Or, if authentication is configured:

```
$ mongo -u *userName*

```

## Configuration

### File Format

MongoDB 2.6 introduced a YAML-based configuration file format. The 2.4 configuration file format remains for backward compatibility [[3]](https://docs.mongodb.com/manual/reference/configuration-options/#file-format):

 `/etc/mongodb.conf` 
```
systemLog:
   destination: file
   path: "/var/log/mongodb/mongod.log"
   logAppend: true
storage:
   journal:
      enabled: true
processManagement:
   fork: true
net:
   bindIp: 127.0.0.1
   port: 27017
setParameter:
   enableLocalhostAuthBypass: false
..
```

See [https://docs.mongodb.com/manual/reference/configuration-options/](https://docs.mongodb.com/manual/reference/configuration-options/) for available configuration options.

### Requiring Authentication

**Warning:** By default, MongoDB does not require any authentication. Although MongoDB only listens on the localhost interface by default, this still allows any local user to connect without authenticating and may exposes the database(s). It is recommended to enable access control to prevent any unwanted access.

To create a MongoDB user account with administrator access [[4]](https://docs.mongodb.com/manual/tutorial/enable-authentication/):

 `$ mongodb` 
```
use admin
db.createUser(
  {
    user: "myUserAdmin",
    pwd: "abc123",
    roles: [ { role: "userAdminAnyDatabase", db: "admin" }, "readWriteAnyDatabase" ]
  }
)
```

If your `/etc/mongodb.conf` uses the new YAML format, [append](/index.php/Append "Append"):

 `/etc/mongodb.conf` 
```
security:
 authorization: "enabled"

```

If it uses the v2.4 format, add:

 `/etc/mongodb.conf`  `auth = true` 

[Restart](/index.php/Restart "Restart") `mongodb.service`.

### NUMA

Running MongoDB with Non-Uniform Access Memory (NUMA) can significantly impact performance. [[5]](https://docs.mongodb.com/manual/administration/production-notes/#mongodb-and-numa-hardware)

To see if your system uses NUMA:

```
$ dmesg | grep -i numa

```

Also, `/var/log/mongodb/mongod.log` will show warnings if NUMA is in use and MongoDB is not started through `numactl`. (The `mongo` shell will also show this, but only if you do not have authentication enabled.)

If your system uses NUMA, to improve performance, you should make MongoDB start through `numactl`:

```
# cp /usr/lib/systemd/system/mongodb.service /etc/systemd/system

```

And change how `/etc/systemd/system/mongodb.service` starts MongoDB.

If using [mongodb](https://aur.archlinux.org/packages/mongodb/), change it from:

```
ExecStart=/usr/bin/mongod $OPTIONS

```

To:

```
ExecStart=**/usr/bin/numactl --interleave=all** /usr/bin/mongod $OPTIONS

```

If using [mongodb-bin](https://aur.archlinux.org/packages/mongodb-bin/), change it from:

```
ExecStart=/usr/bin/mongod --quiet --config /etc/mongodb.conf

```

To:

```
ExecStart=**/usr/bin/numactl --interleave=all** /usr/bin/mongod --quiet --config /etc/mongodb.conf

```

Zone claim also needs to be disabled, but on arch, `/proc/sys/vm/zone_reclaim_mode` defaults to `0`.

[Reenable](/index.php/Systemd#Replacement_unit_files "Systemd") and [Restart](/index.php/Restart "Restart") `mongodb.service`. (Merely restarting it will not switch to the `/etc` version.)

### Clean Start and Stop

By default, [systemd](/index.php/Systemd "Systemd") immediately kills anything after asking it to start or stop, if it has not finished doing so within 90 seconds.

[mongodb](https://aur.archlinux.org/packages/mongodb/) makes [systemd](/index.php/Systemd "Systemd") wait as long as it takes for MongoDB to start, but [mongodb-bin](https://aur.archlinux.org/packages/mongodb-bin/) does not. Both packages allow [systemd](/index.php/Systemd "Systemd") to kill MongoDB after it's asked to stop, if it hasn't finished within 90 seconds.

Large MongoDB databases can take a considerable amount of time to cleanly shut down, especially if swap is being used. (An active 450GB database on a top of the line NVMe with 64GB RAM and 16GB swap can take an hour to shut down.)

By default, MongoDB uses journaling. [[6]](https://docs.mongodb.com/manual/reference/configuration-options/#storage-options) With journaling, an unclean shutdown should not pose a risk of data loss. But, if not shutdown cleanly, large MongoDB databases can take a considerable amount of time to start back up. In this case, choosing whether to require a clean shutdown is a choice of a slower shutdown versus a slower startup. [[7]](https://groups.google.com/forum/?utm_medium=email&utm_source=footer#!msg/mongodb-user/KjBU_GcNcmw/gR2UxRIFAgAJ)

**Warning:** If you disable journaling, failing to require a clean shutdown severely risks data loss, so you really need to require a clean shutdown. [[8]](https://docs.mongodb.com/manual/tutorial/recover-data-following-unexpected-shutdown/)

To prevent [systemd](/index.php/Systemd "Systemd") from killing MongoDB after 90 seconds, make and then [edit](/index.php/Edit "Edit") your own `.service` file, i.e.:

```
# cp /usr/lib/systemd/system/mongodb.service /etc/systemd/system

```

To allow MongoDB to cleanly shutdown, [append](/index.php/Append "Append") to the `[Service]` section: (On large databases, this may substantially slow down your system shutdown time, but speeds up your next MongoDB start time)

```
TimeoutStopSec=infinity

```

If MongoDB needs a long time to start back up, it can be very problematic for [systemd](/index.php/Systemd "Systemd") to keep killing and restarting it every 90 seconds [[9]](https://jira.mongodb.org/browse/SERVER-38086), so [mongodb](https://aur.archlinux.org/packages/mongodb/) prevents this. If using [mongodb-bin](https://aur.archlinux.org/packages/mongodb-bin/), to make [systemd](/index.php/Systemd "Systemd") wait as long as it takes for MongoDB to start, [append](/index.php/Append "Append") to the `[Service]` section:

```
TimeoutStartSec=infinity

```

## Troubleshooting

### MongoDB won't start

If MongoDB won't start, and you just upgraded to [mongodb](https://aur.archlinux.org/packages/mongodb/) 4.0.6-2+, you probably have a custom `/etc/mongodb.conf`. When MongoDB was in the [Official repositories](/index.php/Official_repositories "Official repositories"), it used an Arch-specific configuration file that used the systemd service type of simple. It now supplies upstream's systemd service and configuration files, which instead use a systemd service type of forking. Pacman will automatically upgrade your systemd service file, but will only automatically upgrade your `/etc/mongodb.conf` [if you never modified it](/index.php/Pacman/Pacnew_and_Pacsave "Pacman/Pacnew and Pacsave"). In that case, systemd will be expecting `mongod` to fork, but its configuration file will tell it not to. You need to: switch to the new configuration file installed at `/etc/mongodb.conf.pacnew`, and duplicate changes you made to the old one that you still need, considering the new one is now in the YAML format, and the old one is probably in the MongoDB 2.4 format; or modify your existing one to enable forking. (To continue using the old 2.4 file format instead of YAML, adding `fork: true` should be what is needed.)

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