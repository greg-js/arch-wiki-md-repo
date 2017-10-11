Related articles

*   [SCP and SFTP](/index.php/SCP_and_SFTP "SCP and SFTP")
*   [SFTP chroot](/index.php/SFTP_chroot "SFTP chroot")
*   [Pure-FTPd](/index.php/Pure-FTPd "Pure-FTPd")
*   [SSH](/index.php/SSH "SSH")
*   [sftpman](/index.php/Sftpman "Sftpman")

[SSHFS](https://github.com/libfuse/sshfs) is a FUSE-based filesystem client for mounting directories over [SSH](/index.php/SSH "SSH").

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Mounting](#Mounting)
    *   [1.2 Unmounting](#Unmounting)
*   [2 Options](#Options)
*   [3 Chrooting](#Chrooting)
*   [4 Automounting](#Automounting)
    *   [4.1 On demand](#On_demand)
    *   [4.2 On boot](#On_boot)
    *   [4.3 Secure user access](#Secure_user_access)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 Checklist](#Checklist)
    *   [5.2 Connection reset by peer](#Connection_reset_by_peer)
    *   [5.3 Remote host has disconnected](#Remote_host_has_disconnected)
    *   [5.4 Freezing apps (e.g. Gnome Files, Gedit)](#Freezing_apps_.28e.g._Gnome_Files.2C_Gedit.29)
    *   [5.5 fstab mounting issues](#fstab_mounting_issues)
*   [6 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [sshfs](https://www.archlinux.org/packages/?name=sshfs) package.

**Tip:**

*   If you often need to mount sshfs filesystems you may be interested in using an sshfs helper, such as [qsshfs](https://aur.archlinux.org/packages/qsshfs/), [sftpman](/index.php/Sftpman "Sftpman"), [sshmnt](https://aur.archlinux.org/packages/sshmnt/) or [fmount.py](https://github.com/lahwaacz/Scripts/blob/master/fmount.py).
*   You may want to use [Google Authenticator](/index.php/Google_Authenticator "Google Authenticator") providing additional security as in two-step authentication.
*   [SSH keys](/index.php/SSH_keys "SSH keys") may be used over traditional password authentication.

### Mounting

In order to be able to mount a directory the SSH user needs to be able to access it. Invoke *sshfs* to mount a remote directory:

```
$ sshfs *[user@]host:[dir] mountpoint [options]*

```

For example:

```
$ sshfs myuser@mycomputer:/remote/path /local/path -C -p 9876

```

Here `-p 9876` specifies the port number and `-C` enables compression. For more options see the [#Options](#Options) section.

When not specified, the remote path defaults to the remote user home directory. Default user names and options can be predefined on a host-by-host basis in `~/.ssh/config` to simplify the *sshfs* usage. For more information see [Secure Shell#Client usage](/index.php/Secure_Shell#Client_usage "Secure Shell").

SSH will ask for the password, if needed. If you do not want to type in the password multiple times a day, see [SSH keys](/index.php/SSH_keys "SSH keys").

### Unmounting

To unmount the remote system:

```
$ fusermount -u *local_mount_point*

```

Example:

```
$ fusermount -u /mnt/sessy

```

## Options

*sshfs* can automatically convert between local and remote user IDs. Use the `idmap=user` option to translate the UID of the connecting user to the remote user `myuser` (GID remains unchanged):

```
$ sshfs myuser@mycomputer:/remote/path /local/path -o idmap=user

```

If you need more control over UID and GID translation, look at the options `idmap=file`, `uidfile` and `gidfile`.

A complete list of options can be found in [sshfs(1)](http://jlk.fjfi.cvut.cz/arch/manpages/man/sshfs.1).

## Chrooting

You may want to restrict a specific user to a specific directory on the remote system. This can be done by editing `/etc/ssh/sshd_config`:

 `/etc/ssh/sshd_config` 
```
.....
Match User *someuser* 
       ChrootDirectory */chroot/%u*
       ForceCommand internal-sftp
       AllowTcpForwarding no
       X11Forwarding no
.....

```

**Note:** The chroot directory **must** be owned by root, otherwise you will not be able to connect.

See also [SFTP chroot](/index.php/SFTP_chroot "SFTP chroot"). For more information check the [sshd_config(5)](http://jlk.fjfi.cvut.cz/arch/manpages/man/sshd_config.5) man page for `Match`, `ChrootDirectory` and `ForceCommand`.

## Automounting

Automounting can happen on boot, or on demand (when accessing the directory). For both, the setup happens in the [fstab](/index.php/Fstab "Fstab").

**Note:** Keep in mind that automounting is done through the root user, therefore you cannot use hosts configured in `.ssh/config` of your normal user.

To let the root user use an SSH key of a normal user, specify its full path in the `IdentityFile` option.

**And most importantly**, use each sshfs mount at least once manually **while root** so the host's signature is added to the `/root/.ssh/known_hosts` file.

### On demand

With systemd on-demand mounting is possible using `/etc/fstab` entries.

Example:

```
user@host:/remote/folder /mount/point  fuse.sshfs noauto,x-systemd.automount,_netdev,users,idmap=user,IdentityFile=/home/user/.ssh/id_rsa,allow_other,reconnect 0 0

```

The important mount options here are *noauto,x-systemd.automount,_netdev*.

*   *noauto* tells it not to mount at boot
*   *x-systemd.automount* does the on-demand magic
*   *_netdev* tells it that it is a network device, not a block device (without it "No such device" errors might happen)

**Note:** After editing `/etc/fstab`, (re)start the required service: `systemctl daemon-reload && systemctl restart <target>` where `<target>` can be found by running `systemctl list-unit-files --type automount`

**Tip:** [autosshfs-git](https://aur.archlinux.org/packages/autosshfs-git/) do not require editing `/etc/fstab` to add a new mountpoint. Instead, regular users can create one by simply attempting to access it (with e. g. something like `ls ~/mnt/ssh/[user@]yourremotehost[:port]`). [autosshfs-git](https://aur.archlinux.org/packages/autosshfs-git/) uses AutoFS. Users need to be enabled to use it with `autosshfs-user`.

### On boot

An example on how to use sshfs to mount a remote filesystem through `/etc/fstab`

```
USERNAME@HOSTNAME_OR_IP:/REMOTE/DIRECTORY  /LOCAL/MOUNTPOINT  fuse.sshfs  defaults,_netdev  0  0

```

Take for example the *fstab* line

```
llib@192.168.1.200:/home/llib/FAH  /media/FAH2  fuse.sshfs  defaults,_netdev  0  0

```

The above will work automatically if you are using an SSH key for the user. See [Using SSH Keys](/index.php/Using_SSH_Keys "Using SSH Keys").

If you want to use sshfs with multiple users:

```
user@domain.org:/home/user  /media/user   fuse.sshfs    defaults,allow_other,_netdev    0  0

```

Again, it is important to set the *_netdev* mount option to make sure the network is available before trying to mount.

### Secure user access

When automounting via [fstab](/index.php/Fstab "Fstab"), the filesystem will generally be mounted by root. By default, this produces undesireable results if you wish access as an ordinary user and limit access to other users.

An example mountpoint configuration:

```
USERNAME@HOSTNAME_OR_IP:/REMOTE/DIRECTORY  /LOCAL/MOUNTPOINT  fuse.sshfs noauto,x-systemd.automount,_netdev,user,idmap=user,follow_symlinks,identityfile=/home/USERNAME/.ssh/id_rsa,allow_other,default_permissions,uid=USER_ID_N,gid=USER_GID_N 0 0

```

Summary of the relevant options:

*   *allow_other* - Allow other users than the mounter (i.e. root) to access the share.
*   *default_permissions* - Allow kernel to check permissions, i.e. use the actual permissions on the remote filesystem. This allows prohibiting access to everybody otherwise granted by *allow_other*.
*   *uid*, *gid* - set reported ownership of files to given values; *uid* is the numeric user ID of your user, *gid* is the numeric group ID of your user.

## Troubleshooting

### Checklist

Read the [SSH Checklist](/index.php/Secure_Shell#Checklist "Secure Shell") Wiki entry first. Further issues to check are:

1\. Is your SSH login sending additional information from server's `/etc/issue` file e.g.? This might confuse SSHFS. You should temporarily deactivate server's `/etc/issue` file:

```
$ mv /etc/issue /etc/issue.orig

```

2\. Keep in mind that most SSH related troubleshooting articles you will find on the web are **not** Systemd related. Often `/etc/fstab` definitions wrongly begin with `*sshfs#*user@host:/mnt/server/folder ... fuse ...` instead of using the syntax `user@host:/mnt/server/folder ... fuse.*sshfs* ... *x-systemd*, ...`.

3\. Check that the owner of server's source folder and content is owned by the server's user.

```
$ chown -R USER_S: /mnt/servers/folder

```

4\. The server's user ID can be different from the client's one. Obviously both user names have to be the same. You just have to care for the client's user IDs. SSHFS will translate the UID for you with the following mount options:

```
uid=*USER_C_ID*,gid=*GROUP_C_ID*

```

5\. Check that the client's target mount point (folder) is owned by the client user. This folder should have the same user ID as defined in SSHFS's mount options.

```
$ chown -R USER_C: /mnt/client/folder

```

6\. Check that the client's mount point (folder) is empty. By default you cannot mount SSHFS folders to non-empty folders.

### Connection reset by peer

*   If you are trying to access the remote system with a hostname, try using its IP address, as it can be a domain name solving issue. Make sure you edit `/etc/hosts` with the server details.
*   If you are using non-default key names and are passing it as `-i .ssh/my_key`, this will not work. You have to use `-o IdentityFile=/home/user/.ssh/my_key`, with the full path to the key.
*   If your `/root/.ssh/config` is a symlink, you will be getting this error as well. See [this serverfault topic](http://serverfault.com/questions/507748/bad-owner-or-permissions-on-root-ssh-config)
*   Adding the option '`sshfs_debug`' (as in '`sshfs -o sshfs_debug user@server ...`') can help in resolving the issue.
*   If that doesn't reveal anything useful, you might also try adding the option '`debug`'
*   If you are trying to sshfs into a router running DD-WRT or the like, there is a solution [here](http://www.dd-wrt.com/wiki/index.php/SFTP_with_DD-WRT). (note that the -osftp_server=/opt/libexec/sftp-server option can be used to the sshfs command in stead of patching dropbear)
*   Old Forum thread: [sshfs: Connection reset by peer](https://bbs.archlinux.org/viewtopic.php?id=27613)
*   Make sure your user can log into the server (especially when using AllowUsers)
*   Make sure `Subsystem sftp /usr/lib/ssh/sftp-server` is enabled in `/etc/ssh/sshd_config`.

**Note:** When providing more than one option for sshfs, they must be comma separated. Like so: '`sshfs -o sshfs_debug,IdentityFile=</path/to/key> user@server ...`')

### Remote host has disconnected

If you receive this message directly after attempting to use *sshfs*:

*   First make sure that the **remote** machine has *sftp* installed! It will not work, if not.
*   Then, check that the path of the `Subsystem sftp` in `/etc/ssh/sshd_config` on the remote machine is valid.

### Freezing apps (e.g. Gnome Files, Gedit)

**Warning:** This prevents the recently used file list from being populated and may lead to possible write errors.

If you experience freezing/hanging (stopped responding) applications, you may need to disable write-access to the `~/recently-used.xbel` file.

```
# chattr +i /home/USERNAME/.local/share/recently-used.xbel

```

See the following [bug report](https://bugs.archlinux.org/task/40260) for more details and/or solutions.

### fstab mounting issues

To get verbose debugging output, add the following to the mount options:

```
ssh_command=ssh\040-vv,sshfs_debug,debug

```

**Note:** Here, `\040` represents a space which fstab uses to separate fields.

To be able to run `mount -av` and see the debug output, remove the following:

```
 noauto,x-systemd.automount

```

## See also

*   [How to mount chrooted SSH filesystem](http://wiki.gilug.org/index.php/How_to_mount_SFTP_accesses), with special care with owners and permissions questions.
*   [SSHFS – Installation and Performance](http://www.admin-magazine.com/HPC/Articles/Sharing-Data-with-SSHFS) — Comparison with NFS and optimization tips.