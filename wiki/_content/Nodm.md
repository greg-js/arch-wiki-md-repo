# Nodm

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Related articles

*   [Display manager](/index.php/Display_manager "Display manager")

[nodm](http://enricozini.org/sw/nodm/) is an automatic display manager which automatically starts an X session at system boot. It is meant for devices like smartphones, but can be used on a regular computer as well, if the security implications are acceptable.

## Installation

[Install](/index.php/Install "Install") the [nodm](https://www.archlinux.org/packages/?name=nodm) package.

Now ensure no other display managers get started by [disabling](/index.php/Disabling "Disabling") their systemd services.

After installing nodm, you should modify the /etc/nodm.conf file.

Now set the NODM_USER variable to the user that should be automatically logged in, and change the NODM_XSESSION variable to point to the script that starts your session. This script must be executable!

```
NODM_USER='{user}'
NODM_XSESSION='/home/{user}/.xinitrc'

```

Enable the systemd service so it will be started on boot.

```
sudo systemctl enable nodm

```

Retrieved from "[https://wiki.archlinux.org/index.php?title=Nodm&oldid=409449](https://wiki.archlinux.org/index.php?title=Nodm&oldid=409449)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Display managers](/index.php/Category:Display_managers "Category:Display managers")