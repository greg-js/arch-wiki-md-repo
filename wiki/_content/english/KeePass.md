KeePass is an encrypted password database format. It is an alternative to online password managers and is supported on all major platforms.

There are two versions of the format: *KeePass 1.x (Classic)* and *KeePass 2.x*

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Integration](#Integration)
    *   [2.1 Plugin Installation in KeePass](#Plugin_Installation_in_KeePass)
    *   [2.2 Browser Integration](#Browser_Integration)
        *   [2.2.1 keepassxc-browser for KeepassXC](#keepassxc-browser_for_KeepassXC)
        *   [2.2.2 KeePassRPC / Kee](#KeePassRPC_/_Kee)
        *   [2.2.3 KeePassHTTP for Keepass](#KeePassHTTP_for_Keepass)
        *   [2.2.4 via autotype feature](#via_autotype_feature)
    *   [2.3 Nextcloud](#Nextcloud)
    *   [2.4 Yubikey](#Yubikey)
        *   [2.4.1 Configuration with KeePass](#Configuration_with_KeePass)
    *   [2.5 SSH Agent](#SSH_Agent)
*   [3 Tips and tricks](#Tips_and_tricks)
    *   [3.1 Disable your clipboard manager](#Disable_your_clipboard_manager)
*   [4 See Also](#See_Also)

## Installation

There are three major implementations of KeePass, two are available in the official repositories:

*   **[KeePass](https://en.wikipedia.org/wiki/KeePass "wikipedia:KeePass")** — A cross-platform password manager that has autotype and clipboard support when respectively `xdotool` and `xsel` are installed. It lets you import [many formats](https://keepass.info/help/base/importexport.html) and has [many plugins](https://keepass.info/plugins.html).

	[http://keepass.info](http://keepass.info) || [keepass](https://www.archlinux.org/packages/?name=keepass)

*   **[KeePassXC](https://en.wikipedia.org/wiki/KeePassXC "wikipedia:KeePassXC")** — Fork of KeePassX that is actively maintained and has additional features like browser integration, ssh agent support, yubikey support, a TOTP generator and KeeShare included. Also provides a CLI.

	[https://keepassxc.org](https://keepassxc.org) || [keepassxc](https://www.archlinux.org/packages/?name=keepassxc)

*   **[KeePassX](https://en.wikipedia.org/wiki/KeePassX "wikipedia:KeePassX")** — Started as a Linux port of KeePass. [keepassx2](https://aur.archlinux.org/packages/keepassx2/) uses the KeePass 2.x format, but can import 1.x databases. It also lets you import PwManager and KWallet XML databases. It does not support plugins. [[1]](https://www.keepassx.org/faq) No active development since 2016\. [[2]](https://dev.keepassx.org/projects/keepassx/repository/revisions)

	[https://www.keepassx.org/](https://www.keepassx.org/) || [keepassx](https://aur.archlinux.org/packages/keepassx/) [keepassx2](https://aur.archlinux.org/packages/keepassx2/)

Other lesser-known alternatives can be found in the AUR:

*   **keepassc** — A curses-based password manager compatible to KeePass v.1.x and KeePassX. It uses `xsel` for clipboard functions.

	[https://raymontag.github.io/keepassc/](https://raymontag.github.io/keepassc/) || [keepassc](https://aur.archlinux.org/packages/keepassc/)

*   **kpcli** — A command line interface for KeePass database files `*.kdb` or `*.kdbx`.

	[https://sourceforge.net/projects/kpcli/](https://sourceforge.net/projects/kpcli/) || [kpcli](https://aur.archlinux.org/packages/kpcli/)

*   **keepmenu** — Dmenu/Rofi frontend for Keepass database files.

	[https://github.com/firecat53/keepmenu](https://github.com/firecat53/keepmenu) || [python-keepmenu-git](https://aur.archlinux.org/packages/python-keepmenu-git/)

*   **keeweb** — A web app (online / Electron) compatible with KeePass 2.x. KeeWeb is the only version with default Sync support for major cloud services, Gdrive, Onedrive, Dropbox etc...

	[https://keeweb.info](https://keeweb.info) || [keeweb-desktop](https://aur.archlinux.org/packages/keeweb-desktop/) [nextcloud-app-keeweb](https://aur.archlinux.org/packages/nextcloud-app-keeweb/)

## Integration

Many [plugins and extensions](http://keepass.info/plugins.html) are available for integrating KeePass to other software. KeePassX and KeePassXC do not have a plugin interface, but KeePassXC has various integrations built-in.

### Plugin Installation in KeePass

**Note:** KeePassX and KeePassXC do not support plugins. KeepassXC has some integrations built-in.

KeePass is by default installed at `/usr/share/keepass/`. Copy `plugin.plgx` to a plugins sub-directory under the KeePass installation directory as demonstrated below:

```
# mkdir /usr/share/keepass/plugins
# cp plugin.plgx /usr/share/keepass/plugins

```

### Browser Integration

#### keepassxc-browser for KeepassXC

[keepassxc-browser](https://github.com/keepassxreboot/keepassxc-browser) is the browser extension of KeePassXC’s built-in browser integration using native-messaging and transport encryption using libsodium. It was developed to replace KeePassHTTP, as KeePassHTTP’s protocol has fundamental security problems.

The developers provide the browser extension on

*   [Firefox Add-ons](https://addons.mozilla.org/en-US/firefox/addon/keepassxc-browser/) (for [Firefox](/index.php/Firefox "Firefox") and [Tor Browser](/index.php/Tor_Browser "Tor Browser")) and
*   in the [chrome web store](https://chrome.google.com/webstore/detail/keepassxc-browser/oboonakemofpalcgghocfoadofidjkkk) (for [Chromium](/index.php/Chromium "Chromium"), [Google Chrome](/index.php/Google_Chrome "Google Chrome"), [Vivaldi](/index.php/Vivaldi "Vivaldi") and [Brave](/index.php/List_of_applications/Internet#Privacy-focused_chromium_spin-offs "List of applications/Internet"))

The [source code and an explanation how it works](https://github.com/keepassxreboot/keepassxc-browser) can be found on GitHub, the KeePassXC developers provide a [configuration guide](https://keepassxc.org/docs/keepassxc-browser-migration/) on their website.

#### KeePassRPC / Kee

[Kee](https://www.kee.pm/) ([GitHub repo](https://github.com/kee-org/browser-addon)) is a browser extension for [Firefox](/index.php/Firefox "Firefox") and [Chromium](/index.php/Chromium "Chromium") which integrates KeePass through [KeePassRPC](https://github.com/kee-org/keepassrpc), a KeePass plugin from the same developers.

The KeePass plugin is available from [GitHub](https://github.com/kee-org/keepassrpc/releases) or from the AUR ([keepass-plugin-rpc](https://aur.archlinux.org/packages/keepass-plugin-rpc/)).

The browser extension can be found on [GitHub](https://github.com/kee-org/browser-addon/releases), [Firefox Add-ons](https://addons.mozilla.org/en/firefox/addon/keefox/) and the [chrome web store](https://chrome.google.com/webstore/detail/kee-password-manager/mmhlniccooihdimnnjhamobppdhaolme).

#### KeePassHTTP for Keepass

**Tip:** Starting from KeePassXC version 2.3, an [official plugin is available](https://keepassxc.org/docs/keepassxc-browser-migration/) which replaces KeePassHTTP.

**Warning:** **It is strongly advised to not use KeePassHTTP and to disable the extension because of security issues.**

The KeePassHTTP protocol uses a proprietary crypto protocol and is vulnerable to CBC padding oracle attacks. Also the key exchange is not encrypted and some implementations do not bind to localhost only. For more Information see [[3]](https://github.com/pfn/keepasshttp/issues/258), [[4]](https://github.com/keepassxreboot/keepassxc/issues/147).

Due to these problems, KeePassHTTP should **never** be used remotely.

KeePassHTTP is available as plugin for KeePass. KeePassHTTP is not supported anymore in KeePassXC since version 2.4.0, [keepassxc-browser](#keepassxc-browser_for_KeepassXC) is a secure replacement. KeePass users can use [KeePassRPC](#KeePassRPC_/_Kee) as more secure alternative.

The Plugin can be found on [GitHub](https://github.com/pfn/keepasshttp) and in the AUR ([keepass-plugin-http](https://aur.archlinux.org/packages/keepass-plugin-http/), [keepass-plugin-http-git](https://aur.archlinux.org/packages/keepass-plugin-http-git/)). The KeePassHTTP GitHub repository has not seen any commits since 2017, the security flaws are known since 2016.

The [browser extensions provided by the plugin developer](https://github.com/pfn/passifox/), PassIFox and ChromeIPass, are currently (May 2019) not available on the respective Add-On-Stores.

There are alternative extensions available, e.g. KeePassHttp-Connector [for Firefox](https://addons.mozilla.org/en/firefox/addon/keepasshttp-connector/) and [for Chromium/Chrome](https://chrome.google.com/webstore/detail/keepasshttp-connector/dafgdjggglmmknipkhngniifhplpcldb), but the [corresponding GitHub repository](https://github.com/smorks/keepasshttp-connector) is *archived* and marked *deprecated*.

#### via autotype feature

An alternative to having a direct channel between browser and KeePass(XC) is using the autotype feature. There are browser extensions which support this way by putting the page URL into the window name:

*   [KeePass Helper](https://addons.mozilla.org/en/firefox/addon/keepass-helper-url-in-title/) or [TitleURL](https://addons.mozilla.org/en/firefox/addon/url-in-title/) for [Firefox](/index.php/Firefox "Firefox")
*   [Url in title](https://chrome.google.com/webstore/detail/url-in-title/ignpacbgnbnkaiooknalneoeladjnfgb) for [Chromium](/index.php/Chromium "Chromium")

### Nextcloud

*   [Keeweb for Nextcloud](https://github.com/jhass/nextcloud-keeweb) ([nextcloud-app-keeweb](https://aur.archlinux.org/packages/nextcloud-app-keeweb/))

	Open Keepass stores inside Nextcloud

### Yubikey

[YubiKey](/index.php/YubiKey "YubiKey") can be integrated with KeePass thanks to contributors of KeePass plugins. KeepassXC provides built-in support for Yubikey Challenge-Response without plugins.

#### Configuration with KeePass

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

### SSH Agent

KeePassXC offers SSH Agent support, a similar feature is also available for KeePass using the [KeeAgent](https://lechnology.com/software/keeagent/) plugin.

The feature allows to store SSH keys in KeePass databases, KeePassXC/KeeAgent acts as OpenSSH Client and dynamically adds and removes the key to the Agent.

The feature in KeePassXC is documented in its [FAQ](https://keepassxc.org/docs/#faq-ssh-agent-how).

**Note:** The [SSH agent emulation of *gpg-agent*](/index.php/GnuPG#SSH_agent "GnuPG") does not support removing keys from the agent on demand using `ssh-add -d` or `ssh-add -D`, therefore KeePassXC/KeeAgent cannot remove them when locking the database. [[5]](https://github.com/keepassxreboot/keepassxc/issues/2029#issuecomment-395933402) [[6]](https://unix.stackexchange.com/questions/185393/gpg-agent-doesnt-remove-my-ssh-key-from-the-keyring)

## Tips and tricks

### Disable your clipboard manager

If you are an avid user of clipboard managers, you can may need to disable your clipboard manager before you launch keepass and then re-start your clipboard manager afterwards.

## See Also

*   [List of applications/Security#Password managers](/index.php/List_of_applications/Security#Password_managers "List of applications/Security")