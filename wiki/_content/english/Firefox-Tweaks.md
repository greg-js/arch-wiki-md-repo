Related articles

*   [Firefox](/index.php/Firefox "Firefox")
*   [Browser plugins](/index.php/Browser_plugins "Browser plugins")
*   [Firefox/Profile on RAM](/index.php/Firefox/Profile_on_RAM "Firefox/Profile on RAM")
*   [Firefox/Privacy](/index.php/Firefox/Privacy "Firefox/Privacy")

This page contains advanced Firefox configuration options and performance tweaks.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Performance](#Performance)
    *   [1.1 Change Performance settings](#Change_Performance_settings)
    *   [1.2 Enable OpenGL Off-Main-Thread Compositing (OMTC)](#Enable_OpenGL_Off-Main-Thread_Compositing_(OMTC))
    *   [1.3 Enable WebRender](#Enable_WebRender)
    *   [1.4 Enable Accelerated Azure Canvas](#Enable_Accelerated_Azure_Canvas)
    *   [1.5 Stop urlclassifier3.sqlite from being created again](#Stop_urlclassifier3.sqlite_from_being_created_again)
    *   [1.6 Turn off the disk cache](#Turn_off_the_disk_cache)
    *   [1.7 Longer interval between session information record](#Longer_interval_between_session_information_record)
    *   [1.8 Referrer header control](#Referrer_header_control)
    *   [1.9 Defragment the profile's SQLite databases](#Defragment_the_profile's_SQLite_databases)
    *   [1.10 Cache the entire profile into RAM via tmpfs](#Cache_the_entire_profile_into_RAM_via_tmpfs)
    *   [1.11 Disable Pocket](#Disable_Pocket)
*   [2 Appearance](#Appearance)
    *   [2.1 Fonts](#Fonts)
        *   [2.1.1 Configure the DPI value](#Configure_the_DPI_value)
        *   [2.1.2 Default font settings from Microsoft Windows](#Default_font_settings_from_Microsoft_Windows)
    *   [2.2 General user interface CSS settings](#General_user_interface_CSS_settings)
        *   [2.2.1 Change the interface font](#Change_the_interface_font)
        *   [2.2.2 Hide button icons](#Hide_button_icons)
        *   [2.2.3 Hiding various tab buttons](#Hiding_various_tab_buttons)
        *   [2.2.4 Horizontal tabs](#Horizontal_tabs)
        *   [2.2.5 Hide window border and title bar](#Hide_window_border_and_title_bar)
        *   [2.2.6 Auto-hide Bookmarks Toolbar](#Auto-hide_Bookmarks_Toolbar)
        *   [2.2.7 Remove sidebar width restrictions](#Remove_sidebar_width_restrictions)
        *   [2.2.8 Unreadable input fields with dark GTK themes](#Unreadable_input_fields_with_dark_GTK_themes)
            *   [2.2.8.1 Override input field color with CSS](#Override_input_field_color_with_CSS)
            *   [2.2.8.2 Change the GTK theme](#Change_the_GTK_theme)
            *   [2.2.8.3 Change the GTK theme for content process only](#Change_the_GTK_theme_for_content_process_only)
    *   [2.3 Tabs in title bar](#Tabs_in_title_bar)
    *   [2.4 Web content CSS settings](#Web_content_CSS_settings)
        *   [2.4.1 Import other CSS files](#Import_other_CSS_files)
        *   [2.4.2 Block certain parts of a domain](#Block_certain_parts_of_a_domain)
        *   [2.4.3 Add [pdf] after links to PDF files](#Add_[pdf]_after_links_to_PDF_files)
        *   [2.4.4 Block ads](#Block_ads)
*   [3 Mouse and keyboard](#Mouse_and_keyboard)
    *   [3.1 Mouse wheel scroll speed](#Mouse_wheel_scroll_speed)
    *   [3.2 Pixel-perfect trackpad scrolling](#Pixel-perfect_trackpad_scrolling)
    *   [3.3 Enable touchscreen gestures](#Enable_touchscreen_gestures)
    *   [3.4 Mouse click on URL bar's behavior](#Mouse_click_on_URL_bar's_behavior)
    *   [3.5 Set backspace's behavior](#Set_backspace's_behavior)
    *   [3.6 Disable middle mouse button clipboard paste](#Disable_middle_mouse_button_clipboard_paste)
    *   [3.7 Emacs key bindings](#Emacs_key_bindings)
*   [4 Miscellaneous](#Miscellaneous)
    *   [4.1 Enable additional media codecs](#Enable_additional_media_codecs)
        *   [4.1.1 Widevine and Netflix/Amazon Video](#Widevine_and_Netflix/Amazon_Video)
    *   [4.2 Remove full screen warning](#Remove_full_screen_warning)
    *   [4.3 Change the order of search engines in the Firefox Search Bar](#Change_the_order_of_search_engines_in_the_Firefox_Search_Bar)
    *   [4.4 "I'm Feeling Lucky" mode](#"I'm_Feeling_Lucky"_mode)
    *   [4.5 Secure DNS with DNSSEC validator](#Secure_DNS_with_DNSSEC_validator)
    *   [4.6 Adding magnet protocol association](#Adding_magnet_protocol_association)
    *   [4.7 Prevent accidental closing](#Prevent_accidental_closing)
    *   [4.8 Plugins do not work with latest version](#Plugins_do_not_work_with_latest_version)
    *   [4.9 Jerky or choppy scrolling](#Jerky_or_choppy_scrolling)
    *   [4.10 Run Firefox inside an nspawn container](#Run_Firefox_inside_an_nspawn_container)
    *   [4.11 Disable WebRTC audio post processing](#Disable_WebRTC_audio_post_processing)
    *   [4.12 Fido U2F authentication](#Fido_U2F_authentication)
    *   [4.13 Get ALSA working back](#Get_ALSA_working_back)
*   [5 See also](#See_also)

## Performance

Improving Firefox's performance is divided into parameters that can be inputted while running Firefox or otherwise modifying its configuration as intended by the developers, and advanced procedures that involve foreign programs or scripts.

**Note:** Listed options may only be available for the latest version of Firefox.

This section contains advanced Firefox options for performance tweaking. For additional information see [these MozillaZine articles](http://kb.mozillazine.org/Category:Tweaking_preferences).

### Change Performance settings

Firefox automatically uses settings based on the computer's hardware specifications [[1]](https://support.mozilla.org/en-US/kb/performance-settings).

Adjusting these settings can be done in Preferences or by changing the `dom.ipc.processCount` value to `1-8` and `browser.preferences.defaultPerformanceSettings.enabled` to `false` manually in `about:config`.

However you may want to manually adjust this setting to increase performance even further or decrease memory usage on low-end devices.

In this case the **Content process limit** for the current [user](/index.php/User "User") has been increased to *4*:

 `$ ps -e | grep 'Web Content'` 
```
13991 tty1     00:00:04 Web Content
14027 tty1     00:00:09 Web Content
14031 tty1     00:00:20 Web Content
14040 tty1     00:00:26 Web Content

```

### Enable OpenGL Off-Main-Thread Compositing (OMTC)

Basic software OMTC is enabled by default.

To check if OpenGL OMTC is enabled, go to `about:support` and under the "Graphics" section look for "Compositing". If it reports "Basic", OpenGL OMTC is disabled; if it reports "OpenGL" it is enabled.

If OpenGL OMTC is disabled, you can force-enable it by going to `about:config` and enabling `layers.acceleration.force-enabled`. Restart Firefox for changes to take effect.

**Note:** If OpenGL OMTC is disabled for a specific hardware, it may be due to stability issues, high system resources consumption, driver bugs or a number of different variables, and so instead of speeding things up it might slow them down. Proceed with force-enabling it at your own risk, benchmark if you aren’t sure.

For more information on OMTC in Firefox read [MozillaWiki:Platform/GFX/OffMainThreadCompositing](https://wiki.mozilla.org/Platform/GFX/OffMainThreadCompositing "mozillawiki:Platform/GFX/OffMainThreadCompositing").

### Enable WebRender

Enables WebRender compositor in Servo, instead of Gecko. It improves performance on supported hardware, fixes some black visual glitches when "OpenGL Off-Main-Thread" is enabled. Currently it has some known bugs. You can read more in [MozillaWiki:Platform/GFX/Quantum Render](https://wiki.mozilla.org/Platform/GFX/Quantum_Render "mozillawiki:Platform/GFX/Quantum Render").

Mozilla is slowly deploying WebRender to "qualified" Linux configurations. The qualification mostly depends on the GPU, the driver's version and the screen resolution.

One can force-enable it using one of the two methods below:

1.  by setting the `MOZ_WEBRENDER` [environment variable](/index.php/Environment_variable "Environment variable") to `1` before launching Firefox.
2.  by going to `about:config` and setting `gfx.webrender.all` to `true`. Restart Firefox for changes to take effect.

To check if WebRender is enabled go to `about:support` and under the "Graphics" section, in the "Decision Log" sub-section, look for "WEBRENDER". If it reports "available by user: Force enabled by pref", it means is enabled. Otherwise it will just report "opt-in by default: WebRender is an opt-in feature".

**Note:** If WebRender is disabled for a specific hardware, it may be due to stability issues, high system resources consumption, driver bugs or a number of different variables, and so instead of speeding things up it might slow them down. Proceed with force-enabling it at your own risk, benchmark if you are not sure.

### Enable Accelerated Azure Canvas

**Warning:** Accelerated Azure Canvas may cause invalid/corrupt rendering of images on unsupported devices and/or drivers, see [#Enable OpenGL Off-Main-Thread Compositing (OMTC)](#Enable_OpenGL_Off-Main-Thread_Compositing_(OMTC)).

Go to `about:config`, accept the warning, right click and create a new boolean value. Set the name as `gfx.canvas.azure.accelerated` and set it to `true`.

To verify restart Firefox then go to `about:support` and search for `AzureCanvasAccelerated` which should be set to *1*.

The acceleration efficiency can be tested by comparing the speed of a [javascript demo](http://js1k.com/2016-elemental/demo/2445) with and without the setting.

### Stop urlclassifier3.sqlite from being created again

Removing all `urlclassifier*` files can prevent the use of megabytes of storage in your firefox profile. If you remove all the `urlclassifier*` files, you may find out that `urlclassifier3.sqlite` keeps growing again after a certain time. Here is a simple solution to avoid it for now and ever.

```
$ cd ~/.mozilla/firefox/<profile_dir>
$ echo "" > urlclassifier3.sqlite
$ chmod 400 urlclassifier3.sqlite

```

This effectively makes the file empty and then read-only so Firefox cannot write to it anymore.

### Turn off the disk cache

Every object loaded (html page, jpeg image, css stylesheet, gif banner) is saved in the Firefox cache for future use without the need to download it again. It is estimated that only a fraction of these objects will be reused, usually about 30%. This is because of very short object expiration time, updates or simply user behavior (loading new pages instead of returning to the ones already visited). The Firefox cache is divided into memory and disk cache and the latter results in frequent disk writes: newly loaded objects are written to memory and older objects are removed.

The disk cache can be turned off by enabling *Preferences > Privacy & Security > Cached Web Content - Override automatic cache management* and setting to `0` *Limit cache to ... MB of space*.

An alternative approach is to use `about:config` settings:

*   Set `browser.cache.disk.enable` to `false`
*   Verify that `browser.cache.memory.enable` is set to `true`, more information about this option can be found in the [browser.cache.memory Mozilla article](http://kb.mozillazine.org/Browser.cache.memory.enable)
*   Add the entry (*right click > new > integer*) `browser.cache.memory.capacity` and set it to the amount of KB you want to spare, or to `-1` for [automatic](http://kb.mozillazine.org/Browser.cache.memory.capacity#-1) cache size selection (skipping this step has the same effect as setting the value to `-1`)
    *   The "automatic" size selection is based on a decade-old table that only contains settings for systems at or below 8GB of system memory. The following formula very closely approximates this table, and can be used to set the Firefox cache more dynamically: `41297 - (41606 / (1 + ((RAM / 1.16) ^ 0.75)))`, where `RAM` is in GB and the result is in KB.

This method has some drawbacks:

*   The content of currently browsed webpages is lost if the browser crashes or after a reboot, this can be avoided using [anything-sync-daemon](/index.php/Anything-sync-daemon "Anything-sync-daemon") or any similar periodically-syncing script so that cache gets copied over to the drive on a regular basis
*   The settings need to be configured for each user individually

### Longer interval between session information record

Firefox stores the current session status (opened urls, cookies, history and form data) to the disk on a regular basis. It is used to recover a previous session in case of crash. The default setting is to save the session every 15 seconds, resulting in frequent disk access.

To increase the save interval to 10 minutes (600000 milliseconds) for example, change in `about:config` the setting of `browser.sessionstore.interval` to `600000`

To disable completely this feature, change `browser.sessionstore.resume_from_crash` to `false`

### Referrer header control

The HTTP `Referer` header can be extensively configured via `about:config`. See [MozillaWiki:Security/Referrer](https://wiki.mozilla.org/Security/Referrer "mozillawiki:Security/Referrer") for the available preferences.

### Defragment the profile's SQLite databases

**Warning:** This procedure may damage the databases in such a way that sessions are not saved properly.

Firefox keeps bookmarks, history, passwords in SQLite databases. SQLite databases become fragmented over time and empty spaces appear all around. But, since there are no managing processes checking and optimizing the database, these factors eventually result in a performance hit. A good way to improve start-up and some other bookmarks and history related tasks is to defragment and trim unused space from these databases.

You can use [profile-cleaner](https://aur.archlinux.org/packages/profile-cleaner/) to do this, while Firefox is **not** running:

<caption>profile-cleaner usage example:</caption>
| SQLite database | Size Before | Size After | % change |
| urlclassifier3.sqlite | 37 M | 30 M | 19 % |
| places.sqlite | 16 M | 2.4 M | 85 % |

Firefox provides a tool to defragment and optimize the places database, which is the source of most slowdowns and profile corruptions. To access this tool, open the `about:support` page, search for `Places Database` and click the `Verify Integrity` button.

### Cache the entire profile into RAM via tmpfs

If the system has memory to spare, `tmpfs` can be used to [cache the entire profile directory](/index.php/Firefox/Profile_on_RAM "Firefox/Profile on RAM"), which might result in increased Firefox responsiveness.

### Disable Pocket

If you do not use the Pocket-service, you may want to disable it by setting `extensions.pocket.enabled` to *false* in `about:config`.

## Appearance

### Fonts

See the main article: [Font configuration](/index.php/Font_configuration "Font configuration")

#### Configure the DPI value

Modifying the following value can help improve the way fonts looks in Firefox if the system's DPI is below 96\. Firefox, by default, uses 96 and only uses the system's DPI if it is a higher value. To force the system's DPI regardless of its value, type `about:config` into the address bar and set `layout.css.dpi` to **0**.

Note that the above method only affects the Firefox user interface's DPI settings. Web page contents still use a DPI value of 96, which may look ugly or, in the case of high-resolution displays, may be rendered too small to read. A solution is to change `layout.css.devPixelsPerPx` to system's DPI divided by 96\. For example, if your system's DPI is 144, then the value to add is 144/96 = 1.5\. Changing `layout.css.devPixelsPerPx` to **1.5** makes web page contents use a DPI of 144, which looks much better.

See also [HiDPI#Firefox](/index.php/HiDPI#Firefox "HiDPI") for information about HiDPI displays and [[2]](https://www.sven.de/dpi/) for calculating the DPI.

#### Default font settings from Microsoft Windows

Below are the default font preferences when Firefox is installed in Microsoft Windows. Many web sites use the Microsoft fonts.

```
Proportional: Serif Size (pixels): 16
Serif: Times New Roman
Sans-serif: Arial
Monospace: Courier New Size (pixels): 13

```

### General user interface CSS settings

Firefox's user interface can be modified by editing the `userChrome.css` and `userContent.css` files in `~/.mozilla/firefox/<profile_dir>/chrome/` (*profile_dir* is of the form *hash.name*, where the *hash* is an 8 character, seemingly random string and the profile *name* is usually *default*).

**Note:** The `chrome/` folder and `userChrome.css`/`userContent.css` files may not necessarily exist, so they may need to be created.

This section only deals with the `userChrome.css` file which modifies Firefox's user interface, and not web pages.

#### Change the interface font

The setting effectively overrides the global GTK font preferences, and does not affect webpages, only the user interface itself:

 `~/.mozilla/firefox/<profile_dir>/chrome/userChrome.css` 
```
* {
    font-family: "FONT_NAME";
}

```

#### Hide button icons

Enables text-only buttons:

 `~/.mozilla/firefox/<profile_dir>/chrome/userChrome.css` 
```
.button-box .button-icon {
    display: none;
}

```

#### Hiding various tab buttons

These settings hide the arrows that appear to the horizontal edges of the tab bar, the button that toggles the "all tabs" drop-down list, and the plus sign button that creates a new tab.

 `~/.mozilla/firefox/<profile_dir>/chrome/userChrome.css` 
```
/* Tab bar */

.tabbrowser-strip *[class^="scrollbutton"] {
    /* Hide tab scroll buttons */
    display: none;
}

.tabbrowser-strip *[class^="tabs-alltabs"] {
    /* Hide tab drop-down list */
    display: none;
}

.tabbrowser-strip *[class^="tabs-newtab-button"] {
    /* Hide new-tab button */
    display: none;
}

```

#### Horizontal tabs

To place the tab bar horizontally stacked along the sides of the browser window:

 `~/.mozilla/firefox/<profile_dir>/chrome/userChrome.css` 
```
/* Display the tabbar on the left */
#content > tabbox {
    -moz-box-orient: horizontal;
}

.tabbrowser-strip {
    -moz-box-orient: vertical;
    /*
     * You can set this to -moz-scrollbars-vertical instead,
     * but then the scrollbar will *always* be visible.  this way
     * there is never a scrollbar, so it behaves like the tab bar
     * normally does
     */
     overflow: -moz-scrollbars-none;
}

.tabbrowser-tabs {
    -moz-box-orient: horizontal;
    min-width: 20ex;   /* You may want to increase this value */
    -mox-box-pack: start;
    -moz-box-align: start;
}

.tabbrowser-tabs > hbox {
    -moz-box-orient: vertical;
    -moz-box-align: stretch;
    -moz-box-pack: start;
}

.tabbrowser-tabs > hbox > tab {
    -moz-box-align: start;
    -moz-box-orient: horizontal;
}

```

#### Hide window border and title bar

Go to "Menu", then "Customize" and then at the bottom-left corner find checkbox named "Title Bar". Uncheck it. If the checkbox is missing, make sure the `XDG_CURRENT_DESKTOP` environment variable is correctly set and/or the `MOZ_GTK_TITLEBAR_DECORATION` environment variable is set to "client" or "system".

#### Auto-hide Bookmarks Toolbar

 `~/.mozilla/firefox/<profile_dir>/chrome/userChrome.css` 
```
#PersonalToolbar {
    visibility: collapse !important;
}

#navigator-toolbox:hover > #PersonalToolbar {
    visibility: visible !important;
}

```

#### Remove sidebar width restrictions

 `~/.mozilla/firefox/<profile_dir>/chrome/userChrome.css` 
```
/* remove maximum/minimum  width restriction of sidebar */
#sidebar {
    max-width: none !important;
    min-width: 0px !important;
}

```

#### Unreadable input fields with dark GTK themes

When using a dark [GTK](/index.php/GTK "GTK") theme, one might encounter Internet pages with unreadable input and text fields (e.g. text input field with white text on white background, or black text on dark background). This can happen because the site only sets either background or text color, and Firefox takes the other one from the theme. To prevent Firefox from using theme's colors in web pages confirm `browser.display.use_system_colors` is set to `false` in `about:config`.

Otherwise, if the previous modification didn't solve the issue, it is possible to launch Firefox with a light GTK theme by adding a new string in `about:config` named `widget.content.gtk-theme-override` and setting it to a light theme like `Breeze:light` or `Adwaita:light`.

##### Override input field color with CSS

**Note:** Related bug has been resolved starting with 68\. [[3]](https://bugzilla.mozilla.org/show_bug.cgi?id=1527048#c44)

The extension [Text Contrast for Dark Themes](https://addons.mozilla.org/firefox/addon/text-contrast-for-dark-themes/) sets the other color as needed to maintain contrast.

Alternatively set the standard colors explicitly for all web pages in `userContent.css` or using the [stylus add-on](https://addons.mozilla.org/firefox/addon/styl-us/). The style sheet is usually located in your profile folder (visit `about:profiles` for the path) in `chrome/userContent.css`, if not you can create it there.

The following sets input fields to standard black text / white background; both can be overridden by the displayed site, so that colors are seen as intended:

**Note:** If you want `urlbar` and `searchbar` to be `white` remove the two first `:not` css selectors.

```
input:not(.urlbar-input):not(.textbox-input):not(.form-control):not([type='checkbox']):not([type='radio']), textarea, select {
    -moz-appearance: none !important;
    background-color: white;
    color: black;
}

#downloads-indicator-counter {
    color: white;
}
```

##### Change the GTK theme

To force Firefox to use a light theme (e.g. Adwaita) for both web content and UI, see [GTK#Themes](/index.php/GTK#Themes "GTK").

##### Change the GTK theme for content process only

**Note:** Works with multiprocess enabled. [[4]](https://bugzilla.mozilla.org/show_bug.cgi?id=1158076#c145)

To force Firefox to use a light theme (e.g. Adwaita) for web content only:

1.  Open `about:config` in the address bar.
2.  Create a new `widget.content.gtk-theme-override` string type entry (`right mouse button` *> New > String*).
3.  Set the value to the light theme to use for rendering purposes (e.g. `Adwaita:light`).
4.  Restart Firefox.

### Tabs in title bar

To replace the title bar with the tab bar, enable `browser.tabs.drawInTitlebar` in `about:config`.

### Web content CSS settings

This section deals with the `userContent.css` file in which you can add custom CSS rules for web content. Changes to this file will take effect once the browser is restarted.

This file can be used for making small fixes or to apply personal styles to frequently visited websites. Custom stylesheets for popular websites are available from sources such as [userstyles.org](http://userstyles.org/). You can install an add-on such as [superUserContent](https://addons.mozilla.org/firefox/addon/superusercontent/) to manage themes. This add-on creates the directory `chrome/userContent.css.d` and applies changes to the CSS files therein when the page is refreshed.

#### Import other CSS files

 `~/.mozilla/firefox/<profile_dir>/chrome/userContent.css` 
```
@import url("./imports/some_file.css");

```

#### Block certain parts of a domain

 `~/.mozilla/firefox/<profile_dir>/chrome/userContent.css` 
```
@-moz-document domain(example.com) {
    div#header {
        background-image: none !important;
    } 
}

```

#### Add [pdf] after links to PDF files

 `~/.mozilla/firefox/<profile_dir>/chrome/userContent.css` 
```
/* add '[pdf]' next to links to PDF files */
a[href$=".pdf"]:after {
    font-size: smaller;
    content: " [pdf]";
}

```

#### Block ads

See [floppymoose.com](http://www.floppymoose.com) for an example of how to use `userContent.css` as a basic ad-blocker.

## Mouse and keyboard

### Mouse wheel scroll speed

To modify the default values (i.e. speed-up) of the mouse wheel scroll speed, go to `about:config` and search for `mousewheel.acceleration`. This will show the available options, modifying the following:

*   Set `mousewheel.acceleration.start` to `-1`.
*   Set `mousewheel.acceleration.factor` to the desired number (`10` to `20` are common values).

Mozilla's recommendation for increasing the mousewheel scroll speed is to:

*   Set `mousewheel.default.delta_multiplier_y` between `200` and `500` (default: `100`)

### Pixel-perfect trackpad scrolling

To enable one-to-one trackpad scrolling (as can be witnessed with GTK3 applications like Nautilus), set the `MOZ_USE_XINPUT2=1` [environment variable](/index.php/Environment_variable "Environment variable") before starting Firefox.

If scrolling is undesirably jerky, try enabling Firefox's "Use smooth scrolling" option in Preferences > General > Browsing.

### Enable touchscreen gestures

Make sure `dom.w3c_touch_events.enabled` is either set to 1 (*enabled*) or 2 (*default, auto-detect*).

Add `MOZ_USE_XINPUT2 DEFAULT=1` to `/etc/security/pam_env.conf` and then logout or reboot your system for the changes to take effect.

On some devices, it may be necessary to disable xinput's touchscreen gestures by running the following:

```
$ xsetwacom --set *device* Gesture off

```

### Mouse click on URL bar's behavior

To make the url bar behaves like in Windows regarding mouse clicks: a single click selects everything, a double click selects a single word until a punctuation sign and a triple click selects everything again, set the following in `about:config`:

```
browser.urlbar.clickSelectsAll; true
browser.urlbar.doubleClickSelectsAll; false
layout.word_select.stop_at_punctuation; true (default)

```

### Set backspace's behavior

See [Firefox#Backspace does not work as the 'Back' button](/index.php/Firefox#Backspace_does_not_work_as_the_'Back'_button "Firefox").

### Disable middle mouse button clipboard paste

See [Firefox#Middle-click behavior](/index.php/Firefox#Middle-click_behavior "Firefox").

### Emacs key bindings

To have Emacs/Readline-like key bindings active in text fields, see [GTK#Emacs key bindings](/index.php/GTK#Emacs_key_bindings "GTK").

## Miscellaneous

### Enable additional media codecs

Before continuing, remember there is a reason some of these variables are not enabled by default, e.g. stability, memory leaks, etc. Go to `about:config` and check the following options:

<caption>Suggested values</caption>
| Key | Value | Description |
| media.mediasource.enabled | true (default) | Enable [Media Source Extensions](https://en.wikipedia.org/wiki/Media_Source_Extensions "wikipedia:Media Source Extensions") (MSE) |
| media.mediasource.mp4.enabled | true (default) | Enable [MP4](https://en.wikipedia.org/wiki/MPEG-4_Part_14 "wikipedia:MPEG-4 Part 14") MSE |
| media.mediasource.webm.enabled | true (default) | Enable [WebM](https://en.wikipedia.org/wiki/WebM "wikipedia:WebM") MSE. |
| media.mediasource.ignore_codecs | true | Enable H.264 MSE, amongst other things (This boolean key has to be created!) |
| media.av1.enabled | true | Enable [AV1](https://en.wikipedia.org/wiki/AV1 "wikipedia:AV1") |

#### Widevine and Netflix/Amazon Video

Widevine is a digital rights management tool that Netflix, Amazon Prime Video, and others use to protect their video content.

The first time you visit a Widevine-enabled page Firefox will display a prompt below the address bar asking for permission to install DRM. Approve this and then wait for the "Downloading" bar to disappear, you are now able to watch videos from Netflix, Amazon Prime Video, or any other Widevine protected site.

**Note:** Please make sure to check the *Play DRM content* option under Content-Preference.

It is also required that the private mode browsing is disabled, for the window and in the preferences.

### Remove full screen warning

Warning about video displayed in full screen mode ("… is now fullscreen") can be disabled by setting `full-screen-api.warning.timeout` to `0` in `about:config`.

### Change the order of search engines in the Firefox Search Bar

To change the order search engines are displayed in:

*   Open the drop-down list of search engines and click *Manage Search Engines...* entry.
*   Highlight the engine you want to move and use *Move Up* or *Move Down* to move it. Alternatively, you can use drag-and-drop.

### "I'm Feeling Lucky" mode

Some search engines have a "feeling lucky" feature. For example, Google has "I'm Feeling Lucky", and DuckDuckGo has "I'm Feeling Ducky".

To activate them, search for `keyword.url` in `about:config` and modify its value (if any) to the URL of the search engine.

For Google, set it to:

 `https://www.google.com/search?btnI=I%27m+Feeling+Lucky&q=` 

For DuckDuckGo, set it to:

 `https://duckduckgo.com/?q=\` 

### Secure DNS with DNSSEC validator

You can enable [DNSSEC](/index.php/DNSSEC "DNSSEC") support for safer browsing.

### Adding magnet protocol association

In `about:config` set `network.protocol-handler.expose.magnet` to `false`. In case it does not exist, it needs to be created, right click on a free area and select *New > Boolean*, input `network.protocol-handler.expose.magnet` and set it to `false`.

The next time you open a magnet link, you will be prompted with a *Launch Application* dialogue. From there simply select your chosen [BitTorrent client](/index.php/List_of_applications/Internet#BitTorrent_clients "List of applications/Internet"). This technique can also be used with other protocols: `network.protocol-handler.expose.<protocol>`.

### Prevent accidental closing

There are different approaches to handle this:

Under `about:preferences#general` select `Warn you when quitting the browser`.

An alternative is to add a rule in your window manager configuration file. For example in [Openbox](/index.php/Openbox "Openbox") add:

```
 <keybind key="C-q">
   <action name="Execute">
     <execute>false</execute>
   </action>
 </keybind>

```

in the *<keyboard>* section of your `~/.config/openbox/rc.xml` file.

**Note:** This will be effective for every application used under a graphic server.

The [Disable Ctrl-Q and Cmd-Q](https://addons.mozilla.org/firefox/addon/disable-ctrl-q-and-cmd-q/) extension can be installed to prevent unwanted closing of the browser.

**Note:** This extension no longer works on Linux due to a [bug](https://bugzilla.mozilla.org/show_bug.cgi?id=1325692).

### Plugins do not work with latest version

There can be compatibility issues with plugins not working with the latest Firefox version (e.g. [Pentadactyl](http://5digits.org/pentadactyl/index)). If possible, try installing the nightly/beta builds available, or temporarily [downgrade](/index.php/Downgrade "Downgrade") Firefox.

[Disable Add-on Compatibility Checks](https://addons.mozilla.org/firefox/addon/checkcompatibility/) plugin should take care of spurious compatibility issues when the plugins get disabled, even though they work just fine with the new version.

### Jerky or choppy scrolling

Scrolling in Firefox can feel "jerky" or "choppy". A post on [MozillaZine](http://forums.mozillazine.org/viewtopic.php?f=8&t=2749475/) gives settings that work on Gentoo, but reportedly work on Arch Linux as well:

1.  Set `mousewheel.min_line_scroll_amount` to 40
2.  Set `general.smoothScroll` and `general.smoothScroll.pages` to **false**
3.  Set `image.mem.min_discard_timeout_ms` to something really large such as 2100000000 but no more than 2140000000\. Above that number Firefox will not accept your entry and complain with the error code: "The text you entered is not a number."
4.  Set `image.mem.max_decoded_image_kb` to at least 512K

Now scrolling should flow smoothly.

### Run Firefox inside an nspawn container

If you have problems accessing the X server from within the container, you might want to consider [Systemd-nspawn#Use an X environment](/index.php/Systemd-nspawn#Use_an_X_environment "Systemd-nspawn").

To run as PID 1

```
 # systemd-nspawn --setenv=DISPLAY=:0 \
              --setenv=XAUTHORITY=~/.Xauthority \
              --bind-ro=$HOME/.Xauthority:/root/.Xauthority \
              --bind=/tmp/.X11-unix \
              -D ~/containers/firefox \
              firefox

```

Else rather boot the container, with systemd ideally setting up your networking with [systemd-networkd](/index.php/Systemd-networkd "Systemd-networkd"):

```
# systemd-nspawn --bind-ro=$HOME/.Xauthority:/root/.Xauthority \
              --bind=/tmp/.X11-unix \
              -D ~/containers/firefox \
              --network-veth -b

```

**Note:** There is [a bug](https://github.com/systemd/systemd/issues/7093) in systemd version 235 that causes /tmp/.X11-unix to disappear from the filesystem when doing this. If you are having trouble, try binding /tmp/.X11-unix read-only instead: `--bind-ro=/tmp/.X11-unix`

Once your container is booted, run the Xorg binary like so:

```
# systemd-run -M firefox --setenv=DISPLAY=:0 firefox

```

### Disable WebRTC audio post processing

If you are using the PulseAudio [module-echo-cancel](/index.php/PulseAudio/Troubleshooting#Enable_Echo/Noise-Cancellation "PulseAudio/Troubleshooting"), you probably do not want Firefox to do additional audio post processing.

To disable audio post processing, change the value of the following preferences to `false`:

*   `media.getusermedia.aec_enabled` (Acoustic Echo Cancellation)
*   `media.getusermedia.agc_enabled` (Automatic Gain Control)
*   `media.getusermedia.noise_enabled` (Noise suppression)

### Fido U2F authentication

Install [libu2f-host](https://www.archlinux.org/packages/?name=libu2f-host) for the required udev rules to allow Firefox to communicate with the U2F key.

Firefox supports the Fido U2F authentication protocol.

**Note:** Firefox does not inplement the entire U2F protocol [[5]](https://www.yubico.com/2017/11/how-to-navigate-fido-u2f-in-firefox-quantum/). Some sites might not work correctly.

### Get ALSA working back

As long as Arch keeps building Firefox with *ac_add_options --enable-alsa*, then one can make Firefox allow ioctl syscalls, blocked by default by Firefox sandboxing, and required by ALSA setting `security.sandbox.content.syscall_whitelist` in `about:config`, to the right ioctl syscall number, which is *16* for x86-64 and *54* for x86-32\. See:

[[6]](https://www.linuxquestions.org/questions/slackware-14/firefox-in-current-alsa-sound-4175622116) [[7]](https://codelab.wordpress.com/2017/12/11/firefox-drops-alsa-apulse-to-the-rescue) [[8]](https://www.bleepingcomputer.com/news/security/firefox-57-brings-better-sandboxing-on-linux)

No need for apulse if built as done so far.

## See also

*   [MozillaZine Wiki](http://kb.mozillazine.org/Knowledge_Base)
*   [about:config entries MozillaZine article](http://kb.mozillazine.org/About:config_entries)
*   [Firefox touch-ups that might be desired](http://linuxtidbits.wordpress.com/2009/08/01/better-fox-cat-and-weasel/)