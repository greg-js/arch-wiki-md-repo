# Opera

[Opera](http://www.opera.com) is a free of charge web browser developed since 1994 by the Norwegian company [Opera Software](https://en.wikipedia.org/wiki/Opera_Software "wikipedia:Opera Software"). It is known for being the first to bring new browsing features to the world that have become common on all web browsers, such as tabbed browsing and built-in search.

Opera continues to innovate with its integrated mail client, one-click bookmarking, tab stacks (a way of organizing your tabs) and very good support for [HTML5](https://en.wikipedia.org/wiki/HTML5 "wikipedia:HTML5") features.

## Contents

*   [1 Installation](#Installation)
*   [2 Plugins](#Plugins)
    *   [2.1 Adobe Flash](#Adobe_Flash)
    *   [2.2 Adblock](#Adblock)
*   [3 Performance tweaks](#Performance_tweaks)
    *   [3.1 Disabling features and services](#Disabling_features_and_services)
        *   [3.1.1 Disable the e-mail client](#Disable_the_e-mail_client)
        *   [3.1.2 Disable ARGB, LIRC and mailto links](#Disable_ARGB.2C_LIRC_and_mailto_links)
    *   [3.2 Improving Flash performance](#Improving_Flash_performance)
        *   [3.2.1 .xinitrc example](#.xinitrc_example)
        *   [3.2.2 Command-line example](#Command-line_example)
    *   [3.3 Profile in tmpfs](#Profile_in_tmpfs)
*   [4 Appearance](#Appearance)
    *   [4.1 Themes](#Themes)
    *   [4.2 Title bar](#Title_bar)
    *   [4.3 Tab modes](#Tab_modes)
    *   [4.4 Fonts](#Fonts)
*   [5 Private tabs](#Private_tabs)
*   [6 Accessibility Tips](#Accessibility_Tips)
    *   [6.1 Disable text selection](#Disable_text_selection)
    *   [6.2 Grab and scroll mode](#Grab_and_scroll_mode)
    *   [6.3 Long pressing a link opens it in a background tab (extension)](#Long_pressing_a_link_opens_it_in_a_background_tab_.28extension.29)
    *   [6.4 Virtual On-Screen keyboard (extension)](#Virtual_On-Screen_keyboard_.28extension.29)
*   [7 Troubleshooting](#Troubleshooting)
    *   [7.1 Slow scrolling on NVIDIA cards](#Slow_scrolling_on_NVIDIA_cards)
    *   [7.2 Horizontal mouse wheel scrolling](#Horizontal_mouse_wheel_scrolling)
    *   [7.3 Launching an external browser](#Launching_an_external_browser)
    *   [7.4 Opera crashes when starting or closing with GTK+ 2.24.7+](#Opera_crashes_when_starting_or_closing_with_GTK.2B_2.24.7.2B)
    *   [7.5 Unreadable input fields and address bar with dark GTK+ themes](#Unreadable_input_fields_and_address_bar_with_dark_GTK.2B_themes)
*   [8 See Also](#See_Also)

## Installation

In early December 2014, Opera version 26 was released, but only for 64-bit systems: with this milestone, the old proprietary Presto layout engine is replaced with the more modern and open-source Blink engine. The previous 12.16 version is still supported for 32-bit systems.

[Installing](/index.php/Install "Install") the [opera](https://www.archlinux.org/packages/?name=opera) package will provide the new Blink version on x86_64 systems, and the old Presto version on i686 systems.

The 12.16 Presto version is also available from the [opera-legacy](https://aur.archlinux.org/packages/opera-legacy/)<sup><small>AUR</small></sup> package for both x86_64 and i686 architectures.

## Plugins

For details about different plugins and installation instructions see [Browser plugins](/index.php/Browser_plugins "Browser plugins"). In Opera, the plugin path can be specified under _Settings > Preferences... > Advanced > Content > Plug-in Options_.

### Adobe Flash

Opera no longer supports the Netscape plugin API (NPAPI), so [chromium-pepper-flash](https://aur.archlinux.org/packages/chromium-pepper-flash/)<sup><small>AUR</small></sup> should be used instead of [flashplugin](https://www.archlinux.org/packages/?name=flashplugin). Make sure the plugin is enabled in `opera://plugins`.

See [Browser plugins#Flash Player](/index.php/Browser_plugins#Flash_Player "Browser plugins") for details.

### Adblock

Install Adblock support using the [opera-adblock-complete](https://aur.archlinux.org/packages/opera-adblock-complete/)<sup><small>AUR</small></sup> package.

## Performance tweaks

Although Opera is quite fast on modern hardware, it can be tweaked even more. For further examples, see the [Opera wiki page](http://operawiki.info/operaperformance) on performance.

### Disabling features and services

One of the keys to maximizing application performance is to disable undesired features and services through the native [opera:config Preferences Editor.](http://www.opera.com/browser/tutorials/personalize/behavior/)

Some commonly disabled features are:

*   **Systray Icon**: uncheck _Show Tray Icon_ under opera:config#UserPrefs.
*   **BitTorrent**: uncheck _Enable_ under opera:config#BitTorrent.
*   **Geolocation**: uncheck _Enable geolocation_ under opera:config#Geolocation.
*   **Multimedia**: unckeck desired options under opera:config#Multimedia.
*   **Web Server**: uncheck _Enable_ under opera:config#Web Server.

To more easily find these options just write the respective path (without spaces) in the address bar, for example `opera:config#UserPrefs|ShowTrayIcon` or use the built-in search.

#### Disable the e-mail client

Additional command-line options are available for further control over browser features and services. To start Opera without the default internal e-mail client:

```
$ opera -nomail

```

Alternatively, if you want to permanently disable the internal e-mail client you can uncheck the _Show E-mail Client_ option under opera:config#UserPrefs.

#### Disable ARGB, LIRC and mailto links

To start Opera without [ARGB](https://en.wikipedia.org/wiki/ARGB "wikipedia:ARGB") (32-bit) visuals, [LIRC](http://www.lirc.org/) infrared control support and with `mailto:` links disabled:

```
$ opera -noargb -nolirc -nomaillinks 

```

### Improving Flash performance

To improve Flash performance you can set the following environment variables before starting Opera, or export the entries in [xinitrc](/index.php/Xinitrc "Xinitrc"), or [~/.bash_profile](/index.php/Bash "Bash"), or for system-wide changes, to `/etc/profile`:

```
 OPERAPLUGINWRAPPER_PRIORITY=0
 OPERA_KEEP_BLOCKED_PLUGIN=1

```

Another environment variable which may help resolve Flash issues:

```
GDK_NATIVE_WINDOWS=1

```

See the blog article [Flash problems on Linux?](http://my.opera.com/ruario/blog/flash-problems-on-linux) for additional details.

#### .xinitrc example

 `~/.xinitrc` 

```
...
export OPERAPLUGINWRAPPER_PRIORITY=0
export OPERA_KEEP_BLOCKED_PLUGIN=0
...

```

#### Command-line example

To use the variables from the command line call Opera as:

```
$ OPERAPLUGINWRAPPER_PRIORITY=0 OPERA_KEEP_BLOCKED_PLUGIN=1 opera &

```

### Profile in tmpfs

Relocate the browser profile to a [tmpfs](/index.php/Fstab#tmpfs "Fstab") filesystem, including `/tmp` for improvements in application response as the entire profile is now stored in RAM. Another benefit is a reduction in disk read and write operations, of which SSDs benefit the most.

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

	To make Opera use [KDE](/index.php/KDE "KDE") icons, you can install a theme such as [this one](http://my.opera.com/community/customize/skins/info/?id=8141)<sup>[[dead link](https://en.wikipedia.org/wiki/Wikipedia:Link_rot "wikipedia:Wikipedia:Link rot") 2014-04-05]</sup>.

	GTK+

	A nice GTK+ skin that uses the Tango icon theme can be found [here](http://my.opera.com/community/customize/skins/info/?id=3465)<sup>[[dead link](https://en.wikipedia.org/wiki/Wikipedia:Link_rot "wikipedia:Wikipedia:Link rot") 2014-04-05]</sup>.

### Title bar

The title bar can be hidden by right-clicking on the tab bar, then unchecking "Show Border".

### Tab modes

Opera has native support for tab cascading and tiling mode. Appropriate buttons can be found by activating the "Main" toolbar or by dragging and dropping the buttons anywhere desired, found in _Menu > Appearance > Buttons > Browser_.

### Fonts

Fonts can be configured under _Settings > Preferences... > Advanced > Fonts_.

If the [ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/)<sup><small>AUR</small></sup> package has been installed before running Opera for the first time, Opera will use those fonts by default, regardless of what is specified by local GTK+ options, [GNOME](/index.php/GNOME "GNOME") or KDE font management. To force existing installations of Opera to use the options set by your system:

*   Close all running instances of Opera.
*   Un-install the [ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/)<sup><small>AUR</small></sup> package.
*   Move the existing profile folder: `mv -i ~/.opera ~/.opera.bak`
*   Run an instance of Opera and verify that your font manager settings have been applied.
*   Restore bookmarks and desired filter files from `~/.opera.bak` to `~/.opera` except for the `operaprefs.ini` file.
*   Re-install the [ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/)<sup><small>AUR</small></sup> package, if desired.

**Note:** If no text except numbers is showing on some of the webpages that might be a problem with the fonts. A known issue that causes this problem is the _helvetica_ pfb postscript fonts.

## Private tabs

To browse without leaving obvious traces of the Web sites you visit, you can use a private tab. When you close a private tab, the following data related to the tab is deleted:

*   Cache
*   Cookies
*   History
*   Logins

This is similar to the [--incognito option](http://www.google.com/support/chrome/bin/answer.py?hl=en&answer=95464) in Chrome/[Chromium](/index.php/Chromium "Chromium") and [PrivateBrowsing](https://wiki.mozilla.org/PrivateBrowsing) in [Firefox](/index.php/Firefox "Firefox").

To open a private tab from the command-line use:

```
$ opera -newprivatetab

```

To ensure only private tabs are used throughout the duration of the browsing session:

*   Set _Settings > Preferences... > General > Startup > Start without open tabs_.
*   Clear any entries in _Settings > Preferences... > General > Home page option_.
*   Enable _Settings > Preferences... > Advanced > Tabs > Additional tab options... > Allow windows with no tabs_.

To open a new window for private browsing when already running Opera you can just press `Ctrl+Shift+N` or look under _Menu > New Tabs and Windows > New Private Window_. All subsequent opened tabs with be private as well.

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

It is also possible to change this setting on the fly by dragging and dropping the appropriate Opera button into a toolbar. The button can be found in _Menu > Appearance > Buttons > Browser View_.

### Long pressing a link opens it in a background tab (extension)

It is possible to open up any long-clicked link in a new background tab by installing [this](https://addons.opera.com/en/addons/extensions/details/open-in-background-with-long-press/) extension.

### Virtual On-Screen keyboard (extension)

There is an extension which allows the use of an on-screen virtual keyboard. Further details and installation link can be found [here](https://addons.opera.com/en/addons/extensions/details/virtual-keyboard/).

## Troubleshooting

### Slow scrolling on NVIDIA cards

Try running the following command:

```
$ nvidia-settings -a InitialPixmapPlacement=2

```

On some computers, [http://helion.pl](http://helion.pl) works extremely slow without this hack, making it a perfect site for testing.

### Horizontal mouse wheel scrolling

Check _Settings > Preferences... > Advanced > Shortcuts > Mouse > Middle-Click Options... > Enable horizontal panning_.

or

*   Highlight _Settings > Preferences... > Advanced > Shortcuts > Mouse > Opera Standard_.
*   Duplicate _Settings > Preferences... > Advanced > Shortcuts > Mouse > Opera Standard_.
*   Edit... _Settings > Preferences... > Advanced > Shortcuts > Mouse > Copy of Opera Standard_.
*   Search the `Forward` and `Back` input contexts and edit the appropriate button shortcuts to `scroll left` and `scroll right`.
*   Rename _Settings > Preferences... > Advanced > Shortcuts > Mouse > Copy of Opera Standard_ as desired.

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

### Opera crashes when starting or closing with GTK+ 2.24.7+

If this crash occurs, you can work around it by changing the _DialogToolkit_ option to 4:

```
opera:config#FileSelector|DialogToolkit

```

This will disable GTK+ styling support and hence avoid the issue.

### Unreadable input fields and address bar with dark GTK+ themes

When using a dark GTK theme, one might encounter Opera address bar and Internet pages with unreadable input and text fields (e.g. Amazon can have black text on black text field background). This can happen because the site only sets either background or text color, and Opera takes the other one from the theme.

Using an installed clear theme and a command help to work around the problem: `env GTK2_RC_FILES=/usr/share/themes/<light-theme-name/gtk-2.0/gtkrc opera`

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
env GTK2_RC_FILES=/usr/share/themes/Clearlooks/gtk-2.0/gtkrc /usr/lib/opera/opera "$@"

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

Retrieved from "[https://wiki.archlinux.org/index.php?title=Opera&oldid=404540](https://wiki.archlinux.org/index.php?title=Opera&oldid=404540)"