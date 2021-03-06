[Tryton](http://www.tryton.org/) is a three-tiers high-level general purpose application platform under the license GPL-3 written in Python and using PostgreSQL (or sqlite) as database engine.

## Installation

Install the server application, [trytond](https://aur.archlinux.org/packages/trytond/), from the [AUR](/index.php/AUR "AUR").

Once trydond is installed, install the client application, [tryton](https://aur.archlinux.org/packages/tryton/), from the [AUR](/index.php/AUR "AUR").

## Configuring

As root or using sudo, edit the file `/etc/trytond.conf`.

Here you will find options which you can uncomment and fill out as necessary.

Next, as root, create the directory `/var/lib/trytond`, and chown it so that the trytond user can access it.

Now you can launch trytond and the tryton client.

Run `/etc/rc.d/trytond` start as root, and then launch tryton as a regular user.