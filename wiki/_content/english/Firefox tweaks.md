This page contains advanced Firefox configuration options and performance tweaks.

## Contents

*   [1 Performance](#Performance)
    *   [1.1 Advanced Firefox options](#Advanced_Firefox_options)
        *   [1.1.1 Enable OpenGL Off-Main-Thread Compositing (OMTC)](#Enable_OpenGL_Off-Main-Thread_Compositing_.28OMTC.29)
        *   [1.1.2 Set AzureContentBackend to Skia instead of Cairo](#Set_AzureContentBackend_to_Skia_instead_of_Cairo)
        *   [1.1.3 Network settings](#Network_settings)
        *   [1.1.4 Stop urlclassifier3.sqlite from being created again](#Stop_urlclassifier3.sqlite_from_being_created_again)
        *   [1.1.5 Turn off OCSP validation](#Turn_off_OCSP_validation)
        *   [1.1.6 Turn off the disk cache](#Turn_off_the_disk_cache)
        *   [1.1.7 Longer interval to save session](#Longer_interval_to_save_session)
        *   [1.1.8 Immediate rendering of pages](#Immediate_rendering_of_pages)
    *   [1.2 Other modifications](#Other_modifications)
        *   [1.2.1 Enable firefox optional tracking protection](#Enable_firefox_optional_tracking_protection)
        *   [1.2.2 Referer header control](#Referer_header_control)
        *   [1.2.3 Defragment the profile's SQLite databases](#Defragment_the_profile.27s_SQLite_databases)
        *   [1.2.4 Cache the entire profile into RAM via tmpfs](#Cache_the_entire_profile_into_RAM_via_tmpfs)
        *   [1.2.5 Turn off sponsored content and tiles](#Turn_off_sponsored_content_and_tiles)
        *   [1.2.6 Enable Electrolysis](#Enable_Electrolysis)
*   [2 Appearance](#Appearance)
    *   [2.1 Fonts](#Fonts)
        *   [2.1.1 Configure the DPI value](#Configure_the_DPI_value)
        *   [2.1.2 Default font settings from Microsoft Windows](#Default_font_settings_from_Microsoft_Windows)
    *   [2.2 General user interface CSS settings](#General_user_interface_CSS_settings)
        *   [2.2.1 Change the font](#Change_the_font)
        *   [2.2.2 Hide button icons](#Hide_button_icons)
        *   [2.2.3 Hiding various tab buttons](#Hiding_various_tab_buttons)
        *   [2.2.4 Horizontal tabs](#Horizontal_tabs)
        *   [2.2.5 Hide window border and title bar](#Hide_window_border_and_title_bar)
        *   [2.2.6 Auto-hide Bookmarks Toolbar](#Auto-hide_Bookmarks_Toolbar)
        *   [2.2.7 Remove sidebar width restrictions](#Remove_sidebar_width_restrictions)
    *   [2.3 Web content CSS settings](#Web_content_CSS_settings)
        *   [2.3.1 Import other CSS files](#Import_other_CSS_files)
        *   [2.3.2 Block certain parts of a domain](#Block_certain_parts_of_a_domain)
        *   [2.3.3 Add [pdf] after links to PDF files](#Add_.5Bpdf.5D_after_links_to_PDF_files)
        *   [2.3.4 Firefox 4 New Menu Bar/Firefox Button](#Firefox_4_New_Menu_Bar.2FFirefox_Button)
        *   [2.3.5 Block ads](#Block_ads)
*   [3 Miscellaneous](#Miscellaneous)
    *   [3.1 Enable additional media codecs](#Enable_additional_media_codecs)
        *   [3.1.1 Widevine and Netflix/Amazon Video](#Widevine_and_Netflix.2FAmazon_Video)
    *   [3.2 Mouse wheel scroll speed](#Mouse_wheel_scroll_speed)
    *   [3.3 Change the order of search engines in the Firefox Search Bar](#Change_the_order_of_search_engines_in_the_Firefox_Search_Bar)
    *   [3.4 How to open a *.doc automatically with Abiword or LibreOffice Writer](#How_to_open_a_.2A.doc_automatically_with_Abiword_or_LibreOffice_Writer)
    *   [3.5 "I'm Feeling Lucky" mode](#.22I.27m_Feeling_Lucky.22_mode)
    *   [3.6 Secure DNS with DNSSEC validator](#Secure_DNS_with_DNSSEC_validator)
    *   [3.7 Adding magnet protocol association](#Adding_magnet_protocol_association)
    *   [3.8 Adding magnet protocol association for kTorrent (KDE4)](#Adding_magnet_protocol_association_for_kTorrent_.28KDE4.29)
    *   [3.9 Prevent accidental closing](#Prevent_accidental_closing)
    *   [3.10 Plugins do not work with latest version](#Plugins_do_not_work_with_latest_version)
    *   [3.11 Jerky or choppy scrolling](#Jerky_or_choppy_scrolling)
    *   [3.12 WebRTC exposes LAN IP address](#WebRTC_exposes_LAN_IP_address)
    *   [3.13 Run Firefox inside an nspawn container](#Run_Firefox_inside_an_nspawn_container)
    *   [3.14 Disable 1024-bit Diffie-Hellman primes](#Disable_1024-bit_Diffie-Hellman_primes)
    *   [3.15 Show search matches position in scroll bar](#Show_search_matches_position_in_scroll_bar)
*   [4 See also](#See_also)

## Performance

Improving Firefox's performance is divided into parameters that can be inputted while running Firefox or otherwise modifying its configuration as intended by the developers, and advanced procedures that involve foreign programs or scripts.

**Note:** Listed options may only be available for the latest version of Firefox.

### Advanced Firefox options

This section contains advanced Firefox options for performance tweaking. For additional information see [these Mozillazine forum posts](http://kb.mozillazine.org/Category:Tweaking_preferences).

#### Enable OpenGL Off-Main-Thread Compositing (OMTC)

**Warning:** If OpenGL OMTC is disabled for a specific hardware, it may be due to stability issues, high system resources consumption, driver bugs or a number of different variables. Proceed with force-enabling it at your own risk.

**Note:** Since Firefox version 40 basic software OMTC is enabled by default.

To enable OpenGL OMTC go to `about:config` and set:

*   `layers.acceleration.force-enabled true`

Restart Firefox for changes to take effect.

To check if OpenGL OMTC is enabled, go to `about:support` and under the "Graphics" section look for "Compositing". If it reports "Basic", OpenGL OMTC is disabled; if it reports "OpenGL" it is enabled.

If the above changes do not enable GPU acceleration, try setting the environment variable as follows: `export MOZ_USE_OMTC=1`. Then run Firefox [[1]](http://featherweightmusings.blogspot.se/2013/11/no-more-main-thread-opengl-in-firefox.html).

For more information on OMTC in Firefox read here: [https://wiki.mozilla.org/Platform/GFX/OffMainThreadCompositing](https://wiki.mozilla.org/Platform/GFX/OffMainThreadCompositing)

#### Set AzureContentBackend to Skia instead of Cairo

**Warning:** You may come across visual errors by enabling skia instead of cairo.

[Skia](https://skia.org/) is a 2D open-source graphics library to eventually supersede Cairo as the default Azure backend on Linux.

To set Skia as the default go to `about:config` and set:

*   `gfx.content.azure.backends skia,cairo`

Restart Firefox for changes to take effect.

To confirm the default Azure backend go to `about:support` and under the "Graphics" section look for "AzureContentBackend" and check if it reports "skia".

#### Network settings

Advanced network settings can be found on the `about:config` page (try searching for *network*).

<caption>Suggested values</caption>
| Key | Value | Description |
| network.http.pipelining | true | Enable [pipelining](http://www-archive.mozilla.org/projects/netlib/http/pipelining-faq.html) for normal connections |
| network.http.proxy.pipelining | true | Enable pipelining for proxy connections |

#### Stop urlclassifier3.sqlite from being created again

If you did remove all the `urlclassifier*` files as mentioned above, you may find out that `urlclassifier3.sqlite` keeps growing again after a certain time. Here is a simple solution to avoid it for now and ever.

```
$ cd ~/.mozilla/firefox/<profile_dir>
$ echo "" > urlclassifier3.sqlite
$ chmod 400 urlclassifier3.sqlite

```

This effectively makes the file empty and then read-only so Firefox cannot write to it anymore.

#### Turn off OCSP validation

OCSP validation may cause Firefox [to become slower](http://news.netcraft.com/archives/2013/04/16/certificate-revocation-and-the-performance-of-ocsp.html) for each (HTTPS) connection to a new server. This is worse, recently, where web gadgets are included in pages via HTTPS (e.g., "like" buttons of the social networks), resulting in many connections for a single URL.

*   Turn off the following option under Preferences -> Advanced -> Certificates -> *"Requests: Use the Online Certificate Status Protocol (OCSP) to confirm the current validity of certificates"*.

**Warning:** Disabling OCSP causes vulnerabilities to man-in-the-middle attacks. If you are using a potentially vulnerable connection such as Wi-Fi or VPN, it is strongly advised to leave OCSP on.

#### Turn off the disk cache

Every object loaded (html pages, jpeg images, css stylesheets, gif banners) is saved in the Firefox cache, to be loaded in the future without to download it again from the server, but only fraction of these objects will be really reused without download (usually the 30%). This because of too short expiration times for the objects, updates or simply the user behavior (to load new pages instead the ones already visited). The Firefox cache is divided in memory and disk cache and using the disk cache results to frequent disk writes, because every time an object loaded it is written to the disk and some older object is removed.

*   Turn on the following option under Preferences -> Advanced -> Network -> *"Cached Web Content: Override automatic cache management"* and specify zero in *"Limit cache to"*.

#### Longer interval to save session

The Firefox session store automatically saves the current status (opened urls, cookies, history and bookmarks) to the disk every 15 seconds. It may be too frequent for the user needs, resulting in a frequent disk access.

This setting can be found on the `about:config` page (try searching for *sessionstore*).

*   browser.sessionstore.interval 300000

If you want to disable this feature, then you will need to change the following setting from true to false.

*   browser.sessionstore.resume_from_crash false

#### Immediate rendering of pages

Mozilla applications render web pages incrementally - they display what has been received of a page before the entire page has been downloaded. Since the start of a web page normally does not have much useful information to display, Mozilla applications will wait a short interval before first rendering a page. This preference controls that interval. Note that if you are on slower connections (dial up) changing this setting might make web pages load for longer times even though the page appears faster.

This setting can be created in the `about:config` page as

*   nglayout.initialpaint.delay with a value of 0.

### Other modifications

This section contains some other modifications that may increase Firefox's performance.

#### Enable firefox optional tracking protection

Firefox gained an option for [tracking protection](https://support.mozilla.org/en-US/kb/tracking-protection-firefox). It can be enabled by setting `about:config`:

*   privacy.trackingprotection.enabled true

Apart from privacy benefits, enabling [tracking protection](http://venturebeat.com/2015/05/24/firefoxs-optional-tracking-protection-reduces-load-time-for-top-news-sites-by-44/) may also reduce load time by 44%.

#### Referer header control

Firefox as of version 28 has the ability to control how the HTTP Referer header is send. The options are hidden from the GUI configuration, but available through `about:config`. There are [four related keys](http://security.stackexchange.com/a/80194). The source post mentions recommended and default settings. A short description of the recommended setting is given in table, as well as the values to achieve a perfect score on [ip-check.info](https://ip-check.info).

<caption>Suggested values</caption>
| Key | Recommended | [ip-check.info](https://ip-check.info) | Default | Description |
| network.http.sendRefererHeader | 1 | 1 | 2 | Only for clicked links (0 disabled completely, 1 send referer on link click, 2 always send; incl. images) |
| network.http.referer.XOriginPolicy | 1 | 1 | 0 | Only if base domains match (0 always send, 2 only if host matches) |
| network.http.referer.spoofSource | true | false | false | Send target URI instead |
| network.http.referer.trimmingPolicy | 2 | 0 | 0 | scheme, host and port (0 full; 1 scheme, host port and path) |

#### Defragment the profile's SQLite databases

**Warning:** This procedure may damage the databases in such a way that sessions are not saved properly.

In Firefox 3.0, bookmarks, history, passwords are kept in an SQLite databases. SQLite databases become fragmented over time and empty spaces appear all around. But, since there are no managing processes checking and optimizing the database, these factors eventually result in a performance hit. A good way to improve start-up and some other bookmarks and history related tasks is to defragment and trim unused space from these databases.

[profile-cleaner](https://aur.archlinux.org/packages/profile-cleaner/) does just this.

<caption>Sample size differences comparison</caption>
| SQLite database | Size Before | Size After |  % change |
| urlclassifier3.sqlite | 37 M | 30 M | 19 % |
| places.sqlite | 16 M | 2.4 M | 85 % |

#### Cache the entire profile into RAM via tmpfs

If the system has memory to spare, `tmpfs` can be used to [cache the entire profile directory](/index.php/Firefox_on_RAM "Firefox on RAM"), which might result in increased Firefox responsiveness.

#### Turn off sponsored content and tiles

In `about:config`, set the string value to a blank for both of these: `browser.newtabpage.directory.source` and `browser.newtabpage.directory.ping`. Consider also disabling the tile feature from the tools on a new tab page. A [Wireshark](/index.php/Wireshark "Wireshark") session demonstrates the level of chatter created by these features.

#### Enable Electrolysis

In firefox 48 or later, Electrolysis (multi-process) may be enabled to improve performance and security by setting `browser.tabs.remote.autostart` to true in `about:config`.

## Appearance

### Fonts

See the main article: [Font configuration](/index.php/Font_configuration "Font configuration")

#### Configure the DPI value

Modifying the following value can help improve the way fonts looks in Firefox if the system's DPI is below 96\. Firefox, by default, uses 96 and only uses the system's DPI if it is a higher value. To force the system's DPI regardless of its value, type `about:config` into the address bar and set `layout.css.dpi` to **0**.

Note that the above method only affects the Firefox user interface's DPI settings. Web page contents still use a DPI value of 96, which may look ugly or, in the case of high-resolution displays, may be rendered too small to read. A solution is to change `layout.css.devPixelsPerPx` to system's DPI divided by 96\. For example, if your system's DPI is 144, then the value to add is 144/96 = 1.5\. Changing `layout.css.devPixelsPerPx` to **1.5** makes web page contents use a DPI of 144, which looks much better.

See also [HiDPI#Firefox](/index.php/HiDPI#Firefox "HiDPI") for information about HiDPI displays.

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

#### Change the font

The setting effectively overrides the global GTK+ font preferences, and does not affect webpages, only the user interface itself:

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

Install the [Hide Caption Titlebar Plus](https://addons.mozilla.org/firefox/addon/hide-caption-titlebar-plus-sma/) extension and set the following settings (leaving other settings to default):

| Option | Value |
| Show Custom Caption/TitleBar | Never |
| Activate custom borders and corner resizers | Deactivate |
| Enable Customizable Buttons (min,max,close) | Using a Glass-like window background |
| Custom Minimize, Max, Close Buttons | Auto. Current theme's skin (fixed position) |
| Drag Fx window using Tab-bar background | Enable |
| Alternative hide-titlebar feature | Use |

The extension [Classic Theme Restorer](https://addons.mozilla.org/firefox/addon/classicthemerestorer/) provides more tweaking options to get the best result (e.g. set tab height to 28px, enable/disable toolbars/buttons, etc.).

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

#### Firefox 4 New Menu Bar/Firefox Button

To toggle between the new Firefox button and the classic menu bar:

*   if the button is active, check *Preferences > Menu Bar*, or right click in the toolbar area and check *Menu Bar*.
*   if the menu bar is active, uncheck *View > Toolbars > Menu Bar*, or right click in the toolbar area and uncheck *Menu Bar*.

In GNU/Linux, you will just get a plain grey button instead of the new orange one from Windows. However you can change this to either a Firefox icon or the icon followed by the "Firefox" text.

Adding the following to your `~/.mozilla/firefox/userprofile/chrome/userChrome.css` file will place the icon before the text:

```
#appmenu-toolbar-button {
  list-style-image: url("chrome://branding/content/icon16.png");
}

```

Adding the following to the same file will *remove* the "Firefox" text:

```
#appmenu-toolbar-button > .toolbarbutton-text,
#appmenu-toolbar-button > .toolbarbutton-menu-dropmarker {
  display: none !important;
}

```

This userChrome.css configuration copies the default Windows Firefox 4+ look and adds an orange background to the button, with a purple background in Private Browsing mode:

```
#main-window:not([privatebrowsingmode]) #appmenu-toolbar-button {
    -moz-appearance: none !important;
    color: #FEEDFC !important;
    background: -moz-linear-gradient(hsl(34,85%,60%), hsl(26,72%,53%) 95%) !important;
    border: 1px solid #000000 !important;
}

#main-window:not([privatebrowsingmode]) #appmenu-toolbar-button:hover:not(:active):not([open]) {
    -moz-appearance: none !important;
    color: #FEEDFC !important;
    background: -moz-linear-gradient(hsl(26,72%,53%), hsl(34,85%,60%) 95%) !important;
    border: 1px solid #000000 !important;
}

#main-window:not([privatebrowsingmode]) #appmenu-toolbar-button:hover:active,
#main-window:not([privatebrowsingmode]) #appmenu-toolbar-button[open] {
    -moz-appearance: none !important;
    color: #FEEDFC !important;
    background: -moz-linear-gradient(hsl(26,72%,53%), hsl(26,72%,53%) 95%) !important;
    border: 1px solid #000000 !important;
}

#appmenu-toolbar-button {
    -moz-appearance: none !important;
    color: #FEEDFC !important;
    background: -moz-linear-gradient(hsl(279,70%,46%), hsl(276,75%,38%) 95%) !important;
    border: 1px solid #000000 !important;
}

#main-window #appmenu-toolbar-button:hover:not(:active):not([open]) {
    -moz-appearance: none !important;
    color: #FEEDFC !important;
    background: -moz-linear-gradient(hsl(276,75%,38%), hsl(279,70%,46%) 95%) !important;
    border: 1px solid #000000 !important;
}

#main-window #appmenu-toolbar-button:hover:active,
#main-window #appmenu-toolbar-button[open] {
    -moz-appearance: none !important;
    color: #FEEDFC !important;
    background: -moz-linear-gradient(hsl(276,75%,38%), hsl(276,75%,38%) 95%) !important;
    border: 1px solid #000000 !important;
}

```

**Note:** You need to create both the `chrome` directory and `userChrome.css`, if they do not already exist.

#### Block ads

See [floppymoose.com](http://www.floppymoose.com) for an example of how to use `userContent.css` as a basic ad-blocker.

## Miscellaneous

Other tips and tweaks.

### Enable additional media codecs

Before continuing, remember there is a reason some of these variables are not enabled by default, e.g. stability, memory leaks, etc. Go to `about:config` and check the following options:

<caption>Suggested values</caption>
| Key | Value | Description |
| media.mediasource.enabled | true (default) | Enable [Media Source Extensions](https://en.wikipedia.org/wiki/Media_Source_Extensions "wikipedia:Media Source Extensions") (MSE) |
| media.mediasource.mp4.enabled | true (default) | Enable [MP4](https://en.wikipedia.org/wiki/MPEG-4_Part_14 "wikipedia:MPEG-4 Part 14") MSE |
| media.mediasource.webm.enabled | true (default) | Enable [WebM](https://en.wikipedia.org/wiki/WebM "wikipedia:WebM") MSE. |
| media.mediasource.ignore_codecs | true | Enable H.264 MSE, amongst other things (This boolean key has to be created!) |

#### Widevine and Netflix/Amazon Video

Starting with version 49, Firefox can play Widevine videos, such as those on Netflix and Amazon Prime. Making this actually work properly, however, takes some extra work.

1.  **Allow Firefox to install DRM.** The first time you visit a widevine-enabled page, firefox will pop a prompt below the address bar asking for permission to install DRM. You have to approve this and then wait for the "Downloading" bar to disappear.
2.  **Forge a Chrome user agent.** Netflix uses your user agent string to decide which player to serve you, and if it detects Firefox it will try to use Silverlight. Use a user agent string from Chrome for linux, such as `Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/43.0.2357.93 Safari/537.36`. This can be configured using the [User Agent Switcher extension](https://addons.mozilla.org/firefox/addon/user-agent-switcher/) or with `general.useragent.override` in *about:config*
3.  **Run firefox with the sandboxes turned off.** Some part of the widevine cdm tries to violate [the seccomp sandbox](https://wiki.mozilla.org/Security/Sandbox/Seccomp), which will crash playback (see [bug 1303813](https://bugzilla.mozilla.org/show_bug.cgi?id=1303813)). Launch firefox with the media plugin sandbox disabled using an environment variable: `MOZ_DISABLE_GMP_SANDBOX=1 firefox`

### Mouse wheel scroll speed

To modify the default values (i.e. speed-up) of the mouse wheel scroll speed, go to `about:config` and search for `mousewheel.acceleration`. This will show the available options, modifying the following:

*   Set `mousewheel.acceleration.start` to **-1**.
*   Set `mousewheel.acceleration.factor` to the desired number (10 to 20 are common values).

Alternatively you can install the [SmoothWheel add-on](http://smoothwheel.mozdev.org/).

### Change the order of search engines in the Firefox Search Bar

To change the order search engines are displayed in:

*   Open the drop-down list of search engines and click *Manage Search Engines...* entry.
*   Highlight the engine you want to move and use *Move Up* or *Move Down* to move it. Alternatively, you can use drag-and-drop.

### How to open a *.doc automatically with Abiword or LibreOffice Writer

Go to *Preferences > Applications* and search for *Word Document* (or *Word 2007 Document* for `*.docx`). After finding it, click the drop-down list and select *Use other...*. From there you have to specify the exact path to the Abiword or Writer executable (i.e.`/usr/bin/abiword` or `/usr/bin/lowriter`).

### "I'm Feeling Lucky" mode

Some search engines have a "feeling lucky" feature. For example, Google has "I'm Feeling Lucky", and DuckDuckGo has "I'm Feeling Ducky".

To activate them:

1.  Type `about:config` in the address bar.
2.  Search for the string `keyword.url`.
3.  Modify its value (if any) to the URL of the search engine.

For Google, set it to:

 `https://www.google.com/search?btnI=I%27m+Feeling+Lucky&q=` 

For DuckDuckGo, set it to:

 `https://duckduckgo.com/?q=\` 

### Secure DNS with DNSSEC validator

You can enable [DNSSEC](/index.php/DNSSEC "DNSSEC") support for safer browsing.

### Adding magnet protocol association

In `about:config` set `network.protocol-handler.expose.magnet` to **false**.

The next time you open a magnet link, you will be prompted with a `Launch Application` dialogue. From there simply select your chosen torrent client. This technique can also be used with other protocols.

### Adding magnet protocol association for kTorrent (KDE4)

Create a user copy of `/usr/share/applications/kde4/ktorrent.desktop` to `~/.local/share/applications/kde4/`, and append to `Mimetype=`

```
x-scheme-handler/magnet

```

Modify `~/.config/mimeapps.list` and append:

```
x-scheme-handler/magnet=kde4-ktorrent.desktop

```

See [[2]](http://superuser.com/questions/44072/how-do-i-associate-magnet-links-with-ktorrent-in-firefox)

### Prevent accidental closing

The [Disable Ctrl-Q Shortcut](https://addons.mozilla.org/firefox/addon/disable-ctrl-q-shortcut/) extension can be installed to prevent unwanted closing of the browser.

An alternative is to add a rule in your window manager configuration file. For example in openbox add:

```
 <keybind key="C-q">
   <action name="Execute">
     <execute>false</execute>
   </action>
 </keybind>

```

in the *<keyboard>* section of your `rc.xml` file.

**Note:** This will be effective for every application used under a graphic server.

### Plugins do not work with latest version

Due to Arch's bleeding edge nature, there can be some compatibility issues with plugins not working with the latest Firefox install (e.g. [Pentadactyl](http://5digits.org/pentadactyl/index)). If possible, try installing the nightly/beta builds available, or see [Downgrading packages](/index.php/Downgrading_packages "Downgrading packages").

[Disable Add-on Compatibility Checks](https://addons.mozilla.org/firefox/addon/checkcompatibility/) plugin should take care of spurious compatibility issues when the plugins get disabled, even though they work just fine with the new version.

### Jerky or choppy scrolling

Scrolling in Firefox can feel "jerky" or "choppy". A post on [MozillaZine](http://forums.mozillazine.org/viewtopic.php?f=8&t=2749475/) gives settings that work on Gentoo, but reportedly work on Arch Linux as well:

1.  Set `mousewheel.min_line_scroll_amount` to 40
2.  Set `general.smoothScroll` and `general.smoothScroll.pages` to **false**
3.  Set `image.mem.min_discard_timeout_ms` to something really large such as 2100000000 but no more than 2140000000\. Above that number Firefox will not accept your entry and complain with the error code: "The text you entered is not a number."
4.  Set `image.mem.max_decoded_image_kb` to at least 512K

Now scrolling should flow smoothly.

### WebRTC exposes LAN IP address

To prevent websites from getting your local IP address via [WebRTC](https://en.wikipedia.org/wiki/WebRTC "wikipedia:WebRTC")'s peer-to-peer (and JavaScript), open `about:config` and set:

*   `media.peerconnection.ice.default_address_only` to **true** (Firefox < 51)
*   `media.peerconnection.ice.no_host` to **true** (Firefox >= 51)

or use this [addon](https://addons.mozilla.org/en-US/firefox/addon/disable-hello-pocket-reader/).

You can use this [WebRTC test page](http://net.ipcalf.com/) to confirm that your internal IP address is no longer leaked.

### Run Firefox inside an nspawn container

Note: on newer systems, you must enable local access to the user xserver with 'xhost local:root'

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

Once your container is booted, run the Xorg binary like so:

```
# systemd-run -M firefox --setenv=DISPLAY=:0 firefox

```

### Disable 1024-bit Diffie-Hellman primes

Following [recent research](https://freedom-to-tinker.com/blog/haldermanheninger/how-is-nsa-breaking-so-much-crypto/) it is likely that the NSA has been breaking 1024-bit Diffie-Hellman for some time now. To disable these switch the [following](https://www.eff.org/deeplinks/2015/10/how-to-protect-yourself-from-nsa-attacks-1024-bit-DH) settings to **false** in `about:config`:

```
  security.ssl3.dhe_rsa_aes_128_sha
  security.ssl3.dhe_rsa_aes_256_sha

```

Then consider checking your SSL configuration at [https://www.howsmyssl.com/](https://www.howsmyssl.com/).

### Show search matches position in scroll bar

This chrome feature can be achieved via [FindBar Tweak](https://addons.mozilla.org/firefox/addon/findbar-tweak/) extension.

## See also

*   [MozillaZine Wiki](http://kb.mozillazine.org/Knowledge_Base)
*   [about:config Entries Explained](http://kb.mozillazine.org/About:config_entries)
*   [Firefox touch-ups that might be desired](http://linuxtidbits.wordpress.com/2009/08/01/better-fox-cat-and-weasel/)