Related articles

*   [Firefox](/index.php/Firefox "Firefox")
*   [Tor](/index.php/Tor "Tor")
*   [Browser Plugins](/index.php/Browser_Plugins "Browser Plugins")
*   [Firefox/Tweaks](/index.php/Firefox/Tweaks "Firefox/Tweaks")
*   [Firefox/Profile on RAM](/index.php/Firefox/Profile_on_RAM "Firefox/Profile on RAM")

This article overviews how to configure [Firefox](/index.php/Firefox "Firefox") to enhance security and privacy.

## Contents

*   [1 Configuration tweaks](#Configuration_tweaks)
    *   [1.1 Enable Anti-Fingerprinting](#Enable_Anti-Fingerprinting)
    *   [1.2 Enable tracking protection](#Enable_tracking_protection)
    *   [1.3 Change browser time zone](#Change_browser_time_zone)
    *   [1.4 Change user agent and platform](#Change_user_agent_and_platform)
    *   [1.5 WebRTC exposes LAN IP address](#WebRTC_exposes_LAN_IP_address)
    *   [1.6 Disable 1024-bit Diffie-Hellman primes](#Disable_1024-bit_Diffie-Hellman_primes)
    *   [1.7 Disable telemetry](#Disable_telemetry)
    *   [1.8 Enable Do Not Track Header (DNT)](#Enable_Do_Not_Track_Header_.28DNT.29)
    *   [1.9 Disable geolocation](#Disable_geolocation)
    *   [1.10 Disable Safe Browsing service](#Disable_Safe_Browsing_service)
    *   [1.11 Disable WebGL](#Disable_WebGL)
*   [2 Extensions](#Extensions)
    *   [2.1 NoScript](#NoScript)
    *   [2.2 RequestPolicy Continued](#RequestPolicy_Continued)
    *   [2.3 CanvasBlocker](#CanvasBlocker)
*   [3 Remove system-wide hidden extensions](#Remove_system-wide_hidden_extensions)
*   [4 See also](#See_also)

## Configuration tweaks

The following are privacy-focused configuration tweaks to prevent [browser fingerprinting](https://panopticlick.eff.org/) and tracking.

In addition, see the following links:

*   [MozillaWiki:Privacy/Privacy Task Force/firefox about config privacy tweeks](https://wiki.mozilla.org/Privacy/Privacy_Task_Force/firefox_about_config_privacy_tweeks "mozillawiki:Privacy/Privacy Task Force/firefox about config privacy tweeks") - a wiki page maintained by Mozilla with descriptions of privacy specific settings.
*   [How to stop Firefox from making automatic connections](https://support.mozilla.org/en-US/kb/how-stop-firefox-making-automatic-connections) - Is an annotated list of corresponding Firefox functionality and settings to disable it case-by-case.
*   [ffprofile.com](https://ffprofile.com/) - You select which features you want to enable and disable and in the end you get a download link for a zip-file with your profile template. You can for example disable some functions, which send data to Mozilla and Google, or disable several annoying Firefox functions like Mozilla Hello or the Pocket integration.
*   [pyllyukko/user.js](https://github.com/pyllyukko/user.js) - Firefox configuration hardening and documentation

### Enable Anti-Fingerprinting

Mozilla has started an [anti-fingerprinting project in Firefox](https://wiki.mozilla.org/Security/Fingerprinting "mozillawiki:Security/Fingerprinting"), as part of a project to upstream features from [Tor Browser](/index.php/Tor "Tor"). Many of these anti-fingerprinting features are enabled by setting `about:config`:

*   `privacy.resistFingerprinting` `true`

There is no user-facing documentation about this flag, and Mozilla does not recommend users enable it, since it will break a few websites (it exists mostly to make life easier for the Tor Browser developers). But it does automatically enable many of the features listed below (such as changing your reported timezone and user agent), as well as protection against other, lesser-known fingerprinting techniques. See the [tracking bug](https://bugzilla.mozilla.org/show_bug.cgi?id=1333933) that lists many of these features.

### Enable tracking protection

Firefox gained an option for [tracking protection](https://support.mozilla.org/en-US/kb/tracking-protection-firefox). It can be enabled by setting `about:config`:

*   `privacy.trackingprotection.enabled` `true`

Apart from privacy benefits, enabling [tracking protection](http://venturebeat.com/2015/05/24/firefoxs-optional-tracking-protection-reduces-load-time-for-top-news-sites-by-44/) may also reduce load time by 44%.

Note that this is not a replacement for ad blocking extensions such as [#uBlock Origin](#uBlock_Origin) and it may or may not work with [Firefox forks](/index.php/List_of_applications/Internet#Firefox_spin-offs "List of applications/Internet"). If you are already running such an ad blocker with the correct lists, tracking protection might be redundant.

### Change browser time zone

The time zone of your system can be used in browser fingerprinting. To set Firefox's time zone to UTC launch it as:

```
$ TZ=UTC firefox

```

Or, set a script to launch the above (for example, at `/usr/local/bin/firefox`).

### Change user agent and platform

You can override Firefox's user agent with the `general.useragent.override` preference in `about:config`.

The value for the key is your browser's user agent. Select a known common one.

**Tip:**

*   The value `Mozilla/5.0 (Windows NT 6.1; rv:52.0) Gecko/20100101 Firefox/52.0` is used as the user agent for the Tor browser, thus being very common.
*   The [#Enable Anti-Fingerprinting](#Enable_Anti-Fingerprinting) option also enables the Tor browser user agent and changes your browser platform automatically.

**Warning:** Changing the user agent without changing to a corresponding platform will make your browser nearly unique.

To change the platform for firefox, add the following `string` key in `about:config`:

```
general.platform.override

```

Select a known common platform that corresponds with your user agent.

**Tip:** The value `Win32` is used as the platform for the Tor browser, corresponding with the user agent provided above.

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

Set `toolkit.telemetry.enabled` to `false` and/or disable it under *Preferences > Privacy & Security > Firefox Data Collection and Use*.

### Enable Do Not Track Header (DNT)

**Note:** The remote server may choose to not honour the Do Not Track request.

**Warning:** The Do Not Track header may be used to fingerprint your browser, since most users leave the option disabled.

Set `privacy.donottrackheader.enabled` to `true` or toggle it in *Preferences > Privacy & Security > Tracking Protection*

### Disable geolocation

Set `geo.enabled` to `false` in `about:config`.

### Disable Safe Browsing service

Safe Browsing offers phishing protection and malware checks, however it may send user information (e.g. URL, file hashes, etc.) to third parties like Google.

To disable the Safe Browsing service, in `about:config` set:

*   `browser.safebrowsing.malware.enabled` to `false`
*   `browser.safebrowsing.phishing.enabled` to `false`

In addition disable download checking, by setting `browser.safebrowsing.downloads.enabled` to `false`.

### Disable WebGL

WebGL is a potential security risk.[[1]](http://security.stackexchange.com/questions/13799/is-webgl-a-security-concern) Set `webgl.disabled` to `true` in `about:config` if you want to disable it.

## Extensions

This section lists Firefox-only privacy extensions, for cross-browser privacy extensions, see [Browser extensions#Privacy](/index.php/Browser_extensions#Privacy "Browser extensions").

### NoScript

[NoScript](http://noscript.net/) is an extension which disables JavaScript and Flash on any website not specifically whitelisted by the user. This extension will protect you from exploitation of security vulnerabilities by not letting anything but trusted sites (e.g: your bank, webmail) serve you executable content.

Once installed you can configure settings for NoScript by either clicking its icon on the toolbar or right clicking a page and navigating to NoScript. You will then have the option to enable/disable scripts for the current page, as well as any third party scripts that the page is linking to. Alternatively you can choose to enable scripts temporarily for that session only.

Be aware a lot of modern websites use scripts for layout purposes, hence content may look different. For example, failed rendering due to missing fonts might occur on websites that load fonts at runtime via scripts, which were blocked by NoScript.

For more detailed configuration see the [NoScript FAQ](http://noscript.net/faq).

### RequestPolicy Continued

[RequestPolicy Continued](https://addons.mozilla.org/firefox/addon/requestpolicy-continued/) (a successor to the original [RequestPolicy](https://addons.mozilla.org/firefox/addon/requestpolicy/)) is an extension for Mozilla browsers which lets you have control over cross-site requests. It also lets you blacklist or whitelist requests by default. Disabling unnecessary cross-site requests leads to better privacy, safety and faster browsing.

**Note:** This addon is currently [in the process of being updated](https://github.com/RequestPolicyContinued/requestpolicy/issues/704) for use on modern versions of Firefox (57+).

### CanvasBlocker

[CanvasBlocker](https://addons.mozilla.org/firefox/addon/canvasblocker/) Blocks or fakes the JS-API for modifying <canvas> to prevent Canvas-Fingerprinting.</canvas>

**Note:** Mozilla is adding a built-in permission system to allow blocking of HTML5 canvas image track requests, [targeted for release with verion 59](https://wiki.mozilla.org/Security/Fingerprinting "mozillawiki:Security/Fingerprinting").

## Remove system-wide hidden extensions

Several extensions, hidden to the user, are installed by default in `/usr/lib/firefox/browser/features`. Many can be safely removed via `rm *extension-name*.xpi` in order to completely remove unwanted features. Many of these extensions are not enabled by default and have a menu option for enabling or disabling. Note that any files removed will return upon update of the [firefox](https://www.archlinux.org/packages/?name=firefox) package. To keep these extensions removed, consider adding the directories to `NoExtract=` in `pacman.conf`, see [Pacman#Skip files from being installed to system](/index.php/Pacman#Skip_files_from_being_installed_to_system "Pacman"). Below are a few examples of these extensions and their features.

*   `activity-stream@mozilla.org.xpi` - "Activity Stream" which replaces the new tab page. See [[2]](https://github.com/mozilla/activity-stream)

*   `firefox@getpocket.com.xpi` - [Pocket](https://getpocket.com/firefox/)

*   `followonsearch@mozilla.com.xpi` - Search telemetry. See also [#Disable telemetry](#Disable_telemetry).

*   `shield-recipe-client@mozilla.org.xpi` [SHIELD studies](https://support.mozilla.org/en-US/kb/shield)

See also [[3]](https://dxr.mozilla.org/mozilla-release/source/browser/extensions/) for a full list of system extensions including README files describing their functions.

## See also

*   [privacytools.io Firefox Privacy Add-ons](https://www.privacytools.io/#addons)
*   [prism-break.org Web Browser Addons](https://prism-break.org/en/categories/gnu-linux/#web-browser-addons)