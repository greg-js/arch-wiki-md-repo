[Mosh](https://mosh.org/) is an alternative interactive [SSH](/index.php/SSH "SSH") terminal. It has support for roaming and local echo. It also aims to improve responsiveness on intermittent, and high latency connections.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Setup and Usage](#Setup_and_Usage)
    *   [2.1 Server Setup](#Server_Setup)
    *   [2.2 Using the Client](#Using_the_Client)
*   [3 Notes](#Notes)

## Installation

**Note:** Mosh must be installed on both the server and client.

[Install](/index.php/Install "Install") the [mosh](https://www.archlinux.org/packages/?name=mosh) package, or [mosh-git](https://aur.archlinux.org/packages/mosh-git/) for the latest revision.

## Setup and Usage

**Note:** Mosh by design does not let you access session history, consider installing a terminal multiplexer such as [tmux](/index.php/Tmux "Tmux") or [GNU Screen](/index.php/GNU_Screen "GNU Screen").

### Server Setup

Start a simple mosh server use:

```
 $ mosh-server new -p port

```

An enabled [systemd](/index.php/Systemd "Systemd") service is strongly reccomended.

 `$ systemctl edit mosh.service` 
```
[Unit]
Description=Mosh Service

[Service]
ExecStart=/usr/bin/mosh-server

[Install]
WantedBy=multi-user.target
```

### Using the Client

To connect to a running mosh server run:

```
$ mosh -p *mosh-udp-port* *user@server-address*

```

To send ssh options for connecting:

```
$ mosh --ssh="ssh -p 2222" *user@server-address*

```

## Notes

**Note:** Mosh has an undocumented command line option `--predict=experimental` which produces more aggressive echoing of local keystrokes. Users interested in low-latency visual confirmation of keyboard input may prefer this prediction mode.