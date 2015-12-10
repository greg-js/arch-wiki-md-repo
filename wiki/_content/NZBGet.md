# NZBGet

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

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

Install the [nzbget](https://www.archlinux.org/packages/?name=nzbget) package, or install [nzbget-git](https://aur.archlinux.org/packages/nzbget-git/)<sup><small>AUR</small></sup> from [AUR](/index.php/AUR "AUR") to get the latest build and a [systemd](/index.php/Systemd "Systemd") `nzbget` service file.

## Configuring NZBGet

Copy the template configuration file to a custom directory:

```
# cp /usr/share/nzbget/nzbget.conf /etc/nzbget.conf

```

Update `/etc/nzbget.conf` config file before starting `nzbget`.

## Starting NZBGet

**Note:** The official [nzbget](https://www.archlinux.org/packages/?name=nzbget) package doesn't provide a systemd service file. You will have to start it manually instead.

*   Running as root in console-mode: `# nzbget -c /etc/nzbget.conf -s` 

*   Running as root in daemon-mode: `# nzbget -c /etc/nzbget.conf -D` 

NZBGet should now be accessible on [http://localhost:6789](http://localhost:6789).

## Running NZBGet under a different user

**Tip:** The [nzbget-git](https://aur.archlinux.org/packages/nzbget-git/)<sup><small>AUR</small></sup> provides already a `nzbget` user/group, so there is no need of adding a system user.

For better security it is better to run NZBGet under a [system user](/index.php/Users_and_groups#Example_adding_a_system_user "Users and groups").

After adding a system user, update the main configuration file:

 `/etc/nzbget.conf` 

```
..
DaemonUsername=nzbget # system user
MainDir=/home/user/Downloads/NZBGet
UMask=0007
```

It may be necessary to update permissions of the `/usr/share/nzbget` directory:

```
# chown -R nzbget:nzbget /usr/share/nzbget
# chmod -R 755 /usr/share/nzbget

```

Create and set permissions for the desired directories:

```
# mkdir /home/user/Downloads/NZBGet
# chown -R nzbget:nzbget /home/user/Downloads/NZBGet
# chmod -R 770 /home/user/Downloads/NZBGet

```

The `/home/user/Downloads/NZBGet` will be accessible for the user `nzbget` and for the `nzbget` group. Making the target directory world read/writable is highly discouraged (i.e. do not _chmod_ the directory to _777_). Instead, give individual users/groups appropriate permissions to the appropriate directories (e.g. by adding 'yourself' to the `nzbget` group).

Starting NZBGet as user `nzbget` in daemon-mode:

```
$ sudo -u nzbget /usr/bin/nzbget -c /etc/nzbget.conf -D

```

## Troubleshooting

### Default NZBGet credentials

The default credentials for NZBGet are `nzbget` as user and `tegbzn6789` as password. For security reasons it is recommended to change the default credentials.

### NZBGet crashes on start

This may happen when the user edited the NZBGet configuration by the Web-interface (located at [http://localhost:6789](http://localhost:6789)), corrupting the configuration-file. Clean-up the configuration-file and restart the server/daemon again.

## See also

*   [NZBGet Documentation](http://nzbget.net/Documentation)
*   [Performance Tips](http://nzbget.net/Performance_tips)

Retrieved from "[https://wiki.archlinux.org/index.php?title=NZBGet&oldid=399919](https://wiki.archlinux.org/index.php?title=NZBGet&oldid=399919)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Internet applications](/index.php/Category:Internet_applications "Category:Internet applications")