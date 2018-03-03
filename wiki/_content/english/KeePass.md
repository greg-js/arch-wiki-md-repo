KeePass is an encrypted password database format. It is an alternative to online password managers and is supported on all major platforms.

There are two versions of the format: *KeePass 1.x (Classic)* and *KeePass 2.x*

## Contents

*   [1 Installation](#Installation)
*   [2 Integration](#Integration)
    *   [2.1 Plugin Installation](#Plugin_Installation)
    *   [2.2 Firefox](#Firefox)
    *   [2.3 Chrome/Chromium](#Chrome.2FChromium)
    *   [2.4 Nextcloud](#Nextcloud)
    *   [2.5 Yubikey](#Yubikey)
*   [3 Tips and tricks](#Tips_and_tricks)
    *   [3.1 Disable your clipboard manager](#Disable_your_clipboard_manager)
*   [4 See Also](#See_Also)

## Installation

There are three major implementations of KeePass, which are all available in the official repositories:

*   **[KeePass](https://en.wikipedia.org/wiki/KeePass "wikipedia:KeePass")** — A cross-platform password manager that has autotype and clipboard support when respectively `xdotool` and `xsel` are installed. It lets you import [many formats](http://keepass.info/help/base/importexport.html) and has [many plugins](http://keepass.info/plugins.html).

	[http://keepass.info](http://keepass.info) || [keepass](https://www.archlinux.org/packages/?name=keepass)

*   **[KeePassX](https://en.wikipedia.org/wiki/KeePassX "wikipedia:KeePassX")** — Started as a Linux port of KeePass. [keepassx2](https://www.archlinux.org/packages/?name=keepassx2) uses the KeePass 2.x format, but can import 1.x databases. It also lets you import PwManager and KWallet XML databases. It does not support plugins. [[1]](https://www.keepassx.org/faq).

	[https://www.keepassx.org/](https://www.keepassx.org/) || [keepassx](https://www.archlinux.org/packages/?name=keepassx) [keepassx2](https://www.archlinux.org/packages/?name=keepassx2)

*   **[KeePassXC](https://en.wikipedia.org/wiki/KeePassXC "wikipedia:KeePassXC")** — Fork of KeePassX that aims to incorporate stalled pull requests, that are not being incorporated into KeePassX.

	[https://keepassxc.org](https://keepassxc.org) || [keepassxc](https://www.archlinux.org/packages/?name=keepassxc)

Other lesser-known alternatives can be found in the AUR:

*   **keepassc** — A curses-based password manager compatible to KeePass v.1.x and KeePassX. It uses `xsel` for clipboard functions.

	[https://raymontag.github.io/keepassc/](https://raymontag.github.io/keepassc/) || [keepassc](https://aur.archlinux.org/packages/keepassc/)

*   **kpcli** — A command line interface for KeePassX database files `*.kdb`.

	[https://sourceforge.net/projects/kpcli/](https://sourceforge.net/projects/kpcli/) || [kpcli](https://aur.archlinux.org/packages/kpcli/)

*   **keeweb** — A web app (online / Electron) compatible with KeePass 2.x.

	[https://keeweb.info](https://keeweb.info) || [keeweb-desktop](https://aur.archlinux.org/packages/keeweb-desktop/) [nextcloud-app-keeweb](https://aur.archlinux.org/packages/nextcloud-app-keeweb/)

## Integration

Many [plugins and extensions](http://keepass.info/plugins.html) are available for integrating KeePass to other software.

### Plugin Installation

**Tip:** Starting from KeePassXC version 2.3, an [official plugin is available](https://keepassxc.org/docs/keepassxc-browser-migration/) that supports [Chrome](/index.php/Chrome "Chrome"), [Chromium](/index.php/Chromium "Chromium"), [Firefox](/index.php/Firefox "Firefox") and [Vivaldi](/index.php/Vivaldi "Vivaldi") - which replaces KeePassHTTP.

**Note:** KeePassX does not support plugins on its master branch. An alternative is to use global autotype feature.

KeePass is by default, installed at `/usr/share/keepass/`. Copy `plugin.plgx` to a plugins sub-directory under the KeePass installation directory as demonstrated below:

```
# mkdir /usr/share/keepass/plugins
# cp plugin.plgx /usr/share/keepass/plugins

```

**Warning:** Upstream strongly advises to disable KeePassHTTP because of security issues. For more information see, [pfn/keepasshttp/issues](https://github.com/pfn/keepasshttp/issues/258) and [keepassxreboot/keepassxc/issues](https://github.com/keepassxreboot/keepassxc/issues/147). To [mitigate the impact](https://github.com/keepassxreboot/keepassxc/issues/147#issuecomment-274669750) of the KeePassHTTP flaw, KeePassXC has [issued a hotfix](https://github.com/keepassxreboot/keepassxc/pull/196) as of version 2.1.1\. Some users consider the improvement good enough ([1](https://github.com/keepassxreboot/keepassxc/issues/147#issuecomment-274682664), [2](https://github.com/keepassxreboot/keepassxc/issues/147#issuecomment-274669042)) for practical purposes, as long as the system is not compromised. However, as there is still [some risk](https://github.com/keepassxreboot/keepassxc/issues/147#issuecomment-274671861) involved, KeePassHTTP support is [no longer enabled by default](https://github.com/keepassxreboot/keepassxc/blob/2.1.1/README.md#note-about-keepasshttp) in KeePassXC.

### Firefox

*   [KeeFox](http://keefox.org/) ([keepass-plugin-rpc](https://aur.archlinux.org/packages/keepass-plugin-rpc/))

	Firefox extension that links the browser to existing or new KeePass database. KeeFox needs to be setup before it is fully functional.

*   [PassIFox](https://addons.mozilla.org/en-US/firefox/addon/passifox/) ([KeepassHTTP plugin](https://github.com/pfn/keepasshttp/))

	Extension allowing Firefox to form-fill passwords stored in KeePass.

*   [KeePass Helper (legacy addon)](https://addons.mozilla.org/en-us/firefox/addon/keepass-helper/), [TitleURL](https://addons.mozilla.org/en-US/firefox/addon/url-in-title/)

	Modifies window title to assist autotype feature.

*   [KeePassXC-Browser](https://addons.mozilla.org/en-US/firefox/addon/keepassxc-browser/)

	Official browser plugin for the KeePassXC password manager (Firefox version).

### Chrome/Chromium

*   [ChromeIPass](https://chrome.google.com/webstore/detail/chromeipass/ompiailgknfdndiefoaoiligalphfdae) ([KeepassHTTP plugin](https://github.com/pfn/keepasshttp/))

	Extension allowing Google Chrome and Chromium to form-fill passwords stored in KeePass.

*   [Url in title](https://chrome.google.com/webstore/detail/url-in-title/ignpacbgnbnkaiooknalneoeladjnfgb)

	Modifies window title to assist autotype feature. Similar to KeePass Helper for Firefox in function.

*   [KeePassXC-Browser](https://chrome.google.com/webstore/detail/url-in-title/oboonakemofpalcgghocfoadofidjkkk)

	Official browser plugin for the KeePassXC password manager (Chrome/Chromium version).

### Nextcloud

*   [Keeweb for Nextcloud](https://github.com/jhass/nextcloud-keeweb) ([nextcloud-app-keeweb](https://aur.archlinux.org/packages/nextcloud-app-keeweb/))

	Open Keepass stores inside Nextcloud

### Yubikey

[Yubikey](/index.php/Yubikey "Yubikey") can be integrated with KeePass thanks to contributors of KeePass plugins.

1.  StaticPassword

    	Configure one of Yubikey slots to store static password. You can make the password as strong as 65 characters (64 characters with leading `!`). This password can then be used as master password for your KeePass database.

2.  one-time passwords (OATH-HOTP)

    1.  Download plugin from KeePass website: [http://keepass.info/plugins.html#otpkeyprov](http://keepass.info/plugins.html#otpkeyprov)
    2.  Use [yubikey-personalization-gui-git](https://aur.archlinux.org/packages/yubikey-personalization-gui-git/) to setup OATH-HOTP
    3.  In advanced mode untick `OATH Token Identifier`
    4.  In KeePass additional option will show up under `Key file / provider` called `One-Time Passwords (OATH HOTP)
    5.  Copy secret, key length (6 or 8), and counter (in Yubikey personalization GUI this parameter is called `Moving Factor Seed`)
    6.  You may need to setup `Look-ahead count` option to something greater than 0, please see [thread](https://forum.yubico.com/viewtopic.php?f=16&t=1120%7Cthis) for more information
    7.  See [video](https://www.yubico.com/products/services-software/personalization-tools/oath/%7Cthis) for more help

3.  Challenge-Response (HMAC-SHA1)

    1.  Get the plugin from AUR: [keepass-plugin-keechallenge](https://aur.archlinux.org/packages/keepass-plugin-keechallenge/)
    2.  In KeePass additional option will show up under `Key file / provider` called `Yubikey challenge-response`
    3.  Plugin assumes slot 2 is used

## Tips and tricks

### Disable your clipboard manager

If you are an avid user of clipboard managers, you can may need to disable your clipboard manager before you launch keepass and then re-start your clipboard manager afterward.

## See Also

*   [List of applications/Security#Password_managers](/index.php/List_of_applications/Security#Password_managers "List of applications/Security")