**翻译状态：** 本文是英文页面 [SSHFS](/index.php/SSHFS "SSHFS") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2017-07-03，点击[这里](https://wiki.archlinux.org/index.php?title=SSHFS&diff=0&oldid=481165)可以查看翻译后英文页面的改动。

[SSHFS](https://github.com/libfuse/sshfs) 是一个通过 [SSH](/index.php/Secure_Shell_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Secure Shell (简体中文)") 挂载基于 FUSE 的文件系统的客户端程序。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
    *   [1.1 挂载](#.E6.8C.82.E8.BD.BD)
    *   [1.2 卸载](#.E5.8D.B8.E8.BD.BD)
*   [2 Chrooting](#Chrooting)
*   [3 助手程序](#.E5.8A.A9.E6.89.8B.E7.A8.8B.E5.BA.8F)
*   [4 自动挂载](#.E8.87.AA.E5.8A.A8.E6.8C.82.E8.BD.BD)
    *   [4.1 On demand](#On_demand)
    *   [4.2 引导时挂载](#.E5.BC.95.E5.AF.BC.E6.97.B6.E6.8C.82.E8.BD.BD)
    *   [4.3 安全用户访问](#.E5.AE.89.E5.85.A8.E7.94.A8.E6.88.B7.E8.AE.BF.E9.97.AE)
*   [5 选项](#.E9.80.89.E9.A1.B9)
*   [6 排错](#.E6.8E.92.E9.94.99)
    *   [6.1 检查清单](#.E6.A3.80.E6.9F.A5.E6.B8.85.E5.8D.95)
    *   [6.2 Connection reset by peer](#Connection_reset_by_peer)
    *   [6.3 远程主机连接断开（Remote host has disconnected）](#.E8.BF.9C.E7.A8.8B.E4.B8.BB.E6.9C.BA.E8.BF.9E.E6.8E.A5.E6.96.AD.E5.BC.80.EF.BC.88Remote_host_has_disconnected.EF.BC.89)
    *   [6.4 冻结应用（Freezing apps (e.g. Gnome Files, Gedit)）](#.E5.86.BB.E7.BB.93.E5.BA.94.E7.94.A8.EF.BC.88Freezing_apps_.28e.g._Gnome_Files.2C_Gedit.29.EF.BC.89)
    *   [6.5 Shutdown hangs when sshfs is mounted](#Shutdown_hangs_when_sshfs_is_mounted)
    *   [6.6 fstab 挂载问题](#fstab_.E6.8C.82.E8.BD.BD.E9.97.AE.E9.A2.98)
*   [7 参阅](#.E5.8F.82.E9.98.85)

## 安装

[安装](/index.php/Install "Install") [sshfs](https://www.archlinux.org/packages/?name=sshfs) 软件包。

### 挂载

**提示：** sshfs 结合 [Google Authenticator](/index.php/Google_Authenticator "Google Authenticator") 使用可以提供额外的安全性。

In order to be able to mount a directory the SSH user needs to be able to access it. Invoke `sshfs` to mount a remote directory:

```
$ sshfs [user@]host:[dir] mountpoint [options]

```

For example:

```
$ sshfs sessy@mycomputer:/remote/path /local/path -C -p 9876 -o allow_other

```

Where `-p 9876` stands for the port number, `-C` enables compression and `-o allow_other` grants non-rooted users read/write access.

**注意:** The `allow_other` option is disabled by default. To enable it, uncomment the line `user_allow_other` in `/etc/fuse.conf` to enable non-root users to use the allow_other mount option.

**注意:** Users may also define a non-standard port on a host-by-host basis in `~/.ssh/config` to avoid appending the -p switch here. For more information see [Secure Shell#Client usage](/index.php/Secure_Shell#Client_usage "Secure Shell").

必要时，SSH 将询问口令。如果你不希望频繁输入口令，可参阅：[SSH 如何使用 RSA 密钥做认证](http://linuxmafia.com/~karsten/Linux/FAQs/sshrsakey.html) 或 [SSH 密钥](/index.php/SSH_Keys_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "SSH Keys (简体中文)")。

### 卸载

To unmount the remote system:

```
$ fusermount -u *LOCAL_MOUNT_POINT*

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

**注意:** The chroot directory **must** be owned by root, otherwise you will not be able to connect.

See also [SFTP chroot](/index.php/SFTP_chroot "SFTP chroot"). For more information check the manpages for `Match, ChrootDirectory` and `ForceCommand`.

## 助手程序

If you often need to mount sshfs filesystems you may be interested in using an sshfs helper, such as [sftpman](/index.php/Sftpman "Sftpman").

It provides a command-line and a GTK frontend, to make mounting and unmounting a simple one click/command process.

## 自动挂载

Automounting can happen on boot, or on demand (when accessing the directory). For both, the setup happens in `/etc/[fstab](/index.php/Fstab "Fstab")`.

**注意:** Be mindful that automounting is done through the root user, therefore you cannot use Hosts configured in `.ssh/config` of your normal user.

To let root user use an SSH key of a normal user, specify its full path in option `IdentityFile`.

**And most importantly**, use each sshfs mount at least once manually **while root** so the host's signature is added to the `.ssh/known_hosts` file.

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

**注意:** After editing `/etc/fstab`, (re)start the required service: `systemctl daemon-reload && systemctl restart <target>` where `<target>` can be found by running `systemctl list-unit-files --type automount`

**提示：** [autosshfs-git](https://aur.archlinux.org/packages/autosshfs-git/) do not require editing `/etc/fstab` to add a new mountpoint. Instead, regular users can create one by simply attempting to access it (with e. g. something like `ls ~/mnt/ssh/[user@]yourremotehost[:port]`). [autosshfs-git](https://aur.archlinux.org/packages/autosshfs-git/) uses AutoFS. Users need to be enabled to use it with `autosshfs-user`.

### 引导时挂载

An example on how to use sshfs to mount a remote filesystem through `/etc/[fstab](/index.php/Fstab "Fstab")`

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

### 安全用户访问

When automounting via `/etc/[fstab](/index.php/Fstab "Fstab")`, the filesystem will generally be mounted by root. By default, this produces undesireable results if you wish access as an ordinary user and limit access to other users.

An example mountpoint configuration:

```
USERNAME@HOSTNAME_OR_IP:/REMOTE/DIRECTORY  /LOCAL/MOUNTPOINT  fuse.sshfs noauto,x-systemd.automount,_netdev,user,idmap=user,follow_symlinks,identityfile=/home/USERNAME/.ssh/id_rsa,allow_other,default_permissions,uid=USER_ID_N,gid=USER_GID_N 0 0

```

Summary of the relevant options:

*   *allow_other* - Allow other users than the mounter (i.e. root) to access the share.
*   *default_permissions* - Allow kernel to check permissions, i.e. use the actual permissions on the remote filesystem. This allows prohibiting access to everybody otherwise granted by *allow_other*.
*   *uid*, *gid* - set reported ownership of files to given values; *uid* is the numeric user ID of your user, *gid* is the numeric group ID of your user.

## 选项

sshfs can automatically convert your local and remote user IDs.

Add the *idmap* option with *user* value to translate UID of connecting user:

```
# sshfs -o idmap=user sessy@mycomputer:/home/sessy /mnt/sessy -C -p 9876

```

This will map UID of the remote user "sessy" to the local user, who runs this process ("root" in the above example) and GID remains unchanged. If you need more precise control over UID and GID translation, look at the options *idmap=file* and *uidfile* and *gidfile*.

## 排错

### 检查清单

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

7\. If you want to automount SSH shares by using an SSH public key authentication (no password) via `/etc/fstab`, you can use this line as an example:

```
*USER_S*@*SERVER*:/mnt/on/server      /nmt/on/client        fuse.sshfs      x-systemd.automount,_netdev,user,idmap=user,transform_symlinks,identityfile=/home/*USER_C*/.ssh/id_rsa,allow_other,default_permissions,uid=*USER_C_ID*,gid=*GROUP_C_ID*,umask=0   0 0

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
*   If your `/root/.ssh/config` is a symlink, you will be getting this error as well. See [this serverfault topic](http://serverfault.com/questions/507748/bad-owner-or-permissions-on-root-ssh-config)
*   Adding the option '`sshfs_debug`' (as in '`sshfs -o sshfs_debug user@server ...`') can help in resolving the issue.
*   If that doesn't reveal anything useful, you might also try adding the option '`debug`'
*   If you are trying to sshfs into a router running DD-WRT or the like, there is a solution [here](http://www.dd-wrt.com/wiki/index.php/SFTP_with_DD-WRT). (note that the -osftp_server=/opt/libexec/sftp-server option can be used to the sshfs command in stead of patching dropbear)
*   Old Forum thread: [sshfs: Connection reset by peer](https://bbs.archlinux.org/viewtopic.php?id=27613)
*   Make sure your user can log into the server (especially when using AllowUsers)
*   Make sure `Subsystem sftp /usr/lib/ssh/sftp-server` is enabled in `/etc/ssh/sshd_config`.

**注意:** When providing more than one option for sshfs, they must be comma separated. Like so: '`sshfs -o sshfs_debug,IdentityFile=</path/to/key> user@server ...`')

### 远程主机连接断开（Remote host has disconnected）

If you receive this message directly after attempting to use *sshfs*:

*   First make sure that the **remote** machine has *sftp* installed! It will not work, if not.

**提示：** If your remote server is running OpenWRT: `opkg install openssh-sftp-server` will do the trick

*   Then, try checking the path of the `Subsystem` listed in `/etc/ssh/sshd_config` on the remote machine to see, if it is valid. You can check the path to it with `find / -name sftp-server`.

For Arch Linux the default value in `/etc/ssh/sshd_config` is `Subsystem sftp /usr/lib/ssh/sftp-server`.

### 冻结应用（Freezing apps (e.g. Gnome Files, Gedit)）

**注意:** This prevents the recently used file list from being populated and may lead to possible write errors.

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

### fstab 挂载问题

To get verbose debugging output, add the following to the mount options:

```
ssh_command=ssh\040-vv,sshfs_debug,debug

```

**注意:** Here, `\040` represents a space which fstab uses to separate fields.

To be able to run `mount -av` and see the debug output, remove the following:

```
 noauto,x-systemd.automount

```

## 参阅

*   [How to mount chrooted SSH filesystem](http://wiki.gilug.org/index.php/How_to_mount_SFTP_accesses), with special care with owners and permissions questions.
*   [SSHFS – Installation and Performance](http://www.admin-magazine.com/HPC/Articles/Sharing-Data-with-SSHFS) — Comparison with NFS and optimization tips.