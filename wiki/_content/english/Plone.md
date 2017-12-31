[Plone](http://plone.org/) is a free and open source content management system built on top of the Zope application server written in [Python](/index.php/Python "Python"). Plone can be used for all kinds of websites, including blogs, internet sites, webshops and intranets. The strengths of Plone are its flexible and adaptable workflow, very good security, extensibility, high usability and flexibility.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Manual Installation](#Manual_Installation)
*   [2 Starting Plone](#Starting_Plone)
    *   [2.1 Automatically using Systemd](#Automatically_using_Systemd)
*   [3 Customizing](#Customizing)
*   [4 Upgrades](#Upgrades)
*   [5 See Also](#See_Also)

## Installation

[Install](/index.php/Install "Install") package [plone](https://aur.archlinux.org/packages/plone/) from the [AUR](/index.php/AUR "AUR"). Please be aware, that the AUR package copies the Plone Unified Installer to `/opt/plone`, which is then run by Pacman upon initial install. The Unified Installer compiles and installs Plone in `/opt/plone`. The package provides a convenient way to quickly install and get up and running with Plone, as it handles the dependencies and bundles a systemd unit file.

Note, that Plone site version upgrades are not handled by [Pacman](/index.php/Pacman "Pacman") using the AUR package, because the files in `/opt/plone` are not managed by Pacman directly. Re-running the installer is not the recommended way to upgrade Plone (see below for instructions on how to upgrade a Plone site).

### Manual Installation

The official way to install Plone is by using the Unified Installer, which is also used by the [plone](https://aur.archlinux.org/packages/plone/) package. Doing a manual install will give you additional options.

The following prerequisites need to be installed:

*   Required: [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/)
*   Recommended:[libxml2](https://www.archlinux.org/packages/?name=libxml2) [libxslt](https://www.archlinux.org/packages/?name=libxslt) [libjpeg-turbo](https://www.archlinux.org/packages/?name=libjpeg-turbo) [openssl](https://www.archlinux.org/packages/?name=openssl) [sudo](https://www.archlinux.org/packages/?name=sudo)
*   Optional: [wv](https://www.archlinux.org/packages/?name=wv) [poppler](https://www.archlinux.org/packages/?name=poppler) for Word and PDF document indexing

Download the latest installer from [here](http://plone.org/products) and follow the [Plone Install Docs](https://plone.org/documentation) and some Arch Linux specific [Server Preparations](http://docs.plone.org/manage/deploying/preparing.html)

For example to install Plone for production use, using a ZEO server configuration do the following as root:

```
pacman -S base-devel libxml2 libxslt libjpeg-turbo openssl sudo
pver=4.3.2 # replace this with the latest version
wget [http://launchpad.net/plone/${pver:0:3}/$pver/+download/Plone-$pver-UnifiedInstaller.tgz](http://launchpad.net/plone/${pver:0:3}/$pver/+download/Plone-$pver-UnifiedInstaller.tgz)
tar -xzf *UnifiedInstaller.tgz
./Plone-$pver-UnifiedInstaller/install.sh --target=/opt/plone zeo

```

The installer provides informative messages as well as saving an `install.log` to help analyse potential problems.

## Starting Plone

Manually start the service with:

```
sudo -u plone_daemon /opt/plone/zeocluster/bin/plonectl start

```

Then try the site on `[http://yoursite:8080](http://yoursite:8080)`

Use the displayed login password, which can also be found in `/opt/Plone/zeocluster/adminPassword.txt` The start page allows you to create an initial site, by filling in the name of the new site and choosing optional add-ons.

Stop the service with:

```
sudo -u plone_daemon /opt/plone/zeocluster/bin/plonectl stop

```

#### Automatically using Systemd

To enable the Plone service by default at start-up, run:

```
systemctl enable plone

```

## Customizing

To change ports, or to install add-ons and themes edit the file `buildout.cfg` at `/opt/plone/zeocluster`.

Apply the new settings by running:

```
cd /opt/plone/zeocluster
sudo -u plone_buildout bin/buildout 

```

## Upgrades

Upgrades are done in a similar way using buildout. This should be fairly straightforward, from one minor version to another. For example to upgrade to Plone 4.3.x do the following: In your `buildout.cfg`, comment out `versions.cfg` and uncomment the line pointing to dist.plone.org, so it looks like this:

```
extends = 
base.cfg
# versions.cfg
[http://dist.plone.org/release/4.3-latest/versions.cfg](http://dist.plone.org/release/4.3-latest/versions.cfg) 

```

Then stop Plone and re-run buildout:

```
cd /opt/plone/zeocluster
sudo -u plone_buildout bin/buildout  

```

Restart Plone and visit the Management Interface at ([http://yoursite:8080](http://yoursite:8080)). You will likely see a message prompting you to run Plone's migration script. Click the Upgrade button next to the site and the upgrade script will run.

For more information on upgrades, especially between major versions of Plone read the [Upgrade Guide](http://plone.org/documentation/manual/upgrade-guide)

## See Also

*   [Plone Official Site](http://http://plone.org/)
*   [Official Documentation](http://plone.org/documentation)
*   [Plone Wikipedia Article](https://en.wikipedia.org/wiki/Plone_(software) "wikipedia:Plone (software)")