[pyLoad](https://pyload.net) is a fast, lightweight and full featured download manager for many One-Click-Hoster, container formats like DLC, video sites or just plain http/ftp links ([supported hosts](https://github.com/pyload/pyload/wiki/Supported-Hoster)). It aims for low hardware requirements and platform independence to be runnable on all kind of systems (desktop pc, netbook, NAS, router). Despite its strict restriction it is packed full of features just like webinterface, captcha recognition, unrar and much more.

pyLoad is divided into core and clients, to make it easily remote accessible.

Available clients ([screenshots](https://github.com/pyload/pyload/wiki/Screenshots)):

*   a web interface
*   a command line interface
*   a GUI written in Qt
*   and an Android client.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Manual](#Manual)
    *   [2.2 Scripts](#Scripts)
*   [3 Running](#Running)
    *   [3.1 Essential](#Essential)
    *   [3.2 Interfacing with pyLoadCore](#Interfacing_with_pyLoadCore)
*   [4 Daemon](#Daemon)
*   [5 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") [pyload-git](https://aur.archlinux.org/packages/pyload-git/) from the [AUR](/index.php/AUR "AUR") for the stable version or [pyload-nightly](https://aur.archlinux.org/packages/pyload-nightly/) for a development build of the new pyload 0.5 version.

## Configuration

Run Setup Assistant:

```
# pyLoadCore -s

```

**Note:** This command must be run as the same user that will run pyload. For example if you run pyload as a daemon using the systemd service, either run this command as user pyload or change `/etc/systemd/system/pyload.service` to another user. If you choose to run this command as user pyload you will have to edit `/etc/passwd` to modify pyload's shell from `/bin/false` to `/bin/bash`.

The Setup Assistant gives you a jump start, by providing a *basic* but *working* setup. Being a basic setup, there are more options and you should at least look at them, since some sections are untouched by the Assistant, like the permissions section.

**Tip:** Most (if not all) of the options can be changed with `pyLoadGui` or with the the web interface.

### Manual

You can also directly edit `pyload.conf` (located in `~/.pyload/` by default.

While also editable with the web interface, you can change the plugins configuration by editing `~/.pyload/plugins.conf`.

Extraction passwords are stored in `~/.pyload/unrar_passwords.txt`.

### Scripts

For more info on this read `/opt/pyload/scripts/Readme.txt`.

If you are interested in running userscripts, before running, you need to either

```
# chmod 777 /opt/pyload/scripts/

```

or

```
# chown *user* /opt/pyload/scripts/

```

(the *user* being the one you defined in pyload.conf / permissions settings) in order for pyLoadCore to create the necessary folders.

## Running

### Essential

```
# pyLoadCore

```

```
  to run pyload without having the terminal stay running use

# pyLoadCore --daemon

```

### Interfacing with pyLoadCore

```
# pyLoadCli

```

```
# pyLoadGui

```

Or, as stated above, with the web interface. If the default settings are true, then:

```
http://localhost:8000

```

## Daemon

**Tip:** Do not forget to change `$USER` and `$GROUP`
 `/etc/systemd/system/pyload.service` 
```
[Unit]
Description=Downloadtool for One-Click-Hoster written in python.
After=network.target

[Service]
ExecStart=/usr/bin/pyLoadCore
User=$USER
Group=$GROUP

[Install]
WantedBy=multi-user.target
```

To start pyload start *pyload* service.

To have it started automatically on boot, enable *pyload* service.

## See also

[List of applications/Internet#Download managers](/index.php/List_of_applications/Internet#Download_managers "List of applications/Internet")