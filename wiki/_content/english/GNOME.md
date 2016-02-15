GNOME (pronounced _gah-nohm_ or _nohm_) is a [desktop environment](/index.php/Desktop_environment "Desktop environment") that aims to be simple and easy to use. It is designed by [The GNOME Project](https://en.wikipedia.org/wiki/The_GNOME_Project "wikipedia:The GNOME Project") and is composed entirely of free and open-source software. GNOME is a part of the [GNU Project](https://en.wikipedia.org/wiki/GNU_Project "wikipedia:GNU Project").

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Additional packages](#Additional_packages)
*   [2 GNOME Sessions](#GNOME_Sessions)
*   [3 Starting GNOME](#Starting_GNOME)
    *   [3.1 Graphically](#Graphically)
    *   [3.2 Manually](#Manually)
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
*   [6 Tips and tricks](#Tips_and_tricks)
    *   [6.1 Keyboard](#Keyboard)
        *   [6.1.1 Turn on NumLock on login](#Turn_on_NumLock_on_login)
        *   [6.1.2 Hotkey alternatives](#Hotkey_alternatives)
        *   [6.1.3 Keyboard switch with command](#Keyboard_switch_with_command)
        *   [6.1.4 XkbOptions keyboard options](#XkbOptions_keyboard_options)
        *   [6.1.5 De-bind Windows key](#De-bind_Windows_key)
    *   [6.2 Disks](#Disks)
    *   [6.3 Hiding applications from the menu](#Hiding_applications_from_the_menu)
    *   [6.4 Screencast recording](#Screencast_recording)
    *   [6.5 Screenshot](#Screenshot)
    *   [6.6 Log out delay](#Log_out_delay)
    *   [6.7 Disable animations](#Disable_animations)
    *   [6.8 Retina (HiDPI) display support](#Retina_.28HiDPI.29_display_support)
    *   [6.9 Passwords and keys (PGP Keys)](#Passwords_and_keys_.28PGP_Keys.29)
    *   [6.10 Terminal](#Terminal)
        *   [6.10.1 Change default terminal size](#Change_default_terminal_size)
        *   [6.10.2 New terminals adopt current directory](#New_terminals_adopt_current_directory)
        *   [6.10.3 Pad the terminal](#Pad_the_terminal)
        *   [6.10.4 Disable blinking cursor](#Disable_blinking_cursor)
        *   [6.10.5 Disable confirmation window when closing Terminal](#Disable_confirmation_window_when_closing_Terminal)
    *   [6.11 Middle mouse button](#Middle_mouse_button)
    *   [6.12 Enable button and menu icons](#Enable_button_and_menu_icons)
    *   [6.13 Use custom colours and gradients for desktop background](#Use_custom_colours_and_gradients_for_desktop_background)
    *   [6.14 Transitioning backgrounds](#Transitioning_backgrounds)
    *   [6.15 Custom GNOME sessions](#Custom_GNOME_sessions)
*   [7 Troubleshooting](#Troubleshooting)
    *   [7.1 Shell freezes](#Shell_freezes)
    *   [7.2 Incorrect application defaults](#Incorrect_application_defaults)
    *   [7.3 Tracker & Documents do not list any local files](#Tracker_.26_Documents_do_not_list_any_local_files)
    *   [7.4 Unable to add accounts in Empathy and GNOME Online Accounts](#Unable_to_add_accounts_in_Empathy_and_GNOME_Online_Accounts)
    *   [7.5 Cannot change settings in dconf-editor](#Cannot_change_settings_in_dconf-editor)
    *   [7.6 When an extension breaks the shell](#When_an_extension_breaks_the_shell)
    *   [7.7 Extensions do not work after GNOME 3 update](#Extensions_do_not_work_after_GNOME_3_update)
    *   [7.8 Keyboard shortcut do not work with only conky running](#Keyboard_shortcut_do_not_work_with_only_conky_running)
    *   [7.9 Unable to apply stored configuration for monitors](#Unable_to_apply_stored_configuration_for_monitors)
    *   [7.10 Consistent cursor theme](#Consistent_cursor_theme)
    *   [7.11 Windows cannot be modified with Alt-Key + mouse-button](#Windows_cannot_be_modified_with_Alt-Key_.2B_mouse-button)
    *   [7.12 Slow loading of system icons/slow GDM login](#Slow_loading_of_system_icons.2Fslow_GDM_login)
    *   [7.13 Artifacts when maximizing windows](#Artifacts_when_maximizing_windows)
    *   [7.14 Tear-free video with Intel HD Graphics](#Tear-free_video_with_Intel_HD_Graphics)
    *   [7.15 Window opens behind other windows when using multiple monitors](#Window_opens_behind_other_windows_when_using_multiple_monitors)
    *   [7.16 Lock button fails to re-enable touchpad](#Lock_button_fails_to_re-enable_touchpad)
    *   [7.17 GNOME Shell keyboard sources menu not visible](#GNOME_Shell_keyboard_sources_menu_not_visible)
    *   [7.18 Mouse cursor missing](#Mouse_cursor_missing)
    *   [7.19 No restart button in session menu when screen is locked](#No_restart_button_in_session_menu_when_screen_is_locked)
    *   [7.20 PulseAudio system-wide causes delay in GNOME and GDM](#PulseAudio_system-wide_causes_delay_in_GNOME_and_GDM)
    *   [7.21 GNOME crashes when trying to reorder applications in the GNOME Shell Dash](#GNOME_crashes_when_trying_to_reorder_applications_in_the_GNOME_Shell_Dash)
*   [8 See also](#See_also)

## Installation

Two groups are available:

*   [gnome](https://www.archlinux.org/groups/x86_64/gnome/) contains the base GNOME desktop and a subset of well-integrated [applications](https://wiki.gnome.org/Apps);
*   [gnome-extra](https://www.archlinux.org/groups/x86_64/gnome-extra/) contains further GNOME applications, including an archive manager, disk manager, [text editor](/index.php/Gedit "Gedit"), and a set of games. Note that this group builds on the [gnome](https://www.archlinux.org/groups/x86_64/gnome/) group.

The base desktop consists of [GNOME Shell](https://en.wikipedia.org/wiki/GNOME_Shell "wikipedia:GNOME Shell"), a plugin for the [Mutter](https://en.wikipedia.org/wiki/Mutter_(software) "wikipedia:Mutter (software)") window manager. It can be installed separately with [gnome-shell](https://www.archlinux.org/packages/?name=gnome-shell).

**Note:** _mutter_ acts as a composite manager for the desktop, employing hardware graphics acceleration to provide effects aimed at reducing screen clutter. The GNOME session manager automatically detects if your video driver is capable of running GNOME Shell and if not, falls back to software rendering using _llvmpipe_.

### Additional packages

These packages are not in the above mentioned groups:

*   **[Boxes](https://en.wikipedia.org/wiki/GNOME_Boxes "wikipedia:GNOME Boxes")** — A simple user interface to access [libvirt](/index.php/Libvirt "Libvirt") virtual machines.

	[https://wiki.gnome.org/Apps/Boxes](https://wiki.gnome.org/Apps/Boxes) || [gnome-boxes](https://www.archlinux.org/packages/?name=gnome-boxes)

*   **GNOME Initial Setup** — A simple, easy, and safe way to prepare a new system.

	[https://github.com/GNOME/gnome-initial-setup](https://github.com/GNOME/gnome-initial-setup) || [gnome-initial-setup](https://www.archlinux.org/packages/?name=gnome-initial-setup)

*   **GNOME PackageKit** — Collection of graphical tools for PackageKit to be used in the GNOME desktop.

	[https://github.com/GNOME/gnome-packagekit](https://github.com/GNOME/gnome-packagekit) || [gnome-packagekit](https://www.archlinux.org/packages/?name=gnome-packagekit)

*   **[Nemiver](https://en.wikipedia.org/wiki/Nemiver "wikipedia:Nemiver")** — A C/C++ debugger.

	[https://wiki.gnome.org/Apps/Nemiver](https://wiki.gnome.org/Apps/Nemiver) || [nemiver](https://www.archlinux.org/packages/?name=nemiver)

*   **[Software](https://en.wikipedia.org/wiki/GNOME_Software "wikipedia:GNOME Software")** — Lets you install and update applications and system extensions.

	[https://wiki.gnome.org/Apps/Software/](https://wiki.gnome.org/Apps/Software/) || [gnome-software](https://www.archlinux.org/packages/?name=gnome-software)

## GNOME Sessions

GNOME has three available sessions, all using GNOME Shell.

*   **GNOME** is the default, innovative layout.
*   **GNOME Classic** is a traditional desktop layout with a similar interface to GNOME 2, using pre-activated extensions and parameters. [[1]](http://worldofgnome.org/welcome-to-gnome-3-8-flintstones-mode/) Hence it is more a customized GNOME Shell than a truly distinct mode.
*   **GNOME on Wayland** runs GNOME Shell using the new Wayland protocol. Traditional X applications are run through Xwayland.

## Starting GNOME

GNOME can be started either graphically, using a [display manager](/index.php/Display_manager "Display manager"), or manually from the console. For optimal desktop integration, using [GDM](/index.php/GDM "GDM") (the GNOME Display manager) is recommended. Note that [enabling](/index.php/Enabling "Enabling") a display manager (such as GDM) means that Xorg will run with root rights.

**Note:** Support for screen locking in GNOME is provided by GDM. If GNOME is not started using GDM, you will have to use another screen locker to provide this functionality - see [List of applications/Security#Screen lockers](/index.php/List_of_applications/Security#Screen_lockers "List of applications/Security").

### Graphically

Select the session: _GNOME_, _GNOME Classic_ or _GNOME on Wayland_ from the display manager's session menu.

### Manually

*   For the standard GNOME session, add to the `~/.xinitrc` file: `exec gnome-session`.
*   For the GNOME Classic session, add to the `~/.xinitrc` file:

    ```
    export XDG_CURRENT_DESKTOP=GNOME-Classic:GNOME
    export GNOME_SHELL_SESSION_MODE=classic
    exec gnome-session --session=gnome-classic
    ```

After editing the `~/.xinitrc` file, GNOME can be launched with the `startx` command (see [xinitrc](/index.php/Xinitrc "Xinitrc") for additional details, such as preserving the logind session). After setting up the `~/.xinitrc` file it can also be arranged to [Start X at login](/index.php/Start_X_at_login "Start X at login").

**Note:** GNOME on Wayland requires the [xorg-server-xwayland](https://www.archlinux.org/packages/?name=xorg-server-xwayland) package, and **cannot** be started using _startx_ and `~/.xinitrc`. Instead, run `gnome-session --session=gnome-wayland`. For more information, see [Wayland](/index.php/Wayland "Wayland").

### GNOME applications in Wayland

Currently, by default, GNOME applications will be run as traditional X applications through Xwayland. To test GNOME applications with Wayland, use the command line to run the application and prefix the command with `env GDK_BACKEND='wayland,x11' <command>`.

**Note:** Setting a global Wayland environment, by running `env GDK_BACKEND=wayland gnome-session --session=gnome-wayland`, currently does not work - _gnome-session_ will exit immediately. Instead, use `export GDK_BACKEND='wayland,x11'` in your bash profile, or use `env GDK_BACKEND='wayland,x11' gnome-session --session=gnome-wayland` on the command line. But in general, neither of these environment settings are necessary, and running `gnome-session` with the `--session=gnome-wayland` switch is sufficient. Without the `GDK_BACKEND` environment variable, the GNOME Application must be "Wayland aware" to run as a Wayland application, or default to running on Xwayland otherwise. See also `GDK_BACKEND` under GNOME [Environment variables](https://developer.gnome.org/gtk3/stable/gtk-running.html).

See the following page for the status of [GNOME Applications under Wayland](https://wiki.gnome.org/Initiatives/Wayland/Applications/).

## Navigation

To learn how to use the GNOME shell effectively read the [GNOME Shell Cheat Sheet](https://wiki.gnome.org/Projects/GnomeShell/CheatSheet); it highlights GNOME shell features and keyboard shortcuts. Features include task switching, keyboard use, window control, the panel, overview mode, and more. A few of the shortcuts are:

*   `Super` + `m`: show message tray
*   `Super` + `a`: show applications menu
*   `Alt-` + `Tab`: cycle active applications
*   `Alt-` + ``` (the key above `Tab` on US keyboard layouts): cycle windows of the application in the foreground
*   `Alt` + `F2`, then enter `r` or `restart`: restart the shell in case of graphical shell problems.

### Legacy names

**Note:** Some GNOME programs have undergone name changes where the application's name in documentation and about dialogs has been changed but the executable name has not. A few such applications are listed in the table below.

**Tip:** Searching for the legacy name of an application in the Shell search bar will successfully return the application in question. For instance, searching for _nautilus_ will return _Files_.

| Current | Legacy |
| [Files](/index.php/Files "Files") | Nautilus |
| [Web](/index.php/GNOME_Web "GNOME Web") | Epiphany |
| Videos | Totem |
| Main Menu | Alacarte |
| Document Viewer | Evince |
| Disk Usage Analyser | Baobab |
| Image Viewer | EoG (Eye of GNOME) |
| [Passwords and Keys](/index.php/GNOME_Keyring "GNOME Keyring") | Seahorse |

## Configuration

The GNOME desktop relies on a configuration database backend (DConf) to store system and application settings. The desktop comes with default configuration settings, installed applications add their own to the database. The basic configuration is done either via the GNOME System Settings panel (_gnome-control-center_) or the preferences of the individual applications. A direct configuration of the DConf database is always possible as well and performed with the _gsettings_ command line tool. In particular it can be used to configure settings which are not exposed via the user interface.

GNOME settings are then applied by the GNOME Settings Daemon. Note that the daemon can be run outside of a GNOME session in order to apply GNOME configuration in a non-GNOME environment. Execute `nohup /usr/lib/gnome-settings-daemon/gnome-settings-daemon > /dev/null &` to do so.

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

Additionally, to show week numbers in the Shell calendar, execute:

```
$ gsettings set org.gnome.shell.calendar show-weekdate true

```

#### Default applications

Upon installing GNOME for the first time, you may find that the wrong applications are handling certain protocols. For example, _totem_ opens videos instead of a previously used [VLC](/index.php/VLC "VLC"). Some of the associations can be set from system settings via: _System_ > _Details_ > _Default applications_.

For other protocols and methods see [Default applications](/index.php/Default_applications "Default applications") for configuration.

#### Mouse and touchpad

To help reduce touchpad interference you may wish to implement the settings below:

*   Disable touchpad while typing
*   Disable scrolling
*   Disable tap-to-click

#### Network

[NetworkManager](/index.php/NetworkManager "NetworkManager") is the native tool of the GNOME project to control network settings from the shell. It is installed by default as a dependency for [tracker](https://www.archlinux.org/packages/?name=tracker) package, which is a part of [gnome](https://www.archlinux.org/groups/x86_64/gnome/) group, and just needs to be [enabled](/index.php/NetworkManager#Enable_NetworkManager "NetworkManager").

While any other [network manager](/index.php/List_of_applications/Internet#Network_managers "List of applications/Internet") can be used as well, NetworkManager provides the full integration via the shell network settings and a status indicator applet [network-manager-applet](https://www.archlinux.org/packages/?name=network-manager-applet) (not required for GNOME).

#### Online accounts

Backends for the GNOME messaging application [empathy](https://www.archlinux.org/packages/?name=empathy) as well as the GNOME Online Accounts section of the System Settings panel are provided in a separate group: [telepathy](https://www.archlinux.org/groups/x86_64/telepathy/). See [#Unable to add accounts in Empathy and GNOME Online Accounts](#Unable_to_add_accounts_in_Empathy_and_GNOME_Online_Accounts). Some online accounts, such as [ownCloud](/index.php/OwnCloud "OwnCloud"), require [gvfs-goa](https://www.archlinux.org/packages/?name=gvfs-goa) to be installed for full functionality in GNOME applications such as [GNOME Files](/index.php/GNOME_Files "GNOME Files") and GNOME Documents [[2]](https://wiki.gnome.org/ThreePointSeven/Features/Owncloud).

#### Search

The GNOME shell has a search that can be quickly accessed by pressing the `Super` key and starting to type. The [tracker](https://www.archlinux.org/packages/?name=tracker) package is installed by default as a part of [gnome](https://www.archlinux.org/groups/x86_64/gnome/) group and provides an indexing application and metadata database. It can be configured with the _Search and Indexing_ menu item; monitor status with _tracker-control_. It is started automatically by _gnome-session_ when the user logs in. Indexing can be started manually with `tracker-control -s`. Search settings can also be configured in the _System Settings_ panel.

The Tracker database can be queried using the _tracker-sparql_ command. View its manual page `man tracker-sparql` for more information.

### Advanced settings

As noted above, many configuration options such as changing the [GTK+](/index.php/GTK%2B "GTK+") theme or the [window manager](/index.php/Window_manager "Window manager") theme are not exposed in the GNOME System Settings panel (_gnome-control-center_). Those users that want to configure these settings may wish to use the GNOME Tweak Tool ([gnome-tweak-tool](https://www.archlinux.org/packages/?name=gnome-tweak-tool)), a convenient graphical tool which exposes many of these settings.

GNOME settings (which are stored in the DConf database) can also be configured using the [_dconf-editor_](https://developer.gnome.org/dconf/unstable/dconf-editor.html) (a graphical DConf configuration tool) or the [_gsettings_](https://developer.gnome.org/gio/stable/GSettings.html) command line tool. The GNOME Tweak Tool does not do anything else in the background of the GUI; note though that you will not find all settings described in the following sections in it.

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
*   [GTK3 themes in the AUR](https://aur.archlinux.org/packages.php?O=0&K=gtk3&do_Search=Go).
*   [Cursor themes in the AUR](https://aur.archlinux.org/packages.php?O=0&K=xcursor&do_Search=Go&PP=50&SB=v&SO=d).
*   [Icon themes in the AUR](https://aur.archlinux.org/packages.php?O=0&K=icon-theme&do_Search=Go&PP=50&SB=v&SO=d).

Once installed, they can be selected using the GNOME Tweak Tool or GSettings - see below for GSettings commands:

For the GTK+ theme:

```
$ gsettings set org.gnome.desktop.interface gtk-theme _theme-name_

```

For the icon theme

```
$ gsettings set org.gnome.desktop.interface icon-theme _theme-name_

```

###### Global dark theme

GNOME will use the Adwaita light theme by default however a dark variant of this theme (called the Global Dark Theme) also exists and can be selected using the Tweak Tool or by editing the GTK+ 3 settings file - see [GTK+#Dark theme variant](/index.php/GTK%2B#Dark_theme_variant "GTK+"). Some applications such as Image Viewer (_eog_) use the dark theme by default. It should be noted that the Global Dark Theme only works with GTK+ 3 applications; some GTK+ 3 applications may only have partial support for the Global Dark theme. Qt and GTK+ 2 support for the Global Dark Theme may be added in the future.

##### Window manager themes

The window manager theme (the style of the window titlebars) can be set using the GNOME Tweak Tool or the following GSettings command:

```
$ gsettings set org.gnome.desktop.wm.preferences theme _theme-name_

```

###### Titlebar height

**Note:** As of GNOME 3.16, Mutter no longer uses Metacity themes. Instead, the titlebar decorations are themed using GTK+.

To change the titlebar height, create the following file, adjusting the padding as desired:

 `~/.config/gtk-3.0/gtk.css` 

```
.header-bar {
	padding-top: 3px;
	padding-bottom: 3px;
	font-size: 9px;
}

.header-bar .button {
	padding-top: 5px;
	padding-bottom: 5px;
}

```

###### Titlebar button order

To set the order for the GNOME window manager (Mutter, Metacity):

```
$ gsettings set org.gnome.desktop.wm.preferences button-layout ':minimize,maximize,close'

```

**Tip:** The colon indicates which side of the titlebar the window buttons will appear.

###### Hide titlebar when maximized

*   [Install](/index.php/Install "Install") [mutter-hide-legacy-decorations](https://aur.archlinux.org/packages/mutter-hide-legacy-decorations/). It changes a default setting in the window manager, so as to automatically hide the titlebar on legacy (non-headerbar) apps when they are maximized or tiled to the side.

*   [Install](/index.php/Install "Install") [maximus](https://aur.archlinux.org/packages/maximus/). To start the application, execute _maximus_ from a terminal. When running, the daemon will automatically maximize windows. It will undecorate maximized windows and redecorate them when they are unmaximized. If you do not want all windows to start maximized, run `maximus -m` instead. Note that this will only work with windows decorated by the window manager; applications that use client-side decoration such as [GNOME Files](/index.php/GNOME_Files "GNOME Files") will not be undecorated when maximized.

##### GNOME Shell themes

The theme of GNOME Shell itself is configurable. To use a Shell theme, firstly ensure that you have the [gnome-shell-extensions](https://www.archlinux.org/packages/?name=gnome-shell-extensions) package installed. Then enable the _User Themes_ extension, either through GNOME Tweak Tool or through the [GNOME Shell Extensions](https://extensions.gnome.org) webpage. Shell themes can then be loaded and selected using the GNOME Tweak Tool.

There are a number of GNOME Shell themes available [in the AUR](https://aur.archlinux.org/packages.php?O=0&K=gnome-shell-theme&do_Search=Go&PP=50&SB=v&SO=d).

Shell themes can also be downloaded from [gnome-look.org](http://gnome-look.org/index.php?xcontentmode=191).

#### Desktop

Various Desktop settings can be applied.

##### Icons on the Desktop

See [GNOME Files#Desktop Icons](/index.php/GNOME_Files#Desktop_Icons "GNOME Files").

##### Lock screen and background

When setting the Desktop or Lock screen background, it is important to note that the Pictures tab will only display pictures located in `/home/_username_/Pictures` folder. If you wish to use a picture not located in this folder, use the commands indicated below.

For the desktop background:

```
$ gsettings set org.gnome.desktop.background picture-uri 'file:///path/to/my/picture.jpg'

```

For the lock screen background

```
$ gsettings set org.gnome.desktop.screensaver picture-uri 'file:///path/to/my/picture.jpg'

```

#### Extensions

**Note:** The GNOME Shell browser plugin which allows users to install extensions from [extensions.gnome.org](https://extensions.gnome.org) is not compatible with Chrome/Chromium versions 35 and over. Users wishing to install extensions from the webpage will have to use a compatible browser such as [Firefox](/index.php/Firefox "Firefox") or [GNOME Web](/index.php/GNOME_Web "GNOME Web").

GNOME Shell can be customized with extensions per user or system-wide.

The catalogue of extensions is available at [extensions.gnome.org](https://extensions.gnome.org). By a user they can be installed and activated in the browser by setting the switch in the top left of the screen to **ON** and clicking **Install** on the resulting dialog (if the extension in question is not installed). After installation it is shown in the [extensions.gnome.org/local/](https://extensions.gnome.org/local/) tab, which has to be visited as well to check for available updates. Installed extensions can also be enabled or disabled using [gnome-tweak-tool](https://www.archlinux.org/packages/?name=gnome-tweak-tool).

More information about GNOME shell extensions is available on the [GNOME Shell Extensions about page](https://extensions.gnome.org/about/).

[Installing](/index.php/Installing "Installing") extensions via a package makes them available for all users of the system and automates the update process.

The [gnome-shell-extensions](https://www.archlinux.org/packages/?name=gnome-shell-extensions) package provides a set of extensions maintained as part of the GNOME project (many of the included extensions are used by the GNOME Classic session).

Users who want a taskbar but do not wish to use the GNOME Classic session may want to enable the _Window list_ extension (provided by the [gnome-shell-extensions](https://www.archlinux.org/packages/?name=gnome-shell-extensions) package).

#### Input methods

GNOME has integrated support for input methods through [IBus](/index.php/IBus "IBus"), only [ibus](https://www.archlinux.org/packages/?name=ibus) and the wanted input method engine (e.g. [ibus-libpinyin](https://www.archlinux.org/packages/?name=ibus-libpinyin) for Intelligent Pinyin) needed to be installed, after installation the input method engine can be added as a keyboard layout in GNOME's Regional & Language Settings.

#### Fonts

**Tip:** If you set the _Scaling factor_ to a value above 1.00, the Accessibility menu will be automatically enabled.

Fonts can be set for Window titles, Interface (applications), Documents and Monospace. See the Fonts tab in the Tweak Tool for the relevant options.

For hinting, RGBA will likely be desired as this fits most monitors types, and if fonts appear too blocked reduce hinting to _Slight_ or _None_.

#### Startup applications

To start certain applications on login, copy the relevant `.desktop` file from `/usr/share/applications/` to `~/.config/autostart/`.

The same effect can be achieved using the Tweak Tool.

**Tip:** If the plus sign button in the Tweak Tool's Startup Applications section is unresponsive, try start the Tweak Tool from the terminal using the following command: `gnome-tweak-tool`. See the following [forum thread](https://bbs.archlinux.org/viewtopic.php?pid=1413631#p1413631).

**Note:** The _gnome-session-properties_ dialog was removed as of GNOME 3.12\. It can be added back by [installing](/index.php/Install "Install") the [gnome-session-properties](https://aur.archlinux.org/packages/gnome-session-properties/) package.

#### Power

The basic power settings that may want to be altered (these example settings assume the user is using a laptop - change them as desired):

```
$ gsettings set org.gnome.settings-daemon.plugins.power button-power _hibernate_
$ gsettings set org.gnome.settings-daemon.plugins.power sleep-inactive-ac-timeout _3600_
$ gsettings set org.gnome.settings-daemon.plugins.power sleep-inactive-ac-type _hibernate_
$ gsettings set org.gnome.settings-daemon.plugins.power sleep-inactive-battery-timeout _1800_
$ gsettings set org.gnome.settings-daemon.plugins.power sleep-inactive-battery-type _hibernate_
$ gsettings set org.gnome.desktop.lockdown disable-lock-screen _true_

```

To keep a monitor active on lid close:

```
$ gsettings set org.gnome.settings-daemon.plugins.xrandr default-monitors-setup do-nothing

```

##### Configure behaviour on lid switch close

The GNOME Tweak Tool, as of version 3.17.1, can optionally _inhibit_ the _systemd_ setting for the lid close ACPI event.[[3]](http://ftp.gnome.org/pub/GNOME/sources/gnome-tweak-tool/3.17/gnome-tweak-tool-3.17.1.news) To _inhibit_ the setting, start the Tweak Tool and, under the power tab, check the _Don't suspend on lid close_ option. This means that the system will do nothing on lid close instead of suspending - the default behaviour. Checking the setting creates `~/.config/autostart/ignore-lid-switch-tweak.desktop` which will autostart the Tweak Tool's inhibitor.

If you do not want the system to suspend or do nothing on lid close, you will need to ensure that the setting described above is **not** checked and then configure _systemd_ with `HandleLidSwitch=_preferred_behaviour_` as described in [Power management#ACPI events](/index.php/Power_management#ACPI_events "Power management").

##### Change critical battery level action

The System Settings panel only allows the user to choose between _Suspend_ or _Hibernate_. To choose another option such as _Do Nothing_ open the `dconf-editor` and navigate to `org.gnome.settings-daemon.plugins.power`. Edit the `"critical-battery-action"` value to `"nothing"`.

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

Applications can also be sorted by their category (specified in their _.desktop_ file):

```
$ gsettings set org.gnome.desktop.app-folders.folder:/org/gnome/desktop/app-folders/folders/Sundry/ categories "['Office']"

```

If certain applications matching a category are not wanted in a certain folder, exclusions can be set:

```
$ gsettings set org.gnome.desktop.app-folders.folder:/org/gnome/desktop/app-folders/folders/Sundry/ excluded-apps "['libreoffice-draw.desktop']"

```

For further information, refer to the [app-folders schema](https://git.gnome.org/browse/gsettings-desktop-schemas/tree/schemas/org.gnome.desktop.app-folders.gschema.xml.in.in).

## Tips and tricks

Other GNOME system settings and tips.

### Keyboard

#### Turn on NumLock on login

Run the following command:

```
$ gsettings set org.gnome.settings-daemon.peripherals.keyboard numlock-state on

```

#### Hotkey alternatives

A lot of hotkeys can be changed via system settings menu. For example, to re-enable the show desktop keybinding:

_System settings_ > _Keyboard_ > _Shortcuts_ > _Navigation_ > _Hide all normal windows_

However, certain hotkeys cannot be changed directly via system settings. In order to change these keys, use _dconf-editor_. An example of particular note is the hotkey `Alt-` + ``` (the key above `Tab` on US keyboard layouts). In GNOME Shell it is pre-configured to cycle through windows of an application, however it is also a hotkey often used in the [Emacs](/index.php/Emacs "Emacs") editor. It can be changed by opening _dconf-editor_ and modifying the _switch-group_ key found in `org.gnome.desktop.wm.keybindings`.

It is possible to manually change the keys via an application's so-called **accel** map file. Where it is to be found is up to the application: For instance, Thunar's is at `~/.config/Thunar/accels.scm`, whereas Files's is located at `~/.config/nautilus/accels` and `~/.gnome2/accels/nautilus` on old release.

The file should contain a list of possible hotkeys, each unchanged line commented out with a leading ";" that has to be removed for a change to become active. For example to replace the hotkey used by Files to move files to the trash folder, change the line:

```
; (gtk_accel_path "<Actions>/DirViewActions/Trash" "<Primary>Delete")

```

to this:

```
(gtk_accel_path "<Actions>/DirViewActions/Trash" "Delete")

```

The file is regenerated regularly so do not comment the file. The uncommented line will stay but every comment you add will be lost.

#### Keyboard switch with command

To have keyboard shortcut **Alt** + **Shift** switch keyboards:

Open Gnome-Tweak-Tool (or Keyboard Settings, in GNOME 3.16) and set _Typing_ > _Modifiers-only input sources_ > _select Alt-shift_. For more information see also the forum [thread](https://bbs.archlinux.org/viewtopic.php?id=152127).

#### XkbOptions keyboard options

Using the **dconf-editor**, navigate to the key named `org.gnome.desktop.input-sources.xkb-options` and add desired XkbOptions (e.g. _caps:swapescape_) to the list.

See `/usr/share/X11/xkb/rules/xorg` for all XkbOptions and `/usr/share/X11/xkb/symbols/*` for the respective descriptions.

**Note:** To enable the `Ctrl+Alt+Backspace` combination to terminate Xorg, use the [gnome-tweak-tool](https://www.archlinux.org/packages/?name=gnome-tweak-tool). Within the **Tweak Tool**, navigate to _Typing > Key sequence to kill the X server_ and select the option `Ctrl+Alt+Backspace` from the dropdown menu.

#### De-bind Windows key

By default, the 'Windows key' will open the GNOME Shell overview mode. You can unbind this key by running the command below

```
$ gsettings set org.gnome.mutter overlay-key 'Foo'

```

### Disks

GNOME provides a disk utility to manipulate storage drive settings. These are some of its features:

*   **Enable write cache** is a feature that most hard drives provide. Data is cached and allocated at chosen times to improve system performance. Not recommended unless the computer has a backup battery pack or is a laptop as data would be lost on power failure.

	_Settings_ > _Drive Settings_ > _Write Cache_ > **On**

*   **Automatic Mount Options** can mount drives and partitions that are GPT based - will use default, recommended options.

**Warning:** This setting erases related [fstab](/index.php/Fstab "Fstab") entries

	_Partition Settings_ > _Edit Mount Options_ > _Automatic Mount Options_ > **On**

### Hiding applications from the menu

**Tip:** Desktop entries can be hidden by editing the `.desktop` files themselves. See [Desktop entries#Hide desktop entries](/index.php/Desktop_entries#Hide_desktop_entries "Desktop entries").

Use the _Main Menu_ application (provided by the [alacarte](https://www.archlinux.org/packages/?name=alacarte) package) to hide any applications you do not wish to show in the menu.

### Screencast recording

GNOME features built-in screencast recording with the **Ctrl** + **Shift** + **Alt** + **R** key combination. A red circle is displayed in the bottom right corner of the screen when the recording is in progress. After the recording is finished, a file named `Screencast from %d%u-%c.webm` is saved in the Videos directory. In order to use the screencast feature the gst plugins need to be installed.

### Screenshot

Default save directory:

```
$ gsettings set org.gnome.gnome-screenshot auto-save-directory file:///home/_USER_/Desktop

```

Check the _gnome-screenshot_ manual page for more options.

### Log out delay

To eliminate the default 60 second delay when logging out:

```
$ gsettings set org.gnome.SessionManager logout-prompt false

```

### Disable animations

To disable Shell animations (such as "Show Applications" and the wave animation in the top left activities hot corner), run:

```
$ gsettings set org.gnome.desktop.interface enable-animations false

```

### Retina (HiDPI) display support

GNOME introduced HiDPI support in version 3.10\. If your display does not provide the correct screen size through EDID, this can lead to incorrectly scaled UI elements. As a workaround you can open _dconf-editor_ and find the key `scaling-factor` in `org.gnome.desktop.interface`. Set it to `1` to get the standard scale.

Also see [HiDPI](/index.php/HiDPI "HiDPI").

### Passwords and keys (PGP Keys)

You can use the Passwords and Keys program (_seahorse_) to create a PGP key as it is a front end for [GnuPG](/index.php/GnuPG "GnuPG") and installs it as dependency. This may be useful in the future (for instance if to encrypt a file). Create a key as shown below (the process may take about 10 minutes):

_File_ > _New_ > _PGP Key_ > _Name_ > _Email_ > _Defaults_ > _Passphrase_.

### Terminal

#### Change default terminal size

The default size of a new terminal can be adjusted in the menu _Edit > Profile preferences_ .

#### New terminals adopt current directory

By default new terminals open in the `$HOME` directory. To have new terminals adopt the current working directory: `source /etc/profile.d/vte.sh`. Add the command to the shell configuration to retain the behaviour. [[4]](http://unix.stackexchange.com/questions/93476/gnome-terminal-keep-track-of-directory-in-new-tab)

#### Pad the terminal

To pad the terminal (create a small, invisible border between the window edges and the terminal contents) create the file below:

 `~/.config/gtk-3.0/gtk.css` 

```
VteTerminal,
TerminalScreen {
    padding: 10px 10px 10px 10px;
    -VteTerminal-inner-border: 10px 10px 10px 10px;
}
```

#### Disable blinking cursor

Since GNOME 3.8 and the migration to GSettings and DConf the key required to modify in order to disable the blinking cursor in the Terminal differs slightly in contrast to the old GConf key. To disable the blinking cursor in GNOME 3.8 and above use:

```
$ gsettings set org.gnome.desktop.interface cursor-blink false

```

To disable the blinking cursor in Terminal only use (make sure profile uid is correct one):

```
$ dconf write /org/gnome/terminal/legacy/profiles:/:b1dcc9dd-5262-4d8d-a863-c897e6d979b9/cursor-blink-mode "'off'"

```

Note that `gnome-settings-daemon`, from the package of the same name, must be running for this and other settings changes to take effect in GNOME applications - see [#Configuration](#Configuration).

#### Disable confirmation window when closing Terminal

The Terminal will always display a confirmation window when trying to close the window while one is logged in as root. To avoid this, execute the following:

```
$ gsettings set org.gnome.Terminal.Legacy.Settings confirm-close false

```

### Middle mouse button

By default, GNOME 3 disables middle mouse button emulation regardless of [Xorg](/index.php/Xorg "Xorg") settings (**Emulate3Buttons**). To enable middle mouse button emulation use:

```
$ gsettings set org.gnome.settings-daemon.peripherals.mouse middle-button-enabled true

```

### Enable button and menu icons

Since GTK+ 3.10, the GSettings key 'menus-have-icons' has been deprecated. Icons in buttons and menus can still be enabled by setting the following overrides:

```
$ gsettings set org.gnome.settings-daemon.plugins.xsettings overrides "{'Gtk/ButtonImages': <1>, 'Gtk/MenuImages': <1>}"

```

### Use custom colours and gradients for desktop background

To use custom colours and gradients for your desktop background, you will first need to set either a transparent picture or else a non-existent picture as your desktop background. For instance, the command below will set a non-existent picture as the background.

```
$ gsettings set org.gnome.desktop.background picture-uri none

```

At this point, the desktop background should be a flat colour - the default colour setting is for a deep blue.

For a different flat colour you need only change the primary colour setting:

```
$ gsettings set org.gnome.desktop.background primary-color <my color>

```

where <my color> is a hex value (such as _ffffff_ for white).

For a colour gradient, you will also need to change secondary colour setting `org.gnome.desktop.background secondary-color` and select a shading type. For instance, if you want a horizontal gradient, execute the following:

```
$ gsettings set org.gnome.desktop.background color-shading-type horizontal

```

If you are using a transparent picture as your background, you can set the opacity by executing the following:

```
$ gsettings set org.gnome.desktop.background picture-opacity <value>

```

where value is a number between 1 and 100 (100 for maximum opacity).

### Transitioning backgrounds

GNOME can transition between different wallpapers at specific time intervals. This is done by creating an XML file specifying the pictures to be used and the time interval. For more information on creating such files, see the following [article](http://www.linuxjournal.com/content/create-custom-transitioning-background-your-gnome-228-desktop).

Alternatively, a number of tools are available to automate the process:

*   **mkwlppr** — This script creates XML files that can act as dynamic wallpapers for GNOME by referring to multiple wallpapers.

	[http://pastebin.com/019G2rCy](http://pastebin.com/019G2rCy) || see [mkwlppr](http://pastebin.com/019G2rCy)

*   **[Wallpapoz](/index.php/Wallpapoz "Wallpapoz")** — Wallpapoz is a tool that provides dynamic wallpapers for GNOME and Xfce desktops.

	[https://vajrasky.wordpress.com/](https://vajrasky.wordpress.com/) || [wallpapoz](https://aur.archlinux.org/packages/wallpapoz/)

*   **CreBS** — A Python/GTK application used to create and set desktop wallpaper slideshows for GNOME.

	[http://www.obfuscatepenguin.net/](http://www.obfuscatepenguin.net/) || [crebs](https://aur.archlinux.org/packages/crebs/)

For setting the XML file as the default background, see [#Lock screen and background](#Lock_screen_and_background).

### Custom GNOME sessions

It is possible to create custom GNOME sessions which use the GNOME session manager but start different sets of components ([Openbox](/index.php/Openbox "Openbox") with [tint2](/index.php/Tint2 "Tint2") instead of GNOME Shell for example).

Two files are required for a custom GNOME session: a session file in `/usr/share/gnome-session/sessions/` which defines the components to be started and a [desktop entry](/index.php/Desktop_entry "Desktop entry") in `/usr/share/xsessions` which is read by the [display manager](/index.php/Display_manager "Display manager"). An example session file is provided below:

 `/usr/share/gnome-session/sessions/gnome-openbox.session` 

```
[GNOME Session]
Name=GNOME Openbox
RequiredComponents=openbox;tint2;gnome-settings-daemon;

```

And an example desktop file:

 `/usr/share/xsessions/gnome-openbox.desktop` 

```
[Desktop Entry]
Name=GNOME Openbox
Exec=gnome-session --session=gnome-openbox

```

**Note:** GNOME Session calls upon the `.desktop` files of each of the components to be started. If a component you wish to start does not provide a `.desktop` file, you must create a suitable desktop entry in a directory such as `/usr/local/share/applications`.

## Troubleshooting

### Shell freezes

In the event of a Shell freeze (which might be caused by certain appearance tweaks, malfunctioning extensions or perhaps a lack of available memory) restarting the Shell by pressing `Alt` + `F2` and then entering **r** may not be possible.

In this case, try switching to another TTY (**Ctrl** + **Alt** + **F2**) and entering the following command: `pkill -HUP gnome-shell`. It may take a few seconds before the Shell successfully restarts. Restarting the shell in this fashion should not log the user out but it is a good idea to try and ensure that all work is saved anyway.

If this fails, the [Xorg](/index.php/Xorg "Xorg") server will need to be restarted either by: `pkill X` for console logins or: `systemctl restart gdm` for GDM logins. Bear in mind that restarting the Xorg server will log the user out so try to ensure that all work is saved before attempting this.

### Incorrect application defaults

When installing applications for the first time you may find that GNOME has the wrong application associated to a certain protocols - for instance, _easytag_ becomes the folder handler instead of [GNOME Files](/index.php/GNOME_Files "GNOME Files").

For GNOME Files see the following page: [GNOME Files#Files is no longer the default file manager](/index.php/GNOME_Files#Files_is_no_longer_the_default_file_manager "GNOME Files").

For Document Viewer, run the following command:

```
$ xdg-mime default evince.desktop application/pdf

```

For other applications, default handler settings are detailed on the following page: [Default applications](/index.php/Default_applications "Default applications").

Optionally, you can [install](/index.php/Install "Install") [gnome-defaults-list](https://aur.archlinux.org/packages/gnome-defaults-list/). It will place your configuration file at `/etc/gnome/defaults.list`.

### Tracker & Documents do not list any local files

In order for Tracker (and, therefore, Documents) to detect your local files, they must be stored in an [XDG compliant directory](http://standards.freedesktop.org/basedir-spec/basedir-spec-latest.html) (such as 'Documents' or 'Music'). For more information, see [Xdg user directories](/index.php/Xdg_user_directories "Xdg user directories").

You can also configure Tracker to recursively search inside specific directories such as your home directory. These settings can be made using `tracker-preferences`.

### Unable to add accounts in Empathy and GNOME Online Accounts

Empathy, the engine behind integrated messaging, GNOME Online Accounts, and all other system settings based on messaging accounts will not function correctly unless the [telepathy](https://www.archlinux.org/groups/x86_64/telepathy/) group of packages or at least one of the backends ([telepathy-gabble](https://www.archlinux.org/packages/?name=telepathy-gabble), or [telepathy-haze](https://www.archlinux.org/packages/?name=telepathy-haze), for example) is [installed](/index.php/Install "Install"). View descriptions of _telepathy_ components on the [freedesktop.org telepathy wiki](http://telepathy.freedesktop.org/wiki/Components).

**Note:** [Avahi](/index.php/Avahi "Avahi") daemon is required for connecting with the People Nearby account, and also in order for some desktop extensions to work correctly like [Chat Status](https://extensions.gnome.org/extension/746/chat-status/)

### Cannot change settings in dconf-editor

When one cannot set settings in [dconf](https://www.archlinux.org/packages/?name=dconf), it is possible their dconf user settings are corrupt. In this case it is best to delete the user dconf files in `~/.config/dconf/user*` and set the settings in dconf-editor after.

### When an extension breaks the shell

When enabling shell extensions causes GNOME breakage, you should first remove the _user-theme_ and _auto-move-windows_ extensions from their installation directory.

The installation directory could be one of `~/.local/share/gnome‑shell/extensions`, `/usr/share/gnome‑shell/extensions` or `/usr/local/share/gnome‑shell/extensions`. Removing these two extension-containing folders may fix the breakage. Otherwise, isolate the problem extension with trial‑and‑error.

Removing or adding an extension-containing folder to the aforementioned directories removes or adds the corresponding extension to your system. Details on GNOME Shell extensions are available at the [GNOME web site.](https://live.gnome.org/GnomeShell/Extensions)

If you have trouble with uninstalling an extension via [extensions.gnome.org/local](https://extensions.gnome.org/local/), then probably they have been installed as system-wide extensions with the [gnome-shell-extensions](https://www.archlinux.org/packages/?name=gnome-shell-extensions) package. Removing the package again obviously affects all user accounts.

### Extensions do not work after GNOME 3 update

**Note:** Please bear in mind that whilst the methods below will allow you to **try** and activate an extension with an unsupported version of GNOME Shell, it is by no means a guarantee that the extension will work successfully. The most likely outcome of trying to activate such an extension is that GNOME Shell will crash and then restart.

Before trying the workarounds below, check if an update is available for the extension by visiting [extensions.gnome.org/local](https://extensions.gnome.org/local).

If there is no update for your current GNOME version yet, use the following command to disable version validation for extensions:

```
$ gsettings set org.gnome.shell disable-extension-version-validation true

```

Alternatively, you could modify the extension itself, changing the supported shell version to satisfy the version validation. See the method below.

Locate the folder where your extensions are installed. It might be `~/.local/share/gnome-shell/extensions` or `/usr/share/gnome-shell/extensions`.

Edit each occurrence of `metadata.json` which appears in each extension sub-folder.

| Insert: | `"shell-version": ["3.x"]` |
| Instead of (for example): | `"shell-version": ["3.4"]` |

`"3.x"` indicates the extension works with every shell version. If it breaks, you will know to change it back.

### Keyboard shortcut do not work with only conky running

The GNOME shell keyboard shortcuts like `Alt+F2`, `Alt+F1`, and the media key shortcuts do not work if conky is the only program running. However, if another application like _gedit_ is running, then the keyboard shortcuts work.

Solution: edit `.conkyrc`

```
own_window yes
own_window_transparent yes
own_window_argb_visual yes
own_window_type dock
own_window_class Conky
own_window_hints undecorated,below,sticky,skip_taskbar,skip_pager

```

### Unable to apply stored configuration for monitors

If you encounter this message try to disable the _xrandr_ `gnome-settings-daemon plugin`:

```
$ dconf write /org/gnome/settings-daemon/plugins/xrandr/active false

```

### Consistent cursor theme

See [Cursor themes#Desktop environments](/index.php/Cursor_themes#Desktop_environments "Cursor themes").

### Windows cannot be modified with Alt-Key + mouse-button

In GNOME 3.6 and above, the mouse button modifier (the key that allows you to drag a window from a location other than the titlebar) is the `Super` key instead of the `Alt` key which was used in the past. The change was made in response to the following [bug report](https://bugzilla.gnome.org/show_bug.cgi?id=607797).

To change the mouse button modifier back to the `Alt` key, execute the following:

```
$ gsettings set org.gnome.desktop.wm.preferences mouse-button-modifier '<Alt>'  

```

**Note:** It is not possible to change this with _System settings_ > _Keyboard_ > _Shortcuts_

### Slow loading of system icons/slow GDM login

Problems with the loading of system icons, such the ones in the title bar of Files, might be solved by executing the following command:

```
# gdk-pixbuf-query-loaders --update-cache

```

Running the aforementioned command may also fix repeated occurrences of the "Oh no! Something has gone wrong!" error screen and/or very slow loading and login with GDM as described in the following [forum thread](https://bbs.archlinux.org/viewtopic.php?pid=1414157).

### Artifacts when maximizing windows

Maximizing windows may cause artifacts as of GNOME 3.12.0 - see the following [forum thread](https://bbs.archlinux.org/viewtopic.php?id=183617) and [bug report](https://bugzilla.gnome.org/show_bug.cgi?id=728385). A solution is detailed in the following section: [#Tear-free video with Intel HD Graphics](#Tear-free_video_with_Intel_HD_Graphics).

### Tear-free video with Intel HD Graphics

	DRI3

According to [this bug report](https://bugzilla.gnome.org/show_bug.cgi?id=711028#c2), DRI3 includes the `buffer_age` extension that allows GNOME Shell's Mutter compositor to sync windows to vblank in an efficient way. [Enable](/index.php/Intel_Graphics#Direct_Rendering_Infrastructure_3_.28DRI3.29 "Intel Graphics") it in the Xorg driver. You can change `AccelMethod` to your preference in the configuration file created, but the line must be included when the file is created; otherwise, `gnome-session` will crash upon login in a non-Wayland session.

	Intel TearFree

Enabling the [Xorg Intel TearFree option](/index.php/Intel_Graphics#Tear-free_video "Intel Graphics") is a known workaround for tearing problems on Intel adapters. However, the way this option acts makes it redundant with the use of a compositor (it increases memory consumption and lowers performance, see [the original bug report's final comment](https://bugs.freedesktop.org/show_bug.cgi?id=37686#c123)).

	Mutter tweaks

**Note:** This workaround has been [reported](https://bugzilla.gnome.org/show_bug.cgi?id=711028#c0) to have side effects and may not fix tearing in all cases.

GNOME Shell's Mutter compositor has a tweak known to address tearing problems (see [the original suggestion for this fix](https://bugzilla.gnome.org/show_bug.cgi?id=657071#c1) and its mention in [the Freedesktop bug report](https://bugs.freedesktop.org/show_bug.cgi?id=37686#c59)). To enable this tweak, append the following line to `/etc/environment`: `CLUTTER_PAINT=disable-clipped-redraws:disable-culling`. Then restart the Xorg server.

### Window opens behind other windows when using multiple monitors

This is possibly a bug in GNOME Shell which causes new windows to open behind others. To fix this issue, one can run the following command:

```
$ gsettings set org.gnome.shell.overrides workspaces-only-on-primary false

```

### Lock button fails to re-enable touchpad

Some laptops have a touchpad lock button that disables the touchpad so that users can type without worrying about touching the touchpad. Currently, it appears that although GNOME can lock the touchpad by pressing this button, it cannot unlock it. If the touchpad gets locked you can run the following to unlock it:

```
$ xinput set-prop "SynPS/2 Synaptics TouchPad" "Device Enabled" 1

```

### GNOME Shell keyboard sources menu not visible

A menu showing the keyboard input sources (for example 'en' for an English keyboard layout) should be visible next to the status area containing icons for network, volume and power sources. If the keyboard sources menu is not visible, this is probably because you have configured your [Xorg](/index.php/Xorg "Xorg") keyboard layout in a way which GNOME does not recognise.

To ensure that the menu is visible, remove any Xorg keyboard configuration you might have created and set the keyboard locale using [localectl](/index.php/Keyboard_configuration_in_Xorg#Using_localectl "Keyboard configuration in Xorg").

Upon running the command and then logging out, you should find that the keyboard input sources menu is visible in GDM and in the GNOME Shell desktop. See [Input sources in GNOME](http://blogs.gnome.org/mclasen/2012/09/21/input-sources-in-gnome/) for more information.

### Mouse cursor missing

When using a separate [window manager](/index.php/Window_manager "Window manager") with _gnome-settings-daemon_, the mouse cursor may vanish. Run:

```
$ gsettings set org.gnome.settings-daemon.plugins.cursor active false

```

### No restart button in session menu when screen is locked

If [XScreenSaver](/index.php/XScreenSaver "XScreenSaver") is installed, ensure that it is not running at startup, see [#Startup applications](#Startup_applications).

### PulseAudio system-wide causes delay in GNOME and GDM

If you are running [PulseAudio](/index.php/PulseAudio "PulseAudio") in system-wide mode, the PulseAudio 7.0 upgrade breaks [GDM](/index.php/GDM "GDM") and GNOME. See [this forum post](https://bbs.archlinux.org/viewtopic.php?id=203051) for more information.

### GNOME crashes when trying to reorder applications in the GNOME Shell Dash

The dash is the "toolbar" that appears, by default, [on the left](https://en.wikipedia.org/wiki/GNOME_Shell#Design_components "wikipedia:GNOME Shell") when you click Activities. Applications can be reordered in the dash by dragging and dropping. If this fails, and/or causes GNOME to crash, try [changing your icon theme](https://bbs.archlinux.org/viewtopic.php?id=171689).

## See also

*   [The Official Website of GNOME](http://www.gnome.org/)
*   [Extensions for GNOME-shell](http://extensions.gnome.org/)
*   [GNOME Shell Cheat Sheet](https://wiki.gnome.org/Projects/GnomeShell/CheatSheet), commands, keyboard shortcuts and other tips for using GNOME Shell.
*   Themes, icons, and backgrounds:
    *   [GNOME Art](http://art.gnome.org/)
    *   [GNOME Look](http://www.gnome-look.org/)
*   GTK/GNOME programs:
    *   [GNOME Files](http://www.gnomefiles.org/)
    *   [GNOME Project Listing](http://www.gnome.org/projects/)
*   [Customizing the GNOME Shell](http://blog.fpmurphy.com/2011/03/customizing-the-gnome-3-shell.html)