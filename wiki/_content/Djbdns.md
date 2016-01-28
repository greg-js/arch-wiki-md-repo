# Djbdns

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

This article outlines how to install [djbdns](http://cr.yp.to/djbdns.html) (dnscache and tinydns) on Arch Linux.

## Installation

Currently the [djbdns](https://aur.archlinux.org/packages/djbdns/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/djbdns)]</sup> suite of tools are only available via [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository"), but they are perfectly functional and up to date.

dnscache and tinydns processes are managed by [daemontools](https://aur.archlinux.org/packages/daemontools/)<sup><small>AUR</small></sup>, which is installed as dependency. Enable and start [systemd](/index.php/Systemd "Systemd") daemontools service, `svscan`.

Configure and run dnscache:

```
dnscache-conf dnscache dnslog /etc/dnscache [myip]
ln -s /etc/dnscache /service

```

Configure and run tinydns:

```
tinydns-conf tinydns dnslog /etc/tinydns myip
ln -s /etc/tinydns /service

```

**Note**: Change `myip` to your public ip. If `[myip]` is omitted dnscache will run on localhost.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Djbdns&oldid=413315](https://wiki.archlinux.org/index.php?title=Djbdns&oldid=413315)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Domain Name System](/index.php/Category:Domain_Name_System "Category:Domain Name System")

Hidden category:

*   [Pages with broken package links](/index.php/Category:Pages_with_broken_package_links "Category:Pages with broken package links")