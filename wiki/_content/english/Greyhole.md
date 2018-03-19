Related articles

*   [Samba](/index.php/Samba "Samba")

[Greyhole](http://www.greyhole.net/) is an application that uses [Samba](/index.php/Samba "Samba") to create a storage pool of all your available hard drives (whatever their size, however they are connected), and allows you to create redundant copies of the files you store, in order to prevent data loss when part of your hardware fails.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Install from AUR](#Install_from_AUR)
    *   [1.2 Manual Installation](#Manual_Installation)
*   [2 Configuration](#Configuration)

## Installation

### Install from AUR

Install [greyhole](https://aur.archlinux.org/packages/greyhole/) from the [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository").

### Manual Installation

1\. Install the required packages

```
# pacman -S mysql php php-pear samba base-devel rsync postfix

```

2\. Download the latest source package from [here](http://www.greyhole.net/download/)

3\. Extract the Greyhole files

```
# tar zxvf greyhole-*.tar.gz
# cd greyhole-*
# GREYHOLE_INSTALL_DIR=`pwd`

```

4\. Create work directory for Greyhole

```
# mkdir -p /var/spool/greyhole
# chmod 777 /var/spool/greyhole

```

5\. Install Greyhole files

```
# install -m 0755 -D -p greyhole /usr/bin
# install -m 0755 -D -p greyhole-dfree /usr/bin
# install -m 0750 -D -p greyhole-config-update /usr/bin
# install -m 0644 -D -p logrotate.greyhole /etc/logrotate.d/greyhole
# install -m 0644 -D -p greyhole.cron.d /etc/cron.d/greyhole
# install -m 0644 -D -p greyhole.example.conf /etc/greyhole.conf
# install -m 0755 -D -p greyhole.cron.weekly /etc/cron.weekly/greyhole
# install -m 0755 -D -p greyhole.cron.daily /etc/cron.daily/greyhole

```

6\. Two files required for php-pear do not seem to be supplied with archive so grab them from Github and move them into the required location

```
# wget https://raw.github.com/gboudreau/Greyhole/master/includes/common.php
# wget https://raw.github.com/gboudreau/Greyhole/master/includes/sql.php
# include_path=`php -i | grep include_path | awk -F':' '{print $NF}'`
# mkdir "$include_path/includes"
# install -m 0644 -D -p includes/common.php "$include_path/includes"
# install -m 0644 -D -p includes/sql.php "$include_path/includes"

```

When setting the include_path if PHP complains about the timezone then set your timezone in the `/etc/php/php.ini` file.

7\. Install the Samba VFS module Find out what version of Samba you are running

```
# smbd --version

```

If you are running Samba 3.4

```
# if [ -x /usr/lib64/samba/vfs/ ]; then cp samba-module/bin/greyhole-x86_64.so /usr/lib64/samba/vfs/greyhole.so; else cp samba-module/bin/greyhole-i386.so /usr/lib/samba/vfs/greyhole.so; fi

```

If you are running Samba 3.5

```
# if [ -x /usr/lib64/samba/vfs/ ]; then cp samba-module/bin/3.5/greyhole-x86_64.so /usr/lib64/samba/vfs/greyhole.so; else cp samba-module/bin/3.5/greyhole-i386.so /usr/lib/samba/vfs/greyhole.so; fi

```

If you are running Samba 3.6 then you will need to compile the module manually

```
# SAMBA_VERSION=`smbd --version | awk '{print $2}'`
# wget http://samba.org/samba/ftp/stable/samba-${SAMBA_VERSION}.tar.gz
# tar zxf samba-${SAMBA_VERSION}.tar.gz && rm samba-${SAMBA_VERSION}.tar.gz
# cd samba-${SAMBA_VERSION}/source3
# ./configure

```

Before building the module we need to fix a few files to work with Samba 3.6\. Firstly copy the code from [here](http://pastebin.com/Khmex6sz) in to a file called `Greyhole-Samba-3.6.patch`

```
# patch -p1 < Greyhole-Samba-3.6.patch

```

Next copy the code from [here](http://pastebin.com/U51s5yKb) into a file called `vfs_greyhole.c` in the `modules` directory. Now we can build Samba

```
# make

```

This step may take a long time depending on how powerful your machine is. Once the process has finished you can copy the Greyhole module to the correct directory

 `# if [ -x /usr/lib64/samba/vfs/ ]; then cp bin/greyhole.so /usr/lib64/samba/vfs/greyhole.so; else cp bin/greyhole.so /usr/lib/samba/vfs/greyhole.so; fi` 

8\. Now (re)start Samba

```
# systemctl start smbd

```

or

```
# systemctl restart smbd

```

9\. Next we need to install the Greyhole init script however this will have to follow at a later date as I have not yet made one. A generic Linux example init script is supplied with the Greyhole source and is called `initd_script.sh`

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