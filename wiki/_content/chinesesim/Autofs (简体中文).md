本文将概述AutoFS的配置方法,当未被挂载的可移除文件系统或是网络共享的文件系统被用户访问时，这个软件包可以提供的自动挂载的支持。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 Configuration](#Configuration)
    *   [2.1 Removable media](#Removable_media)
    *   [2.2 NFS network mounts](#NFS_network_mounts)
    *   [2.3 Samba](#Samba)
    *   [2.4 FTP and SSH (with FUSE)](#FTP_and_SSH_.28with_FUSE.29)
        *   [2.4.1 Remote FTP](#Remote_FTP)
        *   [2.4.2 Remote SSH](#Remote_SSH)
*   [3 MTP](#MTP)
*   [4 Troubleshooting and tweaks](#Troubleshooting_and_tweaks)
    *   [4.1 Using NIS](#Using_NIS)
    *   [4.2 Optional parameters](#Optional_parameters)
    *   [4.3 Identify multiple devices](#Identify_multiple_devices)
    *   [4.4 AutoFS permissions](#AutoFS_permissions)
    *   [4.5 fusermount problems](#fusermount_problems)
*   [5 Alternatives to AutoFS](#Alternatives_to_AutoFS)
*   [6 See also](#See_also)

## 安装

[autofs](https://www.archlinux.org/packages/?name=autofs) 可以从[官方源](/index.php/Official_repositories "Official repositories")中[安装](/index.php/Pacman "Pacman").

**提示:** 你将不再需要载入`autofs4` 模式.

## Configuration

AutoFS uses template files for configuration which are located in `/etc/autofs` The main template is called `auto.master`, which can point to one or more other templates for specific media types.

*   Open the file `/etc/autofs/auto.master` with your favorite editor, you will see something similar to this:

 `/etc/autofs/auto.master`  `#/media /etc/autofs/auto.media` 

The first value on each line determines the base directory under which all the media in a template are mounted, the second value is which template to use. The default base path is `/media`, but you can change this to any other location you prefer. For instance:

 `/etc/autofs/auto.master` 

```
/media/misc     /etc/autofs/auto.misc     --timeout=5
/media/net      /etc/autofs/auto.net      --timeout=60
```

**Note:** Make sure there is an empty line on the end of template files (press `ENTER` after last word). If there is no correct EOF (end of file) line, the AutoFS daemon won't properly load.

The optional parameter `timeout` sets the amount of seconds after which to unmount directories.

The base directory will be created if it does not exist on your system. The base directory will be mounted on to load the dynamically loaded media, which means any content in the base directory will not be accessible while autofs is on. This procedure is however non-destructive, so if you accidentally automount into a live directory you can just change the location in `auto.master` and restart AutoFS to regain the original contents.

If you still want to automount to a target non-empty directory and want to have the original files available even after the dynamically loaded directories are mounted, you can use autofs to mount them to another directory (e.g. /var/autofs/net) and create soft links.

```
# ln -s /var/autofs/net/share_name /media/share_name

```

Alternatively, you can have autofs mount your media to a specific folder, rather than inside a common folder.

 `/etc/autofs/auto.master`  `/-     /etc/autofs/auto.template`  `/etc/autofs/auto.template` 

```
/path/to/folder     -options :/device/path
/home/user/usbstick  -fstype=auto,async,nodev,nosuid,umask=000  :/dev/sdb1
```

**Note:** This can cause problems with resources getting locked if the connection to the share is lost. When trying to access the folder, programs will get locked into waiting for a response, and either the connection has to be restored or the process has to be forcibly killed before unmounting is possible. To mitigate this, only use if you will always be connected to the share, and don't use your home folder or other commonly used folders lest your file browser reads ahead into the disconnected folder

*   Open the file `/etc/nsswitch.conf` and add an entry for automount:

```
automount: files

```

*   When you are done configuring your templates (see below), launch the AutoFS daemon as root:

```
# systemctl start autofs

```

To start the daemon on boot:

```
# systemctl enable autofs

```

Devices are now automatically mounted when they are accessed, they will remain mounted as long as you access them.

### Removable media

*   Open `/etc/autofs/auto.misc` to add, remove or edit miscellaneous devices. For instance:

 `/etc/autofs/auto.misc` 

```
#kernel   -ro                                        ftp.kernel.org:/pub/linux
#boot     -fstype=ext2                               :/dev/hda1
usbstick  -fstype=auto,async,nodev,nosuid,umask=000  :/dev/sdb1
cdrom     -fstype=iso9660,ro                         :/dev/cdrom
#floppy   -fstype=auto                               :/dev/fd0

```

If you have a CD/DVD combo-drive you can change the `cdrom` line with `-fstype=auto` to have the media type autodetected.

### NFS network mounts

AutoFS provides a new way of automatically discovering and mounting [NFS](/index.php/NFS "NFS")-shares on remote servers (the AutoFS network template in `/etc/autofs/auto.net` has been removed in autofs5). To enable automagic discovery and mounting of network shares from all accessible servers without any further configuration, you'll need to add the following to the `/etc/autofs/auto.master` file:

```
/net -hosts --timeout=60

```

**Each host name needs to be resolveable, e.g. the name an IP address in `/etc/hosts` or via [DNS](https://en.wikipedia.org/wiki/Domain_Name_System "wikipedia:Domain Name System") and please make sure you have at least [nfs-utils](https://www.archlinux.org/packages/?name=nfs-utils) installed and working. You also have to enable RPC (systemctl start|enable rpcbind) to browse shared Folders.**

For instance, if you have a remote server _fileserver_ with an NFS share named _/home/share_, you can just access the share by typing:

```
# cd /net/fileserver/home/share

```

**Note:** Please note that _ghosting_, i.e. automatically creating directory placeholders before mounting shares is enabled by default, although AutoFS installation notes claim to remove that option from `/etc/conf.d/autofs` in order to start the AutoFS daemon.

The `-hosts` option uses a similar mechanism as the `showmount` command to detect remote shares. You can see the exported shares by typing:

```
# showmount <servername> -e 

```

Replacing _<servername>_ with the name of your own server.

### Samba

The Arch package does not provide any [Samba](/index.php/Samba "Samba") or CIFS templates/scripts (23.07.2009), but the following should work for single shares:

add the following to `/etc/autofs/auto.master`

```
/media/[my_server] /etc/autofs/auto.[my_server]

```

and then create a file `/etc/autofs/auto.[my_server]`

```
[any_name] -fstype=cifs,[other_options] ://[remote_server]/[remote_share_name]

```

You can specify a user name and password to use with the share in the other_options section

```
[any_name] -fstype=cifs,username=[username],password=[password],[other_options] ://[remote_server]/[remote_share_name]

```

**Note:** Escape $, and other characters, with a backslash when neccessary.

### FTP and SSH (with FUSE)

Remote FTP and [SSH](/index.php/SSH "SSH") servers can be accessed seamlessly with AutoFS using [FUSE](https://en.wikipedia.org/wiki/Filesystem_in_Userspace "wikipedia:Filesystem in Userspace"), a virtual file system layer.

#### Remote FTP

First, install the [curlftpfs](https://www.archlinux.org/packages/?name=curlftpfs) package. Load the **fuse** module:

```
# modprobe fuse

```

Create a `/etc/modules-load.d/fuse.conf` file containg `fuse` to load it on each system boot.

Next, add a new entry for FTP servers in `/etc/autofs/auto.master`:

```
/media/ftp        /etc/autofs/auto.ftp    --timeout=60

```

Create the file `/etc/autofs/auto.ftp` and add a server using the `[ftp://myuser:mypassword@host:port/path](ftp://myuser:mypassword@host:port/path)` format:

```
servername -fstype=curl,rw,allow_other,nodev,nonempty,noatime    :ftp\://myuser\:mypassword\@remoteserver

```

**Note:** Your passwords are plainly visible for anyone that can run `df` (only for mounted servers) or view the file `/etc/autofs/auto.ftp`.

If you want slightly more security you can create the file `~root/.netrc` and add the passwords there. Passwords are still plain text, but you can have mode 600, and `df` command will not show them (mounted or not). This method is also less sensitive to special characters (that else must be escaped) in the passwords. The format is:

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

 `/sbin/mount.curl` 

```
 #! /bin/sh
 curlftpfs $1 $2 -o $5,disable_eprt

```

Create the file `/sbin/umount.curl` with this code:

 `/sbin/umount.curl` 

```
 #! /bin/sh
 fusermount -u $1

```

Set the permissions for both files:

```
# chmod 755 /sbin/mount.curl
# chmod 755 /sbin/umount.curl

```

After a restart your new FTP server should be accessible through `/media/ftp/servername`.

#### Remote SSH

These are basic instructions to access a remote filesystem over [SSH](/index.php/SSH "SSH") with AutoFS.

**Note:** The example below does not use an ssh-passphrase to simplify the installation procedure, please note that this may be a security risk in case your local system gets compromised.

Install the [sshfs](https://www.archlinux.org/packages/?name=sshfs) package.

Load the `fuse` module:

```
# modprobe fuse

```

Create a `/etc/modules-load.d/fuse.conf` file containg `fuse` to load it on each system boot if you have not one yet.

Install [openssh](https://www.archlinux.org/packages/?name=openssh).

Generate an [SSH keypair](/index.php/Using_SSH_Keys "Using SSH Keys"):

```
# ssh-keygen -t dsa

```

When the generator ask for a passphrase, just press `ENTER`. Using SSH keys without a passphrase is less secure, yet running AutoFS together with passphrases poses some additional difficulties which are not (yet) covered in this article.

Next, copy the public key to the remote SSH server:

```
# ssh-copy-id -i /home/username/.ssh/id_dsa.pub username@remotehost

```

See that you can login to the remote server without entering a password:

```
# sudo ssh -i /home/username/.ssh/id_dsa username@remotehost

```

**Note:** The above command is needed to add the remote server to the root's list of `known_hosts`. Alternatively, hosts can be added to `/etc/ssh/ssh_known_hosts`.

Create a new entry for SSH servers in `/etc/autofs/auto.master`:

```
/media/ssh		/etc/autofs/auto.ssh	--timeout=60

```

Create the file `/etc/autofs/auto.ssh` and add an SSH server:

 `/etc/autofs/auto.ssh`  `servername     -fstype=fuse,rw,allow_other,IdentityFile=/home/username/.ssh/id_dsa :sshfs\#username@host\:/` 

After a restart your SSH server should be accessible through `/media/ssh/servername`.

## MTP

Media Transfer Protocol ([MTP](/index.php/MTP "MTP")) is used in some Android devices.

Install the [mtpfs](https://www.archlinux.org/packages/?name=mtpfs) package.

Create a new entry for MTP Device in `/etc/autofs/auto.misc`:

```
android -fstype=fuse,allow_other,umask=000     :mtpfs

```

## Troubleshooting and tweaks

This section contains a few solutions for common issues with AutoFS.

### Using NIS

Version 5.0.5 of AutoFS has more advanced support for [NIS](/index.php/NIS "NIS"). To use AutoFS together with NIS, add `yp:` in front of the template names in `/etc/autofs/auto.master`:

```
/home   yp:auto_home    --timeout=60 
/sbtn   yp:auto_sbtn    --timeout=60
+auto.master

```

On earlier versions of NIS (before 5.0.4), you should add `nis` to `/etc/nsswitch.conf`:

```
automount: files nis

```

### Optional parameters

You can set parameters like `timeout` systemwide for all AutoFS media in `/etc/conf.d/autofs`:

*   Open the `/etc/conf.d/autofs` file and edit the `daemonoptions` line:

```
daemonoptions='--timeout=5'

```

*   To enable logging (default is no logging at all), add `--verbose` to the `daemonoptions` line in `/etc/conf.d/autofs` e.g.:

```
daemonoptions='--verbose --timeout=5'

```

After restarting the `autofs` daemon, verbose output is visible in `/var/log/daemon.log`.

### Identify multiple devices

If you use multiple USB drives/sticks and want to easily tell them apart, you can use AutoFS to set up the mount points and [Udev](/index.php/Udev "Udev") to create distinct names for your USB drives. See [udev#Setting static device names](/index.php/Udev#Setting_static_device_names "Udev") for instructions on setting up Udev rules.

### AutoFS permissions

If AutoFS isn't working for you, make sure that the permissions of the templates files are correct, otherwise AutoFS will not start. This may happen if you backed up your configuration files in a manner which did not preserve file modes. Here are what the modes should be on the configuration files:

*   0644 - /etc/autofs/auto.master
*   0644 - /etc/autofs/auto.media
*   0644 - /etc/autofs/auto.misc
*   0644 - /etc/conf.d/autofs

In general, scripts (like previous `auto.net`) should have executable (`chown a+x filename`) bits set and lists of mounts shouldn't.

If you are getting errors in `/var/log/daemon.log` similar to this, you have a permissions problem:

```
May  7 19:44:16 peterix automount[15218]: lookup(program): lookup for petr failed
May  7 19:44:16 peterix automount[15218]: failed to mount /media/cifs/petr

```

### fusermount problems

With certain versions of util-linux, you may not be able to unmount a fuse file system drive mounted by autofs, even if you use the "user=" option. See the discussion here: [http://fuse.996288.n3.nabble.com/Cannot-umount-as-non-root-user-anymore-tp689p697.html](http://fuse.996288.n3.nabble.com/Cannot-umount-as-non-root-user-anymore-tp689p697.html)

## Alternatives to AutoFS

*   [Systemd](/index.php/Systemd "Systemd") can automount filesystems upon demand; see [here](/index.php/Systemd#Automount "Systemd") for the description and the article on [sshfs](/index.php/Sshfs#On_demand "Sshfs") for an example.
*   [Thunar Volume Manager](/index.php/Thunar#Thunar_Volume_Manager "Thunar") is an automount system for users of the [Thunar](/index.php/Thunar "Thunar") file manager.
*   Pcmanfm-fuse is a lightweight file manager with built-in support for accessing remote shares: [https://aur.archlinux.org/packages.php?ID=22992](https://aur.archlinux.org/packages.php?ID=22992)
*   [udiskie](/index.php/Udiskie "Udiskie") is a minimalistic automatic disk mounting service using udisks

## See also

*   AutoFS configuration cookbook: [http://www.autofs.org/](http://www.autofs.org/)
*   An Ubuntu-based walk though of AutoFS with some useful info: [http://blogging.dragon.org.uk/index.php/howtos/howto-setup-and-configure-autofs](http://blogging.dragon.org.uk/index.php/howtos/howto-setup-and-configure-autofs)
*   FTP and SFTP usage with AutoFS is based on this Gentoo Wiki article: [http://en.gentoo-wiki.com/wiki/Mounting_SFTP_and_FTP_shares](http://en.gentoo-wiki.com/wiki/Mounting_SFTP_and_FTP_shares)
*   More information on SSH can be found on the [SSH](/index.php/SSH "SSH") and [Using SSH Keys](/index.php/Using_SSH_Keys "Using SSH Keys") pages of this wiki.