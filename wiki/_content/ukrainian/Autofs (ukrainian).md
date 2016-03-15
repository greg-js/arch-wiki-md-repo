Стаття пояснює процес інсталяції та налагодження AutoFS, пакета для автоматичного підключення зовнішніх носіїв та ресурсів мережі.

## Contents

*   [1 Вступ](#.D0.92.D1.81.D1.82.D1.83.D0.BF)
*   [2 Інсталяція](#.D0.86.D0.BD.D1.81.D1.82.D0.B0.D0.BB.D1.8F.D1.86.D1.96.D1.8F)
*   [3 Налагодження](#.D0.9D.D0.B0.D0.BB.D0.B0.D0.B3.D0.BE.D0.B4.D0.B6.D0.B5.D0.BD.D0.BD.D1.8F)
    *   [3.1 Removable media](#Removable_media)
    *   [3.2 NFS Network mounts](#NFS_Network_mounts)
    *   [3.3 Samba](#Samba)
    *   [3.4 FTP and SSH (with Fuse)](#FTP_and_SSH_.28with_Fuse.29)
        *   [3.4.1 Remote FTP](#Remote_FTP)
        *   [3.4.2 Remote SSH](#Remote_SSH)
*   [4 Starting AutoFS](#Starting_AutoFS)
*   [5 Troubleshooting and tweaks](#Troubleshooting_and_tweaks)
    *   [5.1 Optional parameters](#Optional_parameters)
    *   [5.2 Identify multiple devices](#Identify_multiple_devices)
    *   [5.3 AutoFS permissions](#AutoFS_permissions)
*   [6 External links and resources](#External_links_and_resources)
*   [7 Alternatives to AutoFS](#Alternatives_to_AutoFS)

## Вступ

Стаття пояснює процес інсталяції та налагодження AutoFS, пакета для автоматичного підключення зовнішніх носіїв та ресурсів мережі.

## Інсталяція

Встановіть пакет Autofs:

```
# pacman -S autofs

```

Загрузіть модуль autofs4 з правами адміністратора:

```
# modprobe autofs4

```

## Налагодження

AutoFS вікористовує для конфігурації файли шаблонів, що розміщені в `/etc/autofs`. Головний шаблон називається auto.master, він може звертатися до одного чи більше шаблонів для окремих типів медіа.

*   Відкрийте файл `/etc/autofs/auto.master` у вашому улюбленому редакторі, Ві побачите щось подібне до цього:

```
/var/autofs/misc	/etc/autofs/auto.misc
/var/autofs/net	/etc/autofs/auto.net

```

Перше значення в цій строці позначає основну деректорію, до якої підключаються носії, друга позначка - це шаблон, що використовується. The default base path is /var/autofs, but you can change this to any other location you prefer. For instance:

```
/media/misc     /etc/autofs/auto.misc     --timeout=5,ghost
/media/net      /etc/autofs/auto.net      --timeout=60,ghost

```

The optional parameter `timeout` sets the amount of seconds after which to unmount directories. The parameter `ghost` determines that configured mounts will always be shown, instead of only when they are inserted and accessed. This can be useful since you won't have to remember or guess the names of removable media and network shares.

The target directories have to exist on your system and need to be empty, since their contents will be swapped with the dynamically loaded media. This procedure is however non-destructive, so if you accidentally automount into a live directory you can just change the location in auto.master and restart AutoFS to regain the original contents.

**Note:** Make sure there is an empty line on the end of template files (press ENTER after last word). If there is no correct EOF line, the AutoFS daemon won't properly load.

*   Open the file `/etc/nsswitch.conf` and add an entry for automount:

```
automount: files

```

### Removable media

*   Open `/etc/autofs/auto.misc` to add, remove or edit miscellaneous devices. For instance:

```
#kernel   -ro                                        ftp.kernel.org:/pub/linux
#boot     -fstype=ext2                               :/dev/hda1
usbstick  -fstype=auto,async,nodev,nosuid,umask=000  :/dev/sdb1
cdrom     -fstype=iso9660,ro                         :/dev/cdrom
#floppy   -fstype=auto                               :/dev/fd0

```

If you have a CD/DVD combo-drive you can change the cdrom line with "-fstype=auto" to have the media type autodetected.

### NFS Network mounts

AutoFS provides a new way of automatically discovering and mounting NFS-shares on remote servers (the AutoFS network template in `/etc/autofs/auto.net` has been removed in autofs5). To enable automagic discovery and mounting of network shares from all accessible servers without any further configuration, you'll need to add the following to the `/etc/autofs/auto.master` file:

```
/net -hosts --timeout=60

```

Each host name needs to be resolveable, e.g. the name an IP address in `/etc/hosts` or via DNS.

For instance, if you have a remote server *fileserver* with an NFS share named */home/share*, you can just access the share by typing:

```
# cd /net/fileserver/home/share

```

**Note:** Please note that *ghosting*, i.e. automatically creating directory placeholders before mounting shares is enabled by default, although AutoFS installation notes claim to remove that option from `/etc/conf.d/autofs` in order to start the AutoFS daemon.

The `-hosts` option uses a similar mechanism as the *showmount* command to detect remote shares. You can see the exported shares by typing:

```
# showmount <servername> -e 

```

Replacing *<servername>* with the name of your own server.

### Samba

The Arch package does not provide any samba or cifs templates/scripts (23.07.2009), but the following should work for single shares:

add the following to `/etc/autofs/auto.master`

```
/media/[my_server] /etc/autofs/auto.[my_server]

```

and then create a file `/etc/autofs/auto.[my_server]`

```
[my_share] -fstype=cifs,[other_options] ://[my_server_ip]/[my_share]

```

### FTP and SSH (with Fuse)

Remote FTP and SSH servers can be accessed seamlessly with AutoFS using Fuse, a virtual file system layer.

#### Remote FTP

First, install the curlftpfs package from the Community repository:

```
# pacman -S curlftpfs

```

Load the Fuse module:

```
# modprobe fuse

```

Add fuse to the *modules* array in `/etc/rc.conf` to load it on each system boot.

Next, add a new entry for FTP servers in `/etc/autofs/auto.master`:

```
/media/ftp        /etc/autofs/auto.ftp    --timeout=60,ghost

```

Create the file `/etc/autofs/auto.ftp` and add a server using the `[ftp://myuser:mypassword@host:port/path](ftp://myuser:mypassword@host:port/path)` format:

```
servername -fstype=curl,allow_other    :ftp\://myuser\:mypassword\@remoteserver

```

Note: Your passwords are plainly visible for anyone that can run *df* (only for mounted servers) or view the file `/etc/autofs/auto.ftp`. If you want slightly more security you can create the file `~root/.netrc` and add the passwords there. Passwords are still plain text, but you can have mode 600, and *df* command will not show them (mounted or not). This method is also less sensitive to special characters (that else must be escaped) in the passwords. The format is:

```
machine remoteserver  
login myuser
password mypassword

```

The line in `/etc/autofs/auto.ftp` looks like this without user and password:

```
servername -fstype=curl,allow_other    :ftp\://remoteserver

```

Create the file `/sbin/mount.curl` with this code:

```
#! /bin/sh
curlftpfs $1 $2 -o $4,disable_eprt

```

Create the file `/sbin/umount.curl` with this code:

```
#! /bin/sh
fusermount -u $1

```

Set the permissions for both files:

```
# chmod 755 /sbin/mount.curl
# chmod 755 /sbin/umount.curl

```

After a restart your new FTP server should be accessible through `/media/ftp/servername`

#### Remote SSH

These are basic instructions to access a remote filesystem over SSH with AutoFS.

**Note:** The example below does not use an ssh-passphrase to simplify the installation procedure, please note that this may be a security risk in case your local system gets compromised.

Install the sshfs package from the Extra repository:

```
# pacman -S sshfs

```

Load the Fuse module:

```
# modprobe fuse

```

Add fuse to the *modules* array in `/etc/rc.conf` to load it on each system boot:

Install OpenSSH:

```
# pacman -S openssh

```

Generate an SSH keypair:

```
# ssh-keygen -t dsa

```

When the generator ask for a passphrase, just press enter. Using SSH keys without a passphrase is less secure, yet running AutoFS together with passphrases poses some additional difficulties which are not (yet) covered in this article.

Next, copy the public key to the remote SSH server:

```
# ssh-copy-id -i ~/.ssh/id_dsa.pub username@remotehost

```

Copy the private key to the root's home directory so that AutoFS can find it:

```
# sudo cp ~/.ssh/id_dsa /root/.ssh/id_dsa

```

The above is a workaround since AutoFS runs as root and has no default access to the user's home directory containing the private key.

See that you can login to the remote server without entering a password:

```
# ssh username@remotehost

```

Create a new entry for SSH servers in `/etc/autofs/auto.master`:

```
/media/ssh		/etc/autofs/auto.ssh	--timeout=60,ghost

```

Create the file `/etc/autofs/auto.ssh` and add an SSH server:

```
servername     -fstype=fuse,rw,nodev,nonempty,allow_other,max_read=65536 :sshfs\#username@host\:/

```

After a restart your SSH server should be accessible through `/media/ssh/servername`

## Starting AutoFS

*   When you are done configuring, launch the AutoFS daemon as root:

```
# /etc/rc.d/autofs start

```

To start the daemon on boot you can add `autofs` to the DAEMONS array in /etc/rc.conf, and `autofs4` to the modules array in the same file.

If you change the auto.master template while AutoFS is running, you will have to restart the daemon for the changes to become effective:

```
# /etc/rc.d/autofs restart

```

Devices are now automatically mounted when they are accessed, they will remain mounted as long as you access them.

## Troubleshooting and tweaks

This section contains a few solutions for common issues with AutoFS.

### Optional parameters

You can set parameters like `timeout` systemwide for all AutoFS media in `/etc/conf.d/autofs`:

*   Open the `/etc/conf.d/autofs` file and edit the daemonoptions line:

```
daemonoptions='--timeout=5'

```

*   To enable logging (default is no logging at all), add `--verbose` to the daemonoptions line in `/etc/conf.d/autofs`, e.g.:

```
daemonoptions='--verbose --timeout=5'

```

After restarting the autofs daemon, verbose output is visible in /var/log/daemon.log.

### Identify multiple devices

If you use multiple usb drives/sticks and want to easily tell them apart, you can use AutoFS to set up the mount points and udev to create distinct names for your usb drives. See [Map Custom Device Entries with udev](/index.php/Map_Custom_Device_Entries_with_udev "Map Custom Device Entries with udev") for instructions on setting up udev rules.

### AutoFS permissions

If AutoFS isn't working for you, make sure that the permissions of the templates files are correct, otherwise AutoFS will not start. This may happen if you backed up your configuration files in a manner which did not preserve file modes. Here are what the modes should be on the configuration files:

*   0644 - /etc/autofs/auto.master
*   0644 - /etc/autofs/auto.media
*   0644 - /etc/autofs/auto.misc
*   0644 - /etc/conf.d/autofs

In general, scripts (like previous auto.net) should have executable (chown a+x filename) bits set and lists of mounts shouldn't.

If you are getting errors in /var/log/daemon.log similar to this, you have a permissions problem:

```
May  7 19:44:16 peterix automount[15218]: lookup(program): lookup for petr failed
May  7 19:44:16 peterix automount[15218]: failed to mount /media/cifs/petr

```

## External links and resources

*   The original information on this page is based on this topic: [https://bbs.archlinux.org/viewtopic.php?t=7630](https://bbs.archlinux.org/viewtopic.php?t=7630), with additional information found on this page: [http://libranet.com/support/2.8/0381](http://libranet.com/support/2.8/0381)
*   FTP and SFTP usage with AutoFS is based on this Gentoo Wiki article: [http://en.gentoo-wiki.com/wiki/Mounting_SFTP_and_FTP_shares](http://en.gentoo-wiki.com/wiki/Mounting_SFTP_and_FTP_shares)
*   More information on SSH can be found on the [SSH](/index.php/SSH "SSH") and [Using SSH Keys](/index.php/Using_SSH_Keys "Using SSH Keys") pages of this wiki.

## Alternatives to AutoFS

*   [Thunar Volume Manager](/index.php/Thunar_Volume_Manager "Thunar Volume Manager") is an automount system for users of the Thunar file manager.
*   Pcmanfm-fuse is a lightweight file manager with built-in support for accessing remote shares: [https://aur.archlinux.org/packages.php?ID=22992](https://aur.archlinux.org/packages.php?ID=22992)