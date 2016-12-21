KeePass is an offline encrypted password database format. It is an alternative to popular online password managers and is supported on all major distributions and other OS platforms.

Currently, there are two variants of the database formats: *KeePass 1.x (Classic)* and *KeePass 2.x*

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

*   **[KeePassX](https://en.wikipedia.org/wiki/KeePassX "wikipedia:KeePassX")** — KeePassX is a cross platform port of the Windows application *Keepass Password Safe*. The new version [keepassx2](https://www.archlinux.org/packages/?name=keepassx2) is compatible with 2.x database formats, but can import 1.x databases. One may also import PwManager databases and KWallet XML databases.

	[http://www.keepassx.org/](http://www.keepassx.org/) || [keepassx](https://www.archlinux.org/packages/?name=keepassx) [keepassx2](https://www.archlinux.org/packages/?name=keepassx2) [keepassxc](https://aur.archlinux.org/packages/keepassxc/) [keepassxc-git](https://aur.archlinux.org/packages/keepassxc-git/)

Other lesser known implementations are found in the AUR:

*   **keepassc** — A curses-based password manager compatible to KeePass v.1.x and KeePassX. It also uses `xsel` for clipboard functions.

	[https://raymontag.github.com/keepassc](https://raymontag.github.com/keepassc) || [keepassc](https://aur.archlinux.org/packages/keepassc/)

*   **kpcli** — A command line browser of KeePassX database files `*.kdb`.

	[http://sourceforge.net/projects/kpcli/](http://sourceforge.net/projects/kpcli/) || [kpcli](https://aur.archlinux.org/packages/kpcli/)

*   **keeweb** — A desktop webapp compatible to KeePass 2.x.

	[https://github.com/keeweb/keeweb](https://github.com/keeweb/keeweb) || [keeweb-desktop](https://aur.archlinux.org/packages/keeweb-desktop/) [nextcloud-app-keeweb](https://aur.archlinux.org/packages/nextcloud-app-keeweb/)

## Integration

Many [plugins and extensions](http://keepass.info/plugins.html) are available for integrating KeePass to other software.

### Plugin Installation

KeePass is by default, installed at `/usr/share/keepass/`. Copy `plugin.plgx` to a plugins sub-directory under the KeePass installation directory as demonstrated below:

```
# mkdir /usr/share/keepass/plugins
# cp plugin.plgx /usr/share/keepass/plugins

```

**Note:** KeePassX does not support plugins on its master branch (at the moment of writing KeePassX version is 0.4.4 and KeePassX2 version is 2.0.2). An alternative is to use global autotype feature. If plugins are absolutely necessary, [keepassxc](https://aur.archlinux.org/packages/keepassxc/) supports KeepassHTTP protocol. Thus, it allows integration through browser addons such as [ChromeIPass](https://chrome.google.com/webstore/detail/chromeipass/ompiailgknfdndiefoaoiligalphfdae) and [PassIFox](https://addons.mozilla.org/en-US/firefox/addon/passifox/).

### Firefox

*   [KeeFox](http://keefox.org/) ([RPC plugin](https://aur.archlinux.org/packages/keepass-plugin-rpc/))

Firefox extension that links the browser to existing or new KeePass database. KeeFox needs to be setup before it is fully functional.

*   [PassIFox](https://addons.mozilla.org/en-US/firefox/addon/passifox/) ([KeepassHTTP plugin](https://github.com/pfn/keepasshttp/))

Extension allowing Firefox to form-fill passwords stored in KeePass.

*   [KeePass Helper](https://addons.mozilla.org/en-us/firefox/addon/keepass-helper/)

Modifies window title to assist autotype feature.

### Chrome/Chromium

*   [ChromeIPass](https://chrome.google.com/webstore/detail/chromeipass/ompiailgknfdndiefoaoiligalphfdae) ([KeepassHTTP plugin](https://github.com/pfn/keepasshttp/))

Extension allowing Google Chrome and Chromium to form-fill passwords stored in KeePass.

*   [Url in title](https://chrome.google.com/webstore/detail/url-in-title/ignpacbgnbnkaiooknalneoeladjnfgb)

Modifies window title to assist autotype feature. Similar to KeePass Helper for Firefox in function.

## See Also

*   [Pass](/index.php/Pass "Pass")