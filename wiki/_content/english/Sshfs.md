You can use sshfs to mount a remote system - accessible via [SSH](/index.php/SSH "SSH") - to a local folder, so you will be able to do any operation on the mounted files with any tool (copy, rename, edit with vim, etc.). Using sshfs instead of shfs is generally preferred as a new version of shfs has not been released since 2004.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Mounting](#Mounting)
    *   [1.2 Unmounting](#Unmounting)
*   [2 Chrooting](#Chrooting)
*   [3 Helpers](#Helpers)
*   [4 Automounting](#Automounting)
    *   [4.1 On demand](#On_demand)
    *   [4.2 On boot](#On_boot)
    *   [4.3 Secure user access](#Secure_user_access)
*   [5 Options](#Options)
*   [6 Troubleshooting](#Troubleshooting)
    *   [6.1 Checklist](#Checklist)
    *   [6.2 Connection reset by peer](#Connection_reset_by_peer)
    *   [6.3 Remote host has disconnected](#Remote_host_has_disconnected)
    *   [6.4 Freezing apps (e.g. Nautilus, Gedit)](#Freezing_apps_.28e.g._Nautilus.2C_Gedit.29)
    *   [6.5 Shutdown hangs when sshfs is mounted](#Shutdown_hangs_when_sshfs_is_mounted)
*   [7 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") [sshfs](https://www.archlinux.org/packages/?name=sshfs) from the [official repositories](/index.php/Official_repositories "Official repositories").

### Mounting

**Tip:** [Google Authenticator](/index.php/Google_Authenticator "Google Authenticator") can be used with sshfs as additional security.

Before attempting to mount a directory, make sure the file permissions on the target directory allow your user correct access. To mount, invoke `sshfs` to mount a remote directory:

```
$ sshfs _USERNAME@HOSTNAME_OR_IP:/REMOTE_PATH LOCAL_MOUNT_POINT SSH_OPTIONS_

```

For example:

```
$ sshfs sessy@mycomputer:/remote/path /local/path -C -p 9876 -o allow_other

```

Where `-p 9876` stands for the port number, `-C` use compression and `-o allow_other` to allow non-rooted users have read/write access.

**Note:** Users may also define a non-standard port on a host-by-host basis in `~/.ssh/config` to avoid appending the -p switch here. For more information see [Secure Shell#Saving connection data in ssh config](/index.php/Secure_Shell#Saving_connection_data_in_ssh_config "Secure Shell").

SSH will ask for the password, if needed. If you do not want to type in the password multiple times a day, read: [How to Use RSA Key Authentication with SSH](http://linuxmafia.com/~karsten/Linux/FAQs/sshrsakey.html) or [Using SSH Keys](/index.php/Using_SSH_Keys "Using SSH Keys").

**Tip:** To quickly mount a remote dir, do some file-management and unmount it, put this in a script:

```
sshfs USERNAME@HOSTNAME_OR_IP:/REMOTE_PATH LOCAL_MOUNT_POINT SSH_OPTIONS
mc LOCAL_MOUNT_POINT
fusermount -u LOCAL_MOUNT_POINT

```

This will mount the remote directory, launch MC, and unmount it when you exit.

### Unmounting

To unmount the remote system:

```
$ fusermount -u _LOCAL_MOUNT_POINT_

```

Example:

```
$ fusermount -u /mnt/sessy

```

## Chrooting

You may want to jail a (specific) user to a directory by editing `/etc/ssh/sshd_config`:

 `/etc/ssh/sshd_config` 

```
.....
Match User someuser 
       ChrootDirectory /chroot/%u
       ForceCommand internal-sftp #to restrict the user to sftp only
       AllowTcpForwarding no
       X11Forwarding no
.....
```

**Note:** The chroot directory **must** be owned by root, otherwise you will not be able to connect. For more info check the manpages for `Match, ChrootDirectory` and `ForceCommand`.

## Helpers

If you often need to mount sshfs filesystems you may be interested in using an sshfs helper, such as [sftpman](/index.php/Sftpman "Sftpman").

It provides a command-line and a GTK frontend, to make mounting and unmounting a simple one click/command process.

## Automounting

Automounting can happen on boot, or on demand (when accessing the directory). For both, the setup happens in `/etc/[fstab](/index.php/Fstab "Fstab")`.

**Note:** Be mindful that automounting is done through the root user, therefore you cannot use Hosts configured in `.ssh/config` of your normal user.

To let root user use an SSH key of a normal user, specify its full path in option `IdentityFile`.

**And most importantly**, use each sshfs mount at least once manually **while root** so the host's signature is added to the `.ssh/known_hosts` file.

### On demand

With systemd on-demand mounting is possible using `/etc/fstab` entries.

Example:

```
user@host:/remote/folder /mount/point  fuse.sshfs noauto,x-systemd.automount,_netdev,users,idmap=user,IdentityFile=/home/user/.ssh/id_rsa,allow_other,reconnect 0 0

```

The important mount options here are _noauto,x-systemd.automount,_netdev_.

*   _noauto_ tells it not to mount at boot
*   _x-systemd.automount_ does the on-demand magic
*   __netdev_ tells it that it is a network device, not a block device (without it "No such device" errors might happen)

**Tip:**

There are two other ways to do this. Both do not require editing /etc/fstab to add a new mountpoint. Instead, regular users can create one by simply attempting to access it (with e. g. something like `ls ~/mnt/ssh/[user@]yourremotehost[:port]`):

*   [autosshfs-git](https://aur.archlinux.org/packages/autosshfs-git/) uses AutoFS. Users need to be enabled to use it with `autosshfs-user`.
*   [afuse](https://aur.archlinux.org/packages/afuse/) is a general-purpose userspace automounter for FUSE filesystems. It works well with sshfs. No user-activation is necessary. Example invocation: `afuse -o mount_template='sshfs -o ServerAliveInterval=10 -o reconnect %r:/ %m' -o unmount_template='fusermount -u -z %m' ~/mnt/ssh`

### On boot

An example on how to use sshfs to mount a remote filesystem through `/etc/[fstab](/index.php/Fstab "Fstab")`

```
USERNAME@HOSTNAME_OR_IP:/REMOTE/DIRECTORY  /LOCAL/MOUNTPOINT  fuse.sshfs  defaults,_netdev  0  0

```

Take for example the _fstab_ line

```
llib@192.168.1.200:/home/llib/FAH  /media/FAH2  fuse.sshfs  defaults,_netdev  0  0

```

The above will work automatically if you are using an SSH key for the user. See [Using SSH Keys](/index.php/Using_SSH_Keys "Using SSH Keys").

If you want to use sshfs with multiple users:

```
user@domain.org:/home/user  /media/user   fuse.sshfs    defaults,allow_other,_netdev    0  0

```

Again, it is important to set the __netdev_ mount option to make sure the network is available before trying to mount.

### Secure user access

When automounting via `/etc/[fstab](/index.php/Fstab "Fstab")`, the filesystem will generally be mounted by root. By default, this produces undesireable results if you wish access as an ordinary user and limit access to other users.

An example mountpoint configuration:

```
USERNAME@HOSTNAME_OR_IP:/REMOTE/DIRECTORY  /LOCAL/MOUNTPOINT  fuse.sshfs noauto,x-systemd.automount,_netdev,user,idmap=user,transform_symlinks,identityfile=/home/USERNAME/.ssh/id_rsa,allow_other,default_permissions,uid=USER_ID_N,gid=USER_GID_N 0 0

```

Summary of the relevant options:

*   _allow_other_ - Allow other users than the mounter (i.e. root) to access the share.
*   _default_permissions_ - Allow kernel to check permissions, i.e. use the actual permissions on the remote filesystem. This allows prohibiting access to everybody otherwise granted by _allow_other_.
*   _uid_, _gid_ - set reported ownership of files to given values; _uid_ is the numeric user ID of your user, _gid_ is the numeric group ID of your user.

## Options

sshfs can automatically convert your local and remote user IDs.

Add the _idmap_ option with _user_ value to translate UID of connecting user:

```
# sshfs -o idmap=user sessy@mycomputer:/home/sessy /mnt/sessy -C -p 9876

```

This will map UID of the remote user "sessy" to the local user, who runs this process ("root" in the above example) and GID remains unchanged. If you need more precise control over UID and GID translation, look at the options _idmap=file_ and _uidfile_ and _gidfile_.

## Troubleshooting

### Checklist

Read the [SSH Checklist](https://wiki.archlinux.org/index.php/Secure_Shell#Checklist) Wiki entry first. Further issues to check are:

1\. Is your SSH login sending additional information from server's `/etc/issue` file e.g.? This might confuse SSHFS. You should temporarily deactivate server's `/etc/issue` file:

```
$ mv /etc/issue /etc/issue.orig

```

2\. Keep in mind that most SSH related troubleshooting articles you will find on the web are **not** Systemd related. Often `/etc/fstab` definitions wrongly begin with `_sshfs#_user@host:/mnt/server/folder ... fuse ...` instead of using the syntax `user@host:/mnt/server/folder ... fuse._sshfs_ ... _x-systemd_, ...`.

3\. Check that the owner of server's source folder and content is owned by the server's user.

```
$ chown -R USER_S: /mnt/servers/folder

```

4\. The server's user ID can be different from the client's one. Obviously both user names have to be the same. You just have to care for the client's user IDs. SSHFS will translate the UID for you with the following mount options:

```
uid=_USER_C_ID_,gid=_GROUP_C_ID_

```

5\. Check that the client's target mount point (folder) is owned by the client user. This folder should have the same user ID as defined in SSHFS's mount options.

```
$ chown -R USER_C: /mnt/client/folder

```

6\. Check that the client's mount point (folder) is empty. By default you cannot mount SSHFS folders to non-empty folders.

7\. If you want to automount SSH shares by using an SSH public key authentication (no password) via `/etc/fstab`, you can use this line as an example:

```
_USER_S_@_SERVER_:/mnt/on/server      /nmt/on/client        fuse.sshfs      x-systemd.automount,_netdev,user,idmap=user,transform_symlinks,identityfile=/home/_USER_C_/.ssh/id_rsa,allow_other,default_permissions,uid=_USER_C_ID_,gid=_GROUP_C_ID_,umask=0   0 0

```

Considering the following example settings ...

SERVER = Server host name (serv) USER_S = Server user name (pete) USER_C = Client user name (pete) USER_S_ID = Server user ID (1004) USER_C_ID = Client user ID (1000) GROUP_C_ID = Client user's group ID (100)

you get the client user's ID and group ID with

```
$ id USERNAME

```

this is the final SSHFS mount row in `/etc/fstab`;

```
pete@serv:/mnt/on/server      /nmt/on/client        fuse.sshfs      x-systemd.automount,_netdev,user,idmap=user,transform_symlinks,identityfile=/home/pete/.ssh/id_rsa,allow_other,default_permissions,uid=1004,gid=1000,umask=0   0 0

```

8\. If you know another issue for this checklist please add it the list above.

### Connection reset by peer

*   If you are trying to access the remote system with a hostname, try using its IP address, as it can be a domain name solving issue. Make sure you edit `/etc/hosts` with the server details.
*   If you are using non-default key names and are passing it as `-i .ssh/my_key`, this will not work. You have to use `-o IdentityFile=/home/user/.ssh/my_key`, with the full path to the key.
*   If your /root/.ssh/config is a symlink, you will be getting this error as well. See [this serverfault topic](http://serverfault.com/questions/507748/bad-owner-or-permissions-on-root-ssh-config)
*   Adding the option '`sshfs_debug`' (as in '`sshfs -o sshfs_debug user@server ...`') can help in resolving the issue.
*   If that doesn't reveal anything useful, you might also try adding the option '`debug`'
*   If you are trying to sshfs into a router running DD-WRT or the like, there is a solution [here](http://www.dd-wrt.com/wiki/index.php/SFTP_with_DD-WRT). (note that the -osftp_server=/opt/libexec/sftp-server option can be used to the sshfs command in stead of patching dropbear)
*   Old Forum thread: [sshfs: Connection reset by peer](https://bbs.archlinux.org/viewtopic.php?id=27613)
*   Make sure your user can log into the server (especially when using AllowUsers)
*   Make sure `Subsystem sftp /usr/lib/ssh/sftp-server` is enabled in `/etc/ssh/sshd_config`.

**Note:** When providing more than one option for sshfs, they must be comma separated. Like so: '`sshfs -o sshfs_debug,IdentityFile=</path/to/key> user@server ...`')

### Remote host has disconnected

If you receive this message directly after attempting to use _sshfs_:

*   First make sure that the **remote** machine has _sftp_ installed! It will not work, if not.

**Tip:** If your remote server is running OpenWRT: `opkg install openssh-sftp-server` will do the trick

*   Then, try checking the path of the `Subsystem` listed in `/etc/ssh/sshd_config` on the remote machine to see, if it is valid. You can check the path to it with `find / -name sftp-server`.

For Arch Linux the default value in `/etc/ssh/sshd_config` is `Subsystem sftp /usr/lib/ssh/sftp-server`.

### Freezing apps (e.g. Nautilus, Gedit)

**Note:** This prevents the recently used file list from being populated and may lead to possible write errors.

If you experience freezing/hanging (stopped responding) applications, you may need to disable write-access to the `~/recently-used.xbel` file.

```
# chattr +i /home/USERNAME/.local/share/recently-used.xbel

```

See the following [bug report](https://bugs.archlinux.org/task/40260) for more details and/or solutions.

### Shutdown hangs when sshfs is mounted

Systemd may hang on shutdown if an sshfs mount was mounted manually and not unmounted before shutdown. To solve this problem, create this file (as root):

 `/etc/systemd/system/killsshfs.service` 

```
[Unit]
After=network.target

[Service]
RemainAfterExit=yes
ExecStart=-/bin/true
ExecStop=-/usr/bin/pkill sshfs

[Install]
WantedBy=multi-user.target

```

Then enable the service: `systemctl enable killsshfs.service`

## See also

*   [sftpman](/index.php/Sftpman "Sftpman") - sshfs helper tool
*   [SSH](/index.php/SSH "SSH")
*   [How to mount chrooted SSH filesystem](http://wiki.gilug.org/index.php/How_to_mount_SFTP_accesses), with special care with owners and permissions questions.