Related articles

*   [Desktop environment](/index.php/Desktop_environment "Desktop environment")
*   [Display manager](/index.php/Display_manager "Display manager")
*   [Window manager](/index.php/Window_manager "Window manager")
*   [Openbox](/index.php/Openbox "Openbox")
*   [PCManFM](/index.php/PCManFM "PCManFM")
*   [LXDM](/index.php/LXDM "LXDM")
*   [LXQt](/index.php/LXQt "LXQt")
*   [File manager functionality#Mounting](/index.php/File_manager_functionality#Mounting "File manager functionality")

From project [home page](http://lxde.org/):

	The "Lightweight X11 Desktop Environment" is an extremely fast-performing and energy-saving desktop environment. Maintained by an international community of developers, it comes with a beautiful interface, multi-language support, standard keyboard short cuts and additional features like tabbed file browsing. LXDE uses less CPU and less RAM than other environments. It is especially designed for cloud computers with low hardware specifications, such as, netbooks, mobile devices (e.g. MIDs) or older computers.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
    *   [1.1 GTK 3 version](#GTK_3_version)
*   [2 Starting the desktop](#Starting_the_desktop)
    *   [2.1 Graphical log-in](#Graphical_log-in)
    *   [2.2 Console](#Console)
*   [3 Tips and tricks](#Tips_and_tricks)
    *   [3.1 Application menu editing](#Application_menu_editing)
    *   [3.2 Autostart](#Autostart)
    *   [3.3 Bindings](#Bindings)
    *   [3.4 Cursors](#Cursors)
    *   [3.5 Digital clock applet time](#Digital_clock_applet_time)
    *   [3.6 Font settings](#Font_settings)
    *   [3.7 Keyboard layout](#Keyboard_layout)
    *   [3.8 Screen locking](#Screen_locking)
    *   [3.9 LXPanel icons](#LXPanel_icons)
    *   [3.10 LXPanel menus](#LXPanel_menus)
    *   [3.11 Use a different window manager](#Use_a_different_window_manager)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 NTFS with Chinese characters](#NTFS_with_Chinese_characters)
    *   [4.2 LXPanel crashes](#LXPanel_crashes)
    *   [4.3 LXPanel Task Bar icon size](#LXPanel_Task_Bar_icon_size)
    *   [4.4 Fake transparency in LXTerminal](#Fake_transparency_in_LXTerminal)
*   [5 See also](#See_also)

## Installation

LXDE requires at least [lxde-common](https://www.archlinux.org/packages/?name=lxde-common), [lxsession](https://www.archlinux.org/packages/?name=lxsession) and [openbox](https://www.archlinux.org/packages/?name=openbox) (or another window manager) to be [installed](/index.php/Install "Install"). The [lxde](https://www.archlinux.org/groups/x86_64/lxde/) group contains the full desktop.

### GTK 3 version

An experimental GTK 3 build of LXDE can be installed with the [lxde-gtk3](https://www.archlinux.org/groups/x86_64/lxde-gtk3/) group.

While it works mostly, there are some known issues with [gpicview](https://sourceforge.net/p/lxde/bugs/769/), [lxappearance-obconf](https://sourceforge.net/p/lxde/bugs/768/), [lxlauncher](https://sourceforge.net/p/lxde/bugs/803/) and [lxpanel](https://sourceforge.net/p/lxde/bugs/773/).

## Starting the desktop

### Graphical log-in

[LXDM](/index.php/LXDM "LXDM") is the default display manager for LXDE and is installed as part of the [lxde](https://www.archlinux.org/groups/x86_64/lxde/) group. See also [Display manager](/index.php/Display_manager "Display manager").

### Console

To use *startx*, add to [xinitrc](/index.php/Xinitrc "Xinitrc"):

 `~/.xinitrc`  `exec startlxde` 

See also [Start X at login](/index.php/Start_X_at_login "Start X at login").

## Tips and tricks

### Application menu editing

The application menu works by resolving the `.desktop` files located in `/usr/share/applications/` and `~/.local/share/applications/`. To add or edit a menu item, see [desktop entries](/index.php/Desktop_entries "Desktop entries"). Third party menu editor can be found in the [AUR](/index.php/AUR "AUR") (e.g. [lxmed](https://aur.archlinux.org/packages/lxmed/)).

### Autostart

Applications can be automatically started in a couple of ways:

*   With `.desktop` files

LXDE implements [XDG Autostart](/index.php/XDG_Autostart "XDG Autostart").

*   Via LXsession

Each line in `~/.config/lxsession/LXDE/autostart` represents a command to be executed. If a line starts with `@`, and the command following it crashes, the command is automatically re-executed. For example:

 `~/.config/lxsession/LXDE/autostart` 
```
@lxterminal
@leafpad

```

**Note:** These commands do *not* end with a "&" symbol.

There is also a global autostart file at `/etc/xdg/lxsession/LXDE/autostart`.

**Note:** If both files are present, LXsession only executes the local file as of v0.4.9

### Bindings

Mouse and key bindings (i.e. keyboard shortcuts) are implemented with Openbox. LXDE users should follow the [Openbox wiki](http://openbox.org/wiki/Help:Bindings) to edit `~/.config/openbox/lxde-rc.xml`.

An optional GUI for editing the key bindings is provided by the [obkey](https://aur.archlinux.org/packages/obkey/) package. Whle it edits `rc.xml` by default, you can direct it to the LXDE configuration as follows:

```
$ obkey ~/.config/openbox/lxde-rc.xml

```

See [[1]](http://code.google.com/p/obkey/) for more information.

### Cursors

[lxappearance](https://www.archlinux.org/packages/?name=lxappearance) is a graphical tool to set [GTK](/index.php/GTK "GTK") look and feel, including the cursor theme. Settings configured with LXAppearance are written to `~/.gtkrc-2.0`, `~/.config/gtk-3.0/settings.ini` and `~/.icons/default/index.theme`. See also [Cursor themes](/index.php/Cursor_themes "Cursor themes").

### Digital clock applet time

You can right click on the digital clock applet on the panel and set how it displays the current time using the strftime format. See [strftime(3)](https://jlk.fjfi.cvut.cz/arch/manpages/man/strftime.3) for details.

### Font settings

[lxappearance-obconf](https://www.archlinux.org/packages/?name=lxappearance-obconf) configures [Openbox](/index.php/Openbox "Openbox") settings. See also [Font configuration](/index.php/Font_configuration "Font configuration").

### Keyboard layout

[lxpanel](https://www.archlinux.org/packages/?name=lxpanel) includes a keyboard layout applet. See [Keyboard configuration in Xorg](/index.php/Keyboard_configuration_in_Xorg "Keyboard configuration in Xorg") for generic instructions and [#Autostart](#Autostart) to automatically start *setxkbmap* in LXDE.

### Screen locking

LXDE does not come with a screen locker of its own. See [List of applications/Security#Screen lockers](/index.php/List_of_applications/Security#Screen_lockers "List of applications/Security") and [#Autostart](#Autostart) on how to start them.

The *Screen Lock* icon executes a script (located at `/usr/bin/lxlock`) which searches for a number of well known screen lockers and uses the first one it finds to lock the screen. See [lxlock](https://github.com/lxde/lxsession/blob/master/lxlock/lxlock) on GitHub.

`/etc/xdg/lxsession/LXDE/autostart` (from the [lxde-common](https://www.archlinux.org/packages/?name=lxde-common) package) lists [XScreenSaver](/index.php/XScreenSaver "XScreenSaver") which will be launched automatically.

See [DPMS](/index.php/DPMS "DPMS") on how to control the screen saver without external programs.

### LXPanel icons

Default icons used by LXpanel are stored in `/usr/share/pixmaps/` and any custom icons should be saved there as well.

To change default icons for applications, see [Desktop entries#Icons](/index.php/Desktop_entries#Icons "Desktop entries").

### LXPanel menus

The panel's menus can be configured in `/etc/xdg/menus/lxde-applications.menu` as per the [xdg-menu](/index.php/Xdg-menu "Xdg-menu") format to work with applications from other sessions (notably [MATE](/index.php/MATE "MATE")) to add some of the function-ability that LXDE lacks.

### Use a different window manager

LXsession uses the [window manager](/index.php/Window_manager "Window manager") defined in `~/.config/lxsession/LXDE/desktop.conf` ([Openbox](/index.php/Openbox "Openbox") by default). If this file does not exist, it searches in `/etc/xdg/lxsession/LXDE/desktop.conf` instead.

Replace `openbox-lxde` in either file with a window manager of your choice:

For metacity:

```
window_manager=metacity

```

For compiz:

```
window_manager=compiz

```

Alternatively use `*WM* --replace` as defined in [#Autostart](#Autostart), where *WM* is the name of the window manager executable being started. This means that *openbox* will be started first on each login and will then immediately be replaced. Note that Openbox and LXDE do not share the same `rc.xml` and keyboard shortcuts may differ. See [xbindkeys](/index.php/Xbindkeys "Xbindkeys").

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

### LXPanel crashes

With some [GTK](/index.php/GTK "GTK") themes, launching *lxpanel* will lead to the following error:

```
lxpanel: cairo-scaled-font.c:459: _cairo_scaled_glyph_page_destroy: Assertion `!scaled_font->cache_frozen' failed.

```

In this case install [ttf-dejavu](https://www.archlinux.org/packages/?name=ttf-dejavu).

If lxpanel crashes when browsing particular unicode web pages, install [ttf-droid](https://www.archlinux.org/packages/?name=ttf-droid).

### LXPanel Task Bar icon size

The icons of running applications do not match the set *Icon size* in *Panel Settings* > *Geometry* but are 4px smaller which makes some of them blurry. To have clear looking 32px icons in the Task Bar the set *Icon size* has to be 36px which would blur the icons of the rest of your active Panel Applets. To get around this create additional panel(s) and have them collectively make a single continuous looking panel by adjusting the Alignment and Margin in *Panel Settings* > *Geometry*.

### Fake transparency in LXTerminal

The latest version of [VTE terminal widget library](https://wiki.gnome.org/Apps/Terminal/VTE) requires a compositing window manager for background transparency. The unmaintained, legacy GTK 2 version of VTE has fake transparency, where the desktop background image will show through the terminal. It you prefer fake transparency, the GTK 2 version of LXTerminal can be installed with the [lxterminal-gtk2](https://aur.archlinux.org/packages/lxterminal-gtk2/) package.

## See also

*   [Linux LXDE Guide](http://lxlinux.com/)
*   [LXDE (Sourceforge)](http://lxde.sourceforge.net)
*   [LXDE forum](http://forum.lxde.org)