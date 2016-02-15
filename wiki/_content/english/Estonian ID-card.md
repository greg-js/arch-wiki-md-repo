Packages to enable Estonian ID-card support are available from the [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository"). This article explains how to install the official software versions by AS Sertifitseerimiskeskus.

## Quick install

Install [pcsclite](https://www.archlinux.org/packages/?name=pcsclite) from the [official repositories](/index.php/Official_repositories "Official repositories") and [esteidfirefoxplugin](https://aur.archlinux.org/packages/esteidfirefoxplugin/), [qdigidoc](https://aur.archlinux.org/packages/qdigidoc/) and [qesteidutil](https://aur.archlinux.org/packages/qesteidutil/) from the [AUR](/index.php/AUR "AUR").

Enable `pcscd.socket` [using systemd](/index.php/Systemd#Using_units "Systemd").

## Browser plugin (web authentication & digital signatures)

The browser plugin AUR package is called [esteidfirefoxplugin](https://aur.archlinux.org/packages/esteidfirefoxplugin/), which also requires dependencies [esteidpkcs11loader](https://aur.archlinux.org/packages/esteidpkcs11loader/) and [esteidcerts](https://aur.archlinux.org/packages/esteidcerts/).

It also requires you to run the PCSC daemon, which can be installed with [pcsclite](https://www.archlinux.org/packages/?name=pcsclite) from the [official repositories](/index.php/Official_repositories "Official repositories").

Make it auto-start on demand by enabling `pcscd.socket` [using systemd](/index.php/Systemd#Using_units "Systemd").

Don't forget to restart Firefox after finishing.

## ID-card and Digidoc utilities

The ID-card utility packages are [qesteidutil](https://aur.archlinux.org/packages/qesteidutil/) and [qdigidoc](https://aur.archlinux.org/packages/qdigidoc/), with dependencies [esteidcerts](https://aur.archlinux.org/packages/esteidcerts/), [libdigidoc](https://aur.archlinux.org/packages/libdigidoc/) and [libdigidocpp](https://aur.archlinux.org/packages/libdigidocpp/).

These applications will automatically appear in your application menus. You can also start from command line with <tt>qdigidocclient</tt> and <tt>qesteidutil</tt>.