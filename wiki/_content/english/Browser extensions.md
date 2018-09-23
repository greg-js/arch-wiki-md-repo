Related articles

*   [Browser plugins](/index.php/Browser_plugins "Browser plugins")

This articles lists [browser extensions](https://browserext.github.io/) available for both [Firefox](/index.php/Firefox "Firefox") and [Chromium](/index.php/Chromium "Chromium").

## Contents

*   [1 Privacy](#Privacy)
    *   [1.1 Content blockers](#Content_blockers)
        *   [1.1.1 uBlock Origin](#uBlock_Origin)
        *   [1.1.2 Adblock Plus](#Adblock_Plus)
    *   [1.2 Advanced control](#Advanced_control)
        *   [1.2.1 uMatrix](#uMatrix)
        *   [1.2.2 Cookie AutoDelete](#Cookie_AutoDelete)
        *   [1.2.3 ScriptSafe](#ScriptSafe)
    *   [1.3 Automatic tracker blockers](#Automatic_tracker_blockers)
        *   [1.3.1 Privacy Badger](#Privacy_Badger)
        *   [1.3.2 Disconnect](#Disconnect)
    *   [1.4 Noise generators](#Noise_generators)
        *   [1.4.1 AdNauseam](#AdNauseam)
        *   [1.4.2 TrackMeNot](#TrackMeNot)
    *   [1.5 Miscellaneous](#Miscellaneous)
        *   [1.5.1 HTTPS Everywhere](#HTTPS_Everywhere)
        *   [1.5.2 Decentraleyes](#Decentraleyes)
        *   [1.5.3 Privacy Settings](#Privacy_Settings)
*   [2 Website customization](#Website_customization)
*   [3 Keyboard shortcuts](#Keyboard_shortcuts)

## Privacy

This section lists cross-browser privacy extensions, browser-specific extensions are in [Firefox/Privacy#Extensions](/index.php/Firefox/Privacy#Extensions "Firefox/Privacy") and [Chromium/Tips and tricks#Privacy extensions](/index.php/Chromium/Tips_and_tricks#Privacy_extensions "Chromium/Tips and tricks").

**Tip:** It is not recommended to install all the privacy extensions. It can be counterproductive as they conflict with each other and does not increase security whatsoever.

### Content blockers

#### uBlock Origin

[uBlock Origin](https://github.com/gorhill/uBlock/) is a lightweight, efficient blocker which is easy on [memory and CPU](https://github.com/gorhill/uBlock#performance). It comes with several filter lists ready to use out-of-the-box (including EasyList, Peter Lowe's, several malware filter lists).

The lead developer of uBlock forked the project and created uBlock Origin. As of July 2015, most of the development is being done on uBlock Origin and the codebases are deviating substantially.

#### Adblock Plus

[Adblock Plus](https://adblockplus.org/en/) was a popular extension to block ads. Now that it is not blocking some ads on purpose [[1]](https://adblockplus.org/acceptable-ads), it may be a better idea to use a different blocker like [#uBlock Origin](#uBlock_Origin).

### Advanced control

#### uMatrix

[uMatrix](https://github.com/gorhill/uMatrix) is forked and refactored from HTTP Switchboard. It allows you to selectively block Javascript, plugins or other resources and control third-party resources. It also features extensive privacy features like user-agent masquerading, referering blocking and so on. It effectively replaces NoScript and RequestPolicy. See the [old HTTP Switchboard wiki](https://github.com/gorhill/httpswitchboard/wiki/How-to-use-HTTP-Switchboard:-Two-opposing-views) for different ways how to use it.

#### Cookie AutoDelete

[Cookie AutoDelete](https://github.com/Cookie-AutoDelete/Cookie-AutoDelete) is an extension that deletes cookies as soon as the tab closes. Supports automatic and manual cookie cleaning modes. (Support for clearing LocalStorage was added in version 2.1, but only for Firefox versions 58+. The same release added support for first party isolation, but only for Firefox versions 59+).

#### ScriptSafe

[ScriptSafe](https://github.com/andryou/scriptsafe) is a browser extension that gives users control of the web and more secure browsing while emphasizing simplicity and intuitiveness.

**Note:** Due to the nature of this extension, this will break most sites! It is designed to learn over time with sites that you allow.

### Automatic tracker blockers

#### Privacy Badger

[Privacy Badger](https://www.eff.org/privacybadger) is an extension by the EFF that monitors third-party trackers loaded with web content. It blocks trackers once they appear on different sites. It does not block advertisements in the first place, but since a lot of ads are served based on tracking information these are blocked as well. For more information on the mechanism, see its [FAQ](https://www.eff.org/privacybadger#faq-How-is-Privacy-Badger-different-to-Disconnect,-Adblock-Plus,-Ghostery,-and-other-blocking-extensions?).

#### Disconnect

[Disconnect](https://disconnect.me/) is a open source project aimed at stopping 2,000 third-party sites from tracking a user. It encrypts data sent to popular sites and claims to loads web pages 27 percent faster. Disconnect shows its users, in real time, how many tracking attempts from Google, Twitter, Facebook, and more are stopped. It categorizes tracking attempts into advertising, analytical, social, and content, which makes it easy to monitor how one is being tracked.

Disconnect can also stop side-jacking, which utilizes stolen cookies to steal personal data. It is easy to use and well supported.

**Note:** Firefox gained a feature based on the Disconnect list. See [Firefox/Privacy#Tracking protection](/index.php/Firefox/Privacy#Tracking_protection "Firefox/Privacy").

### Noise generators

#### AdNauseam

[AdNauseam](https://adnauseam.io/) is a lightweight browser extension that blends software tool and artware intervention to fight back against tracking by advertising networks. AdNauseam works like an ad-blocker (it is built atop uBlock-Origin) to silently simulate clicks on each blocked ad, confusing trackers as to one's real interests [[2]](https://github.com/dhowe/AdNauseam/).

#### TrackMeNot

[TrackMeNot](https://cs.nyu.edu/trackmenot/) periodically issues randomized search-queries to popular search engines and helps you hide your real ones in a cloud of 'ghost' queries.

### Miscellaneous

#### HTTPS Everywhere

[HTTPS Everywhere](https://www.eff.org/https-everywhere) is an extension which encrypts your communication with a website. It forces a connection over HTTPS instead of HTTP wherever possible.

HTTPS Everywhere will be automatically configured and enabled upon restarting Firefox. For information on how to set up your own rules for different websites please visit [the official website](https://www.eff.org/https-everywhere/rulesets).

**Note:** HTTPS Everywhere does not magically enable HTTPS for every site on the internet. The site needs to support HTTPS and HTTPS Everywhere should have a ruleset configured for that site.

#### Decentraleyes

[Decentraleyes](https://decentraleyes.org/) protects you against tracking through "free", centralized, content delivery. It prevents a lot of requests from reaching networks like Google Hosted Libraries, and serves local files to keep sites from breaking. Complements regular content blockers.

#### Privacy Settings

[Privacy Settings](https://add0n.com/privacy-settings.html) provides a toolbar panel for easily altering the browser's built-in privacy settings.

## Website customization

Websites can be augmented using user style sheets and JavaScript [userscripts](https://en.wikipedia.org/wiki/userscript "wikipedia:userscript").

*   [Stylus](https://add0n.com/stylus.html) – user style sheets manager, fork of defunct [Stylish](https://en.wikipedia.org/wiki/Stylish "wikipedia:Stylish")
*   [Violentmonkey](https://violentmonkey.github.io/) – open source userscript manager
*   [Tampermonkey](https://tampermonkey.net/) – proprietary userscript manager

## Keyboard shortcuts

There are various extensions providing [vi](/index.php/Vi "Vi")-style keyboard shortcuts.

*   [Vimium](https://github.com/philc/vimium) – allows mouse-less browsing, has an experimental Firefox version
*   [Saka Key](https://key.saka.io/) – allows mouse-less browsing, focused on accessibility
*   [wasavi](https://github.com/akahuku/wasavi) – can transform textareas into Vi editors