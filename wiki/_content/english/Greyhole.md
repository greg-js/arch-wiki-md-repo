Related articles

*   [Samba](/index.php/Samba "Samba")

[Greyhole](http://www.greyhole.net/) is an application that uses [Samba](/index.php/Samba "Samba") to create a storage pool of all your available hard drives (whatever their size, however they are connected), and allows you to create redundant copies of the files you store, in order to prevent data loss when part of your hardware fails.

## Installation

[Install](/index.php/Install "Install") the [greyhole](https://aur.archlinux.org/packages/greyhole/) package.

## Configuration

**Note:** This process is taken from the USAGE file that is supplied with Greyhole.

1\. Setup Samba Edit `/etc/samba/smb.conf` and add the following 2 lines to the `[global]` section

```
unix extensions = no
wide links = yes
```

For each of your shares, add a '`dfree command`' and '`vfs objects`' lines, as seen below. Example share definition:

```
[share_name]
    path = /path/to/share_name
    create mask = 0770
    directory mask = 0770
    read only = no
    available = yes
    browseable = yes
    writable = yes
    guest ok = no
    printable = no
    dfree command = /usr/bin/greyhole-dfree
    vfs objects = greyhole
```

[Restart](/index.php/Restart "Restart") `smb.service`.

2\. Setup and start MySQL as described in [MySQL](/index.php/MySQL "MySQL").

3\. Customize the greyhole configuration at `/etc/greyhole.conf`

4\. For each directory you defined as 'storage_pool_directories', execute the following command, to create a hidden file in the root directory of each partition:

 `# touch <dir>/.greyhole_uses_this` 

Those files will be used to differentiate an empty mount from a now-gone mount. i.e. Greyhole will output a warning if this file is not in the root directory where it is about to try to save a file, and it will not use that directory. This will prevent Greyhole from filling the / partition when a partition is unmounted!

5\. The following is needed to work around problems with the CIFS client. This can be added to your /etc/rc.local or you can add cifs to the modules section of rc.conf and use modprobe.d to set OplockEnabled.

```
# modprobe cifs
# echo 0 > /proc/fs/cifs/OplockEnabled

```

6\. Configure PHP Open /etc/php/php.ini in your favorite editor. Set `date.timezone` and uncomment `extension=pdo_mysql`.

7\. [Start](/index.php/Start "Start") `greyhole.service`.