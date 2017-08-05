This article overviews configuration settings and some useful extensions which enhance security and privacy while using the [Firefox](/index.php/Firefox "Firefox") web browser.

## Contents

*   [1 Configuration tweaks](#Configuration_tweaks)
    *   [1.1 Enable tracking protection](#Enable_tracking_protection)
    *   [1.2 Change browser time zone](#Change_browser_time_zone)
    *   [1.3 Change user agent and platform](#Change_user_agent_and_platform)
    *   [1.4 Disable battery API](#Disable_battery_API)
    *   [1.5 WebRTC exposes LAN IP address](#WebRTC_exposes_LAN_IP_address)
    *   [1.6 Disable 1024-bit Diffie-Hellman primes](#Disable_1024-bit_Diffie-Hellman_primes)
    *   [1.7 Disable telemetry](#Disable_telemetry)
    *   [1.8 Enable Do Not Track Header (DNT)](#Enable_Do_Not_Track_Header_.28DNT.29)
    *   [1.9 Disable geolocation](#Disable_geolocation)
    *   [1.10 Disable Safe Browsing service](#Disable_Safe_Browsing_service)
    *   [1.11 Disable WebGL](#Disable_WebGL)
*   [2 Extensions](#Extensions)
    *   [2.1 HTTPS Everywhere](#HTTPS_Everywhere)
    *   [2.2 uBlock Origin](#uBlock_Origin)
    *   [2.3 Adblock Plus](#Adblock_Plus)
    *   [2.4 Privacy Badger](#Privacy_Badger)
    *   [2.5 Disconnect](#Disconnect)
    *   [2.6 NoScript](#NoScript)
    *   [2.7 uMatrix](#uMatrix)
    *   [2.8 Cookie Monster](#Cookie_Monster)
    *   [2.9 Self-Destructing Cookies](#Self-Destructing_Cookies)
    *   [2.10 RefControl](#RefControl)
    *   [2.11 RequestPolicy](#RequestPolicy)
    *   [2.12 Decentraleyes](#Decentraleyes)
    *   [2.13 CanvasBlocker](#CanvasBlocker)
    *   [2.14 Random User Agent](#Random_User_Agent)
    *   [2.15 Privacy Settings](#Privacy_Settings)
    *   [2.16 Stop Fingerprinting](#Stop_Fingerprinting)

## Configuration tweaks

The following are privacy-focused configuration tweaks to prevent [browser fingerprinting](https://panopticlick.eff.org/) and tracking.

In addition, see the following links:

*   [How to stop Firefox from making automatic connections](https://support.mozilla.org/t5/Protect-your-privacy/How-to-stop-Firefox-from-making-automatic-connections/ta-p/1748) - Is an annotated list of corresponding Firefox functionality and settings to disable it case-by-case.
*   [ffprofile.com](https://ffprofile.com/) - You select which features you want to enable and disable and in the end you get a download link for a zip-file with your profile template. You can for example disable some functions, which send data to Mozilla and Google, or disable several annoying Firefox functions like Mozilla Hello or the Pocket integration.
*   [user.js Firefox hardening stuff](https://github.com/pyllyukko/user.js) - This is a user.js configuration file for Mozilla Firefox that's supposed to harden Firefox's settings and make it more secure.

### Enable tracking protection

Firefox gained an option for [tracking protection](https://support.mozilla.org/en-US/kb/tracking-protection-firefox). It can be enabled by setting `about:config`:

*   `privacy.trackingprotection.enabled` `true`

Apart from privacy benefits, enabling [tracking protection](http://venturebeat.com/2015/05/24/firefoxs-optional-tracking-protection-reduces-load-time-for-top-news-sites-by-44/) may also reduce load time by 44%.

Note that this is not a replacement for ad blocking extensions such as [#uBlock Origin](#uBlock_Origin) and it may or may not work with [Firefox forks](/index.php/List_of_applications/Internet#Firefox_spin-offs "List of applications/Internet").

### Change browser time zone

The time zone of your system can be used in browser fingerprinting. To set firefox's time zone to UTC launch it as:

```
$ TZ=UTC firefox

```

Or, set a script to launch the above (for example, at `/usr/local/bin/firefox`).

### Change user agent and platform

You can override Firefox's user agent with the `general.useragent.override` preference in `about:config`.

The value for the key is your browser's user agent. Select a known common one.

**Tip:** The value `Mozilla/5.0 (Windows NT 6.1; rv:52.0) Gecko/20100101 Firefox/52.0` is used as the user agent for the Tor browser, thus being very common.

**Warning:** Changing the user agent without changing to a corresponding platform will make your browser nearly unique.

To change the platform for firefox, add the following `string` key in `about:config`:

```
general.platform.override

```

Select a known common platform that corresponds with your user agent.

**Tip:** The value `Win32` is used as the platform for the Tor browser, corresponding with the user agent provided above.

### Disable battery API

Firefox is disabling the battery API for web content starting with Firefox 52, the API will still be available for add-ons [[1]](https://bugzilla.mozilla.org/show_bug.cgi?id=1313580) [[2]](https://www.theguardian.com/technology/2016/nov/01/firefox-disable-battery-status-api-tracking)

Battery status API may be used to fingerprint the user[[3]](http://eprint.iacr.org/2015/616.pdf). To disable it, set `dom.battery.enabled` to `false` in `about:config`.

### WebRTC exposes LAN IP address

To prevent websites from getting your local IP address via [WebRTC](https://en.wikipedia.org/wiki/WebRTC "wikipedia:WebRTC")'s peer-to-peer (and JavaScript), open `about:config` and set:

*   `media.peerconnection.ice.default_address_only` to `true`
*   `media.peerconnection.enabled` to `false`. (only if you want to completely disable WebRTC)

You can use this [WebRTC test page](http://net.ipcalf.com/) and [WebRTC IP Leak VPN / Tor IP Test](https://www.privacytools.io/webrtc.html) to confirm that your internal/external IP address is no longer leaked.

### Disable 1024-bit Diffie-Hellman primes

Following [recent research](https://freedom-to-tinker.com/blog/haldermanheninger/how-is-nsa-breaking-so-much-crypto/) it is likely that the NSA has been breaking 1024-bit Diffie-Hellman for some time now. To disable these switch the [following](https://www.eff.org/deeplinks/2015/10/how-to-protect-yourself-from-nsa-attacks-1024-bit-DH) settings to `false` in `about:config`:

```
security.ssl3.dhe_rsa_aes_128_sha
security.ssl3.dhe_rsa_aes_256_sha

```

Then consider checking your SSL configuration at [https://www.howsmyssl.com/](https://www.howsmyssl.com/).

### Disable telemetry

Set `toolkit.telemetry.enabled` to `false` and/or disable it under Preferences, Advanced, Data Choices.

### Enable Do Not Track Header (DNT)

**Note:** The user has no control over whether the request is honoured or not.

Set `privacy.donottrackheader.enabled` to `true` or toggle it in *Preferences > Privacy > Manage your Do Not Track settings*.

### Disable geolocation

Set `geo.enabled` to `false` in `about:config`.

### Disable Safe Browsing service

Safe Browsing offers phishing protection and malware checks, however it may send user information (e.g. URL, file hashes, etc.) to third parties like Google.

To disable the Safe Browsing service, in `about:config` set:

*   `browser.safebrowsing.malware.enabled` to `false`
*   `browser.safebrowsing.phishing.enabled` to `false`

In addition disable download checking, by setting `browser.safebrowsing.downloads.enabled` to `false`.

### Disable WebGL

WebGL is a potential security risk.[[4]](http://security.stackexchange.com/questions/13799/is-webgl-a-security-concern) Set `webgl.disabled` to `true` in `about:config` if you want to disable it.

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

[Adblock Plus](https://adblockplus.org/en/) was a popular extension to block ads. Now that it is not blocking some ads on purpose [[5]](https://adblockplus.org/acceptable-ads), it may be a better idea to use a different blocker like uBlock Origin.

### Privacy Badger

[Privacy Badger](https://www.eff.org/privacybadger) is an extension that monitors third-party trackers loaded with web content. It blocks trackers once they appear on different sites. It does not block advertisements in the first place, but since a lot of ads are served based on tracking information these are blocked as well. For more information on the mechanism, see its [FAQ](https://www.eff.org/privacybadger#faq-How-is-Privacy-Badger-different-to-Disconnect,-Adblock-Plus,-Ghostery,-and-other-blocking-extensions?).

### Disconnect

Disconnect is a open source project aimed at stopping 2,000 third-party sites from tracking a user. It encrypts data sent to popular sites and claims to loads web pages 27 percent faster. Disconnect shows its users, in real time, how many tracking attempts from Google, Twitter, Facebook, and more are stopped. It categorizes tracking attempts into advertising, analytical, social, and content, which makes it easy to monitor how one is being tracked.

Disconnect can also stop side-jacking, which utilizes stolen cookies to steal personal data. It is easy to use and well supported. It can be added to Firefox at the [official website](https://disconnect.me/).

**Note:** Firefox gained a feature based on the Disconnect list. See [#Enable tracking protection](#Enable_tracking_protection).

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

**Note:** Firefox has options to control emitted HTTP referers, possibly replacing plugins such as RefControl and Smart Referer. See [Firefox tweaks#Referrer header control](/index.php/Firefox_tweaks#Referrer_header_control "Firefox tweaks").

### RequestPolicy

[RequestPolicy](https://www.requestpolicy.com/) is an extension for Mozilla browsers which lets you have control over cross-site requests. The latest development version lets you blacklist or whitelist requests by default. Disabling unnecessary cross-site requests leads to better privacy, safety and faster browsing.

For more information on cross-site requests and RequestPolicy visit [here](https://www.requestpolicy.com/faq.html).

### Decentraleyes

[Decentraleyes](https://addons.mozilla.org/firefox/addon/decentraleyes/) protects you against tracking through "free", centralized, content delivery. It prevents a lot of requests from reaching networks like Google Hosted Libraries, and serves local files to keep sites from breaking. Complements regular content blockers.

### CanvasBlocker

[CanvasBlocker](https://addons.mozilla.org/firefox/addon/canvasblocker/) Blocks or fakes the JS-API for modifying <canvas> to prevent Canvas-Fingerprinting.</canvas>

### Random User Agent

[Random User Agent](https://addons.mozilla.org/firefox/addon/random-agent-spoofer/) rotates complete browser profiles (from real browsers/devices) at a user defined time interval. It includes many extra privacy enhancing options.

### Privacy Settings

[Privacy Settings](https://addons.mozilla.org/firefox/addon/privacy-settings/) provides a toolbar panel for easily altering Firefox's built-in privacy settings.

### Stop Fingerprinting

[Stop Fingerprinting](https://addons.mozilla.org/firefox/addon/stop-fingerprinting/) disables / modifies some browser APIs that would otherwise allow browser fingerprinting.