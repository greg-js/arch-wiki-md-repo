This page provides an overview of the Arch servers and their functions. Details can be found in the respective links for each server.

## Contents

*   [1 Main development server (formerly gerolde)](#Main_development_server_(formerly_gerolde))
    *   [1.1 dom0.archlinux.org](#dom0.archlinux.org)
    *   [1.2 gerolde.archlinux.org](#gerolde.archlinux.org)
    *   [1.3 gudrun.archlinux.org](#gudrun.archlinux.org)
    *   [1.4 Resource Allocation](#Resource_Allocation)
*   [2 nymeria.archlinux.org](#nymeria.archlinux.org)
*   [3 luna.archlinux.org](#luna.archlinux.org)
*   [4 Releng server (alberich)](#Releng_server_(alberich))
    *   [4.1 alberich.archlinux.org](#alberich.archlinux.org)
*   [5 Build Server (celestia)](#Build_Server_(celestia))
    *   [5.1 pkgbuild.com](#pkgbuild.com)
*   [6 dragon.archlinux.org](#dragon.archlinux.org)
*   [7 Other servers](#Other_servers)
    *   [7.1 stats.archlinux.org](#stats.archlinux.org)

## Main development server (formerly gerolde)

This is a Dual-Xeon 2.8GHz server with 16GB of memory and a 2x300GB software RAID 1 array. It has been bought with Arch donation money and is currently located at velocity, who also donate the power and bandwidth. It runs a Xen hypervisor with the following hosts:

### [dom0.archlinux.org](/index.php/DeveloperWiki:Dom0 "DeveloperWiki:Dom0")

This is the Xen dom0 for the development server. It runs a Debian system with the Debian Xen kernel, as Arch does not maintain a stable Xen kernel. It has no public services. ssh access is limited to a small number of IP addresses and only Thomas, Aaron, Jan and Dale have access to it.

It bridges the physical ethernet interface with the virtual interfaces of the Xen domU instances and runs an IP-based [firewall](/index.php/DeveloperWiki:Dom0#Firewall "DeveloperWiki:Dom0").

### [gerolde.archlinux.org](/index.php/DeveloperWiki:Gerolde_(dev) "DeveloperWiki:Gerolde (dev)")

Legacy development server.

DNS aliases: gerolde.archlinux.org

It offers the following public services:

*   *ssh*(openssh)
*   *smtp*(postfix): SMTP server for outgoing mail

### [gudrun.archlinux.org](/index.php/DeveloperWiki:Gudrun_(web) "DeveloperWiki:Gudrun (web)")

This is the legacy web server. It runs Arch Linux with Arch's own kernel. Only developers who maintain web applications have ssh access. The ssh port is only open to gerolde.

DNS aliases: dev.archlinux.org, mailman.archlinux.org, planet.archlinux.org, projects.archlinux.org, repos.archlinux.org, bugs.archlinux.org

It offers the following public services:

*   *http*(apache): Hosts the following websites:
    *   www.archlinux.org: Main Arch website - uses python/django and a few static html pages
    *   mailman.archlinux.org: redirect to lists.archlinux.org
    *   projects.archlinux.org: Access to the git repositories - uses cgit
    *   planet.archlinux.org: Feeds from Arch-related blogs - uses static html pages
    *   repos.archlinux.org: Access to the *packages* and *community* subversion repositories - uses websvn
    *   bugs.archlinux.org: Bugtracker - uses flyspray(php)
*   *svn*(xinetd/svnserve): Public subversion access
*   *git*(xinetd/git-daemon): Public git access

### Resource Allocation

Because this box is servicing multiple VMs, the resources allocated to each are not static. Here is how the box is currently divided up:

*   dom0: 512 MB RAM, 4 CPUs, 4GB disk
*   gerolde: 9493 MB RAM, 4 CPUs, 193 GB disk
*   gudrun: 6145 MB RAM, 4 CPUs, 30 GB disk

## [nymeria.archlinux.org](/index.php?title=DeveloperWiki:Nymeria_(dev)&action=edit&redlink=1 "DeveloperWiki:Nymeria (dev) (page does not exist)")

This is the main development server.

DNS aliases: rsync.archlinux.org, nymeria.archlinux.org, mail.archlinux.org, svn.archlinux.org

It offers the following public services:

*   *ssh*(openssh): All developers and trusted users have ssh access to this machine.
*   *rsync*(rsyncd): Public mirrors (whitelisted by IP address) can synchronize the FTP directory. Anyone can synchronize the ABS tree.
*   *smtp*(postfix): SMTP server for the @archlinux.org and @aur.archlinux.org domains
*   ``imap``(dovecot): IMAP server for local mail storage
*   *http*(nginx): All developers have direct access to the FTP directory via HTTP (static content only) - this is password-protected, users must use the mirrors.

Developers use this server to maintain the package repositories, the corresponding *packages* subversion repository and access the git repositories for their various arch-related projects.

## [luna.archlinux.org](/index.php/DeveloperWiki:Luna "DeveloperWiki:Luna")

*   *nginx*
    *   bbs.archlinux.org: Forums - uses fluxbb(php)
    *   wiki.archlinux.org: Arch Wiki - uses mediawiki(php)
    *   aur.archlinux.org: AUR; website and GIT access
    *   lists.archlinux.org: Mailing lists (mailman)
    *   sources.archlinux.org: GPL and other sources repository

## Releng server (alberich)

*   hardware: VPS donated by airVM, 125GiB LVM setup, 2GB ram, 1 core E5530 @ 2.40GHz
*   software: Arch Linux

### [alberich.archlinux.org](/index.php?title=DeveloperWiki:Alberich&action=edit&redlink=1 "DeveloperWiki:Alberich (page does not exist)")

This machine is meant for building installation images and hosting testbuilds and such. It runs no other services, because releng image building is "tricky stuff" best kept separate

The machine contains the releng environment, including chroots for each architecture.

DNS aliases: releng.archlinux.org, tracker.archlinux.org

It offers the following public services:

*   *ssh*(openssh): All release engineers have ssh access to this machine.
*   *http*(lighttpd): To host releng files (testbuilds, custom repos/packages), no official media
*   *bit torrent*: Torrent tracker for the ISO

## Build Server ([celestia](/index.php?title=DeveloperWiki:Celestia&action=edit&redlink=1 "DeveloperWiki:Celestia (page does not exist)"))

This is an Intel(R) Core(TM) i7-4770 CPU server with 32GB of memory. The machine is run by Ionut Biru (ioni). It runs Arch Linux.

### [pkgbuild.com](/index.php/DeveloperWiki:PKGBUILD.com "DeveloperWiki:PKGBUILD.com")

DNS: celestia.archlinux.org, pkgbuild.archlinux.org

It offers the following services:

*   *ssh* (openssh): Access to the build server is available to all Trusted Users and Developers on request.

*   Build server.
    *   Each user is given access to a set of build scripts that simplify the build process for users with poor internet connections or lacking a 64-bit machine.

## [dragon.archlinux.org](/index.php/DeveloperWiki:Dragon "DeveloperWiki:Dragon")

DNS: dragon.archlinux.org, backup.archlinux.org

It offers he following services:

*   *ssh*: Access to the server for managing backups
*   storage for backups.

## Other servers

We can always use more of course for our world domination plans! Right now our infrastructure is mostly contained to the above-mentioned servers, but there are a few specialty things running elsewhere.

### stats.archlinux.org

This server is hosted on [Dan's](/index.php/User:Toofishes "User:Toofishes") linode. It runs an instance of munin, which collects various stats from the servers in the archlinux.org domain. If you need access to any of this information and are a developer, get in contact with someone that does [server administration](/index.php/DeveloperWiki:Internal_Projects#Server_Administration "DeveloperWiki:Internal Projects"). If you want an additional server added to the list, just ask.