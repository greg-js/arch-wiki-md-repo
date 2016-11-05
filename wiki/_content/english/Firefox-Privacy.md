This article overviews some useful extensions which enhance security and privacy while using the [Firefox](/index.php/Firefox "Firefox") web browser.

## Contents

*   [1 Extensions](#Extensions)
    *   [1.1 HTTPS Everywhere](#HTTPS_Everywhere)
    *   [1.2 uBlock Origin](#uBlock_Origin)
    *   [1.3 Adblock Plus](#Adblock_Plus)
    *   [1.4 Privacy Badger](#Privacy_Badger)
    *   [1.5 Disconnect](#Disconnect)
    *   [1.6 NoScript](#NoScript)
    *   [1.7 uMatrix](#uMatrix)
    *   [1.8 Cookie Monster](#Cookie_Monster)
    *   [1.9 Self-Destructing Cookies](#Self-Destructing_Cookies)
    *   [1.10 RefControl](#RefControl)
    *   [1.11 RequestPolicy](#RequestPolicy)
    *   [1.12 Decentraleyes](#Decentraleyes)
    *   [1.13 CanvasBlocker](#CanvasBlocker)
*   [2 Configuration tweaks](#Configuration_tweaks)
    *   [2.1 Enable tracking protection](#Enable_tracking_protection)
    *   [2.2 Change browser time zone](#Change_browser_time_zone)
    *   [2.3 Change user agent and platform](#Change_user_agent_and_platform)
    *   [2.4 Disable battery api](#Disable_battery_api)

## Extensions

### HTTPS Everywhere

[HTTPS Everywhere](https://www.eff.org/https-everywhere) is an extension which encrypts your communication with a website. It forces a connection over HTTPS instead of HTTP wherever possible.

HTTPS Everywhere will be automatically configured and enabled upon restarting Firefox. For information on how to set up your own rules for different websites please visit [the official website](https://www.eff.org/https-everywhere/rulesets).

**Note:** HTTPS Everywhere does not magically enable HTTPS for every site on the internet. The site needs to support HTTPS and HTTPS Everywhere should have a ruleset configured for that site.

### uBlock Origin

uBlock Origin is a lightweight, efficient blocker which is easy on [memory and CPU](https://github.com/gorhill/uBlock#performance). It comes with several filter lists ready to use out-of-the-box (including EasyList, Peter Lowe's, several malware filter lists).

The lead developer of uBlock forked the project and created uBlock Origin. As of July 2015, most of the development is being done on uBlock Origin and the codebases are deviating substantially.

uBlock Origin: [Github](https://github.com/gorhill/uBlock); [Firefox Add-ons](https://addons.mozilla.org/firefox/addon/ublock-origin/).

### Adblock Plus

[Adblock Plus](https://adblockplus.org/en/) was a popular exstension to block ads. Now that it is not blocking some ads on purpose [[1]](https://adblockplus.org/acceptable-ads), it may be a better idea to use a different blocker like uBlock Origin.

### Privacy Badger

[Privacy Badger](https://www.eff.org/privacybadger) is an extension that monitors third-party trackers loaded with web content. It blocks trackers once they appear on different sites. It does not block advertisements in the first place, but since a lot of ads are served based on tracking information these are blocked as well. For more information on the mechanism, see its [FAQ](https://www.eff.org/privacybadger#faq-How-is-Privacy-Badger-different-to-Disconnect,-Adblock-Plus,-Ghostery,-and-other-blocking-extensions?).

### Disconnect

Disconnect is a open source project aimed at stopping 2,000 third-party sites from tracking a user. It encrypts data sent to popular sites and claims to loads web pages 27 percent faster. Disconnect shows its users, in real time, how many tracking attempts from Google, Twitter, Facebook, and more are stopped. It categorizes tracking attempts into advertising, analytical, social, and content, which makes it easy to monitor how one is being tracked.

Disconnect can also stop side-jacking, which utilizes stolen cookies to steal personal data. It is easy to use and well supported. It can be added to Firefox at the [official website](https://disconnect.me/).

**Note:** Firefox gained a feature based on the Disconnect list. See [Firefox tweaks#Enable firefox optional tracking protection](/index.php/Firefox_tweaks#Enable_firefox_optional_tracking_protection "Firefox tweaks").

### NoScript

[NoScript](http://noscript.net/) is an extension which disables JavaScript, Java, Flash and other plugins on any website not specifically whitelisted by the user. This extension will protect you from exploitation of security vulnerabilities by not letting anything but trusted sites (e.g: your bank, webmail) serve you executable content.

Once installed you can configure settings for NoScript by either clicking its icon on the toolbar or right clicking a page and navigating to NoScript. You will then have the option to enable/disable scripts for the current page, as well as any third party scripts that the page is linking to. Alternatively you can choose to enable scripts temporarily for that session only.

Be aware a lot of modern websites use scripts for layout purposes, hence content may look different. For example, failed rendering due to missing fonts might occur on websites that load fonts at runtime via scripts, which were blocked by NoScript.

For more detailed configuration see the [NoScript FAQ](http://noscript.net/faq).

### uMatrix

[uMatrix](https://addons.mozilla.org/firefox/addon/umatrix/) is forked and refactored from HTTP Switchboard. It allows you to selectively block Javascript, plugins or other resources and control third-party resources. It also features extensive privacy features like user-agent masquerading, referering blocking and so on. It effectively replaces NoScript and RequestPolicy. See the [old HTTP Switchboard wiki](https://github.com/gorhill/httpswitchboard/wiki/How-to-use-HTTP-Switchboard:-Two-opposing-views) for different ways how to use it.

For more Information visit the [project site](https://github.com/gorhill/uMatrix).

### Cookie Monster

[Cookie Monster](https://addons.mozilla.org/firefox/addon/cookie-monster/) is a similar extension to NoScript but will the goal of managing cookies.

From the preferences for Cookie Monster select "Block All Cookies". Once this is done, just as with NoScript, you can enable the use of cookies for specific pages from either the Cookie Monster icon on the toolbar or by right clicking the page and navigating to Cookie Monster. You have the option to accept cookies from the website in question or alternatively to only temporarily allow cookies for the current session.

### Self-Destructing Cookies

[Self-Destructing Cookies](https://addons.mozilla.org/firefox/addon/self-destructing-cookies/) gets rid of a site's cookies and LocalStorage as soon as you close its tabs. Protects against trackers and zombie-cookies.

### RefControl

[RefControl](http://www.stardrifter.org/refcontrol/) is an extension to control what gets sent as the HTTP Referer. Once installed RefControl can be configured so that no referer gets sent when navigating to a new webpage. This prevents the server from knowing which website you originated from.

To do this open RefControl's preferences and change the setting for "Default for sites not listed:" to <Block>.

**Note:** Firefox has options to control emitted HTTP referers, possibly replacing plugins such as RefControl and Smart Referer. See [Firefox tweaks#Referer header control](/index.php/Firefox_tweaks#Referer_header_control "Firefox tweaks").

### RequestPolicy

[RequestPolicy](https://www.requestpolicy.com/) is an extension for Mozilla browsers which lets you have control over cross-site requests. The latest development version lets you blacklist or whitelist requests by default. Disabling unnecessary cross-site requests leads to better privacy, safety and faster browsing.

For more information on cross-site requests and RequestPolicy visit [here](https://www.requestpolicy.com/faq.html).

### Decentraleyes

[Decentraleyes](https://addons.mozilla.org/firefox/addon/decentraleyes/) protects you against tracking through "free", centralized, content delivery. It prevents a lot of requests from reaching networks like Google Hosted Libraries, and serves local files to keep sites from breaking. Complements regular content blockers.

### CanvasBlocker

[CanvasBlocker](https://addons.mozilla.org/firefox/addon/canvasblocker/) Blocks or fakes the JS-API for modifying <canvas> to prevent Canvas-Fingerprinting.</canvas>

## Configuration tweaks

The following are privacy-focused configuration tweaks to prevent [browser fingerprinting](https://panopticlick.eff.org/) and tracking.

### Enable tracking protection

Mozilla's built-in tracking protection may be enabled in `about:config` by setting the following preference to `true`:

```
privacy.trackingprotection.enabled

```

Note that this is not a replacement for extensions such as UBlock Origin and it may or may not work with [Firefox forks](/index.php/List_of_applications/Internet "List of applications/Internet").

### Change browser time zone

The time zone of your system can be used in browser fingerprinting. To set firefox's time zone to UTC launch it as:

```
$ TZ=UTC firefox

```

Or, set a script to launch the above (for example, at `/usr/local/bin/firefox`).

### Change user agent and platform

To change the user agent in firefox, add the following `string` key in `about:config`:

```
general.useragent.override

```

The value for the key is your browser's user agent. Select a known common one.

**Tip:** The value `Mozilla/5.0 (Windows NT 6.1; rv:38.0) Gecko/20100101 Firefox/38.0` is used as the user agent for the Tor browser, thus being very common.

**Warning:** Changing the user agent without changing to a corresponding platform will make your browser nearly unique.

To change the platform for firefox, add the following `string` key in `about:config`:

```
general.platform.override

```

Select a known common platform that corresponds with your user agent.

**Tip:** The value `Win32` is used as the platform for the Tor browser, corresponding with the user agent provided above.

### Disable battery api

Firefox is disabling the battery api for web content starting with Firefox 52, the api will still be available for add-ons [[2]](https://bugzilla.mozilla.org/show_bug.cgi?id=1313580) [[3]](https://www.theguardian.com/technology/2016/nov/01/firefox-disable-battery-status-api-tracking)

Battery status api may be used to fingerprint the user[[4]](http://eprint.iacr.org/2015/616.pdf). To disable it, set `dom.battery.enabled` to `false` in `about:config`.