[tint2](https://gitlab.com/o9000/tint2) is a simple, unobtrusive and light [panel](/index.php/Panel "Panel") for [Xorg](/index.php/Xorg "Xorg"). It can be configured to include a system tray, a task list, a battery monitor and more. Its look is configurable and it only has few dependencies, making it ideal for window managers like [Openbox](/index.php/Openbox "Openbox"), that do not come with a panel.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Application launchers](#Application_launchers)
    *   [2.2 Applications menu in Openbox](#Applications_menu_in_Openbox)
    *   [2.3 Volume control](#Volume_control)
*   [3 Running tint2](#Running_tint2)
    *   [3.1 Openbox](#Openbox)
    *   [3.2 GNOME 3](#GNOME_3)
    *   [3.3 i3](#i3)
    *   [3.4 Multiple panels](#Multiple_panels)
*   [4 Enabling transparency](#Enabling_transparency)
    *   [4.1 Fake transparency](#Fake_transparency)
    *   [4.2 Real transparency](#Real_transparency)
*   [5 Fullscreen/Overlay](#Fullscreen/Overlay)
*   [6 Third party extensions](#Third_party_extensions)
*   [7 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [tint2](https://www.archlinux.org/packages/?name=tint2) package.

## Configuration

*tint2* has a configuration file in `~/.config/tint2/tint2rc`. A skeleton configuration file with the default settings is created the first time you run *tint2*. You can then change this file to your liking. Full documentation on how to configure *tint2* is found [here](https://gitlab.com/o9000/tint2/blob/master/doc/tint2.md#configuration). You can configure the fonts, colors, looks, location and more in this file. The *tint2* package also contains a GUI configuration tool which can be launched with *tint2conf*.

### Application launchers

With version 0.12, it has become possible to add application launchers to *tint2*. It is necessary to add the following configuration options to your *tint2* config file:

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

`panel_items` is a new configuration option which defines which items *tint2* shows and in what order:

	L

	shows the Launcher

	T

	shows the Taskbar

	S

	shows the Systray (also called notification area)

	B

	shows the Battery status

	C

	shows the Clock

	F

	adds an extensible spacer (freespace). You can specify more than one. Has no effect if `T` is also present. *(since 0.12)*

	E

	adds an executor plugin. You can specify more than one. *(since 0.12.4)*

	P

	adds a push button. You can specify more than one. *(since 0.14)*

	:

	adds a separator. You can specify more than one. *(since 0.13.0)*

### Applications menu in Openbox

Since version 0.12, you have the ability to create launchers. Unfortunately, *tint2* does not support nested menus yet, so there is no native function to enable an applications menu. This section describes a way to create a launcher for Openbox.

Besides *tint2* and Openbox, [install](/index.php/Install "Install") the [xdotool](https://www.archlinux.org/packages/?name=xdotool) package. Next, create a keybinding for opening the Openbox menu. For Openbox, this would require the following entry between the <keyboard> and </keyboard> tags in `~/.config/openbox/rc.xml`:

```
 <keybind key="C-A-space">
   <action name="ShowMenu"><menu>root-menu</menu></action>
 </keybind>

```

This will set `Ctrl+Alt+Space` to open the root-menu (this is the menu that opens when you right-click the desktop). You can change `root-menu` to any menu-id that you have defined in `~/.config/openbox/menu.xml`. Next we need to make that keybinding into a `.desktop` file with `xdotool`. First test that your keybind works with:

```
$ xdotool key ctrl+alt+space

```

If the menu you chose pops up under your mouse cursor, you have done it right! Now create a `open-openbox-menu.desktop` file inside the `~/.local/share/applications` directory. Add the line `Exec=xdotool key ctrl+alt+space` where `Ctrl+Alt+Space` are your chosen key combinations. Open your new `open-openbox-menu.desktop` file from your file manager and, once again, you should see the menu appear under your cursor. Now just add this to *tint2* as a launcher, and you have your Openbox Applications Menu as a launcher for *tint2*. If you need to place the menu at a fixed position, you can use `xdotool mousemove x y`. You can create a script and reference it in `open-openbox-menu.desktop` since it involves two commands.

See [Openbox Menus](http://openbox.org/wiki/Help:Menus) for further help on creating your own menu to use here, and [menumaker](https://www.archlinux.org/packages/?name=menumaker) to generate a nice full `menu.xml` for most (possibly all) of your installed programs.

Since version 0.14, you have the ability to create buttons. Just add "xdotool key ctrl+alt+space" string from example above to button key action you want to be start menu action.

### Volume control

*tint2* does not come with a volume control applet. See [List of applications/Multimedia#Volume control](/index.php/List_of_applications/Multimedia#Volume_control "List of applications/Multimedia").

## Running tint2

### Openbox

You can run *tint2* by simply typing the command:

```
$ tint2

```

If you want to run *tint2* when starting [Openbox](/index.php/Openbox "Openbox"), you will need to edit `~/.config/openbox/autostart` and add the following line:

```
tint2 &

```

### GNOME 3

In GNOME 3, the Activities view has replaced the bottom panel and taskbar. To use *tint2* in its place, run

```
$ gnome-session-properties

```

and add `/usr/bin/tint2` as an application to run on start-up. The next time GNOME starts, *tint2* will run automatically.

### i3

In [i3](/index.php/I3 "I3"), to use *tint2* as a replacement for `i3status`, append the following line to end of the i3 configuration file:

 `~/.i3/config`  `exec --no-startup-id tint2` 

and comment out or remove any section like `bar{status_command i3status`} from the same file.

### Multiple panels

Multiple *tint2* panels can be simultaneously running by using executing *tint2* with different configuration files:

```
tint2 -c <path_to_first_config_file>
tint2 -c <path_to_second_config_file>

```

## Enabling transparency

*tint2* supports both fake and real transparency. Which one is used is regulated by the `disable_transparency` option in the `tint2rc` configuration file.

If you want to completely disable transparency you need to use `disable_transparency = 1` and set the panel background opacity to 100\. Eg:

```
 background_color = #000000 100

```

### Fake transparency

For fake transparency you need to set `disable_transparency = 1`.

Fake transparency captures a portion of the desktop background and uses that as the panel background. Because of that it is important to set the background image before *tint2* is activated. A startup script example for [Openbox](/index.php/Openbox "Openbox") could be (using [Feh](/index.php/Feh "Feh") for the background):

```
...
feh --randomize --no-fehbg --bg-fill ~/Pictures/wallpapers/
(sleep 1 && tint2) &
...

```

### Real transparency

For real transparency you need to activate a compositor like [Compton](/index.php/Compton "Compton") first and set `disable_transparency = 0`.

The opacity is regulated by the second parameter of the `background_color` property in the *tint2* [configuration file](https://gitlab.com/o9000/tint2/blob/master/doc/tint2.md#backgrounds-and-borders).

If you are making changes on the fly, you may need to restart *tint2* for the transparency to take effect.

## Fullscreen/Overlay

To force *tint2* to stay on top of the application (overlay), you need to set the panel_layer option appropriately. This can be helpful when you switch from a fullscreen window to a normal application using Alt-Tab. There is a discussion on this at [Crunchbang Forum](http://crunchbang.org/forums/viewtopic.php?pid=70048)

```
 #Panel
 panel_layer = top
 strut_policy = follow_size

```

## Third party extensions

It is also possible to extend *tint2* with other applications. To add third party extensions, check the [Applets](https://gitlab.com/o9000/tint2/wikis/ThirdPartyApplets) section of official Wiki.

## See also

*   [Tint2 Official Wiki](https://gitlab.com/o9000/tint2/wikis/home)