Related articles

*   [SSHFS](/index.php/SSHFS "SSHFS")

[OpenSSH](/index.php/OpenSSH "OpenSSH") 4.9+ includes a built-in chroot for sftp, but requires a few tweaks to the normal install.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Setup the filesystem](#Setup_the_filesystem)
    *   [2.2 Create an unprivileged user](#Create_an_unprivileged_user)
    *   [2.3 Configure OpenSSH](#Configure_OpenSSH)
        *   [2.3.1 Fixing path for authorized_keys](#Fixing_path_for_authorized_keys)
*   [3 Tips and tricks](#Tips_and_tricks)
    *   [3.1 Write permissions](#Write_permissions)
    *   [3.2 Logging](#Logging)
        *   [3.2.1 Create sub directory](#Create_sub_directory)
        *   [3.2.2 Syslog-ng configuration](#Syslog-ng_configuration)
        *   [3.2.3 OpenSSH configuration](#OpenSSH_configuration)
        *   [3.2.4 Restart service](#Restart_service)
*   [4 Alternatives to SFTP](#Alternatives_to_SFTP)
    *   [4.1 Secure copy protocol (SCP)](#Secure_copy_protocol_.28SCP.29)
        *   [4.1.1 Scponly](#Scponly)
        *   [4.1.2 Adding a chroot jail](#Adding_a_chroot_jail)
*   [5 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") and configure [OpenSSH](/index.php/OpenSSH "OpenSSH"). Once running, make sure `sftp-server` has been set correctly:

 `/etc/ssh/sshd_config` 
```
Subsystem sftp /usr/lib/ssh/sftp-server

```

Access files with *sftp* or [SSHFS](/index.php/SSHFS "SSHFS"). Many standard [FTP clients](/index.php/List_of_applications#File_transfer_clients "List of applications") should work as well.

## Configuration

### Setup the filesystem

Bind mount the live [filesystem](/index.php/Filesystem "Filesystem") to be shared to this directory. In this example, `/mnt/data/share` is to be used, owned by [user](/index.php/User "User") `root` and has octal [permissions](/index.php/Permissions "Permissions") of `755`:

```
# chown root:root /mnt/data/share
# chmod 755 /mnt/data/share
# mkdir -p /srv/ssh/jail
# mount -o bind /mnt/data/share /srv/ssh/jail

```

Add entries to [fstab](/index.php/Fstab "Fstab") to make the bind mount survive on a reboot:

```
/mnt/data/share /srv/ssh/jail  none   bind   0   0

```

**Note:** Readers may select a file access scheme on their own. For example, optionally create a subdirectory for an incoming (writable) space and/or a read-only space. This need not be done directly under `/srv/ssh/jail` - it can be accomplished on the live partition which will be mounted via a bind mount as well.

### Create an unprivileged user

**Note:** You do not need to create a group, it is possible to use `Match User` instead of `Match Group`.

Create the `sftponly` [group](/index.php/Group "Group"):

```
# groupadd sftponly 

```

Create a [user](/index.php/User "User") that uses `sftponly` as main group:

```
# useradd -g sftponly -d */srv/ssh/jail* *username*

```

Set a (complex) password - to prevent `account is locked` error:

```
# passwd *username*

```

You may deny [shell](/index.php/Shell "Shell") login access for the user:

```
# usermod -s /sbin/nologin *username*

```

### Configure OpenSSH

**Note:** You may want to use `Match User` instead of `Match Group` as been given in the previous step.
 `/etc/ssh/sshd_config` 
```
Subsystem sftp /usr/lib/ssh/sftp-server

Match Group sftponly
  ChrootDirectory %h
  ForceCommand internal-sftp
  AllowTcpForwarding no
  X11Forwarding no
  PasswordAuthentication no

```

[Restart](/index.php/Restart "Restart") `sshd.service` to confirm the changes.

#### Fixing path for authorized_keys

**Tip:** Use the [debug mode](/index.php/SSH_keys#Key_ignored_by_the_server "SSH keys") of OpenSSH on the client and server in case of `(pre)auth` error(s).

With the standard path of *AuthorizedKeysFile*, the [SSH keys](/index.php/SSH_keys "SSH keys") authentication will fail for chrooted-users. To fix this, [append](/index.php/Append "Append") a root-owned directory on *AuthorizedKeysFile* to `/etc/openssh/sshd_config` e.g. `/etc/ssh/authorized_keys`, as example:

 `/etc/ssh/sshd_config` 
```
AuthorizedKeysFile */etc/ssh/authorized_keys/%u* .ssh/authorized_keys
PermitRootLogin no
PasswordAuthentication no
PermitEmptyPasswords no
Subsystem sftp /usr/lib/ssh/sftp-server

```

Create *authorized_keys* folder, generate a [SSH-key](/index.php/SSH_keys#Choosing_the_key_location_and_passphrase "SSH keys") on the client, [copy](/index.php/SSH_keys#Manual_method "SSH keys") the contents of the key to `/etc/ssh/authorized_keys` (or any other preferred method) of the server and [set correct permissions](/index.php/SSH_keys#Key_ignored_by_the_server "SSH keys"):

```
# mkdir /etc/ssh/authorized_keys
# chown root:root /etc/ssh/authorized_keys
# chmod 755 /etc/ssh/authorized_keys
# echo 'ssh-rsa <key> <username@host>' >> */etc/ssh/authorized_keys/username*
# chmod 644 /etc/ssh/authorized_keys/*username*

```

[Restart](/index.php/Restart "Restart") `sshd.service`.

## Tips and tricks

### Write permissions

The [bind](#Setup_the_filesystem) path needs to be fully owned by `root`, however files and/or subdirectories don't have to be. In the following example the [user](/index.php/User "User") *www-demo* uses `/srv/ssh/www/demo` as the jail-directory:

```
# mkdir /srv/ssh/www/demo/public_html
# chown www-demo:sftponly /srv/ssh/www/demo/public_html
# chmod 775 /srv/ssh/www/demo/public_html

```

The user should now be able to create files/subdirectories inside this directory. See [File permissions and attributes](/index.php/File_permissions_and_attributes "File permissions and attributes") for more information.

### Logging

The user will not be able to access `/dev/log`. This can be seen by running `strace` on the process once the user connects and attempts to download a file.

#### Create sub directory

Create the sub-directory `dev` in the `ChrootDirectory`, for example:

```
# mkdir /usr/local/chroot/user/dev
# chmod 755 /usr/local/chroot/user/dev

```

`syslog-ng` will create the device `/usr/local/chroot/theuser/dev/log` once configured.

#### Syslog-ng configuration

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

(Optional) If you would like to similarly log SSH messages to its own file:

```
#sshd configuration
destination ssh { file("/var/log/ssh.log"); };
filter f_ssh { program("sshd"); };
log { source(src); filter(f_ssh); destination(ssh); };

```

(From [Syslog-ng#Move log to another file](/index.php/Syslog-ng#Move_log_to_another_file "Syslog-ng"))

#### OpenSSH configuration

Edit `/etc/ssh/sshd_config` to replace all instances of `internal-sftp` with `internal-sftp -f AUTH -l VERBOSE`

#### Restart service

[Restart](/index.php/Restart "Restart") service `syslog-ng` and `sshd`.

`/usr/local/chroot/theuser/dev/log` should now exist.

## Alternatives to SFTP

### Secure copy protocol (SCP)

Installing [openssh](https://www.archlinux.org/packages/?name=openssh) provides the *scp* command to transfer files. SCP may be faster than using SFTP [[1]](https://superuser.com/questions/134901/whats-the-difference-between-scp-and-sftp).

[Install](/index.php/Install "Install") [rssh](https://aur.archlinux.org/packages/rssh/) or [scponly](https://www.archlinux.org/packages/?name=scponly) as alternative shell solutions.

#### Scponly

[install](/index.php/Install "Install") [scponly](https://www.archlinux.org/packages/?name=scponly).

For existing users, simply set the user's shell to scponly:

```
# usermod -s /usr/bin/scponly *username*

```

See [the Scponly Wiki](https://github.com/scponly/scponly/wiki) for more details.

#### Adding a chroot jail

The package comes with a script to create a chroot. To use it, run:

```
# /usr/share/doc/scponly/setup_chroot.sh

```

*   Provide answers
*   Check that `/path/to/chroot` has `root:root` owner and `r-x` for others
*   Change the shell for selected user to `/usr/bin/scponlyc`
*   sftp-server may require some libnss modules such as libnss_files. Copy them to chroot's `/lib` path.

## See also

*   [http://www.minstrel.org.uk/papers/sftp/builtin/](http://www.minstrel.org.uk/papers/sftp/)
*   [http://www.openbsd.org/cgi-bin/man.cgi?query=sshd_config](http://www.openbsd.org/cgi-bin/man.cgi?query=sshd_config)