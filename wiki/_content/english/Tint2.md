[tint2](https://gitlab.com/o9000/tint2) is a system panel/taskbar for Linux. It is described by its developers as "simple, unobtrusive and light". It can be configured to include (or not include), among other things, a system tray, a task list, a battery monitor and a clock. Its look can also be configured a great deal, and it does not have many dependencies. This makes it ideal for window manager users who want a panel but do not have one by default, like [Openbox](/index.php/Openbox "Openbox") users.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Application launchers](#Application_launchers)
    *   [2.2 Applications menu in Openbox](#Applications_menu_in_Openbox)
    *   [2.3 Volume control](#Volume_control)
*   [3 Running tint2](#Running_tint2)
    *   [3.1 Openbox](#Openbox)
    *   [3.2 GNOME 3](#GNOME_3)
    *   [3.3 Multiple panels](#Multiple_panels)
*   [4 Enabling transparency](#Enabling_transparency)
    *   [4.1 Fullscreen/Overlay](#Fullscreen.2FOverlay)
    *   [4.2 Third Party Extensions](#Third_Party_Extensions)
*   [5 See Also](#See_Also)

## Installation

Install the [tint2](https://www.archlinux.org/packages/?name=tint2) package.

## Configuration

tint2 has a configuration file in `~/.config/tint2/tint2rc`. A skeleton configuration file with the default settings is created the first time you run tint2\. You can then change this file to your liking. Full documentation on how to configure tint2 is found [here](https://gitlab.com/o9000/tint2/wikis/Configure). You can configure the fonts, colors, looks, location and more in this file. The tint2 package also contains a GUI configuration tool that can be launched by running *tint2conf*.

### Application launchers

With version 0.12, it has become possible to add application launchers to tint2\. It is necessary to add the following configuration options to your tint2 config file:

Under `#Panel`:

```
# Panel
panel_items = LTSBC

```

And under the new section `#Launchers`:

```
# Launchers
launcher_icon_theme = LinuxLex-8
launcher_padding = 5 0 10
launcher_background_id = 9
launcher_icon_size = 85
launcher_item_app = /some/where/application.desktop
launcher_item_app = /some/where/anotherapplication.desktop

```

The option `launcher_icon_theme` seems not to be documented yet.

`panel_items` is a new configuration option which defines which items tint2 shows and in what order:

	L

	Show Launcher

	T

	Show Taskbar

	S

	Show Systray

	B

	Show Battery status

	C

	Show Clock

	F

	Expanded Spacer (Only Works Without T)

### Applications menu in Openbox

Since version 0.12, you have the ability to create launchers. Unfortunately, tint2 does not support nested menus yet, so there is no native function to enable an applications menu. With a little ingenuity, one can trick tint2 and get an applications menu anyway! This example will create such a launcher for Openbox.

Besides tint2 and Openbox, you have to [install](/index.php/Install "Install") the [xdotool](https://www.archlinux.org/packages/?name=xdotool) package. Next you want to create a keybinding for opening the Openbox menu. For Openbox, this would require the following entry between the <keyboard> and </keyboard> tags in `~/.config/openbox/rc.xml`:

```
 <keybind key="C-A-space">
   <action name="ShowMenu"><menu>root-menu</menu></action>
 </keybind>

```

This will set `Ctrl+Alt+Space` to open the root-menu (this is the menu that opens when you right-click the desktop). You can change `root-menu` to any menu-id that you have defined in `~/.config/openbox/menu.xml`. Next we need to make that keybinding into a `.desktop` file with `xdotool`. First test that your keybind works with:

```
$ xdotool key ctrl+alt+space

```

If the menu you chose pops up under your mouse cursor, you have done it right! Now create a `open-openbox-menu.desktop` file inside `~/.local/share/applications` directory. Be sure to add the line `Exec=xdotool key ctrl+alt+space` where `Ctrl+Alt+Space` are your chosen key combinations. Open your new `open-openbox-menu.desktop` file from your file manager and, once again, you should see the menu appear under your cursor. Now just add this to tint2 as a launcher, and you have your Openbox Applications Menu as a launcher for tint2!

See [Openbox Menus](http://openbox.org/wiki/Help:Menus) for further help on creating your own menu to use here, and [menumaker](https://www.archlinux.org/packages/?name=menumaker) to generate a nice full `menu.xml` for most (possibly all) of your installed programs.

### Volume control

Tint2 does not come with a volume control applet. VolWheel is a simple one that sits in the tray. Install it with [volwheel](https://www.archlinux.org/packages/?name=volwheel) and show it by running `volwheel`.

Another option is [volumeicon](https://www.archlinux.org/packages/?name=volumeicon) or [volumeicon-gtk2](https://aur.archlinux.org/packages/volumeicon-gtk2/).

## Running tint2

### Openbox

You can run tint2 by simply typing the command:

```
$ tint2

```

If you want to run tint2 when starting [Openbox](/index.php/Openbox "Openbox"), you will need to edit `~/.config/openbox/autostart` and add the following line:

```
tint2 &

```

### GNOME 3

In GNOME 3, the Activities view has replaced the bottom panel and taskbar. To use tint2 in its place, run

```
$ gnome-session-properties

```

and add `/usr/bin/tint2` as an application to run on start-up. The next time GNOME starts, tint2 will run automatically.

### Multiple panels

Multiple tint2 panels can be simultaneously running by using executing tint2 with different configuration files:

```
tint2 -c <path_to_first_config_file>
tint2 -c <path_to_second_config_file>

```

## Enabling transparency

To make tint2 look its best, some form of compositing is required. If your tint2 has a large black rectangular box behind it you are either using a window manager without native compositing (like Openbox) or it is not enabled.

To enable compositing under Openbox you can install [Xcompmgr](/index.php/Xcompmgr "Xcompmgr") or [Cairo Compmgr](/index.php/Cairo_Compmgr "Cairo Compmgr"), the packages are [xcompmgr](https://www.archlinux.org/packages/?name=xcompmgr), respectively [cairo-compmgr](https://aur.archlinux.org/packages/cairo-compmgr/).

Xcompmgr can be started like this:

```
$ xcompmgr

```

You will have to kill and restart tint2 to enable transparency.

If Xcompmgr is used solely to provide tint2 with transparency effects it can be run at boot by changing the autostart section in `~/.config/openbox/autostart` to this:

```
# Launch Xcomppmgr and tint2 with openbox
if which tint2 >/dev/null 2>&1; then
  (sleep 2 && xcompmgr) &
  (sleep 2 && tint2) &
fi

```

Various other (better) ways to make Xcompmgr run at startup are discussed in the [Openbox](/index.php/Openbox "Openbox") article.

### Fullscreen/Overlay

To force tint2 to stay on top of the application(overlay), you need to set the panel_layer option appropriately. This can be helpful when you switch from a fullscreen window to a normal application using Alt-Tab. There is a discussion on this at [Crunchbang Forum](http://crunchbang.org/forums/viewtopic.php?pid=70048)

```
 #Panel
 panel_layer = top
 strut_policy = follow_size

```

### Third Party Extensions

Its also possible to extend tint2 with other applications. To add third party extensions, check the "Pages" section in the Official Wiki link below.

## See Also

*   [Tint2 Official Wiki](https://gitlab.com/o9000/tint2/wikis/home)