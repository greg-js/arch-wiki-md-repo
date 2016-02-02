# Pure-FTPd

[Pure-FTPd](http://www.pureftpd.org/project/pure-ftpd) is a FTP server designed with security in mind.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Set up virtual users](#Set_up_virtual_users)
        *   [2.1.1 Changing user password](#Changing_user_password)
        *   [2.1.2 Removing user](#Removing_user)
        *   [2.1.3 Checking user settings](#Checking_user_settings)
    *   [2.2 Backends](#Backends)
*   [3 See also](#See_also)

## Installation

[pure-ftpd](https://aur.archlinux.org/packages/pure-ftpd/)<sup><small>AUR</small></sup> can be installed from the [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository").

The server can be started using `# systemctl start pure-ftpd`.

To start the server automatically, use `# systemctl enable pure-ftpd`.

For more information on how to manage the service, refer to [using units](/index.php/Systemd#Using_units "Systemd").

## Configuration

Pure-FTPd configuration is completely done with its startup arguments.

There is a wrapper script, which reads `/etc/pure-ftpd.conf`. It then starts Pure-FTPd with the corresponding arguments.

### Set up virtual users

With Pure-FTPd, it's possible to use virtual users instead of real system users.

The available users need to be provided by one ore more backends. See [backends](#Backends).

For simplicity and demonstration purposes, the PureDB backend will be used. Uncomment the following two lines:

```
# We disable the anonymous account.
NoAnonymous yes
# We use PureDB as backend and specify its path.
PureDB /etc/pureftpd.pdb

```

Now only authenticated users can connect. To add users to the PureDB we need to create a `/etc/passwd`-like file which is then used to create the PureDB.

To create, view, or modify the `/etc/pureftpd.passwd` file, we use the `pure-pw` command.

```
# pure-pw useradd someuser -u ftp -d /srv/ftp

```

This creates the user **someuser** which runs as the FTP system user. By default, the user is chrooted to `/srv/ftp`. In the event that that's undesirable, replace `-d` with `-D`.

**Note:**

The virtual users running as the FTP system users can not log in by default. To change that behavior, set the option MinUID in `/etc/pure-ftpd.conf` to 14 (UID of the ftp user).

We also need to list the shell of the FTP system user in `/etc/shells`.

`# echo "/bin/false" >> /etc/shells`

**Note:** Symlinks outside of the chrooted directory do not work since the package is not compiled with `--with-virtualchroot`. You can use `mount --bind source target` as a workaround.

Before this account is usable, we need to commit our changes:

```
# pure-pw mkdb

```

The virtual user can now access everything in `/srv/ftp`.

The command `pure-pw mkdb` creates the file mentioned earlier called `/etc/pureftpd.pdb`, which houses all information related to your virtual users. There is no need to restart your service when issuing this command as it is updated on the fly and changes take effect immediately.

#### Changing user password

For example, to change a user's password, type the command:

```
# pure-pw passwd someuser

```

Afterwards, commit your changes by updating `/etc/pureftpd.pdb`:

```
# pure-pw mkdb

```

#### Removing user

To remove a user, type the command:

```
# pure-pw userdel someuser

```

The user's home directory is not removed via this command; therefore, it must be removed manually.

#### Checking user settings

To check a user's current account settings, type the command:

```
# pure-pw show someuser

```

### Backends

You need to specify one or more backends. If you specify more than one, Pure-FTPd will respect the order in which they are specified. It will use the first backend which contains the requested user.

Available backends are:

*   `/etc/passwd`
*   [MySQL](/index.php/MySQL "MySQL")
*   [LDAP](/index.php/LDAP "LDAP")
*   [PostgreSQL](http://www.postgresql.org/)
*   [PAM](https://en.wikipedia.org/wiki/Linux_PAM)
*   PureDB
*   Or you can write [your own](http://download.pureftpd.org/pub/pure-ftpd/doc/README.Authentication-Modules)

## See also

*   [Official homepage](http://www.pureftpd.org/project/pure-ftpd)
*   [Virtual users](http://download.pureftpd.org/pub/pure-ftpd/doc/README.Virtual-Users)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Pure-FTPd&oldid=387008](https://wiki.archlinux.org/index.php?title=Pure-FTPd&oldid=387008)"