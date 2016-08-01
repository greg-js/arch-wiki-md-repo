OpenSSH 4.9+ includes a built-in chroot for sftp, but requires a few tweaks to the normal install.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Change chroot directory rights](#Change_chroot_directory_rights)
    *   [2.2 Fixing path for authorized_keys](#Fixing_path_for_authorized_keys)
    *   [2.3 Adding new chrooted users](#Adding_new_chrooted_users)
*   [3 Logging](#Logging)
    *   [3.1 Create sub directory](#Create_sub_directory)
    *   [3.2 Syslog-ng configuration](#Syslog-ng_configuration)
    *   [3.3 sshd configuration](#sshd_configuration)
    *   [3.4 Restart service](#Restart_service)
*   [4 Testing your chroot](#Testing_your_chroot)
*   [5 Troubleshooting](#Troubleshooting)
*   [6 Write access to chroot dir](#Write_access_to_chroot_dir)
*   [7 See also](#See_also)

## Installation

This package is available in the core repository. To install it, run

```
# pacman -S openssh

```

## Configuration

First, we need to create the `sftponly` group

```
# groupadd sftponly 

```

Following changes to the SSH daemon configure permissions for the `sftponly` group

 `/etc/ssh/sshd_config` 
```
Match Group sftponly
  ChrootDirectory %h
  ForceCommand internal-sftp
  AllowTcpForwarding no
  PermitTunnel no
  X11Forwarding no

```

Or for a single user:

 `/etc/ssh/sshd_config` 
```
Match User username
  ChrootDirectory %h
  ForceCommand internal-sftp
  AllowTcpForwarding no
  PermitTunnel no
  X11Forwarding no

```

### Change chroot directory rights

The chroot directory must be owned by root.

```
 # chown root:root /home/username

```

Add the '*sftponly* group to each user with remote access rights

```
 # gpasswd -a USER sftponly

```

### Fixing path for authorized_keys

With the standard path of *AuthorizedKeysFile*, the public key authentication will fail for chrooted-users. To fix this, we set the *AuthorizedKeysFile* to a root-owned, non-worldwritable directory and move existing users' keys.

**Note:** This has the side effect of improving overall security with the tradeoff of root intervention for revocation in case a user changes their key or their key gets lost or stolen.

```
AuthorizedKeysFile      /etc/ssh/authorized_keys/%u

```

Create *authorized_keys* directory and move existing users' authorized_keys:

```
# mkdir /etc/ssh/authorized_keys
# bash -c 'for user in /home/*; do mv ${user}/.ssh/authorized_keys /etc/ssh/authorized_keys/${user#/home/}; done'

```

**Warning:** Be careful during this step not to lock yourself out of the machine you're working on. Always have a secondary method of access, such as an additional ssh session open or console access should things go awry

[Restart](/index.php/Restart "Restart") `sshd.service`.

### Adding new chrooted users

If using the group method above, ensure all sftp users are put in the appropriate group, i.e.:

```
# usermod -g sftponly username

```

Also, set their shell to */usr/bin/false* to prevent a normal ssh login:

```
# usermod -s /bin/false username

```

Their chroot will be the same as their home directory. The permissions are not the same as a normal home, though. Their home directory must be owned as root and not writable by another user or group. This includes the path leading to the directory.

**Warning:** Make sure that */bin/false* exists in */etc/shells* as well. Otherwise the login will fail with an *invalid password error*.

Note that since this is only for sftp, a proper chroot environment with a shell and */dev* doesn't need to be created. However, if you would like to log access, follow the instructions in the logging section below.

## Logging

The user will not be able to access `/dev/log`. This can be seen by running `strace` on the process once the user connects and attempts to download a file.

### Create sub directory

Create the sub-directory `dev` in the `ChrootDirectory`, for example:

```
 sudo mkdir /usr/local/chroot/theuser/dev
 sudo chmod 755 /usr/local/chroot/theuser/dev

```

`syslog-ng` will create the device `/usr/local/chroot/theuser/dev/log` once configured.

### Syslog-ng configuration

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

### sshd configuration

Edit `/etc/ssh/sshd_config` to replace all instances of `internal-sftp` with `internal-sftp -f AUTH -l VERBOSE`

### Restart service

[Restart](/index.php/Restart "Restart") service `syslog-ng` and `sshd`.

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

## See also

*   [http://www.minstrel.org.uk/papers/sftp/builtin/](http://www.minstrel.org.uk/papers/sftp/)
*   [http://www.openbsd.org/cgi-bin/man.cgi?query=sshd_config](http://www.openbsd.org/cgi-bin/man.cgi?query=sshd_config)