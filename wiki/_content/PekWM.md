# PekWM

[The Pek Window Manager](http://pekwm.org) is written by Claes Nästen. The code is based on the aewm++ window manager, but it has evolved enough that it no longer resembles aewm++ at all. It also has an expanded feature-set, including window grouping (not unlike to [ion3](/index.php/Ion3 "Ion3"), pwm, or even [fluxbox](/index.php/Fluxbox "Fluxbox")), auto properties, xinerama and keygrabber that supports keychains, and much more.

## Contents

*   [1 Installation](#Installation)
*   [2 Start](#Start)
    *   [2.1 Display manager](#Display_manager)
    *   [2.2 xinitrc](#xinitrc)
*   [3 Configuring PekWM](#Configuring_PekWM)
    *   [3.1 Menus](#Menus)
        *   [3.1.1 MenuMaker](#MenuMaker)
        *   [3.1.2 Using pekwm-menu](#Using_pekwm-menu)
        *   [3.1.3 Manually](#Manually)
    *   [3.2 Hotkeys](#Hotkeys)
    *   [3.3 Mouse](#Mouse)
    *   [3.4 Startup Programs](#Startup_Programs)
    *   [3.5 Variables](#Variables)
    *   [3.6 Autoproperties](#Autoproperties)
*   [4 Themes](#Themes)
*   [5 Setting a Wallpaper](#Setting_a_Wallpaper)
*   [6 Troubleshooting](#Troubleshooting)
    *   [6.1 When using Nvidia TwinView, windows maximize across both screens](#When_using_Nvidia_TwinView.2C_windows_maximize_across_both_screens)
    *   [6.2 Compositing/transparency does not work properly](#Compositing.2Ftransparency_does_not_work_properly)
    *   [6.3 Scrolling doesn't work in GTK 3 applications](#Scrolling_doesn.27t_work_in_GTK_3_applications)
*   [7 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") [pekwm](https://www.archlinux.org/packages/?name=pekwm).

## Start

### Display manager

[Install](/index.php/Install "Install") and enable a [Display manager](/index.php/Display_manager "Display manager"). PekWM will be added to the session types. Select PekWM from the session menu before logging in.

### xinitrc

Add the following to [xinitrc](/index.php/Xinitrc "Xinitrc"):

```
exec pekwm

```

## Configuring PekWM

The main configuration file is stored in the file `~/.pekwm/config`. It controls the workspace and viewports settings, the menu and harbour behaviour, window edge resistance, and more. There is an example file with complete documentation in the [PekWM documentation](http://www.pekwm.org/files/pekwm/doc/git/html/config/configfile.html).

### Menus

PekWM comes with pre-created menus by default stored in `~/.pekwm/menu`. These do not reflect an existing system and as such are likely to be inaccurate. These should be seen as an example only.

#### MenuMaker

One way to automatically set up menus for your installed applications is [menumaker](https://www.archlinux.org/packages/?name=menumaker). To set up menus of all your installed applications run it with the following command:

```
mmaker --no-desktop pekwm

```

**Note:** This will not overwrite an existing menu file. If you want it to overwrite, add the -f flag to the above command.

To see a full list of options, run `mmaker --help`

Now you can modify the menu file by hand, or simply regenerate the list whenever you install new software.

#### Using pekwm-menu

[pekwm-menu](https://aur.archlinux.org/packages/pekwm-menu/) from the [AUR](/index.php/AUR "AUR") can create a dynamically updated applications menu based on the freedesktop.org xdg menu specification. Usage is fairly straightforward. Add a section similar to the following to your `~/.pekwm/menu` file:

```
 Submenu = "Applications" { Icon = "ICON"
   Entry { Actions = "Dynamic pekwm-menu MENUFILE" }
 }

```

Change "ICON" and "MENUFILE" to your preferred icon and menu file. The menu file can be supplied via gnome, xfce, lxde or a custom creation. Xdg menu files are normally stored in `/etc/xdg/menus`.

To see a full list of options, run `pekwm-menu --help`.

#### Manually

The menu file is `~/.pekwm/menu`. The syntax is fairly straightforward; a simple entry has the following structure:

```
Entry = "NAME" { Actions = "Exec COMMAND &" }

```

A submenu has the following syntax:

```
Submenu = "NAME" {
     Entry = "NAME" { Actions = "Exec COMMAND &" }
     Entry = "NAME" { Actions = "Exec COMMAND &" }
}

```

**Note:** Make sure these brackets are always closed, or you will have errors and your menu will not display.

To add a separator line to the menu, use the following:

```
Separator {}

```

PekWM also supports dynamic menus. These are menu entries or submenus that display the output of a run script every time the entry or submenu is accessed. Check the exact syntax each menu requires, as they may vary.

You can find dynamic menus for [Gmail and network connections](http://www.hewphoria.com/?p=submission&type=config), and one to display the [time and date](http://urukrama.wordpress.com/2008/01/02/show-the-date-and-time-in-pekwms-menu/). There is also a project called [pekwm_menu_tools](http://www.pekwm.org/projects/11) which aim to be a set of useful applications for generating dynamic menus for PekWM.

### Hotkeys

The hotkey settings are stored in `~/.pekwm/keys`. This file controls all the keyboard bindings and keychains used in PekWM. You can add keyboard bindings to launch programs or to perform actions in PekWM, such as show a menu, move a window, switch desktops, etc. For a full list of PekWM's actions, see [the documentation](http://www.pekwm.org/files/pekwm/doc/git/html/config/keys_mouse.html#config-keys_mouse-actions).

You can have more than one action assigned to one key combination. To do so, just separate the actions by a semicolon. Here is an example:

```
KeyPress = "Ctrl Mod1 R" { Actions = "Exec osdctl -s 'Reconfiguring'; Reload" }

```

When you press Ctrl+Alt+R Pekwm will display on the screen the text 'Reconfiguring' (osdctl -s 'Reconfiguring') and reconfigure (Reload). (Note that this requires osdsh to be installed)

The next example will bind a media key to lower the volume:

```
KeyPress = "XF86AudioLowerVolume" { Actions = "exec amixer set Master 5%- unmute &" }

```

You can also do "chains" of keys, so for example the code

```
Chain = "Ctrl Mod1 C" {
     KeyPress = "Q" { Actions = "MoveToEdge TopLeft" }
     KeyPress = "W" { Actions = "MoveToEdge TopCenterEdge" }
}

```

Would make it so that if you first press `Ctrl+Alt+c` and then `q` you move the active window to the top left corner of the screen, and if you press `Ctrl+Alt+c` and then `w` you move the window to the top center edge.

### Mouse

The Mouse settings are stored in `~/.pekwm/mouse`. This file is also rather self-explanatory in it's layout. For example:

```
FrameTitle {
     ButtonRelease = "1" { Actions = "Raise; Focus" }
}

```

means that if you release button 1 (usually left mouse button) over the frame title of a window the window will be "Raised" above the other windows and it will become the focused window.

One of the things PekWM is set up to do by default is to focus windows when the mouse moves over them (as opposed to the "click to focus" style). This is one thing that quite a few users would like to change to the more "traditional" way. To change this, look for the following lines in the file and do what they say (there are quite a few of the first, but only one occurrence of the second):

```
# Remove the following line if you want to use click to focus.
# Uncomment the following line if windows should raise when clicked.

```

### Startup Programs

The startup programs file is `~/.pekwm/start`. If you'd like to display a wallpaper or launch a panel whenever Pekwm is started, you can add entries for these things in that file. Note, though, that these applications are run every time Pekwm is started -- including when you run 'Restart' in the root menu. The commands are executed only after Pekwm is started.

To add an application, use the following structure:

```
_nameofapplication_ &

```

The & at the end is crucial, or anything after it won't be run. To give you an example of what this file could look like, here is mine:

```
xfce4-panel &
conky &
hsetroot -fill ~/images/darkwood.jpg &

```

Before you can use this file, you will have to make it executable with the following command:

```
$ chmod +x ~/.pekwm/start

```

### Variables

The Variables file contains the general variables used in PekWM, the default entry should explain it quite clearly:

```
$TERM="xterm -fn fixed +sb -bg white -fg black"

```

Whenever the variable $TERM is used in any of PekWM's configuration files, the command xterm -fn fixed +sb -bg white -fg black will be run. For example changing it to:

```
$TERM="urxvt"

```

would mean that _urxvt_ would be loaded for terminal commands.

### Autoproperties

If you'd like certain applications to open on certain workspaces, have a certain title, skip the (window) menus, or be automatically tabbed together, you can specify all that here. It is probably the most confusing configuration file in PekWM, but it is also the most powerful file. The amount of things that can be set in this file are far too great to fit here, but it is explained in detail in the [autoproperties page of the documentation](http://www.pekwm.org/files/pekwm/doc/git/html/config/autoprops.html). The default `~/.pekwm/autoproperties` file also contains a crash course to autopropping.

## Themes

*   [Box-Look PekWM Themes](http://box-look.org/index.php?xcontentmode=7403)
*   [Freshmeat PekWM Themes](http://themes.freshmeat.net/search/?q=pekwm&section=projects)
*   [Hewphoria PekWM Themes](http://hewphoria.com/?p=submission&type=theme&cat=1)

To install a theme extract the archive to a themesdir the default ones are:

*   global: `/usr/share/pekwm/themes`
*   user only: `~/.pekwm/themes`

## Setting a Wallpaper

Since PekWM is just a window manager and requires you to use a separate program to set a desktop wallpaper. See [List of applications#Wallpaper setters](/index.php/List_of_applications#Wallpaper_setters "List of applications").

## Troubleshooting

### When using Nvidia TwinView, windows maximize across both screens

Edit `~/.pekwm/config` and look for the line:

```
HonourRandr = "True"

```

and change it to

```
HonourRandr = "False"

```

[Source](https://projects.pekdon.net/projects/pekwm/tasks/124)

### Compositing/transparency does not work properly

As of v0.1.11, PekWM does not appear to correctly support compositing. [xcompmgr](https://www.archlinux.org/packages/?name=xcompmgr) works, but transparent docks and panels do not, and shading windows creates graphical glitches. To fix that you can set the transparency of every window to `.999` (or any other value) with [devilspie](https://www.archlinux.org/packages/?name=devilspie) and [transset-df](https://www.archlinux.org/packages/?name=transset-df), then shading windows works normally.

An example of a devilspie script setting the transparency of every window to .999 with transset-df:

```
(spawn_async (str "transset-df -i " (window_xid) " .999" ))

```

### Scrolling doesn't work in GTK 3 applications

Try setting the [environment variable](/index.php/Environment_variable "Environment variable") `GDK_CORE_DEVICE_EVENTS`. See [PekWM bug #350](https://www.pekwm.org/projects/pekwm/tasks/350).

## See also

*   [Pekwm Homepage](http://pekwm.org/)
*   [Gentoo wiki PekWM page](http://en.gentoo-wiki.com/wiki/PekWM)
*   [Howto: Install and configure Pekwm](http://ubuntuforums.org/showthread.php?t=662204)

Retrieved from "[https://wiki.archlinux.org/index.php?title=PekWM&oldid=402098](https://wiki.archlinux.org/index.php?title=PekWM&oldid=402098)"