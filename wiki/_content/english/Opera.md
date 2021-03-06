Related articles

*   [Browser plugins](/index.php/Browser_plugins "Browser plugins")
*   [Chromium](/index.php/Chromium "Chromium")
*   [Otter Browser](/index.php/Otter_Browser "Otter Browser")
*   [Vivaldi](/index.php/Vivaldi "Vivaldi")

[Opera](http://www.opera.com) is a free of charge web browser developed since 1994 by the Norwegian company [Opera Software](https://en.wikipedia.org/wiki/Opera_Software "wikipedia:Opera Software"). It is known for being the first to bring new browsing features to the world that have become common on all web browsers, such as tabbed browsing and built-in search.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
    *   [1.1 Old Presto version](#Old_Presto_version)
*   [2 Plugins](#Plugins)
    *   [2.1 Adblock](#Adblock)
*   [3 Performance tweaks](#Performance_tweaks)
    *   [3.1 Disabling features and services](#Disabling_features_and_services)
    *   [3.2 Profile in tmpfs](#Profile_in_tmpfs)
*   [4 Appearance](#Appearance)
    *   [4.1 Themes](#Themes)
    *   [4.2 Title bar](#Title_bar)
    *   [4.3 Tab modes](#Tab_modes)
    *   [4.4 Fonts](#Fonts)
*   [5 Private tabs](#Private_tabs)
*   [6 Accessibility Tips](#Accessibility_Tips)
    *   [6.1 Disable text selection](#Disable_text_selection)
    *   [6.2 Grab and scroll mode](#Grab_and_scroll_mode)
    *   [6.3 Long pressing a link opens it in a background tab (extension)](#Long_pressing_a_link_opens_it_in_a_background_tab_(extension))
    *   [6.4 Virtual On-Screen keyboard (extension)](#Virtual_On-Screen_keyboard_(extension))
*   [7 Security](#Security)
    *   [7.1 Force a password store](#Force_a_password_store)
*   [8 Troubleshooting](#Troubleshooting)
    *   [8.1 Slow scrolling on NVIDIA cards](#Slow_scrolling_on_NVIDIA_cards)
    *   [8.2 Horizontal mouse wheel scrolling](#Horizontal_mouse_wheel_scrolling)
    *   [8.3 Launching an external browser](#Launching_an_external_browser)
    *   [8.4 Opera crashes when starting or closing with GTK 2.24.7+](#Opera_crashes_when_starting_or_closing_with_GTK_2.24.7+)
    *   [8.5 Unreadable input fields and address bar with dark GTK themes](#Unreadable_input_fields_and_address_bar_with_dark_GTK_themes)
*   [9 See Also](#See_Also)

## Installation

[Install](/index.php/Install "Install") the [opera](https://www.archlinux.org/packages/?name=opera) package.

### Old Presto version

The current Opera uses the modern and open-source Blink engine. You can still use the old proprietary Presto layout engine by installing Opera 12.16 with the [opera-legacy](https://aur.archlinux.org/packages/opera-legacy/) package.

Using Presto-based Opera isn't recommended because of security and compliance with modern web standards. Instead you can try [Vivaldi](/index.php/Vivaldi "Vivaldi") by former Opera team members or [Otter Browser](/index.php/Otter_Browser "Otter Browser") with really similar UI.

## Plugins

For details about different plugins and installation instructions see [Browser plugins](/index.php/Browser_plugins "Browser plugins"). Note that Opera no longer supports the Netscape plugin API (NPAPI), but only the newer Pepper plugin API (PPAPI).

### Adblock

**Tip:** Opera also has a built-in ad blocker which can be enabled in Settings.

Install Adblock support using the [opera-adblock-complete](https://aur.archlinux.org/packages/opera-adblock-complete/) package.

## Performance tweaks

Although Opera is fast on modern hardware, it can be made even faster.

### Disabling features and services

One of the keys to maximizing application performance is to disable undesired features and services through the native [opera:config Preferences Editor.](http://www.opera.com/browser/tutorials/personalize/behavior/)

Some commonly disabled features are:

*   **Systray Icon**: uncheck *Show Tray Icon* under opera:config#UserPrefs.
*   **BitTorrent**: uncheck *Enable* under opera:config#BitTorrent.
*   **Geolocation**: uncheck *Enable geolocation* under opera:config#Geolocation.
*   **Multimedia**: unckeck desired options under opera:config#Multimedia.
*   **Web Server**: uncheck *Enable* under opera:config#Web Server.

To more easily find these options just write the respective path (without spaces) in the address bar, for example `opera:config#UserPrefs|ShowTrayIcon` or use the built-in search.

### Profile in tmpfs

Relocate the browser profile to a [tmpfs](/index.php/Tmpfs "Tmpfs") filesystem, including `/tmp` for improvements in application response as the entire profile is now stored in RAM. Another benefit is a reduction in disk read and write operations, of which SSDs benefit the most.

There are currently two ways of doing this:

*   using [Profile-sync-daemon](/index.php/Profile-sync-daemon "Profile-sync-daemon"), that automatically detects and relocates the Opera profile to tmpfs.
*   using the `-pd` command-line flag to tell Opera where to store its profile data:

```
$ opera -pd /tmp/opera

```

## Appearance

### Themes

Although Opera is cross-platform, it can be made to integrate very well into various Linux desktop environments.

	Qt

	To make the menus look integrated with Qt, install your preferred Qt theme and apply it by using `qtconfig`.

	KDE

	To make Opera use [KDE](/index.php/KDE "KDE") icons, you can install a theme such as [this one](http://my.opera.com/community/customize/skins/info/?id=8141).

	GTK

	A nice GTK skin that uses the Tango icon theme can be found [here](http://my.opera.com/community/customize/skins/info/?id=3465).

### Title bar

The title bar can be hidden by right-clicking on the tab bar, then unchecking "Show Border".

### Tab modes

Opera has native support for tab cascading and tiling mode. Appropriate buttons can be found by activating the "Main" toolbar or by dragging and dropping the buttons anywhere desired, found in *Menu > Appearance > Buttons > Browser*.

### Fonts

Fonts can be configured under *Settings > Preferences... > Advanced > Fonts*.

If the [ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/) package has been installed before running Opera for the first time, Opera will use those fonts by default, regardless of what is specified by local GTK options, [GNOME](/index.php/GNOME "GNOME") or KDE font management. To force existing installations of Opera to use the options set by your system:

*   Close all running instances of Opera.
*   Un-install the [ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/) package.
*   Move the existing profile folder: `mv -i ~/.opera ~/.opera.bak`
*   Run an instance of Opera and verify that your font manager settings have been applied.
*   Restore bookmarks and desired filter files from `~/.opera.bak` to `~/.opera` except for the `operaprefs.ini` file.
*   Re-install the [ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/) package, if desired.

**Note:** If no text except numbers is showing on some of the webpages that might be a problem with the fonts. A known issue that causes this problem is the *helvetica* pfb postscript fonts.

## Private tabs

To browse without leaving obvious traces of the Web sites you visit, you can use a private tab. When you close a private tab, the following data related to the tab is deleted:

*   Cache
*   Cookies
*   History
*   Logins

This is similar to the [--incognito option](http://www.google.com/support/chrome/bin/answer.py?hl=en&answer=95464) in Chrome/[Chromium](/index.php/Chromium "Chromium") and [Private Browsing](https://wiki.mozilla.org/Private_Browsing "mozillawiki:Private Browsing") in [Firefox](/index.php/Firefox "Firefox").

To open a private tab from the command-line use:

```
$ opera -newprivatetab

```

To ensure only private tabs are used throughout the duration of the browsing session:

*   Set *Settings > Preferences... > General > Startup > Start without open tabs*.
*   Clear any entries in *Settings > Preferences... > General > Home page option*.
*   Enable *Settings > Preferences... > Advanced > Tabs > Additional tab options... > Allow windows with no tabs*.

To open a new window for private browsing when already running Opera you can just press `Ctrl+Shift+N` or look under *Menu > New Tabs and Windows > New Private Window*. All subsequent opened tabs with be private as well.

## Accessibility Tips

### Disable text selection

It is possible to disable text selection in Opera. However, text selection through JavaScript will still work (for example in forms, etc.). To get to the setting follow the link bellow:

```
opera:config#System|DisableTextSelect

```

### Grab and scroll mode

Besides setting text selection off, grab and scroll mode makes page scrolling possible with mouse dragging. It is very useful, especially when you have a touchscreen. Copy and paste the link bellow to get to the mentioned setting.

```
opera:config#UserPrefs|ScrollIsPan

```

It is also possible to change this setting on the fly by dragging and dropping the appropriate Opera button into a toolbar. The button can be found in *Menu > Appearance > Buttons > Browser View*.

### Long pressing a link opens it in a background tab (extension)

It is possible to open up any long-clicked link in a new background tab by installing [this](https://addons.opera.com/en/addons/extensions/details/open-in-background-with-long-press/) extension.

### Virtual On-Screen keyboard (extension)

There is an extension which allows the use of an on-screen virtual keyboard. Further details and installation link can be found [here](https://addons.opera.com/en/addons/extensions/details/virtual-keyboard/).

## Security

### Force a password store

Since current Opera uses the same engine as Chromium does, you can force Opera to use a specific password store by launching it with the `--password-store` flag. For more details see [Chromium/Tips and tricks#Force a password store](/index.php/Chromium/Tips_and_tricks#Force_a_password_store "Chromium/Tips and tricks").

## Troubleshooting

### Slow scrolling on NVIDIA cards

Try running the following command:

```
$ nvidia-settings -a InitialPixmapPlacement=2

```

On some computers, [http://helion.pl](http://helion.pl) works extremely slow without this hack, making it a perfect site for testing.

### Horizontal mouse wheel scrolling

Check *Settings > Preferences... > Advanced > Shortcuts > Mouse > Middle-Click Options... > Enable horizontal panning*.

or

*   Highlight *Settings > Preferences... > Advanced > Shortcuts > Mouse > Opera Standard*.
*   Duplicate *Settings > Preferences... > Advanced > Shortcuts > Mouse > Opera Standard*.
*   Edit... *Settings > Preferences... > Advanced > Shortcuts > Mouse > Copy of Opera Standard*.
*   Search the `Forward` and `Back` input contexts and edit the appropriate button shortcuts to `scroll left` and `scroll right`.
*   Rename *Settings > Preferences... > Advanced > Shortcuts > Mouse > Copy of Opera Standard* as desired.

### Launching an external browser

If Opera does not display a site well, a workaround is to launch the currently displayed page in an external browser.

**Note:** The following method appears to be deprecated in favor of the built-in `Open With` menu accessed via the right mouse button.

*   Set the following line under `[Site Navigation Toolbar.content]` in `$HOME/.opera/toolbar/standard_toolbar.ini`:

```
Button0, "Chromium"="Execute program, "chromium, "%u", , "Chromium""

```

*   If Firefox is desired, or preferred:

```
Button0, "Firefox"="Execute program, "firefox", "%u", , "Firefox""

```

*   Any number of command-line options may be included in the string:

```
Button0, "Chromium"="Execute program, "chromium --block-nonsandboxed-plugins --disable-java --incognito --safe-plugins --start-maximized --user-data-dir=/tmp/.chromium", "%u", , "Chromium""

```

### Opera crashes when starting or closing with GTK 2.24.7+

If this crash occurs, you can work around it by changing the *DialogToolkit* option to 4:

```
opera:config#FileSelector|DialogToolkit

```

This will disable GTK styling support and hence avoid the issue.

### Unreadable input fields and address bar with dark GTK themes

When using a dark GTK theme, one might encounter Opera address bar and Internet pages with unreadable input and text fields (e.g. Amazon can have black text on black text field background). This can happen because the site only sets either background or text color, and Opera takes the other one from the theme.

Using an installed clear theme and a command help to work around the problem: `env GTK_THEME=<light-theme-name> opera`

to turn it as default, use a prefered text editor and edit the file `/usr/bin/opera`. e.g. using Opera 12.14:

```
sudo gedit /usr/bin/opera
...
#!/bin/sh
export OPERA_DIR=${OPERA_DIR:-/usr/share/opera}
export OPERA_PERSONALDIR=${OPERA_PERSONALDIR:-$HOME/.opera}
exec /usr/lib/opera/opera "$@"

```

edit the file and follow the example changing to...

```
/usr/bin/opera
...
#!/bin/sh
export OPERA_DIR=${OPERA_DIR:-/usr/share/opera}
export OPERA_PERSONALDIR=${OPERA_PERSONALDIR:-$HOME/.opera}
env GTK_THEME=Clearlooks /usr/lib/opera/opera "$@"

```

this will make the browser use a clear theme that you set in the file `/usr/bin/opera` that was used in the above example the theme "Clearlooks" and the problems will be solved.

## See Also

*   [Opera Wiki](http://operawiki.info/Opera)
*   [Opera Knowledge Base](http://www.opera.com/support/kb/)
*   [Opera For UNIX Forums](http://my.opera.com/community/forums/forum.dml?id=3)
*   [Opera Bug Report](http://www.opera.com/support/bugs/)
*   [Opera Tips](http://www.opera.com/browser/tips/)
*   [Opera Documentation](http://www.opera.com/docs/)
*   [Opera Help](http://help.opera.com/Linux/12.10/en/)