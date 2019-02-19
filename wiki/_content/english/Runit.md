Related articles

*   [init](/index.php/Init "Init")

Runit is a process supervisor. It includes `runit-init`, which can serve as [init](/index.php/Init "Init"). This article only describes using runit to run services alongside [systemd](/index.php/Systemd "Systemd"); [replacing systemd is not supported](https://lists.archlinux.org/pipermail/arch-general/2015-July/039460.html).

Runit is a simple and flexible collection of tools adhering to the Unix philosophy.

See [G. Pape's Runit Page](http://smarden.org/runit/) for a complete description.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
    *   [1.1 Standard runit](#Standard_runit)
    *   [1.2 BusyBox's implementation](#BusyBox's_implementation)
*   [2 Using runit](#Using_runit)
    *   [2.1 General use](#General_use)
*   [3 Tips](#Tips)
    *   [3.1 User Level Services](#User_Level_Services)
    *   [3.2 Create an X session service for a user](#Create_an_X_session_service_for_a_user)

## Installation

### Standard runit

It is possible to use runit as a simple process supervisor alongside the default Arch Linux's init system ([systemd](/index.php/Systemd "Systemd")). For this purpose, install [runit-systemd](https://aur.archlinux.org/packages/runit-systemd/), which provides a barebones runit installation without any stage scripts (`/etc/runit/{1..3}`) or runlevels (`/etc/runit/runsvdir/*`), which are generally only useful when using runit as the init system. The package provides a directory (`/var/service`) where the desired runit services can be put and a systemd unit to starts runit monitoring that directory. Only the services configured in `/var/service` will be supervised by runit. Just [enable and start](/index.php/Systemd#Using_units "Systemd") `runit.service`.

### BusyBox's implementation

[BusyBox](/index.php/BusyBox "BusyBox") provides a minimal implementation of runit that can be used for simple processing supervision needs. First, create symbolic links to the BusyBox binary for the necessary tools that are going to be needed:

```
# busybox --list | awk '/runsv|chpst|svlog|^sv$/' | xargs -I{} ln -sv /usr/bin/busybox /usr/local/bin/{}

```

Afterwards, a [systemd](/index.php/Systemd "Systemd") unit file can be created in order to run BusyBox's runit when needed:

 `/etc/systemd/system/busybox-runit.service` 
```
[Unit]
Description=Runit service supervision - BusyBox implementation
Documentation=[http://smarden.org/runit/](http://smarden.org/runit/) [https://busybox.net/downloads/BusyBox.html](https://busybox.net/downloads/BusyBox.html)

[Service]
Environment="PATH=/usr/local/sbin:/usr/local/bin:/usr/bin"
ExecStart=/usr/local/bin/runsvdir -P /var/service
KillSignal=SIGHUP
KillMode=process
Restart=always
SuccessExitStatus=111

[Install]
WantedBy=multi-user.target
```

**Note:**

*   This example unit file presupposes that the directory which is going to contain the enabled services is `/var/service`. This path can be changed according to each specific use case.
*   The `SIGHUP` kill signal is used instead of the default `SIGTERM`, and only on the main *runsvdir* process (thanks to `KillMode=process`) so that processes being controlled by BusyBox's runit implementation are controllably stopped by *runsvdir* before terminating the supervisor. When *runsvdir* ends the processes that are being supervised after receiving a `SIGHUP` signal, it exits with an status code of 111, which needs to be interpreted as a success.

Be sure to create the directory which is going to be supervised by *runsvdir* according to the systemd unit file created. It is also recommended to create a directory in which runit services can be stored (usually `/etc/sv`), and only enabled when needed by creating a symbolic link directed to them from the directory being supervised. See [#General use](#General_use) for more details.

When everything is correctly configured, `busybox-runit.service` can be [enabled and started](/index.php/Systemd#Using_units "Systemd").

## Using runit

<caption>Tools</caption>
| Command | Description |
| `sv` | Control services, analogous to SysV `service` or systemd's `systemctl`. |
| `runsv` | Run a service. This is mostly an internal tool you don't need to call yourself. |
| `runsvdir` | Start a collection of services; it calls `runsv` for every subdirectory. |
| `svlogd` | Log service, usually started from `log/run` in the service directory. |
| `chpst` | Control a process' environment. |

See the man pages for usage details not covered below.

<caption>Paths</caption>
| Path | Description |
| `/etc/sv` | Directory with services; runit has no direct knowledge of this directory. |
| `/var/service` | Service directory being supervised by `runsvdir`. |

### General use

Since runit isn't Arch's default init system you won't get any init scripts by default. Creating them is very easy, for example for [sshd](/index.php/Sshd "Sshd"):

 `/etc/sv/sshd/run` 
```
#!/bin/sh

ssh-keygen -A # Denerate host keys if they don't exist.
exec /usr/sbin/sshd -D
```

Make sure the file is executable. You can enable the service by linking it to `/var/service`:

```
# ln -s /etc/sv/sshd /var/service

```

After `systemctl start runit` it should start automatically.

**Warning:** It's important that tools do NOT daemonize but remain in the foreground, otherwise runit will keep trying to spawn it, resulting in a bunch of copies running!

The [arch-runit-services](https://aur.archlinux.org/packages/arch-runit-services/) package provides some example services in `/etc/sv`.

<caption>Common commands</caption>
| Description | Command |
| List status of services | `sv status /var/service/*` |
| Stop a service immediately (would still start on next boot) | `sv down /var/service/ssh` |
| Start a previously stopped service | `sv up /var/service/sshd` |
| Restart a service | `sv restart /var/service/sshd` |
| Reload a service | `sv reload /var/service/sshd` |
| Stop a service and disable it (won't start next boot): | `rm /var/service/sshd` |

Refer to [sv(8)](http://smarden.org/runit/sv.8.html) for more details.

## Tips

### User Level Services

You can extend the supervision tree by starting a `runsvdir` as a specific user, giving that user control of their own supervise tree.

 `/etc/sv/runsvdir-joe/run` 
```
#!/bin/sh
exec 2>&1
exec chpst -ujoe  runsvdir /home/joe/service
```

### Create an X session service for a user

Create and enanble a runit script:

 `/etc/sv/xorg-joe/run` 
```
#!/bin/sh
exec 2>&1 su -c xinit - joe
```