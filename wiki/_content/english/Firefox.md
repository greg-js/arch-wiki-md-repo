Related articles

*   [Browser plugins](/index.php/Browser_plugins "Browser plugins")
*   [Firefox/Tweaks](/index.php/Firefox/Tweaks "Firefox/Tweaks")
*   [Firefox/Profile on RAM](/index.php/Firefox/Profile_on_RAM "Firefox/Profile on RAM")
*   [Firefox/Privacy](/index.php/Firefox/Privacy "Firefox/Privacy")
*   [Chromium](/index.php/Chromium "Chromium")
*   [Opera](/index.php/Opera "Opera")

[Firefox](https://www.mozilla.org/firefox) is a popular open source graphical web browser from [Mozilla](https://www.mozilla.org).

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installing](#Installing)
*   [2 Add-ons](#Add-ons)
    *   [2.1 Adding search engines](#Adding_search_engines)
        *   [2.1.1 arch-firefox-search](#arch-firefox-search)
*   [3 Plugins](#Plugins)
*   [4 Configuration](#Configuration)
    *   [4.1 Multimedia playback](#Multimedia_playback)
        *   [4.1.1 Open With extension](#Open_With_extension)
    *   [4.2 Spell checking](#Spell_checking)
    *   [4.3 KDE/GNOME integration](#KDE/GNOME_integration)
    *   [4.4 Smooth Scrolling](#Smooth_Scrolling)
*   [5 Tips and tricks](#Tips_and_tricks)
    *   [5.1 Dark themes](#Dark_themes)
    *   [5.2 Screenshot of webpage](#Screenshot_of_webpage)
    *   [5.3 Window manager rules](#Window_manager_rules)
    *   [5.4 Touchscreen gestures and pixel-perfect trackpad scrolling](#Touchscreen_gestures_and_pixel-perfect_trackpad_scrolling)
*   [6 Troubleshooting](#Troubleshooting)
    *   [6.1 Firefox startup takes very long](#Firefox_startup_takes_very_long)
    *   [6.2 Font troubleshooting](#Font_troubleshooting)
    *   [6.3 Setting an email client](#Setting_an_email_client)
    *   [6.4 File association](#File_association)
    *   [6.5 Firefox keeps creating ~/Desktop even when this is not desired](#Firefox_keeps_creating_~/Desktop_even_when_this_is_not_desired)
    *   [6.6 Make plugins respect blocked pop-ups](#Make_plugins_respect_blocked_pop-ups)
    *   [6.7 Middle-click behavior](#Middle-click_behavior)
    *   [6.8 Backspace does not work as the 'Back' button](#Backspace_does_not_work_as_the_'Back'_button)
    *   [6.9 Firefox does not remember login information](#Firefox_does_not_remember_login_information)
    *   [6.10 "Do you want Firefox to save your tabs for the next time it starts?" dialog does not appear](#"Do_you_want_Firefox_to_save_your_tabs_for_the_next_time_it_starts?"_dialog_does_not_appear)
    *   [6.11 Silently fails when installing desktop apps from marketplace](#Silently_fails_when_installing_desktop_apps_from_marketplace)
    *   [6.12 Firefox detects the wrong version of my plugin](#Firefox_detects_the_wrong_version_of_my_plugin)
    *   [6.13 Javascript context menu does not appear on some sites](#Javascript_context_menu_does_not_appear_on_some_sites)
    *   [6.14 Firefox does not remember default spell check language](#Firefox_does_not_remember_default_spell_check_language)
    *   [6.15 Some MathML symbols are missing](#Some_MathML_symbols_are_missing)
    *   [6.16 Tearing video in fullscreen mode](#Tearing_video_in_fullscreen_mode)
    *   [6.17 Firefox WebRTC module cannot detect a microphone](#Firefox_WebRTC_module_cannot_detect_a_microphone)
*   [7 See also](#See_also)

## Installing

Firefox can be [installed](/index.php/Install "Install") with the [firefox](https://www.archlinux.org/packages/?name=firefox) package.

Other alternatives include:

*   **Firefox Developer Edition** — for developers

	[https://www.mozilla.org/firefox/developer/](https://www.mozilla.org/firefox/developer/) || [firefox-developer-edition](https://www.archlinux.org/packages/?name=firefox-developer-edition)

*   **Firefox Extended Support Release** — long-term supported version

	[https://www.mozilla.org/firefox/organizations/](https://www.mozilla.org/firefox/organizations/) || [firefox-esr](https://aur.archlinux.org/packages/firefox-esr/) or [firefox-esr-bin](https://aur.archlinux.org/packages/firefox-esr-bin/)

*   **Firefox Beta** — cutting-edge version

	[https://www.mozilla.org/firefox/channel/desktop/#beta](https://www.mozilla.org/firefox/channel/desktop/#beta) || [firefox-beta](https://aur.archlinux.org/packages/firefox-beta/) or [firefox-beta-bin](https://aur.archlinux.org/packages/firefox-beta-bin/)

*   **Firefox Nightly** — nightly builds for testing ([experimental features](https://developer.mozilla.org/Firefox/Experimental_features))

	[https://www.mozilla.org/firefox/channel/desktop/#nightly](https://www.mozilla.org/firefox/channel/desktop/#nightly) || [firefox-nightly](https://aur.archlinux.org/packages/firefox-nightly/)

*   **Firefox KDE** — Version of Firefox that incorporates an OpenSUSE patch for better [KDE integration](#KDE/GNOME_integration) than is possible through simple Firefox plugins.

	[https://build.opensuse.org/package/show/mozilla:Factory/MozillaFirefox](https://build.opensuse.org/package/show/mozilla:Factory/MozillaFirefox) || [firefox-kde-opensuse](https://aur.archlinux.org/packages/firefox-kde-opensuse/)

*   On top of the different Mozilla build channels, a number of forks exist with more or less special features; see [List of applications#Gecko-based](/index.php/List_of_applications#Gecko-based "List of applications").

A number of language packs are available for Firefox, other than the standard English. Language packs are usually named as `firefox-i18n-*languagecode*` (where `*languagecode*` can be any language code, such as **de**, **ja**, **fr**, etc.). For a list of available language packs see [firefox-i18n](https://www.archlinux.org/packages/extra/any/firefox-i18n/) for [firefox](https://www.archlinux.org/packages/?name=firefox) and [firefox-developer-edition-i18n](https://www.archlinux.org/packages/community/any/firefox-developer-edition-i18n/) for [firefox-developer-edition](https://www.archlinux.org/packages/?name=firefox-developer-edition).

## Add-ons

Firefox is well known for its large library of add-ons which can be used to add new features or modify the behavior of existing features. Firefox's "Add-ons Manager" is used to manage installed add-ons or find new ones.

For instructions on how to install add-ons and a list of add-ons, see [Browser extensions](/index.php/Browser_extensions "Browser extensions").

### Adding search engines

Search engines can be added to Firefox through normal add-ons, see [this page](https://addons.mozilla.org/firefox/search-tools/) for a list of available search engines.

A very extensive list of search engines can be found at the [Mycroft Project](https://mycroftproject.com/).

Also, you can use the [add-to-searchbar](https://firefox.maltekraus.de/extensions/add-to-search-bar) extension to add a search to your search bar from any web site, by simply right clicking on the site's search field and selecting *Add to Search Bar...*

#### arch-firefox-search

[Install](/index.php/Install "Install") the [arch-firefox-search](https://www.archlinux.org/packages/?name=arch-firefox-search) package to add Arch-specific searches (AUR, wiki, forum, etc, as specified by user) to the Firefox search toolbar.

## Plugins

**Note:** Firefox [has removed support](https://support.mozilla.org/en-US/kb/npapi-plugins) for [NPAPI](https://en.wikipedia.org/wiki/NPAPI "w:NPAPI") plugins, except for Flash.

See the main article: [Browser plugins](/index.php/Browser_plugins "Browser plugins")

To find out what plugins are installed/enabled, enter:

```
about:plugins

```

in the Firefox address bar or go to the *Add-ons* entry in the Firefox Menu and select the *Plugins* tab.

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

Firefox uses [PulseAudio](/index.php/PulseAudio "PulseAudio") for audio playback and capture. For sound to work, you need to install the [pulseaudio](https://www.archlinux.org/packages/?name=pulseaudio) package.

In case, for whatever reason, [PulseAudio](/index.php/PulseAudio "PulseAudio") is not an option for you, you can use [apulse](/index.php/Advanced_Linux_Sound_Architecture#PulseAudio_compatibility "Advanced Linux Sound Architecture") instead. To make this work, it is necessary to exclude `/dev/snd/` from Firefox' sandboxing by adding it to the comma-separated list in `about:config`:

```
security.sandbox.content.write_path_whitelist

```

**Note:** The trailing slash on `/dev/snd/` is important, otherwise *apulse* will report "Permission denied" errors.

If you have no audio even when using *apulse*, try adding `16` to `security.sandbox.content.syscall_whitelist` in `about:config`.

#### Open With extension

1.  Install [Open With](https://addons.mozilla.org/firefox/addon/open-with/) add-on.
2.  Go to *Add-ons > Open With > Preferences*.
3.  Proceed with instructions to install a file in your system and test the installation.
4.  Click *Add browser*.
5.  In the dialog write a name for this menu entry and command to start a video streaming capable player (e.g. [/usr/bin/mpv](/index.php/Mpv "Mpv")).
6.  (Optional step) Add needed arguments to the player (e.g. you may want `--force-window --ytdl` for *mpv*)
7.  Right click on links or visit pages containing videos. Select newly created entry from Open With's menu and if the site is supported, the player will open as expected.

The same procedure can be used to associate video downloaders such as *youtube-dl*.

### Spell checking

Install the [hunspell](https://www.archlinux.org/packages/?name=hunspell) package. You also need to install dictionaries for your language, such as [hunspell-fr](https://www.archlinux.org/packages/?name=hunspell-fr) (for the French language) or [hunspell-he](https://www.archlinux.org/packages/?name=hunspell-he) (for Hebrew).

To enable spell checking for a specific language right click on any text field and check the *Check Spelling* box. To select a language for spell checking to you have right click again and select your language from the *Languages* sub-menu.

To get more languages just click *Add Dictionaries...* and select the dictionary you want to install from the list. For Russian there is [firefox-spell-ru](https://www.archlinux.org/packages/?name=firefox-spell-ru).

When your default language choice does not stick, see [#Firefox does not remember default spell check language](#Firefox_does_not_remember_default_spell_check_language).

### KDE/GNOME integration

*   To bring the [KDE](/index.php/KDE "KDE") look to GTK apps (including Firefox), install [breeze-gtk](https://www.archlinux.org/packages/?name=breeze-gtk) and [kde-gtk-config](https://www.archlinux.org/packages/?name=kde-gtk-config). Afterwards, go to *System Settings > Application Style > GNOME/GTK Application Style*. Be sure to choose 'Breeze' in 'Select a GTK2/GTK3 Theme' and check 'Show icons in GTK buttons' and 'Show icons in GTK menus'.
*   To make the left mouse button warp the scrollbar instead of the middle one on KDE, go to *System Settings > Application Style > GNOME/GTK Application Style* and choose 'Jump to the mouse cursor position' in the 'On left-clicking the scroll bar' option.
*   To use the KDE file selection and print dialogs in Firefox 64 or newer:
    1.  Install [xdg-desktop-portal](https://www.archlinux.org/packages/?name=xdg-desktop-portal) and [xdg-desktop-portal-kde](https://www.archlinux.org/packages/?name=xdg-desktop-portal-kde),
    2.  Copy the Firefox [desktop entry](/index.php/Desktop_entry "Desktop entry") `/usr/share/applications/firefox.desktop` to `~/.local/share/applications/firefox.desktop`,
    3.  Edit `~/.local/share/applications/firefox.desktop` and add `GTK_USE_PORTAL=1` to all `Exec` lines before the actual command. E.g.: `Exec=GTK_USE_PORTAL=1 /usr/lib/firefox/firefox %u`.
*   For integration with [KDE](/index.php/KDE "KDE") mime type system and file dialog, one can use [firefox-kde-opensuse](https://aur.archlinux.org/packages/firefox-kde-opensuse/) variant from AUR with OpenSUSE’s patches applied.
*   Extensions/add-ons may provide additional integration, such as:
    *   Browser integration in [Plasma](/index.php/Plasma "Plasma"): requires [plasma-browser-integration](https://www.archlinux.org/packages/?name=plasma-browser-integration) and the [Plasma Integration add-on](https://addons.mozilla.org/firefox/addon/plasma-integration/).
    *   [mozilla-extension-gnome-keyring-git](https://aur.archlinux.org/packages/mozilla-extension-gnome-keyring-git/) (all-JavaScript implementation) to integrate Firefox with [GNOME Keyring](/index.php/GNOME_Keyring "GNOME Keyring"). To make firefox-gnome-keyring use your login keychain, set `extensions.gnome-keyring.keyringName` to `login` in `about:config`. Note the lowercase 'l' despite the the keychain name having an uppercase 'L' in Seahorse.

### Smooth Scrolling

In order to get smooth physics-based scrolling in Firefox, the `general.smoothScroll.msdPhysics` configurations can be changed to emulate a snappier behaviour like in other web browsers. For a quicker configuration, append the following to `~/.mozilla/firefox/**your-profile**/user.js` (requires restart):

```
user_pref("general.smoothScroll.lines.durationMaxMS", 125);
user_pref("general.smoothScroll.lines.durationMinMS", 125);
user_pref("general.smoothScroll.mouseWheel.durationMaxMS", 200);
user_pref("general.smoothScroll.mouseWheel.durationMinMS", 100);
user_pref("general.smoothScroll.msdPhysics.enabled", true);
user_pref("general.smoothScroll.other.durationMaxMS", 125);
user_pref("general.smoothScroll.other.durationMinMS", 125);
user_pref("general.smoothScroll.pages.durationMaxMS", 125);
user_pref("general.smoothScroll.pages.durationMinMS", 125);

```

Additionally the mouse wheel scroll settings have to be changed to react in a smooth way as well:

```
user_pref("mousewheel.min_line_scroll_amount", 30);
user_pref("mousewheel.system_scroll_override_on_root_content.enabled", true);
user_pref("mousewheel.system_scroll_override_on_root_content.horizontal.factor", 175);
user_pref("mousewheel.system_scroll_override_on_root_content.vertical.factor", 175);
user_pref("toolkit.scrollbox.horizontalScrollDistance", 6);
user_pref("toolkit.scrollbox.verticalScrollDistance", 2);

```

If you have troubles on machines with varying performance, try modifying the `mousewheel.min_line_scroll_amount` until it feels snappy enough.

## Tips and tricks

For general enhancements see [Firefox/Tweaks](/index.php/Firefox/Tweaks "Firefox/Tweaks"), for privacy related enhancements see [Firefox/Privacy](/index.php/Firefox/Privacy "Firefox/Privacy").

### Dark themes

If a dark [GTK](/index.php/GTK "GTK") theme is in use (e.g. Arc Dark), it is recommended to start Firefox with a brighter one (e.g. Adwaita). See [GTK#Themes](/index.php/GTK#Themes "GTK") and [Firefox/Tweaks#Unreadable input fields with dark GTK+ themes](/index.php/Firefox/Tweaks#Unreadable_input_fields_with_dark_GTK+_themes "Firefox/Tweaks") for more information.

### Screenshot of webpage

You can *Take a Screenshot* by either clicking the *Page actions* button (the three horizontal dots) in the address bar or by right-clicking on the webpage. See [[1]](https://support.mozilla.org/en-US/kb/firefox-screenshots) for more information.

**Note:**

*   The *Save* button misleadingly uploads your screenshot to a firefox.com subdomain. Set `extensions.screenshots.upload-disabled` to `true` to disable this behaviour. [[2]](https://github.com/mozilla-services/screenshots/issues/3503)
*   If [privacy.resistFingerprinting](/index.php/Firefox/Privacy#Anti-fingerprinting "Firefox/Privacy") is enabled, to take a screenshot of a website using the above method, you need to grant it *Extract Canvas Data* permission.

As an alternative you can use the full-page screenshot button in the *Developer Tools*, which you can open with `F12` (you might need to enable the button first).

### Window manager rules

To apply different configurations to Firefox windows, change the WM_CLASS string by using Firefox's `--class` option, to a custom one. [[3]](https://developer.mozilla.org/en-US/docs/Mozilla/Command_Line_Options#X11_options)

To start new Firefox instances, multiple profiles are required. To create a new profile:

```
$ firefox --ProfileManager

```

Class can be specified when launching Firefox with a not-in-use profile:

```
$ firefox -P *profile_name* --class=*class_name*

```

### Touchscreen gestures and pixel-perfect trackpad scrolling

To enable touch gestures (like scrolling and pinch-to-zoom) and one-to-one trackpad scrolling (as can be witnessed with GTK3 applications like Nautilus), set the `MOZ_USE_XINPUT2=1` [environment variable](/index.php/Environment_variable "Environment variable") before starting Firefox.

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

### Middle-click behavior

To use the middle mouse button to paste whatever text has been highlighted/added to the clipboard, as is common in UNIX-like operating systems, set either `middlemouse.contentLoadURL` or `middlemouse.paste` to `true` in `about:config`. Having `middlemouse.contentLoadURL` enabled was the default behaviour prior to Firefox 57.

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

The solution is to remove the file `pluginreg.dat` from your profile and that is it. Firefox will not complain about the missing file as it will be recreated the next time Firefox will be closed. [[4]](https://bugzilla.mozilla.org/show_bug.cgi?id=1109795#c16)

### Javascript context menu does not appear on some sites

In `about:config`, unset the `dom.w3c_touch_events.enabled` setting.

### Firefox does not remember default spell check language

The default spell checking language can be set as follows:

1.  Type `about:config` in the address bar.
2.  Set `spellchecker.dictionary` to your language of choice, for instance `en_GB`.
3.  Notice that the for dictionaries installed as a Firefox plugin the notation is `en-GB`, and for [hunspell](https://www.archlinux.org/packages/?name=hunspell) dictionaries the notation is `en_GB`.

When you only have system wide dictionaries installed with [hunspell](https://www.archlinux.org/packages/?name=hunspell), Firefox might not remember your default dictionary language settings. This can be fixed by having at least one [dictionary](https://addons.mozilla.org/firefox/language-tools/) installed as a Firefox plugin. Notice that now you will also have a tab **Dictionaries** in **add-ons**.

Related questions on the **StackExchange** platform: [[5]](https://stackoverflow.com/questions/26936792/change-firefox-spell-check-default-language/29446115), [[6]](https://stackoverflow.com/questions/21542515/change-default-language-on-firefox/29446353), [[7]](https://askubuntu.com/questions/184300/how-can-i-change-firefoxs-default-dictionary/576877)

Related bug reports: [Bugzilla 776028](https://bugzilla.mozilla.org/show_bug.cgi?id=776028), [Ubuntu bug 1026869](https://bugs.launchpad.net/ubuntu/+source/firefox/+bug/1026869)

### Some MathML symbols are missing

You need some Math fonts, namely Latin Modern Math and STIX (see this MDN page: [[8]](https://developer.mozilla.org/en-US/docs/Mozilla/MathML_Project/Fonts#Linux)), to display MathML correctly.

In Arch Linux, these fonts are provided by [texlive-core](https://www.archlinux.org/packages/?name=texlive-core) **and** [texlive-fontsextra](https://www.archlinux.org/packages/?name=texlive-fontsextra), but they are not available to fontconfig by default. See [TeX Live#Making fonts available to Fontconfig](/index.php/TeX_Live#Making_fonts_available_to_Fontconfig "TeX Live") for details. You can also try other [Math fonts](/index.php/Fonts#Math "Fonts").

### Tearing video in fullscreen mode

If you are using the Xorg Intel or Nouveau drivers and experience tearing video in fullscreen mode, try [Firefox tweaks#Enable OpenGL Off-Main-Thread Compositing (OMTC)](/index.php/Firefox_tweaks#Enable_OpenGL_Off-Main-Thread_Compositing_(OMTC) "Firefox tweaks").

### Firefox WebRTC module cannot detect a microphone

WebRTC applications for instance [Firefox WebRTC getUserMedia test page](https://mozilla.github.io/webrtc-landing/gum_test.html) say that microphone cannot be found. Issue is reproducible for both ALSA or Pulseaudio setup. Firefox debug logs show the following error:

 `$ NSPR_LOG_MODULES=MediaManager:5,GetUserMedia:5 firefox` 
```
...
[Unnamed thread 0x7fd7c0654340]: D/GetUserMedia  VoEHardware:GetRecordingDeviceName: Failed 1
```

You can try setting `media.navigator.audio.full_duplex` property to `false` at `about:config` Firefox page and restart Firefox.

This can also help if you are using the PulseAudio [module-echo-cancel](/index.php/PulseAudio/Troubleshooting#Enable_Echo/Noise-Cancellation "PulseAudio/Troubleshooting"), and Firefox does not recognise the virtual echo canceling source.

## See also

*   [Official website](https://www.mozilla.org/firefox/)
*   [Mozilla Foundation](https://www.mozilla.org/)
*   [MozillaWiki:Firefox](https://wiki.mozilla.org/Firefox "mozillawiki:Firefox")
*   [Firefox Add-ons](https://addons.mozilla.org/)
*   [Firefox themes](https://addons.mozilla.org/firefox/themes/)
*   [Wikipedia:Mozilla Firefox](https://en.wikipedia.org/wiki/Mozilla_Firefox "wikipedia:Mozilla Firefox")
*   [mozillaZine](http://forums.mozillazine.org/) unofficial forums