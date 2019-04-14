Related articles

*   [Firefox](/index.php/Firefox "Firefox")
*   [Tor](/index.php/Tor "Tor")
*   [Browser extensions](/index.php/Browser_extensions "Browser extensions")
*   [Browser Plugins](/index.php/Browser_Plugins "Browser Plugins")
*   [Firefox/Tweaks](/index.php/Firefox/Tweaks "Firefox/Tweaks")
*   [Firefox/Profile on RAM](/index.php/Firefox/Profile_on_RAM "Firefox/Profile on RAM")

This article overviews how to configure Firefox to enhance security and privacy.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Configuration](#Configuration)
    *   [1.1 Anti-fingerprinting](#Anti-fingerprinting)
    *   [1.2 Tracking protection](#Tracking_protection)
    *   [1.3 Change browser time zone](#Change_browser_time_zone)
    *   [1.4 Change user agent and platform](#Change_user_agent_and_platform)
    *   [1.5 WebRTC exposes LAN IP address](#WebRTC_exposes_LAN_IP_address)
    *   [1.6 Disable telemetry](#Disable_telemetry)
    *   [1.7 Enable Do Not Track Header (DNT)](#Enable_Do_Not_Track_Header_(DNT))
    *   [1.8 Disable/Enforce Trusted Recursive Resolver](#Disable/Enforce_Trusted_Recursive_Resolver)
    *   [1.9 Disable geolocation](#Disable_geolocation)
    *   [1.10 Disable Safe Browsing service](#Disable_Safe_Browsing_service)
    *   [1.11 Disable WebGL](#Disable_WebGL)
*   [2 Extensions](#Extensions)
*   [3 Remove system-wide hidden extensions](#Remove_system-wide_hidden_extensions)
*   [4 Hardened user.js templates](#Hardened_user.js_templates)
*   [5 See also](#See_also)

## Configuration

The following are privacy-focused configuration tweaks to prevent [browser fingerprinting](https://panopticlick.eff.org/) and tracking.

### Anti-fingerprinting

Mozilla has started an [anti-fingerprinting project in Firefox](https://wiki.mozilla.org/Security/Fingerprinting "mozillawiki:Security/Fingerprinting"), as part of a project to upstream features from [Tor Browser](/index.php/Tor_Browser "Tor Browser"). Many of these anti-fingerprinting features are enabled by setting `about:config`:

*   `privacy.resistFingerprinting` `true`

There is no user-facing documentation about this flag, and Mozilla does not recommend users enable it, since it will break a few websites (it exists mostly to make life easier for the Tor Browser developers). But it does automatically enable many of the features listed below (such as changing your reported timezone and user agent), as well as protection against other, lesser-known fingerprinting techniques. See the [tracking bug](https://bugzilla.mozilla.org/show_bug.cgi?id=1333933) that lists many of these features.

### Tracking protection

Firefox gained an option for [tracking protection](https://support.mozilla.org/en-US/kb/tracking-protection-firefox). It can be enabled by setting `about:config`:

*   `privacy.trackingprotection.enabled` `true`

Apart from privacy benefits, enabling [tracking protection](http://venturebeat.com/2015/05/24/firefoxs-optional-tracking-protection-reduces-load-time-for-top-news-sites-by-44/) may also reduce load time by 44%.

Note that this is not a replacement for ad blocking extensions such as [uBlock Origin](/index.php/Browser_extensions#Content_blockers "Browser extensions") and it may or may not work with [Firefox forks](/index.php/List_of_applications/Internet#Firefox_spin-offs "List of applications/Internet"). If you are already running such an ad blocker with the correct lists, tracking protection might be redundant.

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
*   The [#Anti-fingerprinting](#Anti-fingerprinting) option also enables the Tor browser user agent and changes your browser platform automatically.

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

You can use this [WebRTC test page](http://net.ipcalf.com/) and [WebRTC IP Leak VPN / Tor IP Test](https://ipleak.net/) to confirm that your internal/external IP address is no longer leaked.

### Disable telemetry

Set `toolkit.telemetry.enabled` to `false` and/or disable it under *Preferences > Privacy & Security > Firefox Data Collection and Use*.

### Enable Do Not Track Header (DNT)

**Note:** The remote server may choose to not honour the Do Not Track request.

**Warning:** The Do Not Track header may be used to fingerprint your browser, since most users leave the option disabled.

Set `privacy.donottrackheader.enabled` to `true` or toggle it in *Preferences > Privacy & Security > Tracking Protection*

### Disable/Enforce Trusted Recursive Resolver

Firefox 60 introduced a feature called [Trusted Recursive Resolver](https://wiki.mozilla.org/Trusted_Recursive_Resolver "mozillawiki:Trusted Recursive Resolver") (TRR). It circumvents DNS servers configured in your system, instead sending all DNS requests over HTTPS to Cloudflare servers. While this is significantly more secure (as "classic" DNS requests are sent in plain text over the network, and everyone along the way can snoop on these), this also makes all your DNS requests readable by Cloudflare, providing TRR servers.

*   If you trust DNS servers you've configured yourself more than Cloudflare's, you can disable TRR in `about:config` by setting `network.trr.mode` (integer, create it it it doesn't exist) to `5`. (A value of 0 means disabled by default, and might be overridden by future updates - a value of 5 is disabled by choice and will not be overridden.)
*   If you trust Cloudflare DNS servers and would prefer extra privacy (thanks to encrypted DNS requests), you can enforce TRR by setting `network.trr.mode` to `3` (which completely disables classic DNS requests) or `2` (uses TRR by default, falls back to classic DNS requests if that fails). Keep in mind that if you're using any intranet websites or trying to access computers in your local networks by their hostnames, enabling TRR may break name resolving in such cases.
*   If you want to encrypt your DNS requests but not use Cloudflare servers, you can point to a new DNS over HTTPS server by setting `network.trr.uri` to your resolver URL. A list of currently available resolvers can be found in the [curl wiki](https://github.com/curl/curl/wiki/DNS-over-HTTPS#publicly-available-servers), along with other configuration options for TRR.

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

See [Browser extensions#Privacy](/index.php/Browser_extensions#Privacy "Browser extensions").

## Remove system-wide hidden extensions

Several extensions, hidden to the user, are installed by default in `/usr/lib/firefox/browser/features`. Many can be safely removed via `rm *extension-name*.xpi` in order to completely remove unwanted features. Many of these extensions are not enabled by default and have a menu option for enabling or disabling. Note that any files removed will return upon update of the [firefox](https://www.archlinux.org/packages/?name=firefox) package. To keep these extensions removed, consider adding the directories to `NoExtract=` in `pacman.conf`, see [Pacman#Skip files from being installed to system](/index.php/Pacman#Skip_files_from_being_installed_to_system "Pacman"). Below are a few examples of these extensions and their features.

*   `activity-stream@mozilla.org.xpi` - "Activity Stream" which replaces the new tab page. See [[2]](https://github.com/mozilla/activity-stream)

*   `firefox@getpocket.com.xpi` - [Pocket](https://getpocket.com/firefox/)

*   `followonsearch@mozilla.com.xpi` - Search telemetry. See also [#Disable telemetry](#Disable_telemetry).

*   `shield-recipe-client@mozilla.org.xpi` [SHIELD studies](https://support.mozilla.org/en-US/kb/shield)

See also [[3]](https://dxr.mozilla.org/mozilla-release/source/browser/extensions/) for a full list of system extensions including README files describing their functions.

## Hardened user.js templates

Several active projects maintain comprehensive hardened Firefox configurations in the form of a `user.js` config that can be dropped to Firefox profile directory:

*   [pyllyukko/user.js](https://github.com/pyllyukko/user.js)
*   [ghacksuserjs/ghacks-user.js](https://github.com/ghacksuserjs/ghacks-user.js)
*   [ffprofile.com](https://ffprofile.com/) ([github](https://github.com/allo-/firefox-profilemaker)) - online user.js generator. You select which features you want to enable and disable and in the end you get a download link for a zip-file with your profile template. You can for example disable some functions, which send data to Mozilla and Google, or disable several annoying Firefox functions like Mozilla Hello or the Pocket integration.

## See also

*   [privacytools.io Firefox Privacy Add-ons](https://www.privacytools.io/#addons)
*   [prism-break.org Web Browser Addons](https://prism-break.org/en/categories/gnu-linux/#web-browser-addons)
*   [MozillaWiki:Privacy/Privacy Task Force/firefox about config privacy tweeks](https://wiki.mozilla.org/Privacy/Privacy_Task_Force/firefox_about_config_privacy_tweeks "mozillawiki:Privacy/Privacy Task Force/firefox about config privacy tweeks") - a wiki page maintained by Mozilla with descriptions of privacy specific settings.
*   [How to stop Firefox from making automatic connections](https://support.mozilla.org/en-US/kb/how-stop-firefox-making-automatic-connections) - Is an annotated list of corresponding Firefox functionality and settings to disable it case-by-case.