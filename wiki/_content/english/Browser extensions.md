Related articles

*   [Browser plugins](/index.php/Browser_plugins "Browser plugins")

This articles lists [browser extensions](https://browserext.github.io/) available for both [Firefox](/index.php/Firefox "Firefox") and [Chromium](/index.php/Chromium "Chromium").

## Contents

*   [1 Privacy](#Privacy)
    *   [1.1 HTTPS Everywhere](#HTTPS_Everywhere)
    *   [1.2 uBlock Origin](#uBlock_Origin)
    *   [1.3 AdNauseam](#AdNauseam)
    *   [1.4 Adblock Plus](#Adblock_Plus)
    *   [1.5 Privacy Badger](#Privacy_Badger)
    *   [1.6 Disconnect](#Disconnect)
    *   [1.7 uMatrix](#uMatrix)
    *   [1.8 Cookie AutoDelete](#Cookie_AutoDelete)
    *   [1.9 Privacy Settings](#Privacy_Settings)

## Privacy

See also [Firefox/Privacy#Extensions](/index.php/Firefox/Privacy#Extensions "Firefox/Privacy") and [Chromium/Tips and tricks#Privacy extensions](/index.php/Chromium/Tips_and_tricks#Privacy_extensions "Chromium/Tips and tricks").

### HTTPS Everywhere

[HTTPS Everywhere](https://www.eff.org/https-everywhere) is an extension which encrypts your communication with a website. It forces a connection over HTTPS instead of HTTP wherever possible.

HTTPS Everywhere will be automatically configured and enabled upon restarting Firefox. For information on how to set up your own rules for different websites please visit [the official website](https://www.eff.org/https-everywhere/rulesets).

**Note:** HTTPS Everywhere does not magically enable HTTPS for every site on the internet. The site needs to support HTTPS and HTTPS Everywhere should have a ruleset configured for that site.

### uBlock Origin

uBlock Origin is a lightweight, efficient blocker which is easy on [memory and CPU](https://github.com/gorhill/uBlock#performance). It comes with several filter lists ready to use out-of-the-box (including EasyList, Peter Lowe's, several malware filter lists).

The lead developer of uBlock forked the project and created uBlock Origin. As of July 2015, most of the development is being done on uBlock Origin and the codebases are deviating substantially.

uBlock Origin: [Github](https://github.com/gorhill/uBlock); [Firefox Add-ons](https://addons.mozilla.org/firefox/addon/ublock-origin/).

### AdNauseam

[AdNauseam](https://adnauseam.io/) is a lightweight browser extension that blends software tool and artware intervention to fight back against tracking by advertising networks. AdNauseam works like an ad-blocker (it is built atop uBlock-Origin) to silently simulate clicks on each blocked ad, confusing trackers as to one's real interests [[1]](https://github.com/dhowe/AdNauseam/).

### Adblock Plus

[Adblock Plus](https://adblockplus.org/en/) was a popular extension to block ads. Now that it is not blocking some ads on purpose [[2]](https://adblockplus.org/acceptable-ads), it may be a better idea to use a different blocker like [#uBlock Origin](#uBlock_Origin).

### Privacy Badger

[Privacy Badger](https://www.eff.org/privacybadger) is an extension by the EFF that monitors third-party trackers loaded with web content. It blocks trackers once they appear on different sites. It does not block advertisements in the first place, but since a lot of ads are served based on tracking information these are blocked as well. For more information on the mechanism, see its [FAQ](https://www.eff.org/privacybadger#faq-How-is-Privacy-Badger-different-to-Disconnect,-Adblock-Plus,-Ghostery,-and-other-blocking-extensions?).

### Disconnect

[Disconnect](https://disconnect.me/) is a open source project aimed at stopping 2,000 third-party sites from tracking a user. It encrypts data sent to popular sites and claims to loads web pages 27 percent faster. Disconnect shows its users, in real time, how many tracking attempts from Google, Twitter, Facebook, and more are stopped. It categorizes tracking attempts into advertising, analytical, social, and content, which makes it easy to monitor how one is being tracked.

Disconnect can also stop side-jacking, which utilizes stolen cookies to steal personal data. It is easy to use and well supported.

**Note:** Firefox gained a feature based on the Disconnect list. See [Firefox#Enable tracking protection](/index.php/Firefox#Enable_tracking_protection "Firefox").

### uMatrix

[uMatrix](https://addons.mozilla.org/firefox/addon/umatrix/) is forked and refactored from HTTP Switchboard. It allows you to selectively block Javascript, plugins or other resources and control third-party resources. It also features extensive privacy features like user-agent masquerading, referering blocking and so on. It effectively replaces NoScript and RequestPolicy. See the [old HTTP Switchboard wiki](https://github.com/gorhill/httpswitchboard/wiki/How-to-use-HTTP-Switchboard:-Two-opposing-views) for different ways how to use it.

For more Information visit the [project site](https://github.com/gorhill/uMatrix).

### Cookie AutoDelete

[Cookie AutoDelete](https://addons.mozilla.org/firefox/addon/cookie-autodelete/) is an extension that deletes cookies as soon as the tab closes. Supports automatic and manual cookie cleaning modes. (Support for clearing LocalStorage was added in version 2.1, but only for Firefox versions 58+. The same release added support for first party isolation, but only for Firefox versions 59+).

### Privacy Settings

[Privacy Settings](https://addons.mozilla.org/firefox/addon/privacy-settings/) provides a toolbar panel for easily altering Firefox's built-in privacy settings.