[GNOME](https://www.gnome.org/) (pronounced *gah-nohm* or *nohm*) is a [desktop environment](/index.php/Desktop_environment "Desktop environment") that aims to be simple and easy to use. It is designed by [The GNOME Project](https://en.wikipedia.org/wiki/The_GNOME_Project "wikipedia:The GNOME Project") and is composed entirely of free and open-source software. GNOME is a part of the [GNU Project](https://en.wikipedia.org/wiki/GNU_Project "wikipedia:GNU Project"). The default display is [Wayland](/index.php/Wayland "Wayland") instead of [Xorg](/index.php/Xorg "Xorg").

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Additional packages](#Additional_packages)
*   [2 GNOME Sessions](#GNOME_Sessions)
*   [3 Starting GNOME](#Starting_GNOME)
    *   [3.1 Graphically](#Graphically)
    *   [3.2 Manually](#Manually)
        *   [3.2.1 Xorg sessions](#Xorg_sessions)
        *   [3.2.2 Wayland sessions](#Wayland_sessions)
    *   [3.3 GNOME applications in Wayland](#GNOME_applications_in_Wayland)
*   [4 Navigation](#Navigation)
    *   [4.1 Legacy names](#Legacy_names)
*   [5 Configuration](#Configuration)
    *   [5.1 System settings](#System_settings)
        *   [5.1.1 Color](#Color)
        *   [5.1.2 Date & time](#Date_.26_time)
        *   [5.1.3 Default applications](#Default_applications)
        *   [5.1.4 Mouse and touchpad](#Mouse_and_touchpad)
        *   [5.1.5 Network](#Network)
        *   [5.1.6 Online accounts](#Online_accounts)
        *   [5.1.7 Search](#Search)
    *   [5.2 Advanced settings](#Advanced_settings)
        *   [5.2.1 Appearance](#Appearance)
            *   [5.2.1.1 GTK+ themes and icon themes](#GTK.2B_themes_and_icon_themes)
                *   [5.2.1.1.1 Global dark theme](#Global_dark_theme)
            *   [5.2.1.2 Window manager themes](#Window_manager_themes)
                *   [5.2.1.2.1 Titlebar height](#Titlebar_height)
                *   [5.2.1.2.2 Titlebar button order](#Titlebar_button_order)
                *   [5.2.1.2.3 Hide titlebar when maximized](#Hide_titlebar_when_maximized)
            *   [5.2.1.3 GNOME Shell themes](#GNOME_Shell_themes)
            *   [5.2.1.4 Icons on menu](#Icons_on_menu)
        *   [5.2.2 Desktop](#Desktop)
            *   [5.2.2.1 Icons on the Desktop](#Icons_on_the_Desktop)
            *   [5.2.2.2 Lock screen and background](#Lock_screen_and_background)
        *   [5.2.3 Extensions](#Extensions)
        *   [5.2.4 Input methods](#Input_methods)
        *   [5.2.5 Fonts](#Fonts)
        *   [5.2.6 Startup applications](#Startup_applications)
        *   [5.2.7 Power](#Power)
            *   [5.2.7.1 Configure behaviour on lid switch close](#Configure_behaviour_on_lid_switch_close)
            *   [5.2.7.2 Change critical battery level action](#Change_critical_battery_level_action)
        *   [5.2.8 Sort applications into application (app) folders](#Sort_applications_into_application_.28app.29_folders)
*   [6 See also](#See_also)

## Installation

Two groups are available:

*   [gnome](https://www.archlinux.org/groups/x86_64/gnome/) contains the base GNOME desktop and a subset of well-integrated [applications](https://wiki.gnome.org/Apps);
*   [gnome-extra](https://www.archlinux.org/groups/x86_64/gnome-extra/) contains further GNOME applications, including an archive manager, disk manager, [text editor](/index.php/Gedit "Gedit"), and a set of games. Note that this group builds on the [gnome](https://www.archlinux.org/groups/x86_64/gnome/) group.

The base desktop consists of [GNOME Shell](https://en.wikipedia.org/wiki/GNOME_Shell window manager. It can be installed separately with [gnome-shell](https://www.archlinux.org/packages/?name=gnome-shell).

**Note:** *mutter* acts as a composite manager for the desktop, employing hardware graphics acceleration to provide effects aimed at reducing screen clutter. The GNOME session manager automatically detects if your video driver is capable of running GNOME Shell and if not, falls back to software rendering using *llvmpipe*.

### Additional packages

These packages are not in the above mentioned groups:

*   **[Boxes](https://en.wikipedia.org/wiki/GNOME_Boxes "wikipedia:GNOME Boxes")** — A simple user interface to access [libvirt](/index.php/Libvirt "Libvirt") virtual machines.

	[https://wiki.gnome.org/Apps/Boxes](https://wiki.gnome.org/Apps/Boxes) || [gnome-boxes](https://www.archlinux.org/packages/?name=gnome-boxes)

*   **GNOME Initial Setup** — A simple, easy, and safe way to prepare a new system.

	[https://github.com/GNOME/gnome-initial-setup](https://github.com/GNOME/gnome-initial-setup) || [gnome-initial-setup](https://www.archlinux.org/packages/?name=gnome-initial-setup)

*   **GNOME MultiWriter** — Write an ISO file to multiple USB devices at once.

	[https://wiki.gnome.org/Apps/MultiWriter](https://wiki.gnome.org/Apps/MultiWriter) || [gnome-multi-writer](https://www.archlinux.org/packages/?name=gnome-multi-writer)

*   **GNOME PackageKit** — Collection of graphical tools for PackageKit to be used in the GNOME desktop.

	[https://github.com/GNOME/gnome-packagekit](https://github.com/GNOME/gnome-packagekit) || [gnome-packagekit](https://www.archlinux.org/packages/?name=gnome-packagekit)

*   **[Nemiver](https://en.wikipedia.org/wiki/Nemiver "wikipedia:Nemiver")** — A C/C++ debugger.

	[https://wiki.gnome.org/Apps/Nemiver](https://wiki.gnome.org/Apps/Nemiver) || [nemiver](https://www.archlinux.org/packages/?name=nemiver)

*   **[Software](https://en.wikipedia.org/wiki/GNOME_Software "wikipedia:GNOME Software")** — Lets you install and update applications and system extensions.

	[https://wiki.gnome.org/Apps/Software/](https://wiki.gnome.org/Apps/Software/) || [gnome-software](https://www.archlinux.org/packages/?name=gnome-software)

## GNOME Sessions

GNOME has three available sessions, all using GNOME Shell.

*   **GNOME** is the default which uses Wayland. Traditional X applications are run through Xwayland.
*   **GNOME Classic** is a traditional desktop layout with a similar interface to GNOME 2, using pre-activated extensions and parameters. [[1]](http://worldofgnome.org/welcome-to-gnome-3-8-flintstones-mode/) Hence it is more a customized GNOME Shell than a truly distinct mode.
*   **GNOME on Xorg** runs GNOME Shell using Xorg.

## Starting GNOME

GNOME can be started either graphically, using a [display manager](/index.php/Display_manager "Display manager"), or manually from the console.

**Note:** Support for screen locking in GNOME is provided by GDM. If GNOME is not started using GDM, you will have to use another screen locker to provide this functionality - see [List of applications/Security#Screen lockers](/index.php/List_of_applications/Security#Screen_lockers "List of applications/Security").

### Graphically

Select the session: *GNOME*, *GNOME Classic*, or *GNOME on Xorg* from the display manager's session menu.

### Manually

#### Xorg sessions

*   For the GNOME on Xorg session, add to the `~/.xinitrc` file: `exec gnome-session`.
*   For the GNOME Classic session, add to the `~/.xinitrc` file:
    ```
    export XDG_CURRENT_DESKTOP=GNOME-Classic:GNOME
    export GNOME_SHELL_SESSION_MODE=classic
    exec gnome-session --session=gnome-classic
    ```

After editing the `~/.xinitrc` file, GNOME can be launched with the `startx` command (see [xinitrc](/index.php/Xinitrc "Xinitrc") for additional details, such as preserving the logind session). After setting up the `~/.xinitrc` file it can also be arranged to [Start X at login](/index.php/Start_X_at_login "Start X at login").

#### Wayland sessions

**Note:** An X server—provided by the [xorg-server-xwayland](https://www.archlinux.org/packages/?name=xorg-server-xwayland) package—is still necessary to run applications that have not yet been ported to [Wayland](/index.php/Wayland "Wayland").

Manually starting a Wayland session is possible with `XDG_SESSION_TYPE=wayland dbus-run-session gnome-session`.

To start on login to tty1, add the following to your `.bash_profile`:

```
if [[ -z $DISPLAY ]] && [[ $(tty) = /dev/tty1 ]]; then
  XDG_SESSION_TYPE=wayland exec dbus-run-session gnome-session
fi

```

### GNOME applications in Wayland

When the *GNOME* session is used, GNOME applications will be run using Wayland. See the current status of Wayland for GNOME applications at [GNOME Applications under Wayland](https://wiki.gnome.org/Initiatives/Wayland/Applications/). For debugging cases, the [GTK+ manual](https://developer.gnome.org/gtk3/stable/gtk-running.html) lists options and environment variables.

## Navigation

To learn how to use the GNOME shell effectively read the [GNOME Shell Cheat Sheet](https://wiki.gnome.org/Projects/GnomeShell/CheatSheet); it highlights GNOME shell features and keyboard shortcuts. Features include task switching, keyboard use, window control, the panel, overview mode, and more. A few of the shortcuts are:

*   `Super` + `m`: show message tray
*   `Super` + `a`: show applications menu
*   `Alt-` + `Tab`: cycle active applications
*   `Alt-` + ``` (the key above `Tab` on US keyboard layouts): cycle windows of the application in the foreground
*   `Alt` + `F2`, then enter `r` or `restart`: restart the shell in case of graphical shell problems (only in X/legacy mode, not in Wayland mode).

### Legacy names

**Note:** Some GNOME programs have undergone name changes where the application's name in documentation and about dialogs has been changed but the executable name has not. A few such applications are listed in the table below.

**Tip:** Searching for the legacy name of an application in the Shell search bar will successfully return the application in question. For instance, searching for *nautilus* will return *Files*.

| Current | Legacy |
| [Files](/index.php/Files "Files") | Nautilus |
| [Web](/index.php/GNOME/Web "GNOME/Web") | Epiphany |
| Videos | Totem |
| Main Menu | Alacarte |
| Document Viewer | Evince |
| Disk Usage Analyser | Baobab |
| Image Viewer | EoG (Eye of GNOME) |
| [Passwords and Keys](/index.php/GNOME/Keyring "GNOME/Keyring") | Seahorse |

## Configuration

The GNOME desktop relies on a configuration database backend (DConf) to store system and application settings. The desktop comes with default configuration settings, installed applications add their own to the database. The basic configuration is done either via the GNOME System Settings panel (*gnome-control-center*) or the preferences of the individual applications. A direct configuration of the DConf database is always possible as well and performed with the *gsettings* command line tool. In particular it can be used to configure settings which are not exposed via the user interface.

GNOME settings are then applied by the GNOME Settings Daemon. Note that the daemon can be run outside of a GNOME session in order to apply GNOME configuration in a non-GNOME environment. To do so, execute:

```
$ nohup /usr/lib/gnome-settings-daemon/gnome-settings-daemon > /dev/null &

```

The configuration is usually performed per user and the rest of this section does not cover how to create configuration templates for a multi-user-system.

### System settings

Control panel settings of note.

#### Color

The daemon `colord` reads the display's EDID and extracts the appropriate color profile. Most color profiles are accurate and no setup is required; however for those that are not accurate, or for older displays, color profiles can be put in `~/.local/share/icc/` and directed to.

#### Date & time

If the system has a configured [Network Time Protocol daemon](/index.php/Network_Time_Protocol_daemon "Network Time Protocol daemon"), it will be effective for GNOME as well. The synchronization can be set to manual control from the menu, if required.

To show the date in the top bar, execute:

```
$ gsettings set org.gnome.desktop.interface clock-show-date true

```

Additionally, to show week numbers in the calendar opened on the top bar, execute:

```
$ gsettings set org.gnome.desktop.calendar show-weekdate true

```

#### Default applications

Upon installing GNOME for the first time, you may find that the wrong applications are handling certain protocols. For example, *totem* opens videos instead of a previously used [VLC](/index.php/VLC "VLC"). Some of the associations can be set from system settings via: *System* > *Details* > *Default applications*.

For other protocols and methods see [Default applications](/index.php/Default_applications "Default applications") for configuration.

#### Mouse and touchpad

To help reduce touchpad interference you may wish to implement the settings below via *gnome-control-center*:

*   Disable touchpad while typing
*   Disable scrolling
*   Disable tap-to-click

Depending on your device, other configuration settings may be available, but not exposed via the default GUI. For example, a different touchpad `click-method`

 `$ gsettings range org.gnome.desktop.peripherals.touchpad click-method` 
```

enum
'default'
'none'
'areas'
'fingers'
```

to be set manually:

```
$ gsettings set org.gnome.desktop.peripherals.touchpad click-method 'fingers'

```

or via *gnome-tweak-tool*.

**Note:** The [synaptics](/index.php/Synaptics "Synaptics") driver is not supported by GNOME. Instead, you should use [libinput](/index.php/Libinput "Libinput"). See [this bug report](https://bugzilla.gnome.org/show_bug.cgi?id=764257#c12).

#### Network

[NetworkManager](/index.php/NetworkManager "NetworkManager") is the native tool of the GNOME project to control network settings from the shell. [Install](/index.php/Install "Install") the [networkmanager](https://www.archlinux.org/packages/?name=networkmanager) package and [enable](/index.php/Enable "Enable") the `NetworkManager.service` systemd unit.

While any other [network manager](/index.php/Network_manager "Network manager") can be used as well, NetworkManager provides the full integration via the shell network settings and a status indicator applet [network-manager-applet](https://www.archlinux.org/packages/?name=network-manager-applet) (not required for GNOME).

#### Online accounts

Backends for the GNOME messaging application [empathy](https://www.archlinux.org/packages/?name=empathy) as well as the GNOME Online Accounts section of the System Settings panel are provided in a separate group: [telepathy](https://www.archlinux.org/groups/x86_64/telepathy/). See [Unable to add accounts in Empathy and GNOME Online Accounts](/index.php/GNOME/Troubleshooting#Unable_to_add_accounts_in_Empathy_and_GNOME_Online_Accounts "GNOME/Troubleshooting"). Some online accounts, such as [ownCloud](/index.php/OwnCloud "OwnCloud"), require [gvfs-goa](https://www.archlinux.org/packages/?name=gvfs-goa) to be installed for full functionality in GNOME applications such as [GNOME Files](/index.php/GNOME_Files "GNOME Files") and GNOME Documents [[2]](https://wiki.gnome.org/ThreePointSeven/Features/Owncloud).

#### Search

The GNOME shell has a search that can be quickly accessed by pressing the `Super` key and starting to type. The [tracker](https://www.archlinux.org/packages/?name=tracker) package is installed by default as a part of [gnome](https://www.archlinux.org/groups/x86_64/gnome/) group and provides an indexing application and metadata database. It can be configured with the *Search and Indexing* menu item; monitor status with *tracker-control*. It is started automatically by *gnome-session* when the user logs in. Indexing can be started manually with `tracker-control -s`. Search settings can also be configured in the *System Settings* panel.

The Tracker database can be queried using the *tracker-sparql* command. View its manual page `man tracker-sparql` for more information.

### Advanced settings

As noted above, many configuration options such as changing the [GTK+](/index.php/GTK%2B "GTK+") theme or the [window manager](/index.php/Window_manager "Window manager") theme are not exposed in the GNOME System Settings panel (*gnome-control-center*). Those users that want to configure these settings may wish to use the GNOME Tweak Tool ([gnome-tweak-tool](https://www.archlinux.org/packages/?name=gnome-tweak-tool)), a convenient graphical tool which exposes many of these settings.

GNOME settings (which are stored in the DConf database) can also be configured using the [*dconf-editor*](https://developer.gnome.org/dconf/unstable/dconf-editor.html) (a graphical DConf configuration tool) or the [*gsettings*](https://developer.gnome.org/gio/stable/GSettings.html) command line tool. The GNOME Tweak Tool does not do anything else in the background of the GUI; note though that you will not find all settings described in the following sections in it.

#### Appearance

##### GTK+ themes and icon themes

To install a new theme or icon set, add the relevant `~/.local/share/themes` or `~/.local/share/icons` respectively (add to `/usr/share/` instead of `~/.local/share/` for the themes to be available systemwide.) They and other GUI settings can also be defined in `~/.config/gtk-3.0/settings.ini`:

 `~/.config/gtk-3.0/settings.ini` 
```
[Settings]
gtk-theme-name = Adwaita
# next option is applicable only if selected theme supports it
gtk-application-prefer-dark-theme = true
# set font name and dimension
gtk-font-name = Sans 10

```

Additional theme locations:

*   [DeviantArt](http://www.deviantart.com/browse/all/customization/skins/linuxutil/desktopenv/gnome/gtk3/).
*   [gnome-look.org](http://gnome-look.org/index.php?xcontentmode=167).
*   [GTK+ 3 themes in the AUR](https://aur.archlinux.org/packages.php?O=0&K=gtk3&do_Search=Go).
*   [Cursor themes in the AUR](https://aur.archlinux.org/packages.php?O=0&K=xcursor&do_Search=Go&PP=50&SB=v&SO=d).
*   [Icon themes in the AUR](https://aur.archlinux.org/packages.php?O=0&K=icon-theme&do_Search=Go&PP=50&SB=v&SO=d).

Once installed, they can be selected using the GNOME Tweak Tool or GSettings - see below for GSettings commands:

For the GTK+ theme:

```
$ gsettings set org.gnome.desktop.interface gtk-theme *theme-name*

```

For the icon theme

```
$ gsettings set org.gnome.desktop.interface icon-theme *theme-name*

```

###### Global dark theme

GNOME will use the Adwaita light theme by default however a dark variant of this theme (called the Global Dark Theme) also exists and can be selected using the Tweak Tool or by editing the GTK+ 3 settings file - see [GTK+#Dark theme variant](/index.php/GTK%2B#Dark_theme_variant "GTK+"). Some applications such as Image Viewer (*eog*) use the dark theme by default. It should be noted that the Global Dark Theme only works with GTK+ 3 applications; some GTK+ 3 applications may only have partial support for the Global Dark theme. Qt and GTK+ 2 support for the Global Dark Theme may be added in the future.

##### Window manager themes

The window manager theme (the style of the window titlebars) can be set using the GNOME Tweak Tool or the following GSettings command:

```
$ gsettings set org.gnome.desktop.wm.preferences theme *theme-name*

```

###### Titlebar height

**Note:** Applying this configuration shrinks the titlebar of the GNOME-terminal and Chromium, but does not appear to affect the Nautilus titlebar height.
 `~/.config/gtk-3.0/gtk.css` 
```
headerbar.default-decoration {
 padding-top: 0px;
 padding-bottom: 0px;
 min-height: 0px;
 font-size: 0.6em;
}

headerbar.default-decoration button.titlebutton {
 padding: 0px;
 min-height: 0px;
}

```

See [[3]](https://ask.fedoraproject.org/en/question/10035/shrink-title-bar/?answer=86149#post-id-86149) for more information.

###### Titlebar button order

To set the order for the GNOME window manager (Mutter, Metacity):

```
$ gsettings set org.gnome.desktop.wm.preferences button-layout ':minimize,maximize,close'

```

**Tip:** The colon indicates which side of the titlebar the window buttons will appear.

###### Hide titlebar when maximized

*   [Install](/index.php/Install "Install") [gnome-shell-extension-pixel-saver-git](https://aur.archlinux.org/packages/gnome-shell-extension-pixel-saver-git/) or [gnome-shell-extension-pixel-saver](https://aur.archlinux.org/packages/gnome-shell-extension-pixel-saver/). Maximized windows get the title bar merged into the activity bar, saving precious pixels.

*   [Install](/index.php/Install "Install") [mutter-hide-legacy-decorations](https://aur.archlinux.org/packages/mutter-hide-legacy-decorations/). It changes a default setting in the window manager, so as to automatically hide the titlebar on legacy (non-headerbar) apps when they are maximized or tiled to the side.

*   [Install](/index.php/Install "Install") [maximus](https://aur.archlinux.org/packages/maximus/). To start the application, execute *maximus* from a terminal. When running, the daemon will automatically maximize windows. It will undecorate maximized windows and redecorate them when they are unmaximized. If you do not want all windows to start maximized, run `maximus -m` instead. Note that this will only work with windows decorated by the window manager; applications that use client-side decoration such as [GNOME Files](/index.php/GNOME_Files "GNOME Files") will not be undecorated when maximized.

##### GNOME Shell themes

The theme of GNOME Shell itself is configurable. To use a Shell theme, firstly ensure that you have the [gnome-shell-extensions](https://www.archlinux.org/packages/?name=gnome-shell-extensions) package installed. Then enable the *User Themes* extension, either through GNOME Tweak Tool or through the [GNOME Shell Extensions](https://extensions.gnome.org) webpage. Shell themes can then be loaded and selected using the GNOME Tweak Tool.

There are a number of GNOME Shell themes available [in the AUR](https://aur.archlinux.org/packages.php?O=0&K=gnome-shell-theme&do_Search=Go&PP=50&SB=v&SO=d).

Shell themes can also be downloaded from [gnome-look.org](http://gnome-look.org/index.php?xcontentmode=191).

##### Icons on menu

The default GNOME schema doesn't display any icon on menus. To display icons on menus, issue the following command.

```
$ gsettings set org.gnome.settings-daemon.plugins.xsettings overrides "{'Gtk/ButtonImages': <1>, 'Gtk/MenuImages': <1>}"

```

#### Desktop

Various Desktop settings can be applied.

##### Icons on the Desktop

See [GNOME/Files#Desktop Icons](/index.php/GNOME/Files#Desktop_Icons "GNOME/Files").

##### Lock screen and background

When setting the Desktop or Lock screen background, it is important to note that the Pictures tab will only display pictures located in `/home/*username*/Pictures` folder. If you wish to use a picture not located in this folder, use the commands indicated below.

For the desktop background:

```
$ gsettings set org.gnome.desktop.background picture-uri 'file:///path/to/my/picture.jpg'

```

For the lock screen background

```
$ gsettings set org.gnome.desktop.screensaver picture-uri 'file:///path/to/my/picture.jpg'

```

#### Extensions

**Note:** The GNOME Shell browser plugin which allows users to install extensions from [extensions.gnome.org](https://extensions.gnome.org) works out-of-the-box for browsers such as [GNOME/Web](/index.php/GNOME/Web "GNOME/Web"). For [Firefox](/index.php/Firefox "Firefox"), Google Chrome/Chromium, Opera and Vivaldi browsers, it is required to install [chrome-gnome-shell-git](https://aur.archlinux.org/packages/chrome-gnome-shell-git/) and the appropriate browser extension.

GNOME Shell can be customized with extensions per user or system-wide.

The catalogue of extensions is available at [extensions.gnome.org](https://extensions.gnome.org). By a user they can be installed and activated in the browser by setting the switch in the top left of the screen to **ON** and clicking **Install** on the resulting dialog (if the extension in question is not installed). After installation it is shown in the [extensions.gnome.org/local/](https://extensions.gnome.org/local/) tab, which has to be visited as well to check for available updates. Installed extensions can also be enabled or disabled using [gnome-tweak-tool](https://www.archlinux.org/packages/?name=gnome-tweak-tool).

More information about GNOME shell extensions is available on the [GNOME Shell Extensions about page](https://extensions.gnome.org/about/).

[Installing](/index.php/Installing "Installing") extensions via a package makes them available for all users of the system and automates the update process.

The [gnome-shell-extensions](https://www.archlinux.org/packages/?name=gnome-shell-extensions) package provides a set of extensions maintained as part of the GNOME project (many of the included extensions are used by the GNOME Classic session).

Users who want a taskbar but do not wish to use the GNOME Classic session may want to enable the *Window list* extension (provided by the [gnome-shell-extensions](https://www.archlinux.org/packages/?name=gnome-shell-extensions) package).

#### Input methods

GNOME has integrated support for input methods through [IBus](/index.php/IBus "IBus"), only [ibus](https://www.archlinux.org/packages/?name=ibus) and the wanted input method engine (e.g. [ibus-libpinyin](https://www.archlinux.org/packages/?name=ibus-libpinyin) for Intelligent Pinyin) needed to be installed, after installation the input method engine can be added as a keyboard layout in GNOME's Regional & Language Settings.

#### Fonts

**Tip:** If you set the *Scaling factor* to a value above 1.00, the Accessibility menu will be automatically enabled.

Fonts can be set for Window titles, Interface (applications), Documents and Monospace. See the Fonts tab in the Tweak Tool for the relevant options.

For hinting, RGBA will likely be desired as this fits most monitors types, and if fonts appear too blocked reduce hinting to *Slight* or *None*.

#### Startup applications

To start certain applications on login, copy the relevant `.desktop` file from `/usr/share/applications/` to `~/.config/autostart/`.

The [gnome-tweak-tool](https://www.archlinux.org/packages/?name=gnome-tweak-tool) allows managing autostart-entries.

**Tip:** If the plus sign button in the Tweak Tool's Startup Applications section is unresponsive, try start the Tweak Tool from the terminal using the following command: `gnome-tweak-tool`. See the following [forum thread](https://bbs.archlinux.org/viewtopic.php?pid=1413631#p1413631).

**Note:** The deprecated *gnome-session-properties* dialog can be added by [installing](/index.php/Install "Install") the [gnome-session-properties](https://aur.archlinux.org/packages/gnome-session-properties/) package.

#### Power

The basic power settings that may want to be altered (these example settings assume the user is using a laptop - change them as desired):

```
$ gsettings set org.gnome.settings-daemon.plugins.power button-power *hibernate*
$ gsettings set org.gnome.settings-daemon.plugins.power sleep-inactive-ac-timeout *3600*
$ gsettings set org.gnome.settings-daemon.plugins.power sleep-inactive-ac-type *hibernate*
$ gsettings set org.gnome.settings-daemon.plugins.power sleep-inactive-battery-timeout *1800*
$ gsettings set org.gnome.settings-daemon.plugins.power sleep-inactive-battery-type *hibernate*
$ gsettings set org.gnome.desktop.lockdown disable-lock-screen *true*

```

To keep a monitor active on lid close:

```
$ gsettings set org.gnome.settings-daemon.plugins.xrandr default-monitors-setup do-nothing

```

##### Configure behaviour on lid switch close

The GNOME Tweak Tool can optionally *inhibit* the *systemd* setting for the lid close ACPI event.[[4]](http://ftp.gnome.org/pub/GNOME/sources/gnome-tweak-tool/3.17/gnome-tweak-tool-3.17.1.news) To *inhibit* the setting, start the Tweak Tool and, under the power tab, check the *Don't suspend on lid close* option. This means that the system will do nothing on lid close instead of suspending - the default behaviour. Checking the setting creates `~/.config/autostart/ignore-lid-switch-tweak.desktop` which will autostart the Tweak Tool's inhibitor.

If you do not want the system to suspend or do nothing on lid close, you will need to ensure that the setting described above is **not** checked and then configure *systemd* with `HandleLidSwitch=*preferred_behaviour*` as described in [Power management#ACPI events](/index.php/Power_management#ACPI_events "Power management").

##### Change critical battery level action

The settings panel does not provide an option for changing the critical battery level action. These settings have been removed from dconf as well. They are now managed by upower. Edit the upower settings in `/etc/UPower/UPower.conf`. Find these settings and adjust to your needs.

 `/etc/UPower/UPower.conf` 
```
PercentageLow=10
PercentageCritical=3
PercentageAction=2
CriticalPowerAction=HybridSleep
```

#### Sort applications into application (app) folders

**Tip:** The [gnome-catgen](https://github.com/prurigro/gnome-catgen) ([gnome-catgen-git](https://aur.archlinux.org/packages/gnome-catgen-git/)) script allows you to manage folders through the creation of files in `~/.local/share/applications-categories` named after each category and containing a list of the desktop files belonging to apps you would like to have inside. Optionally, you can have it cycle through each app without a folder and input the desired category until you ctrl-c or run out of apps.

In the **dconf-editor** navigate to `org.gnome.desktop.app-folders` and set the value of `folder-children` to an array of comma separated folder names:

```
['Utilities', 'Sundry']

```

Add applications using `gsettings`:

```
$ gsettings set org.gnome.desktop.app-folders.folder:/org/gnome/desktop/app-folders/folders/Sundry/ apps "['alacarte.desktop', 'dconf-editor.desktop']"

```

This adds the applications `alacarte.desktop` and `dconf-editor.desktop` to the Sundry folder. This will also create the folder `org.gnome.desktop.app-folders.folders.Sundry`.

To name the folder (if it has no name that appears at the top of the applications):

```
$ gsettings set org.gnome.desktop.app-folders.folder:/org/gnome/desktop/app-folders/folders/Sundry/ name "Sundry"

```

Applications can also be sorted by their category (specified in their *.desktop* file):

```
$ gsettings set org.gnome.desktop.app-folders.folder:/org/gnome/desktop/app-folders/folders/Sundry/ categories "['Office']"

```

If certain applications matching a category are not wanted in a certain folder, exclusions can be set:

```
$ gsettings set org.gnome.desktop.app-folders.folder:/org/gnome/desktop/app-folders/folders/Sundry/ excluded-apps "['libreoffice-draw.desktop']"

```

For further information, refer to the [app-folders schema](https://git.gnome.org/browse/gsettings-desktop-schemas/tree/schemas/org.gnome.desktop.app-folders.gschema.xml.in).

## See also

*   [The Official Website of GNOME](https://www.gnome.org/)
*   [Extensions for GNOME-shell](https://extensions.gnome.org/)
*   [GNOME Shell Cheat Sheet](https://wiki.gnome.org/Projects/GnomeShell/CheatSheet), commands, keyboard shortcuts and other tips for using GNOME Shell.
*   Themes, icons, and backgrounds:
    *   [Personalize GNOME](https://wiki.gnome.org/Personalization)
    *   [GNOME Look](https://www.gnome-look.org/)
*   GTK+/GNOME programs:
    *   [GNOME Files](http://www.gnomefiles.org/)
    *   [GNOME Apps Index](https://wiki.gnome.org/Apps)
*   [Customizing the GNOME Shell](http://blog.fpmurphy.com/2011/03/customizing-the-gnome-3-shell.html)
*   GNOME Source/Mirrors:
    *   [GNOME Git Repository](https://git.gnome.org/browse/)
    *   [GNOME Github Mirror](https://github.com/GNOME)