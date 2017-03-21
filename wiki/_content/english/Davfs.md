**DAVfs** is a Linux file system driver that allows you to mount a WebDAV server as a disk drive. WebDAV is an extension to HTTP/1.1 that allows remote collaborative authoring of Web resources, defined in RFC 4918.

## Contents

*   [1 Installing DAVfs](#Installing_DAVfs)
*   [2 Mounting the partition](#Mounting_the_partition)
*   [3 Mounting as regular user](#Mounting_as_regular_user)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Creating/copying files not possible](#Creating.2Fcopying_files_not_possible)
*   [5 See also](#See_also)

## Installing DAVfs

[Install](/index.php/Install "Install") [davfs2](https://www.archlinux.org/packages/?name=davfs2) from [official repositories](/index.php/Official_repositories "Official repositories").

## Mounting the partition

Examples:

```
# mount.davfs http://localhost:8080/ /mnt/dav
# mount -t davfs http://localhost:8080/ /mnt/dav

```

## Mounting as regular user

Add yourself to network group (where username is replaced with your username):

```
# usermod -a -G network username

```

Add webdav entry to /etc/fstab (again, replacing username with your actual username):

```
https://webdav.example.com /home/username/webdav davfs user,noauto,uid=username,file_mode=600,dir_mode=700 0 1

```

Create secrets file in your home:

```
$ mkdir ~/.davfs2/
$ echo "https://webdav.example.com webdavuser webdavpassword" >> ~/.davfs2/secrets 
$ chmod 0600 ~/.davfs2/secrets

```

For nextcloud and owncloud the url is:

```
https://webdav.example.com/remote.php/webdav

```

For box.com, the url is:

```
https://dav.box.com/dav

```

For STACK, the url is (replace username with your username):

```
https://username.stackstorage.com/remote.php/webdav

```

If you want to mount several disks from same server, you need specify mount points of this disks instead of server address in file ~/.davfs2/secrets, remember to put the password in double quotes.

```
/home/username/disk1 webdavuser1 "webdavpassword1"
/home/username/disk2 webdavuser1 "webdavpassword2"
.........
/home/username/diskN webdavuserN "webdavpasswordN" 

```

Now you should be able to mount and unmount ~/webdav:

```
# mount ~/webdav
# fusermount -u ~/webdav

```

## Troubleshooting

### Creating/copying files not possible

If creating/copying files is not possible, while the same operations work on directories, edit `/etc/davfs2/davfs2.conf` and change the following line accordingly:

 `/etc/davfs2/davfs2.conf` 
```
[...]
use_locks 0
[...]

```

## See also

[http://doc.owncloud.org/server/6.0/user_manual/files/files.html](http://doc.owncloud.org/server/6.0/user_manual/files/files.html)