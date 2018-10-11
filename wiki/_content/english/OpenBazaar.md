Related articles

*   [ZeroNet](/index.php/ZeroNet "ZeroNet")
*   [Tor](/index.php/Tor "Tor")

[OpenBazaar](https://en.wikipedia.org/wiki/OpenBazaar "wikipedia:OpenBazaar") is an open source project developing a protocol for e-commerce transactions in a fully decentralized marketplace using cryptocurrencies.

This is experimental software. Use at your own risk.

## Contents

*   [1 Installation](#Installation)
*   [2 Start server](#Start_server)
    *   [2.1 As user](#As_user)
        *   [2.1.1 As user with Tor Browser](#As_user_with_Tor_Browser)
        *   [2.1.2 As user with Tor](#As_user_with_Tor)
    *   [2.2 System-wide](#System-wide)
*   [3 Start client](#Start_client)
*   [4 See also](#See_also)

## Installation

The [openbazaar](https://aur.archlinux.org/packages/openbazaar/) package provides the client and [openbazaard](https://aur.archlinux.org/packages/openbazaard/) provides the server.

## Start server

You can view the configuration options with `openbazaard start --help`.

We will use [Tor](/index.php/Tor "Tor") for more anonymity and `--allowip=127.0.0.1` so only you have access to your OB server.

Also consider the options `--password=` to encrypt the database, and `--disablewallet` to disable the wallet functionality of the node.

### As user

We will store the OB server files in `~/.local/share/openbazaar`.

#### As user with Tor Browser

Pro: less configuration, con: you must start [Tor Browser](/index.php/Tor_Browser "Tor Browser") first. see [torbrowser-launcher-git](https://aur.archlinux.org/packages/torbrowser-launcher-git/)

Run as user:

```
$ openbazaard start -d ~/.local/share/openbazaar --tor --allowip=127.0.0.1 --verbose

```

with the `--tor` option, OB server will use your Tor Browser as the Tor entry node.

#### As user with Tor

To use your system-wide Tor proxy, you must configure Tor first.

Choose a password to secure your Tor Control Port. Run

```
$ tor --hash-password *password*

```

to get the password hash.

Add to your `/etc/tor/torrc` file:

```
ControlPort 9051
HashedControlPassword *hash*

```

setting `HashedControlPassword` to your password hash.

Now you can start the OB server as user:

```
$ openbazaard start -d ~/.local/share/openbazaar --torpassword=your_tor_control_password --allowip=127.0.0.1 --verbose

```

setting `--torpassword` to your Tor password.

### System-wide

We will store the OB server files in `/var/lib/openbazaar`.

openbazaard will run as user `openbazaar` in group `openbazaar`.

We will use system-wide Tor, not Tor Browser.

Read section [#As user with Tor](#As_user_with_Tor) to configure tor.

Edit server configuration file `/etc/conf.d/openbazaard` as root

```
# OB_ARGS="-d /var/lib/openbazaar --torpassword=your_tor_control_password --allowip=127.0.0.1 --verbose"

```

To init the server files run as root

```
# mkdir /var/lib/openbazaar
# chown openbazaar:openbazaar /var/lib/openbazaar
# chmod 0700 /var/lib/openbazaar

```

The `openbazaard` [systemd](/index.php/Systemd "Systemd") service seems broken at the moment. It will look good, but not start the OB server. `openbazaard status` will only show your database status, and whether tor is available. it will not show, whether OB server is running.

Instead, run as root

```
# source /etc/conf.d/openbazaard
# sudo -u openbazaar openbazaard start $OB_ARGS

```

You should see some ASCII art

```
________                      __________
\_____  \ ______   ____   ____\______   \_____  _____________  _____ _______
 /   |   \\____ \_/ __ \ /    \|    |  _/\__  \ \___   /\__  \ \__  \\_  __ \ 
/    |    \  |_> >  ___/|   |  \    |   \ / __ \_/    /  / __ \_/ __ \|  | \/
\_______  /   __/ \___  >___|  /______  /(____  /_____ \(____  (____  /__|
        \/|__|        \/     \/       \/      \/      \/     \/     \/

```

... along with error-free log messages

Wait for

```
[INFO] [cmd/newHTTPGateway] Gateway/API server listening on /ip4/127.0.0.1/tcp/4002

```

For more server configuration, see

```
openbazaard gencerts --help
openbazaard setapicreds --help

```

To generate SSL certificates, or set username and password for 'API access' to allow clients to connect. Both will need the option `-d dir` or `--datadir=dir`

## Start client

Run `openbazaar` as user.

The default server configuration should be fine.

If your server admin did configure a login with `openbazaard setapicreds` then fill the Username and Password fields.

To connect to a tor-hidden OB server, set *Server IP* to the `.onion` address, activate *Use Tor*, and enter your_tor_control_password to connect via your system tor node.

Otherwise, when using the localhost OB server, the *Use Tor* setting *should* not be needed.

## See also

*   [Official website](https://openbazaar.org/)