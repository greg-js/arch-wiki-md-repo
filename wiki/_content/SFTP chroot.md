# SFTP chroot

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

**This article or section needs language, wiki syntax or style improvements.**

**Reason:** Several [Help:Style](/index.php/Help:Style "Help:Style") issues. (Discuss in [Talk:SFTP chroot#](https://wiki.archlinux.org/index.php/Talk:SFTP_chroot))

OpenSSH 4.9+ includes a built-in chroot for sftp, but requires a few tweaks to the normal install.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Change chroot directory rights](#Change_chroot_directory_rights)
    *   [2.2 Fixing path for authorized_keys](#Fixing_path_for_authorized_keys)
    *   [2.3 Adding new chrooted users](#Adding_new_chrooted_users)
*   [3 Logging](#Logging)
*   [4 Testing your chroot](#Testing_your_chroot)
*   [5 Troubleshooting](#Troubleshooting)
*   [6 Write access to chroot dir](#Write_access_to_chroot_dir)
*   [7 Links & References](#Links_.26_References)

## Installation

This package is available in the core repository. To install it, run

```
# pacman -S openssh

```

## Configuration

In _/etc/ssh/sshd_config_, modify the Subsystem line for sftp:

```
 Subsystem       sftp    internal-sftp

```

At the end of the file, add something similar to the following for a group:

```
 Match Group sftponly
   ChrootDirectory %h
   ForceCommand internal-sftp
   AllowTcpForwarding no
   PermitTunnel no
   X11Forwarding no

```

Or for a single user:

```
 Match User username
   ChrootDirectory %h
   ForceCommand internal-sftp
   AllowTcpForwarding no
   PermitTunnel no
   X11Forwarding no

```

### Change chroot directory rights

The chroot directory must be owned by root.

```
 sudo chown root:root /home/username

```

Add the '_sftponly_ group to each user with remote access rights

```
 sudo adduser username sftponly

```

### Fixing path for authorized_keys

With the standard path of _AuthorizedKeysFile_, the public key authentication will fail for chrooted-users. To fix this, we set the _AuthorizedKeysFile_ to a root-owned, non-worldwritable directory and move existing users' keys.

**Note:** This has the side effect of improving overall security with the tradeoff of root intervention for revocation in case a user changes their key or their key gets lost or stolen.

```
  AuthorizedKeysFile      /etc/ssh/authorized_keys/%u

```

Create _authorized_keys_ directory and move existing users' authorized_keys:

```
 sudo mkdir /etc/ssh/authorized_keys
 sudo bash -c 'for user in /home/*; do mv ${user}/.ssh/authorized_keys /etc/ssh/authorized_keys/${user#/home/}; done'

```

**Warning:** Be careful during this step not to lock yourself out of the machine you're working on. Always have a secondary method of access, such as an additional ssh session open or console access should things go awry

Restart sshd:

```
 sudo systemctl restart sshd.service

```

### Adding new chrooted users

If using the group method above, ensure all sftp users are put in the appropriate group, i.e.:

```
 sudo usermod -g sftponly username

```

Also, set their shell to _/usr/bin/false_ to prevent a normal ssh login:

```
 sudo usermod -s /bin/false username

```

Their chroot will be the same as their home directory. The permissions are not the same as a normal home, though. Their home directory must be owned as root and not writable by another user or group. This includes the path leading to the directory.

[![Tango-emblem-important.png](/images/c/c8/Tango-emblem-important.png)](/index.php/File:Tango-emblem-important.png)

[![Tango-emblem-important.png](/images/c/c8/Tango-emblem-important.png)](/index.php/File:Tango-emblem-important.png)

**The factual accuracy of this article or section is disputed.**

**Reason:** See e.g [https://bugs.archlinux.org/task/21981](https://bugs.archlinux.org/task/21981) (Discuss in [Talk:SFTP chroot#](https://wiki.archlinux.org/index.php/Talk:SFTP_chroot))

**Warning:** Make sure that _/bin/false_ exists in _/etc/shells_ as well. Otherwise the login will fail with an _invalid password error_.

Note that since this is only for sftp, a proper chroot environment with a shell and _/dev_ doesn't need to be created. However, if you would like to log access, follow the instructions in the logging section below.

## Logging

**1)**

The user will not be able to access `/dev/log`. This can be seen by running `strace` on the process once the user connects and attempts to download a file. Create the sub-directory `dev` in the `ChrootDirectory`, for example:

```
 sudo mkdir /usr/local/chroot/theuser/dev
 sudo chmod 755 /usr/local/chroot/theuser/dev

```

`syslog-ng` will create the device `/usr/local/chroot/theuser/dev/log` once configured.

**2)**

Add to `/etc/syslog-ng/syslog-ng.conf` a new source for the log and add the configuration, for example change the section:

```
source src {
  unix-dgram("/dev/log");
  internal();
  file("/proc/kmsg");
};

```

to:

```
source src {
  unix-dgram("/dev/log");
  internal();
  file("/proc/kmsg");
  unix-dgram("/usr/local/chroot/theuser/dev/log");
};

```

and append:

```
#sftp configuration
destination sftp { file("/var/log/sftp.log"); };
filter f_sftp { program("internal-sftp"); };
log { source(src); filter(f_sftp); destination(sftp); };

```

(Optional) If you'd like to similarly log SSH messages to it's own file:

```
#sshd configuration
destination ssh { file("/var/log/ssh.log"); };
filter f_ssh { program("sshd"); };
log { source(src); filter(f_ssh); destination(ssh); };

```

(From [Syslog-ng#Move log to another file](/index.php/Syslog-ng#Move_log_to_another_file "Syslog-ng"))

**3)**

Edit `/etc/ssh/sshd_config` to replace all instances of `internal-sftp` with `internal-sftp -f AUTH -l VERBOSE`

**4)**

Restart logging and SSH:

```
 systemctl restart syslog-ng.service
 systemctl restart sshd.service

```

`/usr/local/chroot/theuser/dev/log` should now exist.

## Testing your chroot

```
# ssh username@localhost

```

should refuse the connection or fail on login. The response varies, possibly due to the version of OpenSSH used.

```
# sftp username@localhost

```

should place you in the chroot'd environment.

## Troubleshooting

Error while trying to connect

```
Write failed: Broken pipe                                                                                               
Couldn't read packet: Connection reset by peer

```

If you also find similar message in /var/log/auth.log

```
sshd[12399]: fatal: bad ownership or modes for chroot directory component "/path/of/chroot/directory/"  

```

This is a `ChrootDirectory` ownership problem. sshd will reject SFTP connections to accounts that are set to chroot into any directory that has ownership/permissions that sshd considers insecure. sshd's strict ownership/permissions requirements dictate that every directory in the chroot path must be owned by root and only writable by the owner. So, for example, if the chroot environment is /home must be owned by root. See below for possible alternatives.

The reason for this is to [prevent a user from escalating their privileges](http://lists.mindrot.org/pipermail/openssh-unix-dev/2009-May/027651.html) and becoming root, escaping the chroot environment.

If chroot environment is in user's home directory, make sure user have access to it's home directory, or user would not be able to access it's publickey, produce following error

```
Permission denied (publickey).

```

## Write access to chroot dir

As above, if a user is able to write to the chroot directory then it is possible for them to escalate their privileges to root and escape the chroot. One way around this is to give the user two home directories - one "real" home they can write to, and one SFTP home that is locked down to keep sshd happy and your system secure. By using `mount --bind` you can make the real home directory appear as a subdirectory inside the SFTP home directory, allowing them full access to their real home directory.

This can also be used to achieve other goals. For example, a user's home directory can be locked down per the sshd chroot rules, and bind mounts used to provide users access to other directories:

```
# mkdir /home/user/web
# mount --bind /srv/web/example.com /home/user/web

```

Optional add an entry to `/etc/fstab`:

```
# echo '/srv/web/example.com/ /home/user/web        none    bind' >> /etc/fstab

```

Now the user can log in with SFTP, they are chrooted to `/home/user`, but they see a folder called "web" they can access to manipulate files on a web site (assuming they have correct permissions in `/srv/web/example.com`.

## Links & References

*   [http://www.minstrel.org.uk/papers/sftp/builtin/](http://www.minstrel.org.uk/papers/sftp/)
*   [http://www.openbsd.org/cgi-bin/man.cgi?query=sshd_config](http://www.openbsd.org/cgi-bin/man.cgi?query=sshd_config)

Retrieved from "[https://wiki.archlinux.org/index.php?title=SFTP_chroot&oldid=385957](https://wiki.archlinux.org/index.php?title=SFTP_chroot&oldid=385957)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [File Transfer Protocol](/index.php/Category:File_Transfer_Protocol "Category:File Transfer Protocol")
*   [Secure Shell](/index.php/Category:Secure_Shell "Category:Secure Shell")