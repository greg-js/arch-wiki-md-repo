# Quassel

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Quassel (sometimes referred to as Quassel IRC) is a cross-platform IRC client introduced in 2008\. It is dual-licensed under GPLv2 and GPLv3, while most graphical data is licensed under the LGPL and provided by the [Oxygen Team](http://www.oxygen-icons.org/). The client part of Quassel uses the Qt framework for its user interface.

## Contents

*   [1 Structure](#Structure)
*   [2 Installation](#Installation)
    *   [2.1 Basic usage](#Basic_usage)
    *   [2.2 Setting up multiple clients to connect through the same core](#Setting_up_multiple_clients_to_connect_through_the_same_core)
*   [3 Troubleshooting](#Troubleshooting)

## Structure

Quassel is split up into two parts by a server-client model; a client and a core. There is also a monolithic version of the official client that does not require a core. The core(server) is the application that actually does the communication with IRC networks, while the client(s) only communicates with the core. This gives the user a flexibility of having the same instance to IRC networks on different clients (e.g. mobile, desktop at the same time).

**Note:** Arch Linux used to have two packages, where quassel-monolighic was part of quassel-client, this was fixed in [FS#39756](https://bugs.archlinux.org/task/39756) but if you used to run the monolithic version, you might run into problems after the update. You could try by just installing quassel-monolithic or if that does not help see troubleshooting below.

## Installation

### Basic usage

Just install the [quassel-monolithic](https://www.archlinux.org/packages/?name=quassel-monolithic) package if you only want to use Quassel from a single computer.

### Setting up multiple clients to connect through the same core

Install [quassel-core](https://www.archlinux.org/packages/?name=quassel-core) and [quassel-client](https://www.archlinux.org/packages/?name=quassel-client).

Generate a certificate (this will be valid for 1 years, after which it needs to be reissued, just change the -days to another value if you so desire):

 `# openssl req -x509 -nodes -days 365 -newkey rsa:4096 -keyout /var/lib/quassel/quasselCert.pem -out /var/lib/quassel/quasselCert.pem` 

As this is a self-signed certificate, you can type whatever you want in the fields.

Open port 4242 in your firewall.

Start core:

 `# systemctl start quassel` 

Start the client and connect to core:

 `$ quasselclient` 

Accept your self-created certificate.

Now set up your IRC-servers and IRC-nicknames on the core.

**Note:** As this is the first time you connected to the core, you should see a wizard where you can set up the first user-account. If you do not get this wizard, your settings might be messed up, see troubleshooting below.

Once it all works, you can set it up to start automatically through on system boot:

 `# systemctl enable quassel` 

**Note:** This has been fixed as of quassel 0.12.0-1.

```
This is supposed to work but does not because of a bug [FS#38950](https://bugs.archlinux.org/task/38950) but it is easy to work around:

Copy the system service file to make a override in /etc/systemd/system/ (then when the bug is fixed you can just remove this file)

# cp /usr/lib/systemd/system/quassel.service /etc/systemd/system/

Then edit the file /etc/systemd/system/quassel.service and remove --listen=${LISTEN} from ExecStart.
```

## Troubleshooting

If you were previously using quassel-monolithic, your settings might be messed up. Close quasselcore. Move your settings database to a backup copy:

 `$ mv /~/.config/quassel-irc.org/quassel-storage.sqlite /~/.config/quassel-irc.org/quassel-storage.sqlite.bak` 

Then start quasselcore again and connect from your client, you should now get the wizard to show, however, all settings will have to be re-entered.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Quassel&oldid=416151](https://wiki.archlinux.org/index.php?title=Quassel&oldid=416151)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Internet Relay Chat](/index.php/Category:Internet_Relay_Chat "Category:Internet Relay Chat")