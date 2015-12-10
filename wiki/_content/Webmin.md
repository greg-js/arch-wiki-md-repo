# Webmin

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

From the project [home page](http://www.webmin.com/):

_Webmin is a web-based interface for system administration for Unix. Using any modern web browser, you can setup user accounts, Apache, DNS, file sharing and much more. Webmin removes the need to manually edit Unix configuration files like `/etc/passwd`, and lets you manage a system from the console or remotely. See the [standard modules](http://www.webmin.com/standard.html) page for a list of all the functions built into Webmin, or check out the [screenshots](http://www.webmin.com/demo.html)._

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
*   [3 Starting](#Starting)
*   [4 Usage](#Usage)
*   [5 Troubleshooting](#Troubleshooting)

## Installation

You can install [webmin](https://aur.archlinux.org/packages/webmin/)<sup><small>AUR</small></sup> from the [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository"). Webmin requires [perl-net-ssleay](https://www.archlinux.org/packages/?name=perl-net-ssleay) to enable access via [https](https://en.wikipedia.org/wiki/https "wikipedia:https").

## Configuration

To allow access to Webmin from a remote computer, edit `/etc/webmin/miniserv.conf` to include your network address. (Note - 127.0.0.1 is there by default)

```
allow=127.0.0.1 192.168.1.0

```

The above example allows all computers on the 192.168.1.0 network to access Webmin.

## Starting

Start webmin [service](/index.php/Daemon "Daemon") using [systemd](/index.php/Systemd "Systemd"). Enable it if you wish to load webmin at boot.

## Usage

In a web browser, enter the https address of the server with the port number 10000 to access Webmin - for example:

https://192.168.1.1:10000 -or- https://myserver.example.net:10000

You will need to enter the root password of the server running Webmin to use the Webmin interface and administer the server.

## Troubleshooting

If you get a an error similar to

```
Can't locate timelocal.pl in @INC (@INC contains: /opt/webmin /usr/lib/perl5/site_perl /usr/share/perl5/site_perl /usr/lib/perl5/vendor_perl /usr/share/perl5/vendor_perl /usr/lib/perl5/core_perl /usr/share/perl5/core_perl . /opt/webmin/ ..) at /opt/webmin/useradmin/edit_user.cgi line 6.

```

for example, when adding a new system user through Webmin, you [need to install](https://bbs.archlinux.org/viewtopic.php?id=142757) [perl-perl4-corelibs](https://www.archlinux.org/packages/?name=perl-perl4-corelibs).

The password of a webmin user can be reset using the perl script included with the installation tarball (in this example, uncompressed to /opt/webmin):

```
/opt/webmin/changepass.pl /etc/webmin _user password_

```

Retrieved from "[https://wiki.archlinux.org/index.php?title=Webmin&oldid=409656](https://wiki.archlinux.org/index.php?title=Webmin&oldid=409656)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Web server](/index.php/Category:Web_server "Category:Web server")