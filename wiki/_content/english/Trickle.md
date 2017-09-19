[trickle](https://github.com/mariusae/trickle) is a portable lightweight userspace bandwidth shaper, that either runs in collaborative mode (together with trickled) or in stand alone mode.

It works by preloading its own socket library wrappers, that limit traffic by delaying data.

Trickle runs entirely in userspace. [[1]](https://github.com/mariusae/trickle)

## Contents

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
    *   [2.1 Modifying other systemd services](#Modifying_other_systemd_services)
    *   [2.2 Use with rsync](#Use_with_rsync)
*   [3 Daemon configuration](#Daemon_configuration)

## Installation

[Install](/index.php/Install "Install") the [trickle](https://www.archlinux.org/packages/?name=trickle) package.

## Usage

**Warning:**

*   Programs that generate heavy traffic, but get controlled via a web interfaces (with very light traffic), will also have the web interface traffic shaped. This means that they will barely be accessible.
*   Trickle can only limit traffic of programs that do not fork, so shaping a FTP server's traffic will not work that way.

If you are running the daemon (see below), just start any program with "trickle" in front of it:

```
# trickle pacman -Syu

```

Otherwise also specify upload and download limit as well as other configuration options (see [trickle(1)](https://github.com/mariusae/trickle/blob/master/trickle.1) for more information):

```
# trickle -d200 -u50 pacman -Syu

```

### Modifying other systemd services

[Modify](/index.php/Systemd#Editing_provided_units "Systemd") `ExecStart` for a desired systemd service, appending `/usr/bin/trickle`. For example:

```
ExecStart=/usr/bin/*daemon*

```

changes to

```
ExecStart=/usr/bin/trickle /usr/bin/*daemon*

```

When using the standalone mode, also add the config options as described in [#Usage](#Usage). [Restart](/index.php/Restart "Restart") the daemon, which should now have shaped bandwith.

### Use with rsync

Instead of putting trickle in front of the rsync command (which won't work, since rsync presumably forks the ssh process), you call rsync like this:

```
rsync --rsh="trickle -d 10 -u 10 ssh" SRC DEST

```

## Daemon configuration

If you want to have application specific settings with trickled, create the optional `/etc/trickled.conf` file as described in the [trickled.conf(5)](https://github.com/mariusae/trickle/blob/master/trickled.conf.5) man page. For example:

```
[ssh]
Priority = 1
Time-Smoothing = 0.1
Length-Smoothing = 2
[ftp]
Priority = 8
Time-Smoothing = 5
Length-Smoothing = 20

```