Packages to enable Estonian ID-card support are available from the [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository"). This article explains how to install the official software versions by AS Sertifitseerimiskeskus.

## Quick install

1\. Install [pcsclite](https://www.archlinux.org/packages/?name=pcsclite) from the [official repositories](/index.php/Official_repositories "Official repositories") and [chrome-token-signing](https://aur.archlinux.org/packages/chrome-token-signing/), [qdigidoc](https://aur.archlinux.org/packages/qdigidoc/) and [qesteidutil](https://aur.archlinux.org/packages/qesteidutil/) from the [AUR](/index.php/AUR "AUR").

2\. Enable `pcscd.socket` [using systemd](/index.php/Systemd#Using_units "Systemd").

## Web authentication & digital signatures

[chrome-token-signing](https://aur.archlinux.org/packages/chrome-token-signing/) package contains [Native Messaging](https://developer.mozilla.org/en-US/Add-ons/WebExtensions/Native_messaging) host for Google Chrome/Chromium and Firefox and it is the modern way of doing authentication and digital signatures on the web.

For Google Chrome and Chromium you also will probably want to run [esteid-update-nssdb](https://github.com/open-eid/linux-installer/blob/master/esteid-update-nssdb) script that enables TLS client authentication in the browser.

If you still can't login from Firefox with your ID-card you should install [esteidfirefoxplugin](https://aur.archlinux.org/packages/esteidfirefoxplugin/).

## ID-card and Digidoc utilities

The ID-card utility packages are [qesteidutil](https://aur.archlinux.org/packages/qesteidutil/) and [qdigidoc](https://aur.archlinux.org/packages/qdigidoc/), with dependencies [libdigidoc](https://aur.archlinux.org/packages/libdigidoc/) and [libdigidocpp](https://aur.archlinux.org/packages/libdigidocpp/).

These applications will automatically appear in your application menus. You can also start from command line with <tt>qdigidocclient</tt> and <tt>qesteidutil</tt>.