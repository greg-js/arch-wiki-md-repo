**DAVfs** is a Linux file system driver that allows you to [mount](/index.php/Mount "Mount") a [WebDAV](/index.php/WebDAV "WebDAV") resource. WebDAV is an extension to HTTP/1.1 that allows remote collaborative authoring of Web resources, defined in RFC 4918.

## Contents

*   [1 Installing DAVfs](#Installing_DAVfs)
*   [2 Mount WebDAV-resource](#Mount_WebDAV-resource)
    *   [2.1 Using command-line](#Using_command-line)
    *   [2.2 Using systemd](#Using_systemd)
    *   [2.3 Using fstab](#Using_fstab)
*   [3 Tips and tricks](#Tips_and_tricks)
    *   [3.1 Storing credentials](#Storing_credentials)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Creating/copying files not possible and/or freezes](#Creating.2Fcopying_files_not_possible_and.2For_freezes)
*   [5 See also](#See_also)

## Installing DAVfs

[Install](/index.php/Install "Install") [davfs2](https://www.archlinux.org/packages/?name=davfs2) from [official repositories](/index.php/Official_repositories "Official repositories").

## Mount WebDAV-resource

To list all available mount options:

```
$ mount.davfs -h

```

Configuration files are stored under `/etc/davfs2/davfs2.conf` and/or `~/.davfs2/davfs2.conf`.

### Using command-line

```
# mount.davfs http(s)://address:<port>/path /mount/point
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
Options=uid=1000,gid=1000,file_mode=0664,dir_mode=2775,grpid
Type=davfs
TimeoutSec=15

[Install]
WantedBy=multi-user.target

```

See [Fstab#Automount with systemd](/index.php/Fstab#Automount_with_systemd "Fstab") for more tips and tricks when using systemd mount units.

### Using fstab

[Append](/index.php/Append "Append") the following [fstab](/index.php/Fstab "Fstab") entry:

```
[https://webdav.example/path](https://webdav.example/path) /mnt/webdav davfs uid=username,file_mode=0664,dir_mode=2775 0 0

```

To mount as [user](/index.php/User "User"), add yourself to the *network* [group](/index.php/Group "Group"). Replace *username* with the name of the user:

```
# gpasswd network -a *username*

```

Mount as user example:

```
[https://webdav.example/path](https://webdav.example/path) /mnt/webdav davfs user,noauto,uid=username,file_mode=0664,dir_mode=2775 0 0

```

## Tips and tricks

### Storing credentials

Create a *secrets file* to store credentials for a WebDAV-service using `~/.davfs2/secrets` for *user*, and `/etc/davfs2/secrets` for *root*:

 `/etc/davfs2/secrets` 
```
http(s)://address:<port>/path username password

```

Make sure the *secrets file* contains the correct [permissions](/index.php/Permissions "Permissions"):

```
# chmod 600 /etc/davfs2/secrets
# chown root:root /etc/davfs2/secrets

```

For user mouting:

```
$ chmod 600 ~/.davfs2/secrets

```

## Troubleshooting

### Creating/copying files not possible and/or freezes

If creating/copying files is not possible and/or freezes occur, edit the [configuration file](#Mount_WebDAV-resource) to use `use_locks 0` as option.

## See also

*   [http://doc.owncloud.org/server/6.0/user_manual/files/files.html](http://doc.owncloud.org/server/6.0/user_manual/files/files.html)
*   [http://ajclarkson.co.uk/blog/auto-mount-webdav-raspberry-pi/](http://ajclarkson.co.uk/blog/auto-mount-webdav-raspberry-pi/)