Openbox is a lightweight, powerful, and highly configurable *stacking* [window manager](/index.php/Window_manager "Window manager") with extensive standards support. It may be built upon and run independently as the basis of a unique [desktop environment](/index.php/Desktop_environment "Desktop environment"), or within other integrated desktop environments such as [KDE](/index.php/KDE "KDE") and [Xfce](/index.php/Xfce "Xfce"), as an alternative to the window managers they provide. The [LXDE](/index.php/LXDE "LXDE") desktop environment is itself built around Openbox.

A comprehensive list of features are documented at the [official Openbox website](http://openbox.org/). This article pertains to specifically installing Openbox under Arch Linux.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Standalone](#Standalone)
    *   [1.2 Other desktop environments](#Other_desktop_environments)
*   [2 Configuration](#Configuration)
    *   [2.1 rc.xml](#rc.xml)
    *   [2.2 menu.xml](#menu.xml)
    *   [2.3 autostart](#autostart)
    *   [2.4 environment](#environment)
    *   [2.5 GUI configuration](#GUI_configuration)
*   [3 Openbox reconfiguration](#Openbox_reconfiguration)
*   [4 Keybinds](#Keybinds)
    *   [4.1 Special keys](#Special_keys)
        *   [4.1.1 Modifiers](#Modifiers)
        *   [4.1.2 Multimedia keys](#Multimedia_keys)
        *   [4.1.3 Navigation keys](#Navigation_keys)
    *   [4.2 Volume Control](#Volume_Control)
        *   [4.2.1 ALSA](#ALSA)
        *   [4.2.2 Pulseaudio](#Pulseaudio)
        *   [4.2.3 OSS](#OSS)
    *   [4.3 Media player control](#Media_player_control)
    *   [4.4 Brightness control](#Brightness_control)
    *   [4.5 Window snapping](#Window_snapping)
    *   [4.6 Desktop menu](#Desktop_menu)
*   [5 Menus](#Menus)
    *   [5.1 Static](#Static)
        *   [5.1.1 menumaker](#menumaker)
        *   [5.1.2 obmenu](#obmenu)
        *   [5.1.3 xdg-menu](#xdg-menu)
        *   [5.1.4 logout menu options](#logout_menu_options)
    *   [5.2 Pipes](#Pipes)
        *   [5.2.1 Examples](#Examples)
    *   [5.3 Generators](#Generators)
        *   [5.3.1 obmenu-generator](#obmenu-generator)
        *   [5.3.2 openbox-menu](#openbox-menu)
    *   [5.4 Menu icons](#Menu_icons)
    *   [5.5 Desktop menu as a panel menu](#Desktop_menu_as_a_panel_menu)
*   [6 Desktop theming](#Desktop_theming)
    *   [6.1 Configuration](#Configuration_2)
    *   [6.2 Installation: official and AUR](#Installation:_official_and_AUR)
    *   [6.3 Installation: other sources](#Installation:_other_sources)
    *   [6.4 Troubleshooting](#Troubleshooting)
        *   [6.4.1 Theme cannot be used](#Theme_cannot_be_used)
        *   [6.4.2 Theme looks broken](#Theme_looks_broken)
    *   [6.5 Edit or create new themes](#Edit_or_create_new_themes)
*   [7 Compositing effects](#Compositing_effects)
*   [8 Mouse cursor and application icon themes](#Mouse_cursor_and_application_icon_themes)
*   [9 Desktop icons and wallpapers](#Desktop_icons_and_wallpapers)
    *   [9.1 Desktop management using file managers](#Desktop_management_using_file_managers)
    *   [9.2 Wallpaper](#Wallpaper)
    *   [9.3 Icon programs](#Icon_programs)
        *   [9.3.1 idesk](#idesk)
        *   [9.3.2 xfdesktop](#xfdesktop)
    *   [9.4 conky reconfiguration](#conky_reconfiguration)
*   [10 oblogout](#oblogout)
*   [11 Openbox for multihead users](#Openbox_for_multihead_users)
*   [12 Tips and tricks](#Tips_and_tricks)
    *   [12.1 Launch a complex command with hotkey](#Launch_a_complex_command_with_hotkey)
    *   [12.2 Switch desktops using the mouse](#Switch_desktops_using_the_mouse)
    *   [12.3 Set default applications / file associations](#Set_default_applications_.2F_file_associations)
    *   [12.4 Stop continous mouse wheel desktop switching](#Stop_continous_mouse_wheel_desktop_switching)
    *   [12.5 Ad-hoc window transparency](#Ad-hoc_window_transparency)
    *   [12.6 Using obxprop for faster configuration](#Using_obxprop_for_faster_configuration)
    *   [12.7 Xprop values for applications](#Xprop_values_for_applications)
        *   [12.7.1 Firefox](#Firefox)
    *   [12.8 Switching between keyboard layouts](#Switching_between_keyboard_layouts)
    *   [12.9 Set grid layout for virtual desktops](#Set_grid_layout_for_virtual_desktops)
*   [13 Troubleshooting](#Troubleshooting_2)
    *   [13.1 Windows load behind the active window](#Windows_load_behind_the_active_window)
*   [14 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [openbox](https://www.archlinux.org/packages/?name=openbox) package.

### Standalone

[Display managers](/index.php/Display_manager "Display manager") will automatically detect Openbox, allowing for it to be run as a standalone session.

To start openbox with [Xinitrc](/index.php/Xinitrc "Xinitrc"), add the following line:

```
exec openbox-session

```

**Note:** Specifying `openbox` instead of `openbox-session` will prevent [autostart](#autostart) in `/etc/xdg/autostart`.

### Other desktop environments

**Note:**

*   When replacing the native window manager of a [desktop environment](/index.php/Desktop_environment "Desktop environment") with Openbox, keep in mind that Openbox does not provide any compositing effects (such as transparency). See [#Compositing effects](#Compositing_effects).
*   Openbox does work with GNOME applications (but see [GTK+#Client-side decorations](/index.php/GTK%2B#Client-side_decorations "GTK+")). [[1]](http://comments.gmane.org/gmane.comp.window-managers.openbox/6595)

See [Desktop environment#Custom window manager](/index.php/Desktop_environment#Custom_window_manager "Desktop environment").

## Configuration

**Note:** Local configuration files will always override global equivalents.

Four key files form the basis of the openbox configuration, each serving a unique role. They are: `rc.xml`, `menu.xml`, `autostart`, and `environment`. Although these files are discussed in more detail below, to start configuring Openbox, it will first be necessary to create a **local** Openbox profile (i.e for your specific user account) based on them. This can be done by copying them from the **global** `/etc/xdg/openbox` profile (applicable to any and all users) as a template:

```
$ cp -R /etc/xdg/openbox ~/.config/

```

### rc.xml

**Tip:** Custom keyboard shortcuts (keybindings) must be added to the `<keyboard>` section of this file, and underneath the `<!-- Keybindings for running aplications -->` heading.

`~/.config/openbox/rc.xml` is the main configuration file, responsible for determining the behaviour and settings of the overall session, including:

*   Keyboard shortcuts (e.g. starting applications; controlling the volume)
*   Theming
*   Desktop and Virtual desktop settings, and
*   Application Window settings

This file is also pre-configured, meaning that it will only be necessary to amend existing content in order to customise behaviour to suit personal preference.

**Note:** Per-application settings pertaining to fixed placement of applications per monitor will only work if the x & y position have also been defined.

### menu.xml

`~/.config/openbox/menu.xml` defines the type and behaviour of the desktop menu, accessable by right-clicking the background. Although the default provided is a **static menu** (meaning that it will not automatically update when new applications are installed), it is possible to employ the use of **dynamic menus** that will automatically update as well.

The available options are discussed extensively below in the [Menus](#Menus) section.

### autostart

The file `~/.config/openbox/autostart`, if present, is executed by Openbox at startup. A basic example of this file consists of one command per line, like so:

```
xset -b
nm-applet &
conky &

```

Note that a single ampersand (`&`) causes the process in question to be run in the background, allowing the script to continue on to the next command. An ampersand is therefore needed after each command that launches a process of indefinite duration. Commands that are completed essentially instantly (e.g. `xset -b`) may be left alone.

Issues regarding commands in `~/.config/openbox/autostart` being executed out of order (or skipped altogether) are often resolved by the addition of small delays. For instance:

```
xset -b
(sleep 3s && nm-applet) &
(sleep 3s && conky) &

```

**Note:** In addition to running `~/.config/openbox/autostart`, Openbox will also launch programs with `.desktop` files present in `/etc/xdg/autostart`. This is the global [autostart](/index.php/Autostart "Autostart") directory, which is automatically sourced by XDG-compliant desktop environments (e.g. GNOME, KDE). Openbox will source this directory as well, provided that the package [python2-xdg](https://www.archlinux.org/packages/?name=python2-xdg) is installed, and Openbox is launched as `openbox-session` (rather than simply `openbox`, as [noted earlier](#Standalone)). Duplication between `~/.config/openbox/autostart` and `/etc/xdg/autostart` is a common cause of programs launching twice at startup (e.g. two network manager tray icons).

The `/usr/lib/openbox/openbox-xdg-autostart` python2 script runs applications based on the XDG autostart specification.

### environment

`~/.config/openbox/environment` can be used to export and set relevant environmental variables such as to:

*   Define new pathways (e.g. execute commands that would otherwise require the entire pathway to be listed with them)
*   Change language settings, and
*   Define other variables to be used (e.g. the fix for GTK theming could be listed here)

### GUI configuration

Several GUI applications are available to quickly and easily configure your Openbox desktop. From the [official repositories](/index.php/Official_repositories "Official repositories"):

*   **ObConf** — A GTK2 based configuration tool for the Openbox window manager.

	[http://openbox.org/wiki/ObConf:About](http://openbox.org/wiki/ObConf:About) || [obconf](https://www.archlinux.org/packages/?name=obconf)

*   **LXAppearance ObConf** — Plugin for LXAppearance to configure Openbox. Note that not all options to configure Openbox are available in this plugin, so you might want to install obconf anyway.

	[http://lxde.org](http://lxde.org) || [lxappearance-obconf](https://www.archlinux.org/packages/?name=lxappearance-obconf)

*   **LXInput** — LXDE keyboard and mouse configuration

	[http://lxde.org](http://lxde.org) || [lxinput](https://www.archlinux.org/packages/?name=lxinput)

*   **LXRandR** — LXDE monitor configuration.

	[http://wiki.lxde.org/en/LXRandR](http://wiki.lxde.org/en/LXRandR) || [lxrandr](https://www.archlinux.org/packages/?name=lxrandr)

*   **obkey** — Configure Openbox keyboard shortcuts

	[https://code.google.com/p/obkey/](https://code.google.com/p/obkey/) || [obkey](https://aur.archlinux.org/packages/obkey/)

*   **ob-autostart** — A simple autostart application for Openbox.

	[http://pastebin.com/012YgXTk](http://pastebin.com/012YgXTk) || [ob-autostart](https://aur.archlinux.org/packages/ob-autostart/)

Programs and applications relating to the configuration of Openbox's desktop menu are discussed in the [Menus](#Menus) section.

## Openbox reconfiguration

**Tip:** where not already present, it would be worthwhile adding this command to a menu and/or as a keybind for convenience.

Openbox will not always automatically reflect any changes made to its configuration files within a session. As a consequence, it will be necessary to manually reload those files after they have been edited. To do so, enter the following command:

```
$ openbox --reconfigure

```

Where intending to add this command as a keybind to `~/.config/openbox/rc.xml`, it will only be necessary to list the command as `reconfigure`. An example has been provided below, using the `Super`+`F11` keybind:

```
<keybind key="W-F11">
  <action name="Reconfigure"/>
</keybind>

```

## Keybinds

All keybinds must be added to the `~/.config/openbox/rc.xml` file, and below the `<!-- Keybindings for running aplications -->` heading. Although a brief overview has been provided here, a more in-depth explanation of keybindings can be found at [openbox.org](http://openbox.org/wiki/Help:Bindings). [obkey](https://aur.archlinux.org/packages/obkey/) is a utility for adjust key-binding. Before using obkey, you should use obconf to create `~/.config/openbox/rc.xml`.

### Special keys

While the use of standard alpha-numeric keys for keybindings is self-explanatory, special names are assigned to other types of keys, such as `modifers`, `multimedia` keys and `navigation` keys.

#### Modifiers

`Modifer` keys play an important role in keybindings (e.g. holding down the `shift` or `CTRL / control` key in combination with another key to undertake an action). Using modifers helps to prevent conflicting keybinds, whereby two or more actions are linked to the same key or combination of keys. The syntax to use a modifer with another key is:

```
"<modifier>-<key>"

```

The modifer codes are as follows:

*   `S`: Shift
*   `C`: Control / CTRL
*   `A`: Alt
*   `W`: Super / Windows
*   `M`: Meta
*   `H`: Hyper (If it is bound to something)

For example, the code below would use `super` and `t` to launch [lxterminal](https://www.archlinux.org/packages/?name=lxterminal)

```
<keybind key="W-t">
    <action name="Execute">
        <command>lxterminal</command>
    </action>
</keybind>

```

#### Multimedia keys

Where available, it is possible to set the appropriate `multimedia` keys to perform their intended functions, such as to control the volume and/or the screen brightness. These will usually be integrated into the `function` keys, and are identified by their appropriate symbols. See [Extra keyboard keys](/index.php/Extra_keyboard_keys "Extra keyboard keys") for details.

The volume and brightness multimedia codes are as follows (note that commands will still have to be assigned to them to actually function):

*   `XF86AudioRaiseVolume`: Increase volume
*   `XF86AudioLowerVolume`: Decrease volume
*   `XF86AudioMute`: Mute / unmute volume
*   `XF86MonBrightnessUp`: Increase screen brightess
*   `XF86MonBrightnessDown`: Decrease screen brightness

Examples of how these may be used in `~/.config/openbox/rc.xml` have been provided below.

#### Navigation keys

These are the directional / arrow keys, usually used to move the cursor up, down, left, or right. The (self-explanatory) navigation codes are as follows:

*   `Up`: Up
*   `Down`: Down
*   `Left`: Left
*   `Right`: Right

### Volume Control

What commands should be used for controlling the volume will depend on whether [ALSA](/index.php/ALSA "ALSA"), [PulseAudio](/index.php/PulseAudio "PulseAudio"), or [OSS](/index.php/OSS "OSS") is used for sound.

#### ALSA

If [ALSA](/index.php/ALSA "ALSA") is used for sound, the `amixer` program can be used to adjust the volume, which is part of the [alsa-utils](https://www.archlinux.org/packages/?name=alsa-utils) package. The following example - using the `multimedia` keys intended to control the volume - will adjust the volume by +/- 5% (which may be changed, as desired):

```
<keybind key="XF86AudioRaiseVolume">
    <action name="Execute">
        <command>amixer set Master 5%+ unmute</command>
    </action>
</keybind>
<keybind key="XF86AudioLowerVolume">
    <action name="Execute">
        <command>amixer set Master 5%- unmute</command>
    </action>
</keybind>
<keybind key="XF86AudioMute">
    <action name="Execute">
        <command>amixer set Master toggle</command>
    </action>
</keybind>

```

#### Pulseaudio

Where using [PulseAudio](/index.php/PulseAudio "PulseAudio") with [ALSA](/index.php/ALSA "ALSA") as a backend, the `amixer` program commands will have to be modifed, as illustrated below in comparison to the ALSA example:

```
<keybind key="XF86AudioRaiseVolume">
    <action name="Execute">
        <command>amixer -D pulse set Master 5%+ unmute</command>
    </action>
</keybind>
<keybind key="XF86AudioLowerVolume">
    <action name="Execute">
        <command>amixer -D pulse set Master 5%- unmute</command>
    </action>
</keybind>
<keybind key="XF86AudioMute">
    <action name="Execute">
        <command>amixer -D pulse set Master toggle</command>
    </action>
</keybind>

```

#### OSS

**Note:** This option may be suitable for more experienced users.

Where using [OSS](/index.php/OSS "OSS"), it is possible to create keybindings to raise or lower specific mixers. This allows, for example, the volume of a specific application (such as an audio player) to be changed without changing the overall system volume settings in turn. In this instance, the application must first have been [configured](/index.php/OSS#Configuring_Applications_for_OSS "OSS") to use its own mixer.

In the following example, [MPD](/index.php/MPD "MPD") has been configured to use its own mixer - also named `mpd` - to increase and decrease the volume by a single decibel at a time. The `--` that appears after the `ossmix` command has been added to prevent a negative value from being treated as an argument:

```
<keybind key="[chosen keybind]">
    <action name="Execute">
        <command>ossmix -- mpd +1</command>
    </action>
</keybind>
<keybind key="[chosen keybind]">
    <action name="Execute">
        <command>ossmix -- mpd -1</command>
    </action>
</keybind>

```

### Media player control

The [playerctl](https://aur.archlinux.org/packages/playerctl/) command-line utility can be used to bind multimedia keys to player actions. It should work with most media players.

```
<keybind key="XF86AudioPlay">
    <action name="Execute">
        <command>playerctl play</command>
    </action>
</keybind>
<keybind key="XF86AudioPause">
    <action name="Execute">
        <command>playerctl pause</command>
    </action>
</keybind>
<keybind key="XF86AudioNext">
    <action name="Execute">
        <command>playerctl next</command>
    </action>
</keybind>
<keybind key="XF86AudioPrev">
    <action name="Execute">
        <command>playerctl previous</command>
    </action>
</keybind>

```

### Brightness control

The `xbacklight` program is used to control screen brightness, which is part of the [Xorg](/index.php/Xorg "Xorg") X-Window system. In the example below, the `multimedia` keys intended to control the screen brightness will adjust the settings by +/- 10%:

```
<keybind key="XF86MonBrightnessUp">
     <action name="Execute">
       <command>xbacklight +10</command>
     </action>
</keybind>
<keybind key="XF86MonBrightnessDown">
     <action name="Execute">
       <command>xbacklight -10</command>
     </action>
</keybind>

```

### Window snapping

Many desktop environments and window managers support *window snapping* (e.g. Windows 7 Aero snap), whereby they will automatically snap into place when moved to the edge of the screen. This effect can also be simulated in Openbox through the use of keybinds on focused windows.

As illustrated in the example below, percentages must be used to determine window sizes (see [openbox.org](http://openbox.org/wiki/Help:Actions) for further information). In this instance, The `super` key is used in conjunction with the `navigation` keys:

```
<keybind key="W-Left">
    <action name="UnmaximizeFull"/>
    <action name="MaximizeVert"/>
    <action name="MoveResizeTo">
        <width>50%</width>
    </action>
    <action name="MoveToEdge"><direction>west</direction></action>
</keybind>
<keybind key="W-Right">
    <action name="UnmaximizeFull"/>
    <action name="MaximizeVert"/>
    <action name="MoveResizeTo">
        <width>50%</width>
    </action>
    <action name="MoveToEdge"><direction>east</direction></action>
</keybind>

```

However, it should be noted that once a window has been 'snapped' to an edge, it will remain vertically maximised unless subsequently maximised and then restored. The solution is to implement additional keybinds - in this instance using the `down` and `up` keys - to do so. This will also make pulling 'snapped' windows from screen edges faster as well:

```
<keybind key="W-Down">
   <action name="Unmaximize"/>
</keybind>
<keybind key="W-Up">
   <action name="Maximize"/>
</keybind>

```

This [Ubuntu forum thread](http://ubuntuforums.org/showthread.php?t=1796793) provides more information. Applications such as [opensnap-git](https://aur.archlinux.org/packages/opensnap-git/) are also available to automatically simulate window snapping behaviour without the use of keybinds.

### Desktop menu

It is also possible to create a keybind to access the desktop menu. For example, the following code will bring up the menu by pressing `CTRL` + `m`:

```
<keybind key="C-m">
    <action name="ShowMenu">
       <menu>root-menu</menu>
    </action>
</keybind>

```

## Menus

It is possible to employ three types of menu in Openbox: `static`, `pipes` (dynamic), and `generators` (static or dynamic). They may also be used alone or in any combination.

### Static

As the name would suggest, this default type of menu does not change in any way, and may be manually edited and/or (re)generated automatically through the use on an appropriate software package.

Fast and efficient, while this type of menu can be used to select applications, it can also be useful to access specific functions and/or perform specific tasks (e.g. desktop configuration), leaving the access of applications to another process (e.g. the [synapse](https://www.archlinux.org/packages/?name=synapse) or [xfce4-appfinder](https://www.archlinux.org/packages/?name=xfce4-appfinder) applications).

The `~/.config/openbox/menu.xml` file will be the sole source of static desktop menu content.

#### menumaker

**Warning:** A root terminal **must** be installed in order to use MenuMaker, even though a standard user terminal may be used to run it. [xterm](https://www.archlinux.org/packages/?name=xterm) is a good choice.

[menumaker](https://www.archlinux.org/packages/?name=menumaker) automatically generates `xml` menus for several window managers, including Openbox, [Fluxbox](/index.php/Fluxbox "Fluxbox"), [IceWM](/index.php/IceWM "IceWM") and [Xfce](/index.php/Xfce "Xfce"). It will search for all installed executable programs and consequently create a menu file for them. It is also possible to configure MenuMaker to exclude certain application types (e.g. relating to [GNOME](/index.php/GNOME "GNOME") or [KDE](/index.php/KDE "KDE")), if desired.

Once installed and executed, it will automatically generate a new `~/.config/openbox/menu.xml` file. To avoid overwriting an existing file, enter:

```
$ mmaker -v OpenBox3

```

Otherwise, to overwrite an existing file, add the `force` argument (`f`):

```
$ mmaker -vf OpenBox3

```

Once a new `~/.config/openbox/menu.xml` file has been generated it may then be manually edited, or configured using a GUI menu editor, such as [obmenu](https://www.archlinux.org/packages/?name=obmenu).

#### obmenu

**Warning:** `obm-xdg` - a pipe menu to generate a list of [GTK+](/index.php/GTK%2B "GTK+") and [GNOME](/index.php/GNOME "GNOME") applications - is also provided with obmenu. However, it has long-running bugs whereby it may produce an invalid output, or even not function at all. Consequently it has been omitted from discussion.

[obmenu](https://www.archlinux.org/packages/?name=obmenu) is a "user-friendly" GUI application to edit `~/.config/openbox/menu.xml`, without the need to code in `xml`.

#### xdg-menu

[archlinux-xdg-menu](https://www.archlinux.org/packages/?name=archlinux-xdg-menu) will automatically generate a menu based on `xdg` files contained within the `/etc/xdg/` directory for numerous Window Managers, including Openbox. Review the [Xdg-menu#OpenBox](/index.php/Xdg-menu#OpenBox "Xdg-menu") article for further information.

#### logout menu options

**Tip:** The commands provided can also be attached to [keybinds](#Keybinds).

The `~/.config/openbox/menu.xml` file can be edited in order to provide a sub-menu with the same options as provided by [oblogout](#oblogout). The sample script below will provide all of these options, with the exception of the ability to lock the screen:

```
<menu id="exit-menu" label="Exit">
	<item label="Log Out">
		<action name="Execute">
			<command>openbox --exit</command>
		</action>
	</item>
	<item label="Shutdown">
		<action name="Execute">
			<command>systemctl poweroff</command>
		</action>
	</item>
	<item label="Restart">
		<action name="Execute">
		        <command>systemctl reboot</command>
		</action>
	</item>
	<item label="Suspend">
		<action name="Execute">
		        <command>systemctl suspend</command>
		</action>
	</item>
	<item label="Hibernate">
		<action name="Execute">
		        <command>systemctl hibernate</command>
		</action>
	</item>
</menu>

```

Once the entries have been composed, add the following line to present the sub-menu where desired within the main desktop menu (usually as the last entry):

```
<menu id="exit-menu"/>

```

### Pipes

**Tip:** It is entirely feasible for a static menu to contain one or more pipe sub-menus. The functionality of some pipe menus may also rely on the installation of relevant software packages.

This type of menu is in essence a script that provides dynamic, refreshed lists on-the-fly as and when run. These lists may be used for multiple purposes, including to list applications, to provide information, and to provide control functions. Pre-configured pipe menus can be installed, although not from the [official repositories](/index.php/Official_repositories "Official repositories"). More experienced users can also modify and/or create their own custom scripts. Again, `~/.config/openbox/menu.xml` may and commonly will contain several pipe menus.

#### Examples

*   [openbox-xdgmenu](https://aur.archlinux.org/packages/openbox-xdgmenu/): fast xdg-menu converter to xml-pipe-menu
*   [obfilebrowser](https://aur.archlinux.org/packages/obfilebrowser/): Application and file browser
*   [obdevicemenu](https://aur.archlinux.org/packages/obdevicemenu/): Management of removable media with [Udisks](/index.php/Udisks "Udisks")
*   [wifi pipe menu](https://bbs.archlinux.org/viewtopic.php?pid=1345031): Wireless networking using [Netctl](/index.php/Netctl "Netctl")

[Openbox.org](http://openbox.org/download-pipemenus.php) also provides a further list of pipe menus.

### Generators

This type of menu is akin to those provided by the taskbars of desktop environments such as [Xfce](/index.php/Xfce "Xfce") or [LXDE](/index.php/LXDE "LXDE"). Automatically updating on-the-fly, this type of menu can be powerful and very convenient. It may also be possible to add custom categories and menu entries; read the documentation for your intended dynamic menu to determine if and how this can be done.

A menu generator will have to be executed from the `~/.config/openbox/menu.xml` file.

#### obmenu-generator

**Tip:** icons can still be disabled in [obmenu-generator](https://aur.archlinux.org/packages/obmenu-generator/), even where enabled in `~/.config/openbox/rc.xml`.

[obmenu-generator](https://aur.archlinux.org/packages/obmenu-generator/) is highly recommended despite being an unofficial package. With the ability to be used as a static or dynamic menu, it is highly configurable, powerful, and versatile. Menu categories and individual entries may also be easily hidden, customised, and/or added with ease. The [official homepage](http://trizenx.blogspot.co.uk/2012/02/obmenu-generator.html) provides further information and screenshots.

Below is an example of how obmenu-generator would be dynamically executed without icons in `~/.config/openbox/menu.xml`:

```
<?xml version="1.0" encoding="utf-8"?>
<openbox_menu>
    <menu id="root-menu" label="OpenBox 3" execute="/usr/bin/obmenu-generator">
    </menu>
</openbox_menu>

```

To automatically iconify entries, the `-i` option would be added:

```
<menu id="root-menu" label="OpenBox 3" execute="/usr/bin/obmenu-generator -i">

```

#### openbox-menu

**Tip:** If this menu produces an error, it may be solved by enabling icons in `~/.config/openbox/rc.xml`.

[openbox-menu](https://aur.archlinux.org/packages/openbox-menu/) uses the [LXDE](/index.php/LXDE "LXDE") [menu-cache](http://sourceforge.net/projects/lxde/files/menu-cache/) to create dynamic menus. The [official homepage](http://fabrice.thiroux.free.fr/openbox-menu_en.html) provides further information and screenshots.

### Menu icons

To show icons next to menu entries, it will be necessary to ensure they are enabled in the `<menu>` section of the `~/.config/openbox/rc.xml` file:

```
<applicationIcons>yes</applicationIcons>

```

Where using a static menu, it will then be necessary to edit the `~/.config/openbox/menu.xml` file to provide both the `icon =` command, along with the full path and icon name for each entry. An example of the syntax used to provide an icon for a category is:

```
<menu id="apps-menu" label="[label name]" icon="[pathway to icon]/[icon name]">

```

### Desktop menu as a panel menu

**Tip:** XDoTool can simulate any keybind for any action, and as such, it may therefore be used for many other purposes...

[xdotool](https://www.archlinux.org/packages/?name=xdotool) is a package that can issue commands to simulate key presses / keybinds, meaning that it is possible to use it to invoke keybind-related actions without having to actually press their assigned keys. As this includes the ability to invoke an assigned keybind for the Openbox desktop menu, it is therefore possible to use XDoTool to turn the Openbox desktop menu into a panel menu. Especially where the desktop menu is heavily customised and feature-rich, this may prove very useful to:

*   Replace an existing panel menu
*   Implement a panel menu where otherwise not provided or possible (e.g. for [Tint2](/index.php/Tint2 "Tint2"))
*   Compensate where losing access to the desktop menu due to the use of an application like [xfdesktop](#xfdesktop) to [manage the desktop](#Desktop_icons_and_wallpapers).

Once XDoTool has been installed - if not already present - it will be necessary to create a keybind to access the root menu in `~/.config/openbox/rc.xml`, and again below the `<!-- Keybindings for running aplications -->` heading. For example, the following code will bring up the menu by pressing `CTRL` + `m`:

```
<keybind key="C-m">
    <action name="ShowMenu">
       <menu>root-menu</menu>
    </action>
</keybind>

```

Openbox must then be [re-configured](#Openbox_reconfiguration). In this instance, XDoTool will be used to simulate the `CTRL` + `m` keypress to access the desktop menu with the following command (note the use of `+` in place of `-`):

```
xdotool key control+m

```

How this command may be used as a panel launcher / icon is largely dependent on the features of panel used. While some panels will allow the above command to be executed directly in the process of creating a new launcher, others may require the use of an executable script. As an example, a custom executable script called `obpanelmenu.sh` will be created in the `~/.config` folder:

```
$ *text editor* ~/.config/obpanelmenu.sh

```

Once the empty file has been opened, the appropriate XDoTool command must be added to the empty file (i.e. to simulate the `CTRL` + `m` keypress for this example):

```
xdotool key control+m

```

After the file has been saved and closed, it may then be made into an executable script with the following command:

```
$ chmod +x ~/.config/obpanelmenu.sh

```

Executing it will bring up the Openbox desktop menu. Consequently, where using a panel that supports drag-and-drop functionality to add new launchers, simply drag the executable script onto it before changing the icon to suit personal taste.

## Desktop theming

**Tip:** It is **strongly advised** to install the [obconf](https://www.archlinux.org/packages/?name=obconf) and [lxappearance-obconf](https://www.archlinux.org/packages/?name=lxappearance-obconf) GUI applications to configure visual settings and theming. The latter is particularly important as it is responsible for generating the `~/.gtkrc-2.0` file (see [GTK+#GTK+ 2.x](/index.php/GTK%2B#GTK.2B_2.x "GTK+")).

It is important to note that a substantial range of both **Openbox-specific** and generalised, **Openbox-compatible** [GTK](/index.php/GTK "GTK") themes are available to change the look of window decorations and the desktop menu. *Generalised* themes are designed to be simultaneously compatible with a range of popular desktop environments and/or window managers, commonly including Openbox. See these [package descriptions](https://aur.archlinux.org/packages/?O=0&C=0&SeB=n&K=gtk-theme-&outdated=&SB=n&SO=a&PP=50&do_Search=Go) for examples.

### Configuration

[obconf](https://www.archlinux.org/packages/?name=obconf) and/or [lxappearance-obconf](https://www.archlinux.org/packages/?name=lxappearance-obconf) should be used to select and configure available GTK themes. See [Uniform Look for Qt and GTK Applications](/index.php/Uniform_Look_for_Qt_and_GTK_Applications "Uniform Look for Qt and GTK Applications") for information about theming Qt based applications like [VirtualBox](/index.php/VirtualBox "VirtualBox") or [Skype](/index.php/Skype "Skype").

### Installation: official and AUR

A good selection of [openbox-themes](https://www.archlinux.org/packages/?name=openbox-themes) are available from the official repositories.

Both Openbox-specific and Openbox-compatible themes installed from the [official repositories](/index.php/Official_repositories "Official repositories") and/or the [AUR](/index.php/AUR "AUR") will be automatically installed to the `/usr/share/themes` directory. Both will also be immediately available for selection.

### Installation: other sources

[box-look.org](https://www.box-look.org/browse/ord/latest/) is an excellent and well-established source of themes. [deviantART.com](http://www.deviantart.com/) is another excellent resource. Many more can be found through the utilisation of a search engine.

### Troubleshooting

There are two particular problems that may be encountered on rare occasions, especially where downloading themes from unsupported websites. These have been addressed below.

#### Theme cannot be used

If for any reason the newly extracted theme cannot be selected, open the theme directory to first ensure that it is indeed compatible with Openbox by determining that an `openbox-3` directory is present, and that within this directory a `themerc` file is also present. An `.obt` (**O**pen**B**ox **T**heme) file may also be present in some instances, which can then be manually loaded in [obconf](https://www.archlinux.org/packages/?name=obconf).

Where expected files and directories are present and correct, then on occasion it is possible that the theme author has not correctly set permission to access the file (e.g. permission may still be for the account of the author, rather than for **root**). To eliminate this possibility, ensure the folder and file permissions are for **root**:

```
# chown -R root /user/share/themes

```

#### Theme looks broken

Of course, the first line of enquiry would be to check that it is not just a badly made, broken theme! Otherwise, ensure that the [Openbox GTK fix](/index.php/Openbox#GTK.2B_2 "Openbox") has been implemented, and then re-start the session. Unfortunately some older themes can simply break if not maintained sufficiently to keep pace with the changes incurred by [GTK](/index.php/GTK "GTK") updates. To avoid such occurrences, it is best to check that desired themes have recently been created or at least updated / patched.

### Edit or create new themes

**Tip:** Where deciding to modify an existing theme (e.g. the colour scheme), it would be best to work on a copy of it, rather than the original. This will retain the original should anything go wrong, and ensure that your changes are not over-written through an update.

The process of creating new or modifying existing themes is covered extensively at the official [openbox.org](http://openbox.org/wiki/Help:Themes) website. [obtheme](https://aur.archlinux.org/packages/obtheme/) is a user-friendly GUI for doing so.

## Compositing effects

Openbox does not provide native support for [compositing](https://en.wikipedia.org/wiki/Compositing_window_manager "wikipedia:Compositing window manager"), and thus requires an external compositor for this purpose.

Although compositing is not a necessary component, it may specifically avoid issues such as screen distortion with [oblogout](#oblogout), and visual glitches with terminal window transparency. See [Xorg#Composite](/index.php/Xorg#Composite "Xorg") for common choices.

## Mouse cursor and application icon themes

See [Cursor themes](/index.php/Cursor_themes "Cursor themes") and [Icons](/index.php/Icons "Icons") for details.

## Desktop icons and wallpapers

Openbox does not natively support the use of desktop icons or wallpapers. As a consequence, it will be necessary to install additional applications for this purpose, where desired.

### Desktop management using file managers

Some file managers have the capacity to fully **manage the desktop**, meaning that they may be used to provide wallpapers and enable the use of icons on the desktop. The [LXDE](/index.php/LXDE "LXDE") desktop environment itself uses PCManFM for this purpose.

See [PCManFM#Desktop_management](/index.php/PCManFM#Desktop_management "PCManFM") and [SpaceFM#Desktop_management](/index.php/SpaceFM#Desktop_management "SpaceFM").

### Wallpaper

See [List_of_applications#Wallpaper_setters](/index.php/List_of_applications#Wallpaper_setters "List of applications")

### Icon programs

While there are programs dedicated to enabling desktop icons alone, it would seem that they have greater drawbacks than the utilisation of file managers for the task. These programs are discussed briefly, below.

#### idesk

[idesk](/index.php/Idesk "Idesk") is a simple program that can enable icons in addition to managing wallpaper. It will be necessary to create an `~/.idesktop` directory, and desktop icons must also be manually created. To use idesk to provide icons, add the following command to the `~/.config/openbox/autostart` file:

```
idesk &

```

#### xfdesktop

[xfdesktop](https://www.archlinux.org/packages/?name=xfdesktop) is the desktop manager for [Xfce](/index.php/Xfce "Xfce"). The [Thunar](/index.php/Thunar "Thunar") file manager will also be downloaded as a dependency. Where this is used, the Openbox desktop menu will no longer be accessible by right-clicking the background.

As such, it will consequently be necessary to access it by other means, such as by [creating a keybind](#Desktop_menu), and/or by - where permitted - re-configuring an installed panel to use the [desktop menu as a panel menu](#Desktop_menu_as_a_panel_menu). To use xfdesktop to provide icons, add the following command to the `~/.config/openbox/autostart` file:

```
xfdesktop &

```

### conky reconfiguration

Particularly where using a file manager to manage the desktop, it will be necessary to edit `~/.conkyrc` to change the `own_window_type` command in order for [conky](/index.php/Conky "Conky") to continue to be displayed (where used). The revised command that should be used is:

```
own_window_type normal

```

## oblogout

See the [Oblogout](/index.php/Oblogout "Oblogout") article for an overview on how to use this useful, graphical logout script.

## Openbox for multihead users

While Openbox provides better than average multihead support on its own, [openbox-multihead-git](https://aur.archlinux.org/packages/openbox-multihead-git/) provides a development branch called **Openbox Multihead** that gives multihead users per-monitor desktops. This model is not commonly found in floating window managers, but exists mainly in tiling window managers. It is explained well on the [Xmonad web site](http://xmonad.org/tour.html#workspace). Also, please see [README.MULTIHEAD](https://github.com/BurntSushi/openbox-multihead/blob/multihead/README.MULTIHEAD) for a more comprehensive description of the new features and configuration options found in Openbox Multihead.

Openbox Multihead will function like normal Openbox when only a single head is available.

A downside to using Openbox Multihead is that it breaks the EWMH assumption that one and only one desktop is visible at any time. Thus, existing pagers will not work well with it. To remedy this, you can install [pager-multihead-git](https://aur.archlinux.org/packages/pager-multihead-git/) alongside Openbox Multihead.

Finally, [pytyle3-git](https://aur.archlinux.org/packages/pytyle3-git/) is a new version of [PyTyle](/index.php/PyTyle "PyTyle") that will work with Openbox Multihead.

Both *pytyle3* and *pager-multihead-git* will work without Openbox Multihead if only one monitor is active.

## Tips and tricks

### Launch a complex command with hotkey

If you need to execute a complex command, use shell functionality.

Special character replacement are as follows:

*   `&`: &amp;
*   `<`: &lt;
*   `>`: &gt;

This example will turn off display immediately and lock screen with [slock](https://www.archlinux.org/packages/?name=slock). It was taken from [this thread](https://bbs.archlinux.org/viewtopic.php?pid=903057).

```
 <keybind key="W-l">
   <action name="Execute">
     <command>sh -c 'slock &amp; (sleep .5 &amp;&amp; xset dpms force off)'</command>
   </action>
 </keybind>

```

Sometimes one need to specify environment variable for application:

```
 <keybind key="A-F7">
   <action name="Execute">
     <command>sh -c "LC_ALL=C obconf"</command>
   </action>
 </keybind>

```

Another example will launch application preserving all stdout and stderr output to file:

```
 <keybind key="A-f">
   <action name="Execute">
     <command>sh -c sh -c "exec gimp &gt;/tmp/gimp.out 2&gt;&amp;1"</command>
   </action>
 </keybind>

```

### Switch desktops using the mouse

It is possible to switch desktop by moving the mouse cursor to the edges of the screen. First install [xdotool](https://www.archlinux.org/packages/?name=xdotool) and add the following two lines to your `~/.xinitrc`:

```
xdotool behave_screen_edge --delay 500 left set_desktop --relative -- -1 &
xdotool behave_screen_edge --delay 500 right set_desktop --relative -- +1 &

```

### Set default applications / file associations

See the [Default applications](/index.php/Default_applications "Default applications") article.

### Stop continous mouse wheel desktop switching

By default Openbox switches from the last desktop back to the first desktop on mouse wheel scroll. Use `<wrap>no</wrap>` in the `mousebind` section to disable this behaviour.

```
   <context name="Desktop">
     <mousebind button="Up" action="Click">
       <action name="GoToDesktop">
         <to>previous</to>
         <wrap>no</wrap>
       </action>
     </mousebind>
     <mousebind button="Down" action="Click">
       <action name="GoToDesktop">
         <to>next</to>
         <wrap>no</wrap>
       </action>
     </mousebind>
   </context>

```

### Ad-hoc window transparency

**Warning:** This may not work where other actions are defined within the action group.

The program [transset-df](https://www.archlinux.org/packages/?name=transset-df) is available in the official repositories, and can enable window transparency on-the-fly.

For example, using the following code in the `<mouse>` section of the `~/.config/openbox/rc.xml` file will enable control of application window transparency by hovering the mouse-pointer over the title bar and scrolling with the middle button:

```
<context name="Titlebar">
    ...
    <mousebind button="Up" action="Click">
        <action name= "Execute" >
        <execute>transset-df -p .2 --inc  </execute>
        </action>
    </mousebind>
    <mousebind button="Down" action="Click">
        <action name= "Execute" >
        <execute>transset-df -p .2 --dec </execute>
        </action>
    </mousebind>
    ...
</context>

```

### Using obxprop for faster configuration

The [openbox](https://www.archlinux.org/packages/?name=openbox) package provides a `obxprop` binary that can parse relevant values for applications settings in `rc.xml`. Officially `obxprop | grep "^_OB_APP"` is recommended for this task. Start the process by running the command shown, then click a window to see its properties in the terminal.

### Xprop values for applications

[xorg-xprop](https://www.archlinux.org/packages/?name=xorg-xprop) is available in the official repositories, and can be used to relay property values for selected applications. Where frequently using per-application settings, the following [Bash Alias](/index.php/Bash#Aliases "Bash") may be useful: dy:

```
alias xp='xprop | grep "WM_WINDOW_ROLE\|WM_CLASS" && echo "WM_CLASS(STRING) = \"NAME\", \"CLASS\""'

```

To use Xorg-XProp, run using the alias given `xp`, and click on the active program desired to define with per-application settins. The results displayed will only be the information that Openbox itself requires, namely the `WM_WINDOW_ROLE` and `WM_CLASS` (name and class) values:

```
WM_WINDOW_ROLE(STRING) = "roster"
WM_CLASS(STRING) = "gajim.py", "Gajim.py"
WM_CLASS(STRING) = "NAME", "CLASS"

```

#### Firefox

For whatever reason, Firefox and like-minded equivalents ignore application rules (e.g. *<desktop>*) unless `class="Firefox*"` is used. This applies irrespective of whatever values **xprop** may report for the program's `WM_CLASS`.

### Switching between keyboard layouts

See the article section [switching between keyboard layouts](/index.php/Keyboard_configuration_in_Xorg#Switching_between_keyboard_layouts "Keyboard configuration in Xorg") for instructions.

### Set grid layout for virtual desktops

Install [obsetlayout](https://aur.archlinux.org/packages/obsetlayout/). To set a 2x2 grid for example:

```
obsetlayout 0 2 2 0

```

Run it without arguments to know what the arguments mean.

## Troubleshooting

### Windows load behind the active window

Some application windows (such as Firefox windows) may load behind the currently active window, causing you to need to switch to the window you just created to focus it. To fix this behavior add this to your `~/.config/openbox/rc.xml` file, inbetween the `<openbox_config>` and `</openbox_config>` tags:

```
<applications>
  <application class="*">
    <focus>yes</focus>
  </application>
</applications>
```

## See also

*   [Openbox Website](http://openbox.org/) - Official website
*   [Box-Look.org](http://www.box-look.org/) - A good resource for themes and related artwork
*   [Openbox Hacks and Configs Thread](https://bbs.archlinux.org/viewtopic.php?id=93126) @ Arch Linux Forums
*   [Openbox Screenshots Thread](https://bbs.archlinux.org/viewtopic.php?id=45692) @ Arch Linux Forums
*   [An Openbox guide](http://urukrama.wordpress.com/openbox-guide/)