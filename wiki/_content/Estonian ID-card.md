# Estonian ID-card

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[![Tango-go-next.png](/images/f/f0/Tango-go-next.png)](/index.php/File:Tango-go-next.png)

[![Tango-go-next.png](/images/f/f0/Tango-go-next.png)](/index.php/File:Tango-go-next.png)

**This article or section is a candidate for moving to [eID card](/index.php?title=EID_card&action=edit&redlink=1 "EID card (page does not exist)").**

**Notes:** Shared instructions amongst different eID cards (card readers, pcsc), different mostly in middleware and browser plugins. Merge with [Belgian eID card reader](/index.php/Belgian_eID_card_reader "Belgian eID card reader"). (Discuss in [Talk:Estonian ID-card#](https://wiki.archlinux.org/index.php/Talk:Estonian_ID-card))

Packages to enable Estonian ID-card support are available from the [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository"). This article explains how to install the official software versions by AS Sertifitseerimiskeskus.

## Quick install

Install [pcsclite](https://www.archlinux.org/packages/?name=pcsclite) from the [official repositories](/index.php/Official_repositories "Official repositories") and [esteidfirefoxplugin](https://aur.archlinux.org/packages/esteidfirefoxplugin/)<sup><small>AUR</small></sup>, [qdigidoc](https://aur.archlinux.org/packages/qdigidoc/)<sup><small>AUR</small></sup> and [qesteidutil](https://aur.archlinux.org/packages/qesteidutil/)<sup><small>AUR</small></sup> from the [AUR](/index.php/AUR "AUR").

Enable `pcscd.socket` [using systemd](/index.php/Systemd#Using_units "Systemd").

## Browser plugin (web authentication & digital signatures)

The browser plugin AUR package is called [esteidfirefoxplugin](https://aur.archlinux.org/packages/esteidfirefoxplugin/)<sup><small>AUR</small></sup>, which also requires dependencies [esteidpkcs11loader](https://aur.archlinux.org/packages/esteidpkcs11loader/)<sup><small>AUR</small></sup> and [esteidcerts](https://aur.archlinux.org/packages/esteidcerts/)<sup><small>AUR</small></sup>.

It also requires you to run the PCSC daemon, which can be installed with [pcsclite](https://www.archlinux.org/packages/?name=pcsclite) from the [official repositories](/index.php/Official_repositories "Official repositories").

Make it auto-start on demand by enabling `pcscd.socket` [using systemd](/index.php/Systemd#Using_units "Systemd").

Don't forget to restart Firefox after finishing.

## ID-card and Digidoc utilities

The ID-card utility packages are [qesteidutil](https://aur.archlinux.org/packages/qesteidutil/)<sup><small>AUR</small></sup> and [qdigidoc](https://aur.archlinux.org/packages/qdigidoc/)<sup><small>AUR</small></sup>, with dependencies [esteidcerts](https://aur.archlinux.org/packages/esteidcerts/)<sup><small>AUR</small></sup>, [libdigidoc](https://aur.archlinux.org/packages/libdigidoc/)<sup><small>AUR</small></sup> and [libdigidocpp](https://aur.archlinux.org/packages/libdigidocpp/)<sup><small>AUR</small></sup>.

These applications will automatically appear in your application menus. You can also start from command line with <tt>qdigidocclient</tt> and <tt>qesteidutil</tt>.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Estonian_ID-card&oldid=411309](https://wiki.archlinux.org/index.php?title=Estonian_ID-card&oldid=411309)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Other hardware](/index.php/Category:Other_hardware "Category:Other hardware")