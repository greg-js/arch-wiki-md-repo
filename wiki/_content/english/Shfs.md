[Shfs](http://shfs.sourceforge.net/) is a simple and easy to use Linux kernel module which allows you to mount remote filesystems using a plain shell (ssh) connection. When using shfs, you can access all remote files just like the local ones, only the access is governed through the transport security of ssh.

**Note:** The FUSE-based [SSHFS](/index.php/SSHFS "SSHFS") is much more widely used, as shfs has not been updated since 2004.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Why SHFS?](#Why_SHFS?)
*   [2 Installation](#Installation)
*   [3 Configuration](#Configuration)
    *   [3.1 /etc/fstab](#/etc/fstab)
*   [4 See Also](#See_Also)
*   [5 External Links](#External_Links)

## Why SHFS?

Shfs supports some nice features:

*   file cache for access speedup
*   perl and shell code for the remote (server) side
*   could preserve uid/gid (root connection)
*   number of remote host platforms (Linux, Solaris, Cygwin, ...)
*   arbitrary command used for connection (instead of ssh)
*   persistent connection (reconnect after ssh dies)

If these features cannot convince you, I probably cannot either. Yet, consider: the only thing you need on the server is a sshd running - and you can mount your filesystem from **anywhere** in a **secure** way.

## Installation

In order to use shfs it needs to be installed and configured on the client side, NOT on the server side! Server only needs to have working sshd running.

[Install](/index.php/Install "Install") the [shfs-utils](https://www.archlinux.org/packages/?name=shfs-utils) package. If you run a custom kernel, use [ABS](/index.php/ABS "ABS") to compile it yourself.

## Configuration

If you want to use shfsmount as mortal user, you will have to `chmod +s /usr/bin/shfsmount` and `chmod + /usr/bin/shfsumount`. However it is much more comfortable to put your mount options into `/etc/fstab` - this is what mine looks like:

```
remoteuser@Server:/data   /mnt/data   shfs    rw,noauto,uid=localuser,persistent   0       0
remoteuser@Server:/crap   /mnt/crap   shfs    rw,noauto,uid=localuser,persistent   0       0
remoteuser@Server:/backup /mnt/backup shfs    rw,noauto,uid=localuser,persistent   0       0
remoteuser@Server:/home   /mnt/home   shfs    rw,noauto,uid=localuser,persistent   0       0

```

Soon you will get tired typing passwords and once you do, you might consider [Using SSH Keys](/index.php/Using_SSH_Keys "Using SSH Keys").

Btw, if you are a paranoid bastard, like I am, and do not run ssh on port 22 on your server, you will need to complete your option list with `port=<portnumber>`.

### /etc/fstab

To add an entry for an shfs volume in your fstab, add a line of the format:

```
userid@remoteMachine:/remoteDirectory /home/userid/remoteDirectory shfs rw,user,noauto 0 0

```

(Came from [Ubuntu Forums](http://ubuntuforums.org/archive/index.php/t-30332.html)).

## See Also

*   [SSHFS](/index.php/SSHFS "SSHFS") - A more up-to-date, FUSE-based implementation of an SSH-based filesystem.

## External Links

*   [http://shfs.sourceforge.net/](http://shfs.sourceforge.net/) for a supposed to be complete reference.

*   [http://www.openssh.com/](http://www.openssh.com/) for a really complete reference ;)