From project [home page](http://lxde.org/):

	*The "Lightweight X11 Desktop Environment" is an extremely fast-performing and energy-saving desktop environment. Maintained by an international community of developers, it comes with a beautiful interface, multi-language support, standard keyboard short cuts and additional features like tabbed file browsing. LXDE uses less CPU and less RAM than other environments. It is especially designed for cloud computers with low hardware specifications, such as, netbooks, mobile devices (e.g. MIDs) or older computers.*

## Contents

*   [1 Installation](#Installation)
    *   [1.1 GTK+ 3 version](#GTK.2B_3_version)
*   [2 Starting the desktop](#Starting_the_desktop)
    *   [2.1 Graphical log-in](#Graphical_log-in)
    *   [2.2 Console](#Console)
*   [3 Tips and tricks](#Tips_and_tricks)
    *   [3.1 Application menu editing](#Application_menu_editing)
    *   [3.2 Autostart](#Autostart)
        *   [3.2.1 Desktop files](#Desktop_files)
        *   [3.2.2 Lxsession](#Lxsession)
    *   [3.3 Bindings](#Bindings)
    *   [3.4 Cursors](#Cursors)
    *   [3.5 Digital clock applet time](#Digital_clock_applet_time)
    *   [3.6 Font settings](#Font_settings)
    *   [3.7 Keyboard layout](#Keyboard_layout)
    *   [3.8 Screen locking](#Screen_locking)
    *   [3.9 LXPanel icons](#LXPanel_icons)
    *   [3.10 LXPanel menus](#LXPanel_menus)
    *   [3.11 Replace Openbox](#Replace_Openbox)
    *   [3.12 Shutdown, reboot, suspend and hibernate options (LXSession-logout)](#Shutdown.2C_reboot.2C_suspend_and_hibernate_options_.28LXSession-logout.29)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 NTFS with Chinese characters](#NTFS_with_Chinese_characters)
    *   [4.2 LXPanel crashes with some themes or browsing particular web pages](#LXPanel_crashes_with_some_themes_or_browsing_particular_web_pages)
    *   [4.3 LXPanel uses a smaller icon size for the Task Bar](#LXPanel_uses_a_smaller_icon_size_for_the_Task_Bar)
*   [5 See also](#See_also)

## Installation

LXDE requires at least [lxde-common](https://www.archlinux.org/packages/?name=lxde-common), [lxsession](https://www.archlinux.org/packages/?name=lxsession) and [openbox](https://www.archlinux.org/packages/?name=openbox) (or another window manager) to be [installed](/index.php/Install "Install"). The [lxde](https://www.archlinux.org/groups/x86_64/lxde/) group contains the full desktop.

### GTK+ 3 version

An experimental GTK+ 3 build of LXDE can be installed with the [lxde-gtk3](https://www.archlinux.org/groups/x86_64/lxde-gtk3/) group.

While it works mostly, there are some known issues with [gpicview](https://sourceforge.net/p/lxde/bugs/769/), [lxappearance-obconf](https://sourceforge.net/p/lxde/bugs/768/), [lxlauncher](https://sourceforge.net/p/lxde/bugs/803/) and [lxpanel](https://sourceforge.net/p/lxde/bugs/773/).

## Starting the desktop

### Graphical log-in

[LXDM](/index.php/LXDM "LXDM") is the default display manager for LXDE and is installed as part of the [lxde](https://www.archlinux.org/groups/x86_64/lxde/) group. See also [Display manager](/index.php/Display_manager "Display manager").

### Console

To use **startx**, you will need to define LXDE in [xinitrc](/index.php/Xinitrc "Xinitrc"):

 `~/.xinitrc`  `exec startlxde` 

See also [Start X at login](/index.php/Start_X_at_login "Start X at login").

## Tips and tricks

### Application menu editing

The application menu works by resolving the `.desktop` files located in `/usr/share/applications`. Many desktop environments run programs that supersede these settings to allow customization of the menu. LXDE has yet to create an application menu editor but you can manually build them yourself if you are so inclined. Third party menu editor can be found in [AUR](/index.php/AUR "AUR") - [lxmed](https://aur.archlinux.org/packages/lxmed/)

To add or edit a menu item, create or link to the `.desktop` file in `/usr/share/applications`, `/usr/local/share/applications`, or `~/.local/share/applications`. (The latter two have the advantage of putting your application outside of directories governed by `pacman`.) Consult [the desktop entry specification](http://standards.freedesktop.org/desktop-entry-spec/latest/) on freedesktop.org for structures of `.desktop` files.

To remove items from the menu, instead of deleting the `.desktop` files, you can edit the file and add the following line in the file:

```
NoDisplay=true

```

To expedite the process for a good number of files you can put it in a loop. For example:

```
$ cd /usr/share/applications
$ for i in program1.desktop program2.desktop ...; do cp /usr/share/applications/$i \
/home/user/.local/share/applications/; echo "NoDisplay=true" >> \
/home/user/.local/share/applications/$i; done

```

This will work for all applications except KDE applications. For these, the only way to remove them from the menu is to log into KDE itself and use its menu editor. For every item that you do not want displayed, check the 'Show only in KDE' option. If adding NoDisplay=True will not work, you can add ShowOnlyIn=XFCE.

### Autostart

Applications can be automatically started in several ways.

#### Desktop files

**Tip:** `.desktop` files can be manipulated with the [lxsession-edit](https://aur.archlinux.org/packages/lxsession-edit/) package.

See [Desktop entries#Autostart](/index.php/Desktop_entries#Autostart "Desktop entries").

#### Lxsession

Each line in `~/.config/lxsession/LXDE/autostart` represents a command to be executed. If a line starts with `@`, and the command following it crashes, the command is automatically re-executed. For example:

 `~/.config/lxsession/LXDE/autostart` 
```
@lxterminal
@leafpad

```

**Note:** Unlike Openbox, these commands do *not* end with a `&` symbol.

There is also a global autostart file at `/etc/xdg/lxsession/LXDE/autostart`.

**Note:** If both files are present, lxsession only executes the local file as of v0.4.9

### Bindings

Mouse and key bindings (i.e. keyboard shortcuts) are implemented with Openbox. LXDE users should follow the [Openbox wiki](http://openbox.org/wiki/Help:Bindings) to edit `~/.config/openbox/lxde-rc.xml`.

An optional GUI for editing the key bindings is provided by the [obkey](https://aur.archlinux.org/packages/obkey/) package. Whle it edits `rc.xml` by default, you can direct it to the LXDE configuration as follows:

```
$ obkey ~/.config/openbox/lxde-rc.xml

```

See [[1]](http://code.google.com/p/obkey/) for more information.

### Cursors

LXAppearance, provided by the [lxappearance](https://www.archlinux.org/packages/?name=lxappearance) package, is a graphical tool that can determine a number of aspects of the user interface including the cursor theme. Settings configured using LXAppearance are written to `~/.gtkrc-2.0`, `~/.config/gtk-3.0/settings.ini`, and `~/.icons/default/index.theme`. See also [Cursor themes](/index.php/Cursor_themes "Cursor themes").

### Digital clock applet time

You can right click on the digital clock applet on the panel and set how it displays the current time using the strftime format - see [man strftime](http://linux.die.net/man/3/strftime) for details.

### Font settings

See [Font configuration](/index.php/Font_configuration "Font configuration"). [lxappearance-obconf](https://www.archlinux.org/packages/?name=lxappearance-obconf) configures LXDE-specific settings.

### Keyboard layout

See [Keyboard configuration in Xorg](/index.php/Keyboard_configuration_in_Xorg "Keyboard configuration in Xorg") for generic instructions. A keyboard layout applet is included with *lxpanel*.

See [#Autostart](#Autostart) for a way to automatically start *setxkbmap* in LXDE.

### Screen locking

LXDE does not come with a screen locker of its own; see [List of applications/Security#Screen lockers](/index.php/List_of_applications/Security#Screen_lockers "List of applications/Security") for alternatives.

Shipped script `/usr/bin/lxlock`, called by default from the ScreenLock icon, searches for these applications in this order: [light-locker](https://www.archlinux.org/packages/?name=light-locker), [xscreensaver](https://www.archlinux.org/packages/?name=xscreensaver), [gnome-screensaver](https://www.archlinux.org/packages/?name=gnome-screensaver), [slock](https://www.archlinux.org/packages/?name=slock), [xlockmore](https://www.archlinux.org/packages/?name=xlockmore), [i3lock](https://www.archlinux.org/packages/?name=i3lock) and [xdg-utils](https://www.archlinux.org/packages/?name=xdg-utils).

`/etc/xdg/lxsession/LXDE/autostart` from [lxde-common](https://www.archlinux.org/packages/?name=lxde-common) lists [XScreenSaver](/index.php/XScreenSaver "XScreenSaver"), which will be launched automatically. See [#Autostart](#Autostart) when using a different locker. See [DPMS](/index.php/DPMS "DPMS") on how to control the screen saver without external programs.

### LXPanel icons

Default icons used by lxpanel are stored in `/usr/share/pixmaps` and any custom icons you want lxpanel to use need to be saved there as well.

You can change default icons for applications by taking the following steps:

1.  Save the new icon to /usr/share/pixmaps
2.  Use a text editor to open the `.desktop` file of the program whose icon you want to change in `/usr/share/applications`.
3.  Change

```
Icon=/default/icon/.png

```

to:

```
Icon=/name/of/new/icon/added/to/pixmaps/.png

```

### LXPanel menus

The panel's menus can be configured in `/etc/xdg/menus/lxde-applications.menu` as per the [xdg-menu](/index.php/Xdg-menu "Xdg-menu") format to work with applications from other sessions (notably [MATE](/index.php/MATE "MATE")) to add some of the function-ability that lxde lacks.

### Replace Openbox

*lxsession* uses the [window manager](/index.php/Window_manager "Window manager") defined in `~/.config/lxsession/LXDE/desktop.conf`. If this file does not exist, it searches in `/etc/xdg/lxsession/LXDE/desktop.conf` instead.

Replace `openbox-lxde` in either file with a window manager of choice:

```
[Session]
window_manager=openbox-lxde

```

For metacity:

```
window_manager=metacity

```

For compiz:

```
window_manager=compiz

```

Alternatively, you can autostart `wm --replace` using the method defined in [#Lxsession](#Lxsession) where *wm* is the name of the window manager executable being started. This method does mean that Openbox will be started first on each login and will then immediately be replaced by the autostarted window manager.

Note that since openbox dispatches the desktop-wide keyboard shortcuts in LXDE, users who want to replace it and still use these shortcuts will need to reimplement this functionality themselves. A good option is [xbindkeys](/index.php/Xbindkeys "Xbindkeys").

### Shutdown, reboot, suspend and hibernate options (LXSession-logout)

This requires installation of [upower](https://www.archlinux.org/packages/?name=upower).

## Troubleshooting

### NTFS with Chinese characters

For a storage device with an NTFS filesystem, you will need to install the [NTFS-3G](/index.php/NTFS-3G "NTFS-3G") package. Generally, PCManFM works well with NTFS filesystems, however there is one bug affecting NTFS users that if you have files or directories on an NTFS filesystem, the names of which contain non-latin characters (e.g. Chinese characters) may disappear when opening (or auto-mounting) the NTFS volume. This happens because the lxsession mount-helper is not correctly parsing the policies and locale options. There is a workaround for this:

Create a new `/usr/local/bin/mount.ntfs-3g` with a new Bash script containing:

```
#!/bin/bash
/usr/bin/ntfs-3g $1 $2 -o locale=en_US.UTF-8

```

And then make it executable:

```
# chmod +x /usr/local/bin/mount.ntfs-3g

```

### LXPanel crashes with some themes or browsing particular web pages

With some gtk themes, launching lxpanel will lead to the following error:

```
lxpanel: cairo-scaled-font.c:459: _cairo_scaled_glyph_page_destroy: Assertion `!scaled_font->cache_frozen' failed.

```

Try install [ttf-dejavu](https://www.archlinux.org/packages/?name=ttf-dejavu) in this case.

If lxpanel crashes when browsing particular unicode web pages, try install [ttf-droid](https://www.archlinux.org/packages/?name=ttf-droid).

### LXPanel uses a smaller icon size for the Task Bar

The icons of running applications do not match the set Icon size in Panel Settings > Geometry - they are 4px smaller which is making some of them blurry. To have clear looking 32px icons in the Task Bar the set Icon size has to be 36px which would blur the icons of the rest of your active Panel Applets. To get around this create additional panel(s) and have them collectively constitute a single continuous looking panel by adjusting the Alignment and Margin in Panel Settings > Geometry.

## See also

*   [Linux LXDE Guide](http://lxlinux.com/)
*   [LXDE (Sourceforge)](http://lxde.sourceforge.net)
*   [LXDE forum](http://forum.lxde.org)