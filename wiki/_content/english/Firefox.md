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
        *   [4.2.1 System-wide Hunspell dictionaries](#System-wide_Hunspell_dictionaries)
        *   [4.2.2 Dictionaries as extensions](#Dictionaries_as_extensions)
    *   [4.3 KDE/GNOME integration](#KDE/GNOME_integration)
    *   [4.4 Smooth Scrolling](#Smooth_Scrolling)
*   [5 Tips and tricks](#Tips_and_tricks)
    *   [5.1 Dark themes](#Dark_themes)
    *   [5.2 Frame rate](#Frame_rate)
    *   [5.3 Memory limit](#Memory_limit)
    *   [5.4 New tabs position](#New_tabs_position)
    *   [5.5 Screenshot of webpage](#Screenshot_of_webpage)
    *   [5.6 Wayland](#Wayland)
    *   [5.7 Window manager rules](#Window_manager_rules)
        *   [5.7.1 Profiles](#Profiles)
    *   [5.8 Touchscreen gestures and pixel-perfect trackpad scrolling](#Touchscreen_gestures_and_pixel-perfect_trackpad_scrolling)
*   [6 Troubleshooting](#Troubleshooting)
    *   [6.1 All Firefox extensions disabled (May 2019)](#All_Firefox_extensions_disabled_(May_2019))
    *   [6.2 Extension X does not work on some Mozilla owned domains](#Extension_X_does_not_work_on_some_Mozilla_owned_domains)
    *   [6.3 Firefox startup takes very long](#Firefox_startup_takes_very_long)
    *   [6.4 Font troubleshooting](#Font_troubleshooting)
    *   [6.5 Setting an email client](#Setting_an_email_client)
    *   [6.6 File association](#File_association)
    *   [6.7 Firefox keeps creating ~/Desktop even when this is not desired](#Firefox_keeps_creating_~/Desktop_even_when_this_is_not_desired)
    *   [6.8 Make plugins respect blocked pop-ups](#Make_plugins_respect_blocked_pop-ups)
    *   [6.9 Changes to userChrome.css and userContent.css are ignored](#Changes_to_userChrome.css_and_userContent.css_are_ignored)
    *   [6.10 Middle-click behavior](#Middle-click_behavior)
    *   [6.11 Backspace does not work as the 'Back' button](#Backspace_does_not_work_as_the_'Back'_button)
    *   [6.12 Firefox does not remember login information](#Firefox_does_not_remember_login_information)
    *   [6.13 Cannot enter/leave fullscreen](#Cannot_enter/leave_fullscreen)
    *   [6.14 "Do you want Firefox to save your tabs for the next time it starts?" dialog does not appear](#"Do_you_want_Firefox_to_save_your_tabs_for_the_next_time_it_starts?"_dialog_does_not_appear)
    *   [6.15 Firefox detects the wrong version of my plugin](#Firefox_detects_the_wrong_version_of_my_plugin)
    *   [6.16 JavaScript context menu does not appear on some sites](#JavaScript_context_menu_does_not_appear_on_some_sites)
    *   [6.17 Firefox does not remember default spell check language](#Firefox_does_not_remember_default_spell_check_language)
    *   [6.18 Some MathML symbols are missing](#Some_MathML_symbols_are_missing)
    *   [6.19 Tearing video in fullscreen mode](#Tearing_video_in_fullscreen_mode)
    *   [6.20 Tearing when scrolling](#Tearing_when_scrolling)
    *   [6.21 Firefox WebRTC module cannot detect a microphone](#Firefox_WebRTC_module_cannot_detect_a_microphone)
    *   [6.22 Cannot login with my Chinese account](#Cannot_login_with_my_Chinese_account)
    *   [6.23 No audio on certain videos when using JACK and PulseAudio](#No_audio_on_certain_videos_when_using_JACK_and_PulseAudio)
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

A number of language packs are available for Firefox, other than the standard English. Language packs are usually named as `firefox-i18n-*languagecode*` (where `*languagecode*` can be any language code, such as **de**, **ja**, **fr**, etc.). For a list of available language packs see [firefox-i18n](https://www.archlinux.org/packages/extra/any/firefox-i18n/) for [firefox](https://www.archlinux.org/packages/?name=firefox),[firefox-developer-edition-i18n](https://www.archlinux.org/packages/community/any/firefox-developer-edition-i18n/) for [firefox-developer-edition](https://www.archlinux.org/packages/?name=firefox-developer-edition) and [firefox-nightly-](https://aur.archlinux.org/packages/?K=firefox-nightly-) for [firefox-nightly](https://aur.archlinux.org/packages/firefox-nightly/).

## Add-ons

Firefox is well known for its large library of add-ons which can be used to add new features or modify the behavior of existing features. Firefox's "Add-ons Manager" is used to manage installed add-ons or find new ones.

For instructions on how to install add-ons and a list of add-ons, see [Browser extensions](/index.php/Browser_extensions "Browser extensions").

### Adding search engines

Search engines can be added to Firefox through normal add-ons, see [this page](https://addons.mozilla.org/firefox/search-tools/) for a list of available search engines.

A very extensive list of search engines can be found at the [Mycroft Project](https://mycroftproject.com/).

Also, you can use the [add-to-searchbar](https://firefox.maltekraus.de/extensions/add-to-search-bar) extension to add a search to your search bar from any web site, by simply right clicking on the site's search field and selecting *Add to Search Bar...*

#### arch-firefox-search

[Install](/index.php/Install "Install") the [arch-firefox-search](https://aur.archlinux.org/packages/arch-firefox-search/) package to add Arch-specific searches (AUR, wiki, forum, etc, as specified by user) to the Firefox search toolbar.

## Plugins

The only plugin supported by Firefox is [Adobe Flash Player](/index.php/Browser_plugins#Adobe_Flash_Player "Browser plugins") (NPAPI version). Other plugins are [no longer supported](https://support.mozilla.org/en-US/kb/npapi-plugins).

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

Firefox uses [FFmpeg](/index.php/FFmpeg "FFmpeg") for playing multimedia inside HTML5 `<audio>` and `<video>` elements. Go to [video-test page](https://www.quirksmode.org/html5/tests/video.html) or [audio-test page](https://hpr.dogphilosophy.net/test/) to check which formats are actually supported.

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

Firefox can use system-wide installed [Hunspell](/index.php/Hunspell "Hunspell") dictionaries as well as dictionaries installed through its own extension system.

To enable spell checking for a specific language right click on any text field and check the *Check Spelling* box. To select a language for spell checking to you have right click again and select your language from the *Languages* sub-menu.

When your default language choice does not stick, see [#Firefox does not remember default spell check language](#Firefox_does_not_remember_default_spell_check_language).

#### System-wide Hunspell dictionaries

Install [Hunspell](/index.php/Hunspell "Hunspell") and its dictionaries for the languages you require.

#### Dictionaries as extensions

To get more languages right click on any text field and just click *Add Dictionaries...* and select the dictionary you want to install from the [Dictionaries and Language Packs list](https://addons.mozilla.org/firefox/language-tools/).

**Tip:** For Russian, the extension is packaged as [firefox-spell-ru](https://www.archlinux.org/packages/?name=firefox-spell-ru).

### KDE/GNOME integration

*   To bring the [KDE](/index.php/KDE "KDE") look to GTK apps (including Firefox), install [breeze-gtk](https://www.archlinux.org/packages/?name=breeze-gtk) and [kde-gtk-config](https://www.archlinux.org/packages/?name=kde-gtk-config). Afterwards, go to *System Settings > Application Style > GNOME/GTK Application Style*. Be sure to choose 'Breeze' in 'Select a GTK2/GTK3 Theme' and check 'Show icons in GTK buttons' and 'Show icons in GTK menus'.
*   To make the left mouse button warp the scrollbar instead of the middle one on KDE, go to *System Settings > Application Style > GNOME/GTK Application Style* and choose 'Jump to the mouse cursor position' in the 'On left-clicking the scroll bar' option.
*   To use the KDE file selection and print dialogs in Firefox 64 or newer:
    1.  Install [xdg-desktop-portal](https://www.archlinux.org/packages/?name=xdg-desktop-portal) and [xdg-desktop-portal-kde](https://www.archlinux.org/packages/?name=xdg-desktop-portal-kde),
    2.  Set `GTK_USE_PORTAL=1` as [environment variable](/index.php/Environment_variable "Environment variable") or [edit the .desktop file](/index.php/Desktop_entries#Modify_environment_variables "Desktop entries") and add `GTK_USE_PORTAL=1` to the `Exec` lines.
*   For integration with [KDE](/index.php/KDE "KDE") MIME type system and file dialog, one can use [firefox-kde-opensuse](https://aur.archlinux.org/packages/firefox-kde-opensuse/) variant from AUR with OpenSUSE’s patches applied. Alternatively, integration with MIME types can be achieved by creating a symbolic link to the MIME database `~/.config/mimeapps.list` from the deprecated `~/.local/share/applications/mimeapps.list` that is used by Firefox. See [XDG MIME Applications#mimeapps.list](/index.php/XDG_MIME_Applications#mimeapps.list "XDG MIME Applications").
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

If a dark [GTK](/index.php/GTK "GTK") theme is in use (e.g. Arc Dark), it is recommended to start Firefox with a brighter one (e.g. Adwaita). See [GTK#Themes](/index.php/GTK#Themes "GTK") and [Firefox/Tweaks#Unreadable input fields with dark GTK themes](/index.php/Firefox/Tweaks#Unreadable_input_fields_with_dark_GTK_themes "Firefox/Tweaks") for more information.

Alternatively, starting with Firefox 68 you can make the all Firefox interfaces and even other websites respect dark themes, irrespective of the system GTK theme and Firefox theme. To do this, set `browser.in-content.dark-mode` to `true` and `ui.systemUsesDarkTheme` to `1` in `about:config` [[1]](https://bugzilla.mozilla.org/show_bug.cgi?id=1488384#c23).

### Frame rate

If Firefox is unable to automatically detect the right value, it will default to 60 fps. To manually correct this, set `layout.frame_rate` to the refresh rate of your monitor (e.g. 144 for 144 Hz).

### Memory limit

To prevent pages from abusing memory (and possible [OOM](https://en.wikipedia.org/wiki/Out_of_memory "wikipedia:Out of memory")), we can use [Firejail](/index.php/Firejail "Firejail") with the `rlimit-as` option.

### New tabs position

To control where new tabs appears (relative or absolute), use `browser.tabs.insertAfterCurrent` and `browser.tabs.insertRelatedAfterCurrent`. See [[2]](https://support.mozilla.org/en/questions/1229062) for more informations.

### Screenshot of webpage

You can *Take a Screenshot* by either clicking the *Page actions* button (the three horizontal dots) in the address bar or by right-clicking on the webpage. See [[3]](https://support.mozilla.org/en-US/kb/firefox-screenshots) for more information.

As an alternative you can use the screenshot button in the [Developer Tools](https://developer.mozilla.org/en-US/docs/Tools/Taking_screenshots).

### Wayland

More recent versions of Firefox support opting into Wayland via an environment variable.

```
$ MOZ_ENABLE_WAYLAND=1 firefox

```

You may enter `about:support` in the URL bar to check the *Window Protocol*. It should say *wayland* instead of *x11*.

To make this permanent, see [Environment variables#Graphical environment](/index.php/Environment_variables#Graphical_environment "Environment variables") and start Firefox via the desktop launcher like you normally would. To verify it worked check the *Window Protocol* again.

### Window manager rules

To apply different configurations to Firefox windows, change the WM_CLASS string by using Firefox's `--class` option, to a custom one.

#### Profiles

To start new Firefox instances, multiple profiles are required. To create a new profile:

```
$ firefox [--new-instance] -P

```

Class can be specified when launching Firefox with a not-in-use profile:

```
$ firefox [--new-instance] -P *profile_name* --class=*class_name*

```

### Touchscreen gestures and pixel-perfect trackpad scrolling

To enable touch gestures (like scrolling and pinch-to-zoom) and one-to-one trackpad scrolling (as can be witnessed with GTK3 applications like Nautilus), set the `MOZ_USE_XINPUT2=1` [environment variable](/index.php/Environment_variable "Environment variable") before starting Firefox.

## Troubleshooting

### All Firefox extensions disabled (May 2019)

**Warning:** **Do not** delete and re-install your addons to try and fix the issue, as you will lose your addons' data.

Between 3–5 May 2019, all Firefox addons (web extensions, themes, search engines, and language packs) were mistakenly marked as **Legacy addons**, and could not be enabled. The [bug](https://bugzilla.mozilla.org/show_bug.cgi?id=1548973) was caused by an expired intermediate certificate.

For most users, the issue has been fixed in Firefox 66.0.4 and Firefox ESR 60.6.2\. The addons should be automatically re-enabled as soon as the patched version of Firefox is installed. Certain users, such as those who have set a Master Password, might require extra steps. Please see Firefox's [official support page](https://support.mozilla.org/en-US/kb/add-ons-disabled-or-fail-to-install-firefox) for more information.

### Extension X does not work on some Mozilla owned domains

By default extensions will not affect pages designated by `extensions.webextensions.restrictedDomains`. If this is not desired, this field can be cleared (special pages such as `about:*` will not be affected).

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

### Changes to userChrome.css and userContent.css are ignored

Set `toolkit.legacyUserProfileCustomizations.stylesheets` to `true` in `about:config`

### Middle-click behavior

To use the middle mouse button to paste whatever text has been highlighted/added to the clipboard, as is common in UNIX-like operating systems, set either `middlemouse.contentLoadURL` or `middlemouse.paste` to `true` in `about:config`. Having `middlemouse.contentLoadURL` enabled was the default behaviour prior to Firefox 57.

To scroll on middle-click (default for Windows browsers) set `general.autoScroll` to `true`.

### Backspace does not work as the 'Back' button

According to [MozillaZine](http://kb.mozillazine.org/Browser.backspace_action), the `Backspace` key was mapped based on which platform the browser was running on. As a compromise, this preference was created to allow the `Backspace` key to either go back/forward, scroll up/down a page, or do nothing.

To make `Backspace` go back one page in the tab's history and `Shift+Backspace` go forward, set `browser.backspace_action` to `0` in `about:config`.

To have the `Backspace` key scroll up one page and `Shift+Backspace` scroll down one page, set `browser.backspace_action` to `1`. Setting this property to any other value will leave the key unmapped (Arch Linux defaults to `2`, in other words, it is unmapped by default).

### Firefox does not remember login information

It may be due to a corrupted `cookies.sqlite` file in [Firefox's profile](https://support.mozilla.org/en-US/kb/profiles-where-firefox-stores-user-data) folder. In order to fix this, just rename or remove `cookie.sqlite` while Firefox is not running.

Open a terminal of choice and type the following:

```
$ rm -f ~/.mozilla/firefox/<profile id>.default/cookies.sqlite

```

The profile id is a random 8 character string.

Restart Firefox and see if it solved the problem.

### Cannot enter/leave fullscreen

If Firefox detects an [EWMH/ICCCM](https://specifications.freedesktop.org/wm-spec/wm-spec-latest.html) compliant window manager, it will try to send a WM_STATE message to the root window to request Firefox be made to enter (or leave) full-screen mode (as defined by the window manager). Window managers are allowed to ignore it, but if they do, Firefox will assume the request got denied and propagate it to the end user which results in nothing happening. This may result in not being able to full screen a video. A general workaround is to set the `full-screen-api.ignore-widgets` to `true` in `about:config`.

Related bug reports: [Bugzilla 1189622](https://bugzilla.mozilla.org/show_bug.cgi?id=1189622).

### "Do you want Firefox to save your tabs for the next time it starts?" dialog does not appear

From the [Mozilla support](https://support.mozilla.com/en-US/questions/767751) site:

1.  Type `about:config` in the address bar.
2.  Set `browser.warnOnQuit` to `true`.
3.  Set `browser.showQuitWarning` to `true`.

### Firefox detects the wrong version of my plugin

When you close Firefox, the latter saves the current timestamp and version of your plugins inside `pluginreg.dat` located in your profile folder, typically in `~/.mozilla/firefox/*xxxxxxxx*.default/`.

If you upgraded your plugin when Firefox was still running, you will thus have the wrong information inside that file. The next time you will restart Firefox you will get that message `Firefox has prevented the outdated plugin "XXXX" from running on ...` when you will be trying to open content dedicated to that plugin on the web. This problem often appears with the official [Adobe Flash Player plugin](/index.php/Browser_plugins#Adobe_Flash_Player "Browser plugins") which has been upgraded while Firefox was still running.

The solution is to remove the file `pluginreg.dat` from your profile and that is it. Firefox will not complain about the missing file as it will be recreated the next time Firefox will be closed. [[4]](https://bugzilla.mozilla.org/show_bug.cgi?id=1109795#c16)

### JavaScript context menu does not appear on some sites

You can try setting `dom.w3c_touch_events.enabled` to `0` in `about:config`.

### Firefox does not remember default spell check language

The default spell checking language can be set as follows:

1.  Type `about:config` in the address bar.
2.  Set `spellchecker.dictionary` to your language of choice, for instance `en_GB`.
3.  Notice that the for dictionaries installed as a Firefox plugin the notation is `en-GB`, and for [hunspell](https://www.archlinux.org/packages/?name=hunspell) dictionaries the notation is `en_GB`.

When you only have system wide dictionaries installed with [hunspell](https://www.archlinux.org/packages/?name=hunspell), Firefox might not remember your default dictionary language settings. This can be fixed by having at least one [dictionary](https://addons.mozilla.org/firefox/language-tools/) installed as a Firefox plugin. Notice that now you will also have a tab *Dictionaries* in *Add-ons*. You may have to change the order of *preferred language for displaying pages* in `about:preferences#general` to make the spell check default to the language of the addon dictionary.

Related questions on the **StackExchange** platform: [[5]](https://stackoverflow.com/questions/26936792/change-firefox-spell-check-default-language/29446115), [[6]](https://stackoverflow.com/questions/21542515/change-default-language-on-firefox/29446353), [[7]](https://askubuntu.com/questions/184300/how-can-i-change-firefoxs-default-dictionary/576877)

Related bug reports: [Bugzilla 776028](https://bugzilla.mozilla.org/show_bug.cgi?id=776028), [Ubuntu bug 1026869](https://bugs.launchpad.net/ubuntu/+source/firefox/+bug/1026869)

### Some MathML symbols are missing

You need some Math fonts, namely Latin Modern Math and STIX (see this MDN page: [[8]](https://developer.mozilla.org/en-US/docs/Mozilla/MathML_Project/Fonts#Linux)), to display MathML correctly.

In Arch Linux, these fonts are provided by [texlive-core](https://www.archlinux.org/packages/?name=texlive-core) **and** [texlive-fontsextra](https://www.archlinux.org/packages/?name=texlive-fontsextra), but they are not available to fontconfig by default. See [TeX Live#Making fonts available to Fontconfig](/index.php/TeX_Live#Making_fonts_available_to_Fontconfig "TeX Live") for details. You can also try other [Math fonts](/index.php/Fonts#Math "Fonts").

### Tearing video in fullscreen mode

If you are using the Xorg Intel or Nouveau drivers and experience tearing video in fullscreen mode, try [Firefox tweaks#Enable OpenGL Off-Main-Thread Compositing (OMTC)](/index.php/Firefox_tweaks#Enable_OpenGL_Off-Main-Thread_Compositing_(OMTC) "Firefox tweaks").

### Tearing when scrolling

Try disabling smooth scrolling in *Preferences > Browsing*.

### Firefox WebRTC module cannot detect a microphone

WebRTC applications for instance [Firefox WebRTC getUserMedia test page](https://mozilla.github.io/webrtc-landing/gum_test.html) say that microphone cannot be found. Issue is reproducible for both ALSA or PulseAudio setup. Firefox debug logs show the following error:

 `$ NSPR_LOG_MODULES=MediaManager:5,GetUserMedia:5 firefox` 
```
...
[Unnamed thread 0x7fd7c0654340]: D/GetUserMedia  VoEHardware:GetRecordingDeviceName: Failed 1
```

You can try setting `media.navigator.audio.full_duplex` property to `false` at `about:config` Firefox page and restart Firefox.

This can also help if you are using the PulseAudio [module-echo-cancel](/index.php/PulseAudio/Troubleshooting#Enable_Echo/Noise-Cancellation "PulseAudio/Troubleshooting") and Firefox does not recognise the virtual echo canceling source.

### Cannot login with my Chinese account

Firefox provides a local service for Chinese users, with a local account totally different from the international one. Firefox installed with the [firefox](https://www.archlinux.org/packages/?name=firefox) package uses the international account system by default, to change into the Chinese local service, you should install the add-on manager on [this page](http://mozilla.com.cn/thread-343905-1-1.html), then you can login with your Chinese account now.

### No audio on certain videos when using JACK and PulseAudio

If you are using JACK in combination with PulseAudio and cannot hear any sound on some videos it could be because those videos have mono audio. This happens if your JACK setup uses more than just stereo, but you use normal headphones. To fix this you simply have to connect the `front-center` port from the PulseAudio JACK Sink to both `playback_1` and `playback_2` ports of the system output.

You can also do this automatically using a script:

```
jack-mono.sh

```

```
#!/bin/sh
jack_connect "PulseAudio JACK Sink:front-center" "system:playback_1"
jack_connect "PulseAudio JACK Sink:front-center" "system:playback_2"
```

Keep in mind that the names for the sink and the ports might be different for you. You can check what your JACK setup looks like with a Patchbay like Catia from [cadence](https://www.archlinux.org/packages/?name=cadence).

## See also

*   [Official website](https://www.mozilla.org/firefox/)
*   [Mozilla Foundation](https://www.mozilla.org/)
*   [MozillaWiki:Firefox](https://wiki.mozilla.org/Firefox "mozillawiki:Firefox")
*   [Wikipedia:Mozilla Firefox](https://en.wikipedia.org/wiki/Mozilla_Firefox "wikipedia:Mozilla Firefox")
*   [Firefox Add-ons](https://addons.mozilla.org/)
*   [Firefox themes](https://addons.mozilla.org/firefox/themes/)
*   [Mozilla's FTP](https://ftp.mozilla.org/pub/firefox/releases/)
*   [mozillaZine](http://forums.mozillazine.org/) unofficial forums