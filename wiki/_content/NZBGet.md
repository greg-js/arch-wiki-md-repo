# NZBGet

[NZBGet](http://www.nzbget.net/) is an Usenet-client written in C++ and designed with performance in mind to achieve maximum download speed by using very little system resources.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuring NZBGet](#Configuring_NZBGet)
*   [3 Starting NZBGet](#Starting_NZBGet)
*   [4 Running NZBGet under a different user](#Running_NZBGet_under_a_different_user)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 Default NZBGet credentials](#Default_NZBGet_credentials)
    *   [5.2 NZBGet crashes on start](#NZBGet_crashes_on_start)
*   [6 See also](#See_also)

## Installation

Install the [nzbget](https://www.archlinux.org/packages/?name=nzbget) package and the optional [nzbget-systemd](https://aur.archlinux.org/packages/nzbget-systemd/) that provides a `nzbget` [systemd](/index.php/Systemd "Systemd") service.

To install the latest [NZBGet Git](https://github.com/nzbget/nzbget) version with a [systemd](/index.php/Systemd "Systemd") service file, install [nzbget-git](https://aur.archlinux.org/packages/nzbget-git/).

## Configuring NZBGet

Copy the template configuration file to a custom directory:

```
# cp /usr/share/nzbget/nzbget.conf /var/lib/nzbget/.nzbget

```

Update the `/var/lib/nzbget/.nzbget` config file.

## Starting NZBGet

**Note:** The official [nzbget](https://www.archlinux.org/packages/?name=nzbget) package doesn't provide a systemd service file. You will have to start NZBGet manually instead.

*   Running as root in console-mode: `# nzbget -c /var/lib/nzbget/.nzbget -s` 

*   Running as root in daemon-mode: `# nzbget -c /var/lib/nzbget/.nzbget -D` 

NZBGet should now be accessible on [http://localhost:6789](http://localhost:6789).

## Running NZBGet under a different user

**Tip:** The [nzbget-git](https://aur.archlinux.org/packages/nzbget-git/) and [nzbget-systemd](https://aur.archlinux.org/packages/nzbget-systemd/) provides already a `nzbget` user and group, so there is no need of adding a system user.

For better security it is better to run NZBGet under a [system user](/index.php/Users_and_groups#Example_adding_a_system_user "Users and groups").

After adding a system user, update the main configuration file using the webinterface or by editing the config file:

 `/var/lib/nzbget/.nzbget` 

```
..
DaemonUsername=nzbget # system user
MainDir=/home/user/Downloads/NZBGet
UMask=0022 # 755 for dirs - 644 for files
```

It may be necessary to update permissions of the `/var/lib/nzbget` directory:

```
# chown -R nzbget:nzbget /var/lib/nzbget
# chmod 775 /var/lib/nzbget/
# chmod 664 /var/lib/nzbget/.nzbget

```

Create and set permissions for the desired directories:

```
# mkdir /home/myuser/Downloads/NZBGet
# chown -R nzbget:nzbget /home/user/Downloads/NZBGet
# chmod 775 /home/user/Downloads/NZBGet

```

The `/home/user/Downloads/NZBGet` will be accessible for the user `nzbget` and for the `nzbget` group. Making the target directory world read/writable is highly discouraged (i.e. do not _chmod_ the directory to _777_). Instead, give individual users/groups appropriate permissions to the appropriate directories (e.g. by adding 'yourself' to the `nzbget` group).

Starting NZBGet as user `nzbget` in daemon-mode, or start NZBGet by using the `nzbget.service` if installed with the [nzbget-systemd](https://aur.archlinux.org/packages/nzbget-systemd/) instead:

```
$ sudo -u nzbget /usr/bin/nzbget -c /var/lib/nzbget/.nzbget -D

```

## Troubleshooting

### Default NZBGet credentials

The default credentials for NZBGet are `nzbget` as user and `tegbzn6789` as password. For security reasons it is recommended to change the default credentials.

### NZBGet crashes on start

This may happen when the user edited the NZBGet configuration by the Web-interface (located at [http://localhost:6789](http://localhost:6789)), corrupting the configuration-file. Clean-up the configuration-file and restart the server/daemon again.

## See also

*   [NZBGet Documentation](http://nzbget.net/Documentation)
*   [Performance Tips](http://nzbget.net/Performance_tips)

Retrieved from "[https://wiki.archlinux.org/index.php?title=NZBGet&oldid=413832](https://wiki.archlinux.org/index.php?title=NZBGet&oldid=413832)"