[davfs2](http://savannah.nongnu.org/projects/davfs2) is a Linux file system driver that allows to [mount](/index.php/Mount "Mount") a [WebDAV](/index.php/WebDAV "WebDAV") resource. WebDAV is an extension to HTTP/1.1 that allows remote collaborative authoring of Web resources.

## Contents

*   [1 Installing davfs2](#Installing_davfs2)
*   [2 Mount WebDAV-resource](#Mount_WebDAV-resource)
    *   [2.1 Configuration and mount options](#Configuration_and_mount_options)
    *   [2.2 Using command-line](#Using_command-line)
    *   [2.3 Using systemd](#Using_systemd)
    *   [2.4 Using fstab](#Using_fstab)
*   [3 Tips and tricks](#Tips_and_tricks)
    *   [3.1 Storing credentials](#Storing_credentials)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Creating/copying files not possible and/or freezes](#Creating.2Fcopying_files_not_possible_and.2For_freezes)
*   [5 See also](#See_also)

## Installing davfs2

[Install](/index.php/Install "Install") [davfs2](https://www.archlinux.org/packages/?name=davfs2) from [official repositories](/index.php/Official_repositories "Official repositories").

## Mount WebDAV-resource

### Configuration and mount options

There is a system wide **configuration** file `/etc/davfs2/davfs2.conf` and a user configuration file `~/.davfs2/davfs2.conf`. The latter is read in addition to the system configuration when invoked by an ordinary user and takes precedence. There are general, WebDAV related, cache related and debugging options. All the available options and their syntax can be found in the [manual page](https://linux.die.net/man/5/davfs2.conf).

There are also **mount options** used to define if needed the path of the configuration file, the owner and group of the filesystem and some other options related to file access. The list of recognised options can be obtained with the following command:

```
$ mount.davfs -h

```

Also see [mount.davfs(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mount.davfs.8) for description and options.

### Using command-line

To mount a WebDAV-resource use `mount`, not `mount.davfs` directly.

```
# mount -t davfs http(s)://addres:<port>/path /mount/point

```

### Using systemd

To use [systemd mounting](/index.php/Systemd#Mounting "Systemd"):

 `/etc/systemd/system/mnt-webdav-service.mount` 
```
[Unit]
Description=Mount WebDAV Service
After=network-online.target
Wants=network-online.target

[Mount]
What=http(s)://address:<port>/path
Where=/mnt/webdav/service
Options=uid=1000,file_mode=0664,dir_mode=2775,grpid
Type=davfs
TimeoutSec=15

[Install]
WantedBy=multi-user.target

```

You can create an systemd automount unit to set a timeout

 `/etc/systemd/system/mnt-webdav-service.automount` 
```
[Unit]
Description=Mount WebDAV Service
After=network-online.target
Wants=network-online.target

[Automount]
Where=/mnt/dav
TimeoutIdleSec=300

[Install]
WantedBy=remote-fs.target

```

See [Fstab#Automount with systemd](/index.php/Fstab#Automount_with_systemd "Fstab") for more tips and tricks when using systemd mount units.

### Using fstab

To define how the webdav resource should be mounted into the filesystem, [append](/index.php/Append "Append") a [fstab](/index.php/Fstab "Fstab") entry under the following format:

 `/etc/fstab`  `https://*webdav.example/path* /mnt/*webdav* davfs rw,user,uid=*username*,noauto 0 0` 

where *username* is the owner of the mounted file system. It may be a numeric ID or a user name and only *root* can mount a uid different from the mounting user.

## Tips and tricks

### Storing credentials

Create a *secrets file* to store credentials for a WebDAV-service using `~/.davfs2/secrets` for *user*, and `/etc/davfs2/secrets` for *root*:

 `/etc/davfs2/secrets`  `https://*webdav.example/path* *davusername* *davpassword*` 

Make sure the *secrets file* contains the correct [permissions](/index.php/Permissions "Permissions"), for *root* mounting:

```
# chmod 600 /etc/davfs2/secrets
# chown root:root /etc/davfs2/secrets

```

And for *user* mounting:

```
$ chmod 600 ~/.davfs2/secrets

```

## Troubleshooting

### Creating/copying files not possible and/or freezes

If creating/copying files is not possible and/or freezes occur, edit the [configuration file](#Mount_WebDAV-resource) to use `use_locks 0` as option. Default for this parameter is `1` which locks files on the server when they are opened for writing.

## See also

*   [http://ajclarkson.co.uk/blog/auto-mount-webdav-raspberry-pi/](http://ajclarkson.co.uk/blog/auto-mount-webdav-raspberry-pi/)