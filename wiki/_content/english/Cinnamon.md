Related articles

*   [Nemo](/index.php/Nemo "Nemo")

[Cinnamon](https://github.com/linuxmint/Cinnamon) is a [desktop environment](/index.php/Desktop_environment "Desktop environment") which combines a traditional desktop layout with modern graphical effects. The underlying technology was forked from the [GNOME](/index.php/GNOME "GNOME") desktop. As of version 2.0, Cinnamon is a complete desktop environment and not merely a frontend for GNOME like GNOME Shell and Unity.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
    *   [1.1 Cinnamon applications](#Cinnamon_applications)
*   [2 Starting](#Starting)
    *   [2.1 Graphical log-in](#Graphical_log-in)
    *   [2.2 Starting Cinnamon manually](#Starting_Cinnamon_manually)
    *   [2.3 Restarting Cinnamon](#Restarting_Cinnamon)
*   [3 Configuration](#Configuration)
    *   [3.1 Cinnamon settings](#Cinnamon_settings)
    *   [3.2 Applets and extensions](#Applets_and_extensions)
    *   [3.3 Pressing power buttons suspend the system](#Pressing_power_buttons_suspend_the_system)
    *   [3.4 Manage languages used in Cinnamon](#Manage_languages_used_in_Cinnamon)
    *   [3.5 Use a different window manager](#Use_a_different_window_manager)
*   [4 Tips and tricks](#Tips_and_tricks)
    *   [4.1 Creating custom applets](#Creating_custom_applets)
    *   [4.2 Default desktop background wallpaper path](#Default_desktop_background_wallpaper_path)
    *   [4.3 Show home, filesystem desktop icons](#Show_home,_filesystem_desktop_icons)
    *   [4.4 Menu editor](#Menu_editor)
    *   [4.5 Workspaces](#Workspaces)
    *   [4.6 Hide desktop icons](#Hide_desktop_icons)
    *   [4.7 Themes and icons](#Themes_and_icons)
    *   [4.8 Sound events](#Sound_events)
    *   [4.9 Resize windows by mouse](#Resize_windows_by_mouse)
    *   [4.10 Portable keybindings](#Portable_keybindings)
    *   [4.11 Screenshot](#Screenshot)
    *   [4.12 Prevent Cinnamon from overriding xrandr/xinput configuration](#Prevent_Cinnamon_from_overriding_xrandr/xinput_configuration)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 Debugging](#Debugging)
    *   [5.2 cinnamon-settings: No module named Image](#cinnamon-settings:_No_module_named_Image)
    *   [5.3 Video tearing](#Video_tearing)
    *   [5.4 Disable the NetworkManager applet](#Disable_the_NetworkManager_applet)

## Installation

Cinnamon can be [installed](/index.php/Install "Install") with the package [cinnamon](https://www.archlinux.org/packages/?name=cinnamon).

**Note:** If you have an Intel GPU, make sure you are [not using xf86-video-intel](/index.php/Intel_graphics#Installation "Intel graphics") with Cinnamon as it may freeze at random times otherwise, but you can still move the mouse. Use the [modesetting(4)](https://jlk.fjfi.cvut.cz/arch/manpages/man/modesetting.4) driver instead by removing [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) (KDE also [recommends this](https://community.kde.org/Plasma/5.9_Errata#Intel_GPUs)).

### Cinnamon applications

Cinnamon introduces X-Apps which are based on GNOME Core Applications but are changed to work across Cinnamon, MATE and XFCE; they have the traditional user interface (UI).

| Application | GNOME | Cinnamon |
| text editor | Gedit/Pluma | [xed](https://www.archlinux.org/packages/?name=xed) |
| image viewer | Eye of GNOME | [xviewer](https://aur.archlinux.org/packages/xviewer/) |
| document viewer | Evince/Atril | [xreader](https://www.archlinux.org/packages/?name=xreader) |
| media player | Totem | [xplayer](https://aur.archlinux.org/packages/xplayer/) |
| image organizer | gThumb | [pix](https://aur.archlinux.org/packages/pix/) |

## Starting

### Graphical log-in

Choose *Cinnamon* or *Cinnamon (Software Rendering)* from the menu in a [display manager](/index.php/Display_manager "Display manager") of choice. Cinnamon is the 3D accelerated version, which should normally be used. If you experience problems with your video driver (e.g. artifacts or crashing), try the *Cinnamon (Software Rendering)* session, which disables 3D acceleration.

### Starting Cinnamon manually

If you prefer to start Cinnamon manually from the console, add the following line to [Xinitrc](/index.php/Xinitrc "Xinitrc"):

 `~/.xinitrc` 
```
 exec cinnamon-session

```

If the *Cinnamon (Software Rendering)* session is required, use `cinnamon-session-cinnamon2d` instead of `cinnamon-session`.

### Restarting Cinnamon

From a command line, execute the following line:

```
$ nohup cinnamon --replace > /dev/null 2>&1 &

```

## Configuration

Cinnamon is quite easy to configure — most common settings can be configured graphically. Its usability can be expanded with [applets](http://cinnamon-spices.linuxmint.com/applets) and [extensions](http://cinnamon-spices.linuxmint.com/extensions), and also it supports [theming](http://cinnamon-spices.linuxmint.com/themes).

### Cinnamon settings

*cinnamon-settings* launches a settings module specified on the command line. Without (correct) arguments, it launches *System Settings*. For example, to start the panel settings:

```
$ cinnamon-settings panel

```

To list all available modules:

```
$ pacman -Ql cinnamon | awk -F'[_.]' '/cs_.+\.py/ {print $2}'

```

	Printers

	For configure printers, install the [system-config-printer](https://www.archlinux.org/packages/?name=system-config-printer) package.

	Networking

	To add support for the networking module, enable [Network Manager](/index.php/NetworkManager#Configuration "NetworkManager"). In order for NetworkManager to store Wi-Fi passwords, you will need to also install [GNOME Keyring](/index.php/GNOME_Keyring "GNOME Keyring").

	Bluetooth

	For Bluetooth device support, install the [blueberry](https://www.archlinux.org/packages/?name=blueberry) package.

### Applets and extensions

While an **applet** is an addition to the Cinnamon panel, an **extension** can fully change the Cinnamon experience. They can be installed from the [AUR](/index.php/AUR "AUR"), ([package search](https://aur.archlinux.org/packages.php?O=0&K=cinnamon-&do_Search=Go)), or from inside Cinnamon (*Get more online*):

```
$ cinnamon-settings applets
$ cinnamon-settings extensions

```

Alternatively, install manually from [Cinnamon spices](http://cinnamon-spices.linuxmint.com/).

**Note:** If applets do not appear, restart Cinnamon with `r` in the `Alt+F2` dialog box.

### Pressing power buttons suspend the system

This is the default behaviour. To change the setting open the `cinnamon-settings` panel and click on the "Power Management" option. Change the "When the power button is pressed" option to your desired behaviour.

### Manage languages used in Cinnamon

**Note:** The language module was removed from the Cinnamon Control Panel with the release of Cinnamon 2.2\. [[1]](http://segfault.linuxmint.com/2014/04/cinnamon-2-2/)

*   To add/remove languages: see [Locale](/index.php/Locale "Locale").
*   To change between enabled languages: install the [mintlocale](https://aur.archlinux.org/packages/mintlocale/) package.
*   For Cinnamon to correctly display another language: install the [cinnamon-translations](https://www.archlinux.org/packages/?name=cinnamon-translations) package.
*   To change the keyboard layout: navigate to **System Settings > Hardware > Keyboard > Layouts**.

### Use a different window manager

Cinnamon does not support using a different window manager.

## Tips and tricks

### Creating custom applets

The official tutorial on creating a Cinnamon *applet* can be found [here](http://developer.linuxmint.com/reference/git/cinnamon-tutorials/write-applet.html).

### Default desktop background wallpaper path

When you add a wallpaper from a custom path in Cinnamon Settings, Cinnamon copies it to `~/.cinnamon/backgrounds`. Thus, with every change of your wallpaper you would have to add your updated wallpaper again from the settings menu or copy / symlink it manually to `~/.cinnamon/backgrounds`.

Additionally the official mint wallpapers are available for every release. Checkout the [AUR](https://aur.archlinux.org/packages/?O=0&K=mint-backgrounds).

### Show home, filesystem desktop icons

By default Cinnamon starts with desktop icons enabled but with no desktop icons on screen. To show desktop icons for the home folder, the filesystem, the trash, mounted volumes and network servers open Cinnamon settings and click on desktop. Enable the checkboxes of the icons you want to see on screen.

### Menu editor

The Menu applet supports launching custom commands. Right click on the applet, click on *Configure...* and then *Open the menu editor*. Select a sub-menu (or create a new one) and select *New Item*. Set *Name*, *Command* and *Comment*. Check the launch in terminal checkbox if needed. Leave unchecked for graphical applications. Click *OK* and close the menu editor afterwards. The launcher is added to the menu.

### Workspaces

A workspace pager can be added to the panel. Right click the panel and choose the option *Add applets to the panel*. Add the *Workspace switch* applet to the panel. To change its position right click on the panel and change the *Panel edit mode* on/off switch to on. Click and drag the switcher to the desired position and turn the panel edit mode off when finished.

By default there are 2 workspaces. To add more, hit `Control+Alt+Up` to show all workspaces. Then click on the plus sign button on the right of the screen to add more workspaces.

Alternatively, you can choose the number by command-line:

```
$ gsettings set org.cinnamon.desktop.wm.preferences num-workspaces 4

```

Replacing 4 with the number of workspaces you want.

### Hide desktop icons

The desktop icons rendering feature is enabled in [Nemo](/index.php/Nemo "Nemo") by default. To disable this feature, change the setting with the following command:

```
$ gsettings set org.nemo.desktop show-desktop-icons false

```

### Themes and icons

Linux Mint styled themes and icons can be installed with the [mint-themes](https://aur.archlinux.org/packages/mint-themes/), [mint-x-icons](https://aur.archlinux.org/packages/mint-x-icons/), and [mint-y-icons](https://aur.archlinux.org/packages/mint-y-icons/) packages. The themes can be edited in `Settings → Themes → Other settings`.

Official Linux Mint Cinnamon themes are also included in the [mint-themes](https://aur.archlinux.org/packages/mint-themes/) package.

Setting the desktop theme via shell can be done like this:

```
$ gsettings set org.cinnamon.theme name "*Theme-Name*"

```

### Sound events

Cinnamon does not come with sounds used for events like the startup of the desktop that are also used in Linux Mint by default. These sound effects can be installed with the [cinnamon-sound-effects](https://aur.archlinux.org/packages/cinnamon-sound-effects/) and [mint-sounds](https://aur.archlinux.org/packages/mint-sounds/) packages. The sound events can be edited in `Settings → Sound → Sound Effects`.

### Resize windows by mouse

To resize windows with `Alt+Right click`, use `gsettings`:

```
gsettings set org.cinnamon.desktop.wm.preferences resize-with-right-button true

```

### Portable keybindings

To export your keyboard shortcut keys, you should do:

```
dconf dump /org/cinnamon/desktop/keybindings/ >keybindings-backup.dconf

```

To later import it (for example) on another computer, do:

```
dconf load /org/cinnamon/desktop/keybindings/ <keybindings-backup.dconf

```

### Screenshot

As explained in [Taking a screenshot](/index.php/Taking_a_screenshot#Cinnamon "Taking a screenshot"), installing [gnome-screenshot](https://www.archlinux.org/packages/?name=gnome-screenshot) will add this functionality. The default shortcut key is `Prt Sc` key. This binding can be changed in the applet *Menu > Preferences > Keyboard* under *Shortcuts > System > Screenshots and Recording*. The default save directory is `$HOME/Pictures`, but can be customized with eg.

```
$ gsettings set org.gnome.gnome-screenshot auto-save-directory file:///home/*USER*/*some_path*

```

### Prevent Cinnamon from overriding xrandr/xinput configuration

The *cinnamon-settings-daemon* provides a number of plugins which can manage the display, keyboard and mouse. These plugins will override user set configuration (such as *xrandr* commands in the [xinitrc](/index.php/Xinitrc "Xinitrc") file). To stop user set configuration from being overridden, it is necessary to prevent the settings daemon plugins from being started.

This can be done by copying the *.desktop* entry for the relevant settings daemon plugin (these will be located in `/etc/xdg/autostart/`) to `$HOME/.config/autostart`. Then append the line `Hidden=true` to each copied entry.

**Tip:** Start your session with `cinnamon-session --debug` to see which plugins are reported to have been started.

To preserve display, keyboard and mouse settings, consider disabling the following:

```
cinnamon-settings-daemon-a11y-keyboard.desktop
cinnamon-settings-daemon-a11y-settings.desktop
cinnamon-settings-daemon-keyboard.desktop
cinnamon-settings-daemon-mouse.desktop
cinnamon-settings-daemon-xrandr.desktop

```

## Troubleshooting

### Debugging

You can use the `cinnamon-looking-glass` tool (Melange - Cinnamon Debugger) to inspect various things about the Cinnamon environment:

*   a list of currently-open windows
*   a list of currently-loaded extensions (applets, desklets, etc.)
*   logs

The "logs" feature is especially useful if you're encountering crashes (often happening due to extensions no being compatible or buggy).

### cinnamon-settings: No module named Image

If *cinnamon-settings* does not start with the message that it cannot find a certain module, e.g. the Image module, it is likely that it uses outdated compiled files which refer to no longer existing file locations. In this case remove all `*.pyc` files in `/usr/lib/cinnamon-settings` and its sub-folders. See the [upstream bug report](https://github.com/linuxmint/Cinnamon/issues/2495).

### Video tearing

Because [muffin](https://www.archlinux.org/packages/?name=muffin) is based upon [mutter](https://www.archlinux.org/packages/?name=mutter), video tearing fixes for [GNOME](/index.php/GNOME "GNOME") should also work in Cinnamon. See [GNOME/Troubleshooting#Tear-free video with Intel HD Graphics](/index.php/GNOME/Troubleshooting#Tear-free_video_with_Intel_HD_Graphics "GNOME/Troubleshooting") for more information.

### Disable the NetworkManager applet

Even if you do not use [NetworkManager](/index.php/NetworkManager "NetworkManager") and remove the *Network Manager* applet from the default panel, Cinnamon will still load *nm-applet* and display it in the system tray. You cannot uninstall the package, because it is required by [cinnamon](https://www.archlinux.org/packages/?name=cinnamon) and [cinnamon-control-center](https://www.archlinux.org/packages/?name=cinnamon-control-center), but you can still easily disable it. To do so copy the autostart file from `/etc/xdg/autostart/nm-applet.desktop` to `~/.config/autostart/nm-applet.desktop`. Open it with your favorite text editor and add at the end `X-GNOME-Autostart-enabled=false`.

Alternatively you can disable it by creating the following symlink:

```
$ ln -s /bin/true /usr/local/bin/nm-applet

```

The ability to blacklist particular icons from the system tray (such as the *nm-applet* icon) has been [requested upstream](https://github.com/linuxmint/Cinnamon/issues/3318).