Related articles

*   [GTK+](/index.php/GTK%2B "GTK+")
*   [GDM](/index.php/GDM "GDM")
*   [GNOME/Tips and tricks](/index.php/GNOME/Tips_and_tricks "GNOME/Tips and tricks")
*   [GNOME/Troubleshooting](/index.php/GNOME/Troubleshooting "GNOME/Troubleshooting")
*   [GNOME/Files](/index.php/GNOME/Files "GNOME/Files")
*   [GNOME/Gedit](/index.php/GNOME/Gedit "GNOME/Gedit")
*   [GNOME/Web](/index.php/GNOME/Web "GNOME/Web")
*   [GNOME/Evolution](/index.php/GNOME/Evolution "GNOME/Evolution")
*   [GNOME/Flashback](/index.php/GNOME/Flashback "GNOME/Flashback")
*   [GNOME/Keyring](/index.php/GNOME/Keyring "GNOME/Keyring")
*   [GNOME/Document viewer](/index.php/GNOME/Document_viewer "GNOME/Document viewer")
*   [Official repositories#gnome-unstable](/index.php/Official_repositories#gnome-unstable "Official repositories")

[GNOME](https://en.wikipedia.org/wiki/GNOME "wikipedia:GNOME") (/(ɡ)noʊm/) is a [desktop environment](/index.php/Desktop_environment "Desktop environment") that aims to be simple and easy to use. It is designed by [The GNOME Project](https://en.wikipedia.org/wiki/The_GNOME_Project "wikipedia:The GNOME Project") and is composed entirely of free and open-source software. GNOME is a part of the [GNU Project](/index.php/GNU_Project "GNU Project"). The default display is [Wayland](/index.php/Wayland "Wayland") instead of [Xorg](/index.php/Xorg "Xorg").

## Contents

*   [1 Installation](#Installation)
*   [2 GNOME Sessions](#GNOME_Sessions)
*   [3 Starting](#Starting)
    *   [3.1 Graphically](#Graphically)
    *   [3.2 Manually](#Manually)
        *   [3.2.1 Xorg sessions](#Xorg_sessions)
        *   [3.2.2 Wayland sessions](#Wayland_sessions)
    *   [3.3 GNOME applications in Wayland](#GNOME_applications_in_Wayland)
*   [4 Navigation](#Navigation)
*   [5 Legacy names](#Legacy_names)
*   [6 Configuration](#Configuration)
    *   [6.1 System settings](#System_settings)
        *   [6.1.1 Color](#Color)
        *   [6.1.2 Night Light](#Night_Light)
        *   [6.1.3 Date & time](#Date_&_time)
        *   [6.1.4 Default applications](#Default_applications)
        *   [6.1.5 Mouse and touchpad](#Mouse_and_touchpad)
        *   [6.1.6 Network](#Network)
        *   [6.1.7 Online accounts](#Online_accounts)
        *   [6.1.8 Search](#Search)
    *   [6.2 Advanced settings](#Advanced_settings)
        *   [6.2.1 Appearance](#Appearance)
            *   [6.2.1.1 Themes](#Themes)
            *   [6.2.1.2 Titlebar height](#Titlebar_height)
            *   [6.2.1.3 Titlebar button order](#Titlebar_button_order)
            *   [6.2.1.4 Hide titlebar when maximized](#Hide_titlebar_when_maximized)
            *   [6.2.1.5 GNOME Shell themes](#GNOME_Shell_themes)
            *   [6.2.1.6 Icons on menu](#Icons_on_menu)
        *   [6.2.2 Apps grid folders](#Apps_grid_folders)
        *   [6.2.3 Autostart](#Autostart)
        *   [6.2.4 Desktop](#Desktop)
            *   [6.2.4.1 Icons on the Desktop](#Icons_on_the_Desktop)
            *   [6.2.4.2 Lock screen and background](#Lock_screen_and_background)
            *   [6.2.4.3 Disable top left hot corner](#Disable_top_left_hot_corner)
        *   [6.2.5 Extensions](#Extensions)
        *   [6.2.6 Fonts](#Fonts)
        *   [6.2.7 Input methods](#Input_methods)
        *   [6.2.8 Power](#Power)
            *   [6.2.8.1 Don't suspend, when laptop lid is closed](#Don't_suspend,_when_laptop_lid_is_closed)
            *   [6.2.8.2 Change critical battery level action](#Change_critical_battery_level_action)
    *   [6.3 Use a different window manager](#Use_a_different_window_manager)
*   [7 See also](#See_also)

## Installation

Two groups are available:

*   [gnome](https://www.archlinux.org/groups/x86_64/gnome/) contains the base GNOME desktop and a subset of well-integrated [applications](https://wiki.gnome.org/Apps);
*   [gnome-extra](https://www.archlinux.org/groups/x86_64/gnome-extra/) contains further GNOME applications, including an archive manager, disk manager, [text editor](/index.php/Gedit "Gedit"), and a set of games. Note that this group builds on the [gnome](https://www.archlinux.org/groups/x86_64/gnome/) group.

The base desktop consists of [GNOME Shell](https://en.wikipedia.org/wiki/GNOME_Shell window manager. It can be installed separately with [gnome-shell](https://www.archlinux.org/packages/?name=gnome-shell).

**Note:** *mutter* acts as a composite manager for the desktop, employing hardware graphics acceleration to provide effects aimed at reducing screen clutter. The GNOME session manager automatically detects if your video driver is capable of running GNOME Shell and if not, falls back to software rendering using *llvmpipe*.

## GNOME Sessions

GNOME has three available sessions, all using GNOME Shell.

*   **GNOME** is the default which uses Wayland. Traditional X applications are run through Xwayland.
*   **GNOME Classic** is a traditional desktop layout with a similar interface to GNOME 2, using pre-activated extensions and parameters. [[1]](http://worldofgnome.org/welcome-to-gnome-3-8-flintstones-mode/) Hence it is more a customized GNOME Shell than a truly distinct mode.
*   **GNOME on Xorg** runs GNOME Shell using Xorg.

## Starting

GNOME can be started either graphically with a [display manager](/index.php/Display_manager "Display manager") or manually from the console (some features may be missing).

**Note:** Support for screen locking (and more) in GNOME is provided by GDM. If GNOME is not started with GDM, another screen locker may be used. See [List of applications/Security#Screen lockers](/index.php/List_of_applications/Security#Screen_lockers "List of applications/Security").

### Graphically

Select the session: *GNOME*, *GNOME Classic*, or *GNOME on Xorg* from the display manager's session menu.

### Manually

#### Xorg sessions

*   For the GNOME on Xorg session, add to the `~/.xinitrc` file:
    ```
    export GDK_BACKEND=x11
    exec gnome-session
    ```

*   For the GNOME Classic session, add to the `~/.xinitrc` file:
    ```
    export XDG_CURRENT_DESKTOP=GNOME-Classic:GNOME
    export GNOME_SHELL_SESSION_MODE=classic
    exec gnome-session --session=gnome-classic
    ```

After editing the `~/.xinitrc` file, GNOME can be launched with the `startx` command (see [xinitrc](/index.php/Xinitrc "Xinitrc") for additional details, such as preserving the logind session). After setting up the `~/.xinitrc` file it can also be arranged to [Start X at login](/index.php/Start_X_at_login "Start X at login").

#### Wayland sessions

**Note:**

*   An X server—provided by the [xorg-server-xwayland](https://www.archlinux.org/packages/?name=xorg-server-xwayland) package—is still necessary to run applications that have not yet been ported to [Wayland](/index.php/Wayland "Wayland").
*   Wayland with the proprietary [NVIDIA](/index.php/NVIDIA "NVIDIA") driver currently suffers from very poor performance: [FS#53284](https://bugs.archlinux.org/task/53284).

Manually starting a Wayland session is possible with `XDG_SESSION_TYPE=wayland dbus-run-session gnome-session`.

To start on login to tty1, add the following to your `.bash_profile`:

```
if [[ -z $DISPLAY ]] && [[ $(tty) = /dev/tty1 ]] && [[ -z $XDG_SESSION_TYPE ]]; then
  XDG_SESSION_TYPE=wayland exec dbus-run-session gnome-session
fi

```

### GNOME applications in Wayland

When the *GNOME* session is used, GNOME applications will be run using Wayland. For debugging cases, the [GTK+ manual](https://developer.gnome.org/gtk3/stable/gtk-running.html) lists options and environment variables.

## Navigation

To learn how to use the GNOME shell effectively read the [GNOME Shell Cheat Sheet](https://wiki.gnome.org/Projects/GnomeShell/CheatSheet); it highlights GNOME shell features and keyboard shortcuts. Features include task switching, keyboard use, window control, the panel, overview mode, and more. A few of the shortcuts are:

*   `Super` + `m`: show message tray
*   `Super` + `a`: show applications menu
*   `Alt` + `Tab`: cycle active applications
*   `Alt` + ``` (the key above `Tab` on US keyboard layouts): cycle windows of the application in the foreground
*   `Alt` + `F2`, then enter `r` or `restart`: restart the shell in case of graphical shell problems (only in X/legacy mode, not in Wayland mode).

## Legacy names

**Note:** Some GNOME programs have undergone name changes where the application's name in documentation and about dialogs has been changed but the executable name has not. A few such applications are listed in the table below.

**Tip:** Searching for the legacy name of an application in the Shell search bar will successfully return the application in question. For instance, searching for *nautilus* will return *Files*.

| Current | Legacy |
| [Files](/index.php/GNOME/Files "GNOME/Files") | Nautilus |
| [Web](/index.php/GNOME/Web "GNOME/Web") | Epiphany |
| Videos | Totem |
| Main Menu | Alacarte |
| [Document Viewer](/index.php/GNOME/Document_viewer "GNOME/Document viewer") | Evince |
| Disk Usage Analyzer | Baobab |
| Image Viewer | EoG (Eye of GNOME) |
| [Passwords and Keys](/index.php/GNOME/Keyring "GNOME/Keyring") | Seahorse |
| GNOME Translation Editor | Gtranslator |

## Configuration

The GNOME System Settings panel (*gnome-control-center*) and GNOME applications use the [dconf](https://en.wikipedia.org/wiki/Dconf "wikipedia:Dconf") configuration system to store their settings.

You can directly access the dconf database using the `gsettings` or `dconf` command line tools. This also allows you to configure settings not exposed by the user interfaces.

Up until GNOME 3.24 settings were applied by the GNOME settings daemon, which could be run outside of a GNOME session using:

```
$ nohup /usr/lib/gnome-settings-daemon/gnome-settings-daemon > /dev/null &

```

GNOME 3.24 however replaced the GNOME settings daemon with several separate settings plugins `/usr/lib/gnome-settings-daemon/gsd-*`. These plugins are now controlled via desktop files under `/etc/xdg/autostart` (org.gnome.SettingsDaemon.*.desktop). To run these plugins outside of a GNOME session you will now need to copy/edit the appropriate [desktop entries](/index.php/Desktop_entries "Desktop entries") to `~/.config/autostart`.

The configuration is usually performed user-specific, this section does not cover how to create configuration templates for multiple users.

### System settings

#### Color

The daemon `colord` reads the display's EDID and extracts the appropriate color profile. Most color profiles are accurate and no setup is required; however for those that are not accurate, or for older displays, color profiles can be put in `~/.local/share/icc/` and directed to.

#### Night Light

GNOME comes with a built-in blue light filter similar to [Redshift](/index.php/Redshift "Redshift"). You can enable and customise the time you want to enable Night Light from the display settings menu. Furthermore, you can tweak the kelvin temperature with the following [dconf](https://www.archlinux.org/packages/?name=dconf) setting, where 5000 is an example value:

```
$ gsettings set org.gnome.settings-daemon.plugins.color night-light-temperature 5000

```

**Tip:** To change the daytime temperature in a Wayland session install [this extension](https://extensions.gnome.org/extension/1276/night-light-slider/).

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

Upon installing GNOME for the first time, you may find that the wrong applications are handling certain protocols. For example, *totem* opens videos instead of a previously used [VLC](/index.php/VLC "VLC"). Some of the associations can be set from system settings via: *Details* > *Default applications*.

For other protocols and methods see [Default applications](/index.php/Default_applications "Default applications") for configuration.

#### Mouse and touchpad

Most touchpad settings can be set from system settings via: *Devices* > *Mouse & Touchpad*.

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

or via [gnome-tweaks](https://www.archlinux.org/packages/?name=gnome-tweaks).

**Note:** The [synaptics](/index.php/Synaptics "Synaptics") driver is not supported by GNOME. Instead, you should use [libinput](/index.php/Libinput "Libinput"). See [this bug report](https://bugzilla.gnome.org/show_bug.cgi?id=764257#c12).

#### Network

[NetworkManager](/index.php/NetworkManager "NetworkManager") is the native tool of the GNOME project to control network settings from the shell. [Install](/index.php/Install "Install") the [networkmanager](https://www.archlinux.org/packages/?name=networkmanager) package and [enable](/index.php/Enable "Enable") the `NetworkManager.service` systemd unit.

While any other [network manager](/index.php/Network_manager "Network manager") can be used as well, NetworkManager provides the full integration via the shell network settings and a status indicator applet [network-manager-applet](https://www.archlinux.org/packages/?name=network-manager-applet) (not required for GNOME).

#### Online accounts

Backends for the GNOME messaging application [empathy](https://www.archlinux.org/packages/?name=empathy) as well as the GNOME Online Accounts section of the System Settings panel are provided in a separate group: [telepathy](https://www.archlinux.org/groups/x86_64/telepathy/). See [Unable to add accounts in Empathy and GNOME Online Accounts](/index.php/GNOME/Troubleshooting#Unable_to_add_accounts_in_Empathy_and_GNOME_Online_Accounts "GNOME/Troubleshooting"). Some online accounts, such as [ownCloud](/index.php/OwnCloud "OwnCloud"), require [gvfs-goa](https://www.archlinux.org/packages/?name=gvfs-goa) to be installed for full functionality in GNOME applications such as [GNOME Files](/index.php/GNOME_Files "GNOME Files") and GNOME Documents [[2]](https://wiki.gnome.org/ThreePointSeven/Features/Owncloud).

#### Search

The GNOME shell has a search that can be quickly accessed by pressing the `Super` key and starting to type. The [tracker](https://www.archlinux.org/packages/?name=tracker) package is installed by default as a part of [gnome](https://www.archlinux.org/groups/x86_64/gnome/) group and provides an indexing application and metadata database. It can be configured with the *Search and Indexing* menu item; monitor status with *tracker-control*. It is started automatically by *gnome-session* when the user logs in. Indexing can be started manually with `tracker-control -s`. Search settings can also be configured in the *System Settings* panel.

The Tracker database can be queried using the *tracker-sparql* command. View its manual page [tracker-sparql(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/tracker-sparql.1) for more information.

### Advanced settings

As noted above, many configuration options such as changing the [GTK+](/index.php/GTK%2B "GTK+") theme or the [window manager](/index.php/Window_manager "Window manager") theme are not exposed in the GNOME System Settings panel (*gnome-control-center*). Those users that want to configure these settings may wish to use the GNOME Tweaks ([gnome-tweaks](https://www.archlinux.org/packages/?name=gnome-tweaks)), a convenient graphical tool which exposes many of these settings.

GNOME settings (which are stored in the DConf database) can also be configured using the [*dconf-editor*](https://developer.gnome.org/dconf/unstable/dconf-editor.html) (a graphical DConf configuration tool) or the [*gsettings*](https://developer.gnome.org/gio/stable/GSettings.html) command line tool. The GNOME Tweaks does not do anything else in the background of the GUI; note though that you will not find all settings described in the following sections in it.

#### Appearance

##### Themes

GNOME uses Adwaita by default. To apply Adwaita dark only to GTK+2 applications use the following symlink:

```
$ ln -s /usr/share/themes/Adwaita-dark ~/.themes/Adwaita

```

To select new themes (move them to the appropriate directory and) use GNOME Tweaks or the GSettings commands below:

For the GTK+ theme:

```
$ gsettings set org.gnome.desktop.interface gtk-theme *theme-name*

```

For the icon theme:

```
$ gsettings set org.gnome.desktop.interface icon-theme *theme-name*

```

**Note:** The window manager theme follows the GTK+ theme. Using `org.gnome.desktop.wm.preferences theme` is deprecated and ignored.

See [GTK+#Themes](/index.php/GTK%2B#Themes "GTK+") and [Icons#Manually](/index.php/Icons#Manually "Icons").

##### Titlebar height

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

##### Titlebar button order

To set the order for the GNOME window manager (Mutter, Metacity):

```
$ gsettings set org.gnome.desktop.wm.preferences button-layout ':minimize,maximize,close'

```

**Tip:** The colon indicates which side of the titlebar the window buttons will appear.

##### Hide titlebar when maximized

*   [Install](/index.php/Install "Install") [gnome-shell-extension-no-title-bar-git](https://aur.archlinux.org/packages/gnome-shell-extension-no-title-bar-git/) or [gnome-shell-extension-no-title-bar](https://aur.archlinux.org/packages/gnome-shell-extension-no-title-bar/). Maximized windows get the title bar merged into the activity bar.
*   [Install](/index.php/Install "Install") [mutter-hide-legacy-decorations](https://aur.archlinux.org/packages/mutter-hide-legacy-decorations/). It changes a default setting in the window manager, so as to automatically hide the titlebar on legacy (non-headerbar) apps when they are maximized or tiled to the side.
*   [Install](/index.php/Install "Install") [gnome-shell-extension-pixel-saver-git](https://aur.archlinux.org/packages/gnome-shell-extension-pixel-saver-git/) or [gnome-shell-extension-pixel-saver](https://aur.archlinux.org/packages/gnome-shell-extension-pixel-saver/). Maximized windows get the title bar merged into the activity bar, saving precious pixels.

##### GNOME Shell themes

The theme of GNOME Shell itself is configurable. To use a Shell theme, firstly ensure that you have the [gnome-shell-extensions](https://www.archlinux.org/packages/?name=gnome-shell-extensions) package installed. Then enable the *User Themes* extension, either through GNOME Tweaks or through the [GNOME Shell Extensions](https://extensions.gnome.org) webpage. Shell themes can then be loaded and selected using the GNOME Tweaks.

There are a number of GNOME Shell themes available [in the AUR](https://aur.archlinux.org/packages.php?O=0&K=gnome-shell-theme&do_Search=Go&PP=50&SB=v&SO=d). Shell themes can also be downloaded from [gnome-look.org](http://gnome-look.org/).

##### Icons on menu

The default GNOME schema doesn't display any icon on menus. To display icons on menus, issue the following command.

```
$ gsettings set org.gnome.settings-daemon.plugins.xsettings overrides "{'Gtk/ButtonImages': <1>, 'Gtk/MenuImages': <1>}"

```

#### Apps grid folders

**Tip:** The [gnome-catgen](https://github.com/prurigro/gnome-catgen) ([gnome-catgen-git](https://aur.archlinux.org/packages/gnome-catgen-git/)) script allows you to manage folders through the creation of files in `~/.local/share/applications-categories` named after each category and containing a list of the desktop files belonging to apps you would like to have inside. Optionally, you can have it cycle through each app without a folder and input the desired category until you `Ctrl-c` or run out of apps.

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

For more information, see [[4]](https://git.gnome.org/browse/gsettings-desktop-schemas/tree/schemas/org.gnome.desktop.app-folders.gschema.xml.in) and [[5]](https://wiki.gentoo.org/wiki/Gnome_Applications_Folders).

#### Autostart

GNOME implements [XDG Autostart](/index.php/XDG_Autostart "XDG Autostart").

The [gnome-tweaks](https://www.archlinux.org/packages/?name=gnome-tweaks) allows managing autostart-entries.

**Tip:** If the plus sign button in the Tweaks's Startup Applications section is unresponsive, try start the Tweaks from the terminal using the following command: `gnome-tweaks`. See the following [forum thread](https://bbs.archlinux.org/viewtopic.php?pid=1413631#p1413631).

**Note:** The deprecated *gnome-session-properties* dialog can be added by [installing](/index.php/Install "Install") the [gnome-session-properties](https://aur.archlinux.org/packages/gnome-session-properties/) package.

#### Desktop

##### Icons on the Desktop

Up until GNOME 3.28, icons on the desktop were provided by [Files](/index.php/Files "Files") which would draw a transparent window over the desktop containing the icons. As of GNOME 3.28 this functionality has been removed and desktop icons are no longer available in GNOME. Possible workarounds include using [Nemo](/index.php/Nemo "Nemo") (a fork of Files which still has desktop icons functionality) or installing [gnome-shell-extension-desktop-icons](https://aur.archlinux.org/packages/gnome-shell-extension-desktop-icons/) which partially replicates the desktop icon functionality available in GNOME 3.26 and prior. For more information, please see the following [Arch forum thread](https://bbs.archlinux.org/viewtopic.php?id=235633).

##### Lock screen and background

When setting the Desktop or Lock screen background, it is important to note that the Pictures tab will only display pictures located in `/home/*username*/Pictures` folder. If you wish to use a picture not located in this folder, use the commands indicated below.

For the desktop background:

```
$ gsettings set org.gnome.desktop.background picture-uri 'file:///path/to/my/picture.jpg'

```

For the lock screen background:

```
$ gsettings set org.gnome.desktop.screensaver picture-uri 'file:///path/to/my/picture.jpg'

```

##### Disable top left hot corner

You can disable the top left hot corner with the [gnome-shell-extension-no-topleft-hot-corner](https://aur.archlinux.org/packages/gnome-shell-extension-no-topleft-hot-corner/) package.

#### Extensions

The catalogue of extensions is available at [extensions.gnome.org](https://extensions.gnome.org). They can be installed and activated in a browser by setting the switch in the top left of the screen to **ON** and clicking **Install** on the popup window (if the extension in question is not installed). Installed extensions may be seen at [extensions.gnome.org/local](https://extensions.gnome.org/local/), where available updates can be checked. Installed extensions can also be enabled or disabled with [gnome-tweaks](https://www.archlinux.org/packages/?name=gnome-tweaks).

**Note:** Extensions from [extensions.gnome.org](https://extensions.gnome.org) can be installed right away with [GNOME/Web](/index.php/GNOME/Web "GNOME/Web"). For other browsers, it is required to install [chrome-gnome-shell](https://www.archlinux.org/packages/?name=chrome-gnome-shell) and the appropriate browser extension.

GNOME Shell can be customized with extensions per user or system-wide. Installing extensions with [pacman](/index.php/Pacman "Pacman") makes them available for all users of the system and automates the update process. The [gnome-shell-extensions](https://www.archlinux.org/packages/?name=gnome-shell-extensions) package provides a set of extensions maintained as part of the GNOME project (many of the included extensions are used by the GNOME Classic session). Users who want a taskbar but do not wish to use the GNOME Classic session may want to enable the *Window list* extension (provided by the [gnome-shell-extensions](https://www.archlinux.org/packages/?name=gnome-shell-extensions) package).

To list currently enabled extensions:

```
$ gsettings get org.gnome.shell enabled-extensions

```

For more information about GNOME shell extensions, see [[6]](https://extensions.gnome.org/about/).

#### Fonts

**Tip:** If you set the *Scaling factor* to a value above 1.00, the Accessibility menu will be automatically enabled.

Fonts can be set for Window titles, Interface (applications), Documents and Monospace. See the Fonts tab in the Tweaks for the relevant options.

For hinting, RGBA will likely be desired as this fits most monitors types, and if fonts appear too blocked reduce hinting to *Slight* or *None*.

#### Input methods

GNOME has integrated support for [input methods](/index.php/Input_method "Input method") through [IBus](/index.php/IBus "IBus"), only [ibus](https://www.archlinux.org/packages/?name=ibus) and the wanted input method engine (e.g. [ibus-libpinyin](https://www.archlinux.org/packages/?name=ibus-libpinyin) for Intelligent Pinyin) needed to be installed, after installation the input method engine can be added as a keyboard layout in GNOME's Regional & Language Settings.

#### Power

When you are using a laptop you might want to alter the following settings:

```
$ gsettings set org.gnome.settings-daemon.plugins.power sleep-inactive-ac-timeout *3600*
$ gsettings set org.gnome.settings-daemon.plugins.power sleep-inactive-ac-type *hibernate*
$ gsettings set org.gnome.settings-daemon.plugins.power sleep-inactive-battery-timeout *1800*
$ gsettings set org.gnome.settings-daemon.plugins.power sleep-inactive-battery-type *hibernate*
$ gsettings set org.gnome.settings-daemon.plugins.power power-button-action *suspend*
$ gsettings set org.gnome.desktop.lockdown disable-lock-screen *true*

```

To keep the monitor active when the lid is closed:

```
$ gsettings set org.gnome.settings-daemon.plugins.xrandr default-monitors-setup do-nothing

```

GNOME 3.24 deprecated the following settings:

```
org.gnome.settings-daemon.plugins.power button-hibernate
org.gnome.settings-daemon.plugins.power button-power
org.gnome.settings-daemon.plugins.power button-sleep
org.gnome.settings-daemon.plugins.power button-suspend
org.gnome.settings-daemon.plugins.power critical-battery-action

```

##### Don't suspend, when laptop lid is closed

The settings panel of GNOME doesn't provide an option for the user, to change the action, when laptop lid is closed. However [gnome-tweaks](https://www.archlinux.org/packages/?name=gnome-tweaks) can override the setting applied by [systemd](https://www.archlinux.org/packages/?name=systemd), on the tab *General* turn off the switch *Suspend when laptop lid is closed*. The system will therefore not *Suspend to RAM (S3)* on lid close.

To change the lid switch action system-wide, ensure that the setting described above is **not turned off** and edit the systemd settings in `/etc/systemd/logind.conf`. To turn of suspend on lid close, set `HandleLidSwitch=ignore`, as described in [Power management#ACPI events](/index.php/Power_management#ACPI_events "Power management").

##### Change critical battery level action

The settings panel does not provide an option for changing the critical battery level action. These settings have been removed from dconf as well. They are now managed by upower. Edit the upower settings in `/etc/UPower/UPower.conf`. Find these settings and adjust to your needs.

 `/etc/UPower/UPower.conf` 
```
PercentageLow=10
PercentageCritical=3
PercentageAction=2
CriticalPowerAction=HybridSleep
```

### Use a different window manager

GNOME Shell does not support using a different [window manager](/index.php/Window_manager "Window manager"), however [GNOME Flashback](/index.php/GNOME_Flashback "GNOME Flashback") provides sessions for Metacity and [Compiz](/index.php/Compiz "Compiz"). Furthermore, it is possible to define your own [custom GNOME sessions](/index.php/GNOME/Tips_and_tricks#Custom_GNOME_sessions "GNOME/Tips and tricks") which use alternative components.

## See also

*   [Official Website](https://www.gnome.org/)
*   [Wikipedia article](https://en.wikipedia.org/wiki/GNOME "wikipedia:GNOME")
*   [GNOME-Shell Extensions](https://extensions.gnome.org/)
*   [GNOME Shell Cheat Sheet](https://wiki.gnome.org/Projects/GnomeShell/CheatSheet)
*   Customization (themes, icons...):
    *   [Personalize GNOME](https://wiki.gnome.org/Personalization)
    *   [GNOME Look](https://www.gnome-look.org/)
*   GNOME applications:
    *   [GNOME Apps Index](https://wiki.gnome.org/Apps)
    *   [Wikipedia:GNOME Core Applications](https://en.wikipedia.org/wiki/GNOME_Core_Applications "wikipedia:GNOME Core Applications")
*   GNOME Source/Mirrors:
    *   [GNOME Git Repository](https://git.gnome.org/browse/)
    *   [GNOME Github Mirror](https://github.com/GNOME)