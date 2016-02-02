# KeePass

KeePass is an offline encrypted password database format. It is an alternative to popular online password managers and is supported on all major distributions and other OS platforms.

Currently, there are two variants of the database formats: _KeePass 1.x (Classic)_ and _KeePass 2.x_

## Contents

*   [1 Installation](#Installation)
*   [2 Integration](#Integration)
    *   [2.1 Plugin Installation](#Plugin_Installation)
    *   [2.2 Firefox](#Firefox)
    *   [2.3 Chrome/Chromium](#Chrome.2FChromium)
*   [3 See Also](#See_Also)

## Installation

There are two major implementations of KeePass, both of which are included in official repositories:

*   **[KeePass](https://en.wikipedia.org/wiki/KeePass "wikipedia:KeePass")** — An easy-to-use password manager for Windows, Linux, Mac OS X and mobile devices. It also has optional autotype and clipboard support respectively when `xdotool` and `xsel` are installed. Supports importing from [many formats](http://keepass.info/help/base/importexport.html).

	[http://keepass.info](http://keepass.info) || [keepass](https://www.archlinux.org/packages/?name=keepass)

*   **[KeePassX](https://en.wikipedia.org/wiki/KeePassX "wikipedia:KeePassX")** — KeePassX is a cross platform port of the Windows application _Keepass Password Safe (v1.x)_. KeePassX only supports the KeePass 2.x (.kdbx) password database format in the 2.0 branch. However, you can create an export in KeePass 1.x database format (.kdb) from KeePass 2.x, which can be imported to KeePassX. One may also import PwManager databases and KWallet XML databases. While KeepassX does not support plugins on its master branch, the KeepassX-HTTP branch supports KeepassHTTP protocol. Thus, it allows integration through browser addons such as ChromeIPass and PassIFox.

	[http://www.keepassx.org/](http://www.keepassx.org/) || [keepassx](https://www.archlinux.org/packages/?name=keepassx) [keepassx2](https://www.archlinux.org/packages/?name=keepassx2) [keepassx-http](https://aur.archlinux.org/packages/keepassx-http/)

Other lesser known implementations are found in the AUR:

*   **keepassc** — A curses-based password manager compatible to KeePass v.1.x and KeePassX. It also uses `xsel` for clipboard functions.

	[https://raymontag.github.com/keepassc](https://raymontag.github.com/keepassc) || [keepassc](https://aur.archlinux.org/packages/keepassc/)

*   **kpcli** — A command line browser of KeePassX database files `*.kdb`.

	[http://sourceforge.net/projects/kpcli/](http://sourceforge.net/projects/kpcli/) || [kpcli](https://aur.archlinux.org/packages/kpcli/)

*   **keeweb** — A desktop webapp compatible to KeePass 2.x.

	[https://github.com/antelle/keeweb](https://github.com/antelle/keeweb) || [keeweb-desktop](https://aur.archlinux.org/packages/keeweb-desktop/)

## Integration

Many [plugins and extensions](http://keepass.info/plugins.html) are available for integrating KeePass to other software.

### Plugin Installation

KeePass is by default, installed at `/usr/share/keepass/`. Copy `plugin.plgx` to a plugins sub-directory under the KeePass installation directory as demonstrated below:

```
# mkdir /usr/share/keepass/plugins
# cp plugin.plgx /usr/share/keepass/plugins

```

### Firefox

*   [KeeFox](http://keefox.org/) ([RPC plugin](https://aur.archlinux.org/packages/keepass-plugin-rpc/))

Firefox extension that links the browser to existing or new KeePass database. KeeFox needs to be setup before it is fully functional.

*   [PassIFox](https://addons.mozilla.org/en-US/firefox/addon/passifox/) ([KeepassHTTP plugin](https://github.com/pfn/keepasshttp/))

Extension allowing Firefox to form-fill passwords stored in KeePass.

### Chrome/Chromium

*   [ChromeIPass](https://chrome.google.com/webstore/detail/chromeipass/ompiailgknfdndiefoaoiligalphfdae) ([KeepassHTTP plugin](https://github.com/pfn/keepasshttp/))

Extension allowing Google Chrome and Chromium to form-fill passwords stored in KeePass.

## See Also

*   [Pass](/index.php/Pass "Pass")

Retrieved from "[https://wiki.archlinux.org/index.php?title=KeePass&oldid=417241](https://wiki.archlinux.org/index.php?title=KeePass&oldid=417241)"