Related articles

*   [IRC channels](/index.php/IRC_channels "IRC channels")
*   [IRC](/index.php/IRC "IRC")
*   [WeeChat](/index.php/WeeChat "WeeChat")
*   [irssi](/index.php/Irssi "Irssi")
*   [HexChat](/index.php/HexChat "HexChat")

[Quassel](http://quassel-irc.org/) (sometimes referred to as Quassel IRC) is a cross-platform IRC client introduced in 2008\. It is dual-licensed under GPLv2 and GPLv3, while most graphical data is licensed under the LGPL and provided by the [Oxygen Team](http://www.oxygen-icons.org/). The client part of Quassel uses the Qt framework for its user interface.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Structure](#Structure)
*   [2 Installation](#Installation)
    *   [2.1 Basic usage](#Basic_usage)
    *   [2.2 Setting up a bouncer (Quassel core) to be permanently online](#Setting_up_a_bouncer_(Quassel_core)_to_be_permanently_online)
    *   [2.3 Setting up multiple clients to connect through the same core](#Setting_up_multiple_clients_to_connect_through_the_same_core)
*   [3 See also](#See_also)

## Structure

Quassel is split up into two parts by a server-client model; a client and a core. There is also a monolithic version of the official client that does not require a core. The core(server) is the application that actually does the communication with IRC networks, while the client(s) only communicates with the core. This gives the user a flexibility of having the same instance to IRC networks on different clients (e.g. mobile, desktop at the same time).

## Installation

### Basic usage

Just install the [quassel-monolithic](https://www.archlinux.org/packages/?name=quassel-monolithic) package if you only want to use Quassel from a single computer.

### Setting up a bouncer (Quassel core) to be permanently online

Install [quassel-core](https://www.archlinux.org/packages/?name=quassel-core) on the server and [quassel-client](https://www.archlinux.org/packages/?name=quassel-client) (or [quassel-client-small](https://www.archlinux.org/packages/?name=quassel-client-small)) on your desktop. If the server is headless, you could install [quassel-core-small](https://aur.archlinux.org/packages/quassel-core-small/) instead to avoid unnecessary dependencies like X11 libraries.

Generate a certificate (this will be valid for 1 years, after which it needs to be reissued, just change the -days to another value if you so desire):

```
# openssl req -x509 -nodes -days 365 -newkey rsa:4096 -keyout /var/lib/quassel/quasselCert.pem -out /var/lib/quassel/quasselCert.pem
# chown quassel:quassel /var/lib/quassel/quasselCert.pem

```

As this is a self-signed certificate, you can type whatever you want in the fields.

Open port `4242` in your [firewall](/index.php/Firewall "Firewall").

Start core by [starting](/index.php/Start "Start") `quassel.service`.

Start the client and connect to core:

```
$ quasselclient

```

Accept your self-created certificate.

Now set up your IRC-servers and IRC-nicknames on the core.

**Note:** As this is the first time you connected to the core, you should see a wizard where you can set up the first user-account. If you do not get this wizard, your settings might be messed up, see troubleshooting below.

If you choose to use [PostgreSQL](/index.php/PostgreSQL "PostgreSQL") as backend you will need to create a database and user for quasselcore.

```
[postgres]$ psql -c "CREATE USER quassel WITH PASSWORD '*myPassword*';"
[postgres]$ psql -c "CREATE DATABASE quassel WITH OWNER quassel ENCODING 'UTF8';"

```

See also [PostgreSQL instruction on Quassel wiki](https://bugs.quassel-irc.org/projects/quassel-irc/wiki/PostgreSQL).

Once it all works, you can [enable](/index.php/Enable "Enable") `quassel.service` to start automatically on system boot.

### Setting up multiple clients to connect through the same core

If you want additional users to be able to use the same core, run this command to create them:

```
$ sudo -u quassel quasselcore --configdir=/var/lib/quassel --add-user

```

It will then prompt you for a new account's username and password.

## See also

*   [QuasselWiki](http://bugs.quassel-irc.org/projects/quassel-irc/wiki)