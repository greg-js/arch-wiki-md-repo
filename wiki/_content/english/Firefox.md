Related articles

*   [Browser plugins](/index.php/Browser_plugins "Browser plugins")
*   [Firefox/Tweaks](/index.php/Firefox/Tweaks "Firefox/Tweaks")
*   [Firefox/Profile on RAM](/index.php/Firefox/Profile_on_RAM "Firefox/Profile on RAM")
*   [Firefox/Privacy](/index.php/Firefox/Privacy "Firefox/Privacy")
*   [Chromium](/index.php/Chromium "Chromium")
*   [Opera](/index.php/Opera "Opera")

[Firefox](https://www.mozilla.org/firefox) is a popular open source graphical web browser from [Mozilla](https://www.mozilla.org).

## Contents

*   [1 Installing](#Installing)
*   [2 Add-ons](#Add-ons)
    *   [2.1 Adding search engines](#Adding_search_engines)
        *   [2.1.1 arch-firefox-search](#arch-firefox-search)
*   [3 Configuration](#Configuration)
    *   [3.1 Multimedia playback](#Multimedia_playback)
        *   [3.1.1 Open-with extension](#Open-with_extension)
    *   [3.2 Dictionaries for spell checking](#Dictionaries_for_spell_checking)
    *   [3.3 KDE/GNOME integration](#KDE.2FGNOME_integration)
*   [4 Plugins](#Plugins)
*   [5 Tips and tricks](#Tips_and_tricks)
    *   [5.1 Screenshot of webpage](#Screenshot_of_webpage)
*   [6 Troubleshooting](#Troubleshooting)
    *   [6.1 Firefox startup takes very long](#Firefox_startup_takes_very_long)
    *   [6.2 Font troubleshooting](#Font_troubleshooting)
    *   [6.3 Setting an email client](#Setting_an_email_client)
    *   [6.4 File association](#File_association)
    *   [6.5 Firefox keeps creating ~/Desktop even when this is not desired](#Firefox_keeps_creating_.7E.2FDesktop_even_when_this_is_not_desired)
    *   [6.6 Make plugins respect blocked pop-ups](#Make_plugins_respect_blocked_pop-ups)
    *   [6.7 Middle-click errors](#Middle-click_errors)
    *   [6.8 Backspace does not work as the 'Back' button](#Backspace_does_not_work_as_the_.27Back.27_button)
    *   [6.9 Firefox does not remember login information](#Firefox_does_not_remember_login_information)
    *   [6.10 "Do you want Firefox to save your tabs for the next time it starts?" dialog does not appear](#.22Do_you_want_Firefox_to_save_your_tabs_for_the_next_time_it_starts.3F.22_dialog_does_not_appear)
    *   [6.11 Silently fails when installing desktop apps from marketplace](#Silently_fails_when_installing_desktop_apps_from_marketplace)
    *   [6.12 Firefox detects the wrong version of my plugin](#Firefox_detects_the_wrong_version_of_my_plugin)
    *   [6.13 Javascript context menu does not appear on some sites](#Javascript_context_menu_does_not_appear_on_some_sites)
    *   [6.14 Firefox does not remember default spell check language](#Firefox_does_not_remember_default_spell_check_language)
    *   [6.15 Some MathML symbols are missing](#Some_MathML_symbols_are_missing)
    *   [6.16 Tearing video in fullscreen mode](#Tearing_video_in_fullscreen_mode)
    *   [6.17 Firefox ESR 52 looks bad](#Firefox_ESR_52_looks_bad)
    *   [6.18 Firefox WebRTC module cannot detect a microphone](#Firefox_WebRTC_module_cannot_detect_a_microphone)
*   [7 See also](#See_also)

## Installing

Firefox can be [installed](/index.php/Installed "Installed") with the [firefox](https://www.archlinux.org/packages/?name=firefox) package.

Other alternatives include:

*   **Firefox Developer Edition** — for developers

	[https://www.mozilla.org/firefox/developer/](https://www.mozilla.org/firefox/developer/) || [firefox-developer-edition](https://www.archlinux.org/packages/?name=firefox-developer-edition)

*   **Firefox Extended Support Release** — long-term supported version

	[https://www.mozilla.org/firefox/organizations/](https://www.mozilla.org/firefox/organizations/) || [firefox-esr](https://aur.archlinux.org/packages/firefox-esr/) or [firefox-esr-bin](https://aur.archlinux.org/packages/firefox-esr-bin/)

*   **Firefox Beta** — cutting-edge version

	[https://www.mozilla.org/firefox/channel/desktop/#beta](https://www.mozilla.org/firefox/channel/desktop/#beta) || [firefox-beta](https://aur.archlinux.org/packages/firefox-beta/) or [firefox-beta-bin](https://aur.archlinux.org/packages/firefox-beta-bin/)

*   **Firefox Nightly** — nightly builds for testing ([experimental features](https://developer.mozilla.org/Firefox/Experimental_features))

	[https://www.mozilla.org/firefox/channel/desktop/#nightly](https://www.mozilla.org/firefox/channel/desktop/#nightly) || [firefox-nightly](https://aur.archlinux.org/packages/firefox-nightly/)

*   **Firefox KDE** — Version of Firefox that incorporates an OpenSUSE patch for better [KDE integration](#KDE.2FGNOME_integration) than is possible through simple Firefox plugins.

	[https://build.opensuse.org/package/show/mozilla:Factory/MozillaFirefox](https://build.opensuse.org/package/show/mozilla:Factory/MozillaFirefox) || [firefox-kde-opensuse](https://aur.archlinux.org/packages/firefox-kde-opensuse/)

*   On top of the different Mozilla build channels, a number of forks exist with more or less special features; see [List of applications#Gecko-based](/index.php/List_of_applications#Gecko-based "List of applications").

A number of language packs are available for Firefox, other than the standard English. Language packs are usually named as `firefox-i18n-*languagecode*` (where `*languagecode*` can be any language code, such as **de**, **ja**, **fr**, etc.). For a list of available language packs see [firefox-i18n](https://www.archlinux.org/packages/extra/any/firefox-i18n/) for [firefox](https://www.archlinux.org/packages/?name=firefox) and [firefox-developer-edition-i18n](https://www.archlinux.org/packages/community/any/firefox-developer-edition-i18n/) for [firefox-developer-edition](https://www.archlinux.org/packages/?name=firefox-developer-edition).

## Add-ons

Firefox is well known for its large library of add-ons which can be used to add new features or modify the behavior of existing features. Firefox's "Add-ons Manager" is used to manage installed add-ons or find new ones.

For a list of popular add-ons, see [Mozilla's add-on list sorted by popularity](https://addons.mozilla.org/firefox/extensions/?sort=popular). See also [List of Firefox extensions](https://en.wikipedia.org/wiki/List_of_Firefox_extensions "wikipedia:List of Firefox extensions") on Wikipedia.

### Adding search engines

Search engines can be added to Firefox through normal add-ons, see [this page](https://addons.mozilla.org/firefox/search-tools/) for a list of available search engines.

A very extensive list of search engines can be found at the [Mycroft Project](http://mycroftproject.com/).

Also, you can use the [add-to-searchbar](https://firefox.maltekraus.de/extensions/add-to-search-bar) extension to add a search to your search bar from any web site, by simply right clicking on the site's search field and selecting *Add to Search Bar...*

#### arch-firefox-search

Install the [arch-firefox-search](https://www.archlinux.org/packages/?name=arch-firefox-search) package to add Arch-specific searches (AUR, wiki, forum, etc, as specified by user) to the Firefox search toolbar.

## Configuration

Firefox exposes a number of configuration options. To examine them, enter in the Firefox address bar:

```
about:config

```

Once set, these affect the user's current profile, and may be synchronized across all devices via [Firefox Sync](https://www.mozilla.org/firefox/sync/). Please note that only a subset of the `about:config` entries are synchronized by this method, and the exact subset may be found by searching for `services.sync.prefs` in `about:config`. Additional preferences and third party preferences may be synchronized by creating new boolean entries prepending the config value with `services.sync.prefs.sync` ([documentation](https://developer.mozilla.org/en-US/docs/Archive/Mozilla/Firefox_Sync/Syncing_custom_preferences) is still applicable.) To synchronize the whitelist for the extension [NoScript](https://addons.mozilla.org/firefox/addon/noscript/):

```
services.sync.prefs.sync.capability.policy.maonoscript.sites

```

The boolean `noscript.sync.enabled` must be set to `true` to synchronize the remainder of NoScript's preferences via Firefox Sync.

Firefox also allows configuration for a profile via a `user.js` file: [user.js](http://kb.mozillazine.org/User.js_file) kept in the profile folder, usually `~/.mozilla/firefox/*xxxxxxxx*.default/`. For a useful starting point, see e.g [custom user.js](https://github.com/pyllyukko/user.js) which is targeted at privacy/security conscious users.

One drawback of the above approach is that it is not applied system-wide. Furthermore, this is not useful as a "pre-configuration", since the profile directory is created after first launch of the browser. You can, however, let *firefox* create a new profile and, after closing it again, [copy the contents](https://support.mozilla.org/en-US/kb/back-and-restore-information-firefox-profiles#w_restoring-a-profile-backup) of an already created profile folder into it.

Sometimes it may be desired to lock certain settings, a feature useful in widespread deployments of customized Firefox. In order to create a system-wide configuration, follow the steps outlined in [Locking preferences](http://kb.mozillazine.org/Locking_preferences):

1\. Create `/usr/lib/firefox/defaults/pref/local-settings.js`:

```
pref("general.config.obscure_value", 0);
pref("general.config.filename", "mozilla.cfg");

```

2\. Create `/usr/lib/firefox/mozilla.cfg` (this stores the actual configuration):

```
//
//...your settings...
// e.g to disable Pocket, uncomment the following line
// lockPref("browser.pocket.enabled", false);

```

Please note that the first line must contain exactly `//`. The syntax of the file is similar to that of `user.js`.

### Multimedia playback

Firefox uses [FFmpeg](/index.php/FFmpeg "FFmpeg") for playing multimedia inside HTML5 `<audio>` and `<video>` elements. Go to [YouTube's HTML5 page](https://www.youtube.com/html5), [video-test page](https://www.quirksmode.org/html5/tests/video.html) or [audio-test page](https://hpr.dogphilosophy.net/test/) to check which formats are actually supported.

HTML5 DRM playback is supported by the Google Widevine CDM, it is however not enabled by default. See *Preferences > General > Digital Rights Management (DRM) Content* if you want to learn more.

See [Firefox/Tweaks#Enable additional media codecs](/index.php/Firefox/Tweaks#Enable_additional_media_codecs "Firefox/Tweaks") for advanced configuration and enabling support for Widevine (Netflix, Amazon Video, etc.).

Starting with version 54, Firefox uses [PulseAudio](/index.php/PulseAudio "PulseAudio") for audio playback and capture. For sound to work, you need to install the [pulseaudio](https://www.archlinux.org/packages/?name=pulseaudio) package.

In case, for whatever reason, [PulseAudio](/index.php/PulseAudio "PulseAudio") is not an option for you, you can use [apulse](/index.php/Advanced_Linux_Sound_Architecture#PulseAudio_compatibility "Advanced Linux Sound Architecture") instead. To make this work, it is necessary to exclude `/dev/snd/` from Firefox' sandboxing by adding it to the comma-separated list in `about:config`:

```
security.sandbox.content.write_path_whitelist

```

**Note:** The trailing slash on `/dev/snd/` is important, otherwise *apulse* will report "Permission denied" errors.

If you are using Firefox 58 or above and have no audio even when using *apulse*, try adding `16` to `security.sandbox.content.syscall_whitelist` in `about:config`.

#### Open-with extension

1.  Install [Open-with](https://addons.mozilla.org/firefox/addon/open-with/) add-on.
2.  Open `about:openwith`, select *Add...*
3.  In the dialog select a video streaming capable player (e.g. [/usr/bin/mpv](/index.php/Mpv "Mpv")).
4.  (Optional step) Add needed arguments to the player (e.g. you may want `--force-window --ytdl` for *mpv*)
5.  (Optional step) Choose how to display the dialogs using the left panel.
6.  Right click on links or visit pages containing videos. If the site is supported, the player will open as expected.

The same procedure can be used to associate video downloaders such as *youtube-dl*.

### Dictionaries for spell checking

Install the [hunspell](https://www.archlinux.org/packages/?name=hunspell) package. You also need to install dictionaries for your language, such as [hunspell-fr](https://www.archlinux.org/packages/?name=hunspell-fr) (for the French language) or [hunspell-he](https://www.archlinux.org/packages/?name=hunspell-he) (for Hebrew).

By default, Firefox will try to symlink all your hunspell dictionaries in `/usr/lib/firefox/dictionaries/`. If you want to have less dictionaries offered to you in Firefox, you can remove some of those links. Be aware that it may not stand an upgrade of Firefox.

To enable spell checking for a specific language right click on any text field and check the *Check Spelling* box. To select a language for spell checking to you have right click again and select your language from the *Languages* sub-menu.

To get more languages just click *Add Dictionaries...* and select the dictionary you want to install from the list.

When your default language choice does not stick, see [#Firefox does not remember default spell check language](#Firefox_does_not_remember_default_spell_check_language).

### KDE/GNOME integration

*   To bring the [KDE](/index.php/KDE "KDE") look to GTK apps (including Firefox), [install](/index.php/Install "Install") [breeze-gtk](https://www.archlinux.org/packages/?name=breeze-gtk) and [kde-gtk-config](https://www.archlinux.org/packages/?name=kde-gtk-config). Afterwards, go to *System Settings > Application Style > GTK*. Be sure to choose 'Breeze' in 'Select a GTK2/GTK3 Theme' and check 'Show icons in GTK buttons' and 'Show icons in GTK'.
*   To make the left mouse button warp the scrollbar instead of the middle one on KDE, go to *System Settings > Application Style > GTK* and set the checkbox for "Left mouse button warps scrollbar".
*   For integration with [KDE](/index.php/KDE "KDE") mime type system and file dialog, one can use [firefox-kde-opensuse](https://aur.archlinux.org/packages/firefox-kde-opensuse/) variant from AUR with OpenSUSE’s patches applied.
*   Extensions/add-ons may provide additional integration, such as:
    *   Browser integration in [Plasma](/index.php/Plasma "Plasma"): requires [plasma-browser-integration](https://www.archlinux.org/packages/?name=plasma-browser-integration) and the [plasma-integration add-on](https://addons.mozilla.org/firefox/addon/plasma-integration/).
    *   [mozilla-extension-gnome-keyring-git](https://aur.archlinux.org/packages/mozilla-extension-gnome-keyring-git/) (all-JavaScript implementation) to integrate Firefox with [GNOME Keyring](/index.php/GNOME_Keyring "GNOME Keyring"). To make firefox-gnome-keyring use your login keychain, set `extensions.gnome-keyring.keyringName` to `login` in `about:config`. Note the lowercase 'l' despite the the keychain name having an uppercase 'L' in Seahorse.

## Plugins

**Note:** Firefox [has removed support](https://support.mozilla.org/en-US/kb/npapi-plugins) for [NPAPI](https://en.wikipedia.org/wiki/NPAPI "w:NPAPI") plugins, except for Flash. Firefox ESR 52 ([firefox-esr52](https://aur.archlinux.org/packages/firefox-esr52/)) will support plugins until August 2018.

See the main article: [Browser plugins](/index.php/Browser_plugins "Browser plugins")

To find out what plugins are installed/enabled, enter:

```
about:plugins

```

in the Firefox address bar or go to the *Add-ons* entry in the Firefox Menu and select the *Plugins* tab.

## Tips and tricks

For general enhancements see [Firefox/Tweaks](/index.php/Firefox/Tweaks "Firefox/Tweaks"), for privacy related enhancements see [Firefox/Privacy](/index.php/Firefox/Privacy "Firefox/Privacy").

### Screenshot of webpage

You can *Take a Screenshot* by either clicking the *Page actions* button (the three horizontal dots) in the address bar or by right-clicking on the webpage. See [[2]](https://support.mozilla.org/en-US/kb/firefox-screenshots) for more information.

**Note:** The *Save* button misleadingly uploads your screenshot to a firefox.com subdomain. Set `extensions.screenshots.upload-disabled` to `true` to disable this behaviour. [[3]](https://github.com/mozilla-services/screenshots/issues/3503)

Enabling `privacy.resistFingerprinting` apparently still breaks Firefox Screenshots in Firefox 61, even though the bug is marked as fixed.[[4]](https://bugzilla.mozilla.org/show_bug.cgi?id=1412961)

As an alternative you can use the full-page screenshot button in the *Developer Tools*, which you can open with `F12`; you might need to enable the button first.

## Troubleshooting

### Firefox startup takes very long

If Firefox takes much longer to start up than other browsers, it may be due to lacking configuration of the localhost in `/etc/hosts`. See [Network configuration#Local network hostname resolution](/index.php/Network_configuration#Local_network_hostname_resolution "Network configuration") on how to set it up.

### Font troubleshooting

See [Font configuration](/index.php/Font_configuration "Font configuration").

Firefox has a setting which determines how many replacements it will allow from fontconfig. To allow it to use all your replacement-rules, change `gfx.font_rendering.fontconfig.max_generic_substitutions` to `127` (the highest possible value).

### Setting an email client

Inside the browser, `mailto` links by default are opened by a web application such as Gmail or Yahoo Mail. To set an external email program, go to *Preferences > Applications* and modify the *action* corresponding to the `mailto` content type; the file path will need to be designated (e.g. `/usr/bin/kmail` for Kmail).

Outside the browser, `mailto` links are handled by the `x-scheme-handler/mailto` mime type, which can be easily configured with [xdg-mime](/index.php/Xdg-mime "Xdg-mime"). See [Default applications](/index.php/Default_applications "Default applications") for details and alternatives.

### File association

See [Default applications](/index.php/Default_applications "Default applications").

### Firefox keeps creating ~/Desktop even when this is not desired

Firefox uses `~/Desktop` as the default place for download and upload files. To change it to another folder, set the `XDG_DESKTOP_DIR` option as explained in [XDG user directories](/index.php/XDG_user_directories "XDG user directories").

### Make plugins respect blocked pop-ups

Some plugins can misbehave and bypass the default settings, such as the Flash plugin. You can prevent this by doing the following:

1.  Type `about:config` into the address bar.
2.  Right-click on the page and select *New > Integer*.
3.  Name it `privacy.popups.disable_from_plugins`.
4.  Set the value to `2`.

The possible values are:

*   `**0**`: Allow all popups from plugins.
*   `**1**`: Allow popups, but limit them to `dom.popup_maximum`.
*   `**2**`: Block popups from plugins.
*   `**3**`: Block popups from plugins, even on whitelisted sites.

### Middle-click errors

**Note:** This has been fixed in Firefox 57.[[5]](https://www.phoronix.com/scan.php?page=news_item&px=Firefox-Middle-Click-Bug)

A common error message you can get while using the middle mouse button in Firefox is:

```
The URL is not valid and cannot be loaded.

```

Another symptom is that middle-clicking results in unexpected behavior, like accessing a random web page. The reason stems from the use of the middle mouse buttons in UNIX-like operating systems. The middle mouse button is used to paste whatever text has been highlighted/added to the clipboard. Then there is the possibly conflicting feature in Firefox, which defaults to loading the URL of the corresponding text when the button is depressed. This can be disabled by setting `middlemouse.contentLoadURL` and `middlemouse.paste` to `false` in `about:config`.

To scroll on middle-click (default for Windows browsers) set `general.autoScroll` to `true`.

### Backspace does not work as the 'Back' button

According to [mozillaZine](http://kb.mozillazine.org/Browser.backspace_action), the `Backspace` key was mapped based on which platform the browser was running on. As a compromise, this preference was created to allow the `Backspace` key to either go back/forward, scroll up/down a page, or do nothing.

To make `Backspace` behave like the back button and go back one page in the session history, set `browser.backspace_action` to `0` in `about:config`.

To have the `Backspace` key scroll up one page and `Shift+Backspace` scroll down one page, set `browser.backspace_action` to `1`. Setting this property to any other value will leave the key unmapped (Arch Linux defaults to `2`, in other words, it is unmapped by default).

### Firefox does not remember login information

It may be due to a corrupted `cookies.sqlite` file in [Firefox's profile](https://support.mozilla.org/t5/Firefox/Profiles-Where-Firefox-stores-your-bookmarks-passwords-and-other/ta-p/4608#w_how-do-i-find-my-profile) folder. In order to fix this, just rename or remove `cookie.sqlite` while Firefox is not running.

Open a terminal of choice and type the following:

```
$ rm -f ~/.mozilla/firefox/<profile id>.default/cookies.sqlite

```

The profile id is a random 8 character string.

Restart Firefox and see if it solved the problem.

### "Do you want Firefox to save your tabs for the next time it starts?" dialog does not appear

From the [Mozilla support](https://support.mozilla.com/en-US/questions/767751) site:

1.  Type `about:config` in the address bar.
2.  Set `browser.warnOnQuit` to `true`.
3.  Set `browser.showQuitWarning` to `true`.

### Silently fails when installing desktop apps from marketplace

Installation of apps from Firefox OS Marketplace will silently fail if there is no `~/.local/share/applications` folder.

### Firefox detects the wrong version of my plugin

When you close Firefox, the latter saves the current timestamp and version of your plugins inside `pluginreg.dat` located in your profile folder, typically in `~/.mozilla/firefox/*xxxxxxxx*.default/`.

If you upgraded your plugin when Firefox was still running, you will thus have the wrong information inside that file. The next time you will restart Firefox you will get that message `Firefox has prevented the outdated plugin "XXXX" from running on ...` when you will be trying to open content dedicated to that plugin on the web. This problem often appears with the official [Adobe Flash Player plugin](/index.php/Browser_plugins#Adobe_Flash_Player "Browser plugins") which has been upgraded while Firefox was still running.

The solution is to remove the file `pluginreg.dat` from your profile and that is it. Firefox will not complain about the missing file as it will be recreated the next time Firefox will be closed. [[6]](https://bugzilla.mozilla.org/show_bug.cgi?id=1109795#c16)

### Javascript context menu does not appear on some sites

In `about:config`, unset the `dom.w3c_touch_events.enabled` setting.

### Firefox does not remember default spell check language

The default spell checking language can be set as follows:

1.  Type `about:config` in the address bar.
2.  Set `spellchecker.dictionary` to your language of choice, for instance `en_GB`.
3.  Notice that the for dictionaries installed as a Firefox plugin the notation is `en-GB`, and for [hunspell](https://www.archlinux.org/packages/?name=hunspell) dictionaries the notation is `en_GB`.

When you only have system wide dictionaries installed with [hunspell](https://www.archlinux.org/packages/?name=hunspell), Firefox might not remember your default dictionary language settings. This can be fixed by having at least one [dictionary](https://addons.mozilla.org/firefox/language-tools/) installed as a Firefox plugin. Notice that now you will also have a tab **Dictionaries** in **add-ons**.

Related questions on the **StackExchange** platform: [[7]](https://stackoverflow.com/questions/26936792/change-firefox-spell-check-default-language/29446115), [[8]](https://stackoverflow.com/questions/21542515/change-default-language-on-firefox/29446353), [[9]](https://askubuntu.com/questions/184300/how-can-i-change-firefoxs-default-dictionary/576877)

Related bug reports: [Bugzilla 776028](https://bugzilla.mozilla.org/show_bug.cgi?id=776028), [Ubuntu bug 1026869](https://bugs.launchpad.net/ubuntu/+source/firefox/+bug/1026869)

### Some MathML symbols are missing

You need some Math fonts, namely Latin Modern Math and STIX (see this MDN page: [[10]](https://developer.mozilla.org/en-US/docs/Mozilla/MathML_Project/Fonts#Linux)), to display MathML correctly.

In Arch Linux, these fonts are provided by [texlive-core](https://www.archlinux.org/packages/?name=texlive-core) **and** [texlive-fontsextra](https://www.archlinux.org/packages/?name=texlive-fontsextra), but they are not available to fontconfig by default. See [TeX Live#Fonts](/index.php/TeX_Live#Fonts "TeX Live") for details. You can also try other [Math fonts](/index.php/Fonts#Math "Fonts").

### Tearing video in fullscreen mode

If you are using the Xorg Intel or Nouveau drivers and experience tearing video in fullscreen mode, try [Firefox tweaks#Enable OpenGL Off-Main-Thread Compositing (OMTC)](/index.php/Firefox_tweaks#Enable_OpenGL_Off-Main-Thread_Compositing_.28OMTC.29 "Firefox tweaks").

### Firefox ESR 52 looks bad

Firefox 52 [does not support](https://bugzilla.mozilla.org/show_bug.cgi?id=1264079) GTK+ >=3.20 and may look unsightly as a result. A possible resolution is compiling Firefox against GTK2 instead, see [firefox-esr-gtk2](https://aur.archlinux.org/packages/firefox-esr-gtk2/).

### Firefox WebRTC module cannot detect a microphone

WebRTC applications for instance [Firefox WebRTC getUserMedia test page](https://mozilla.github.io/webrtc-landing/gum_test.html) say that microphone cannot be found. Issue is reproducible for both ALSA or Pulseaudio setup. Firefox debug logs show the following error:

 `$ NSPR_LOG_MODULES=MediaManager:5,GetUserMedia:5 firefox` 
```
...
[Unnamed thread 0x7fd7c0654340]: D/GetUserMedia  VoEHardware:GetRecordingDeviceName: Failed 1
```

You can try setting `media.navigator.audio.full_duplex` property to `false` at `about:config` Firefox page and restart Firefox.

This can also help if you are using the PulseAudio [module-echo-cancel](/index.php/PulseAudio/Troubleshooting#Enable_Echo.2FNoise-Cancellation "PulseAudio/Troubleshooting"), and Firefox does not recognise the virtual echo canceling source.

## See also

*   [Official website](https://www.mozilla.org/firefox/)
*   [Mozilla Foundation](https://www.mozilla.org/)
*   [MozillaWiki:Firefox](https://wiki.mozilla.org/Firefox "mozillawiki:Firefox")
*   [Firefox Add-ons](https://addons.mozilla.org/)
*   [Firefox themes](https://addons.mozilla.org/firefox/themes/)
*   [Wikipedia:Mozilla Firefox](https://en.wikipedia.org/wiki/Mozilla_Firefox "wikipedia:Mozilla Firefox")
*   [mozillaZine](http://forums.mozillazine.org/) unofficial forums