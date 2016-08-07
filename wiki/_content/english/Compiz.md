According to [Wikipedia](https://en.wikipedia.org/wiki/Compiz "wikipedia:Compiz"):

	Compiz is a [compositing window manager](https://en.wikipedia.org/wiki/Compositing_window_manager "wikipedia:Compositing window manager") for the [X Window System](/index.php/X_Window_System "X Window System"), using 3D graphics hardware to create fast compositing desktop effects for window management. Effects, such as a minimization animation or a cube workspace, are implemented as loadable plugins.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Installing the 0.9 series](#Installing_the_0.9_series)
    *   [1.2 Installing the 0.8 series](#Installing_the_0.8_series)
*   [2 Starting Compiz](#Starting_Compiz)
    *   [2.1 Enabling important plugins](#Enabling_important_plugins)
        *   [2.1.1 Window decoration](#Window_decoration)
    *   [2.2 Compiz startup](#Compiz_startup)
        *   [2.2.1 Fusion Icon](#Fusion_Icon)
    *   [2.3 Autostarting Compiz in a desktop environment](#Autostarting_Compiz_in_a_desktop_environment)
*   [3 Using Compiz as a standalone window manager](#Using_Compiz_as_a_standalone_window_manager)
    *   [3.1 Starting the session with a display manager](#Starting_the_session_with_a_display_manager)
        *   [3.1.1 Autostarting programs when using a display manager](#Autostarting_programs_when_using_a_display_manager)
    *   [3.2 Starting the session with startx](#Starting_the_session_with_startx)
    *   [3.3 Add a root menu](#Add_a_root_menu)
    *   [3.4 Allow users to shutdown/reboot](#Allow_users_to_shutdown.2Freboot)
*   [4 Tips and tricks](#Tips_and_tricks)
    *   [4.1 Restoring the native window manager](#Restoring_the_native_window_manager)
    *   [4.2 Enabling the Alt+F2 run dialog](#Enabling_the_Alt.2BF2_run_dialog)
    *   [4.3 Remove title bar from maximized windows](#Remove_title_bar_from_maximized_windows)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 Missing GLX_EXT_texture_from_pixmaps](#Missing_GLX_EXT_texture_from_pixmaps)
        *   [5.1.1 On ATI cards (first solution)](#On_ATI_cards_.28first_solution.29)
        *   [5.1.2 On ATI cards (second solution)](#On_ATI_cards_.28second_solution.29)
        *   [5.1.3 On Intel chips](#On_Intel_chips)
    *   [5.2 Compiz starts without window borders with NVIDIA binary drivers](#Compiz_starts_without_window_borders_with_NVIDIA_binary_drivers)
    *   [5.3 Blank screen on resume from suspend-to-ram with NVIDIA binary drivers](#Blank_screen_on_resume_from_suspend-to-ram_with_NVIDIA_binary_drivers)
    *   [5.4 Poor performance from capable graphics cards](#Poor_performance_from_capable_graphics_cards)
    *   [5.5 Screen flicks with NVIDIA card](#Screen_flicks_with_NVIDIA_card)
    *   [5.6 Video tearing](#Video_tearing)
    *   [5.7 Compiz effects not working (GConf backend)](#Compiz_effects_not_working_.28GConf_backend.29)
    *   [5.8 Fusion Icon fails to start](#Fusion_Icon_fails_to_start)
    *   [5.9 Alt+F4 keybinding not working (Xfce)](#Alt.2BF4_keybinding_not_working_.28Xfce.29)
    *   [5.10 Emerald crashes when selecting a theme](#Emerald_crashes_when_selecting_a_theme)
    *   [5.11 No system bell when Compiz is running](#No_system_bell_when_Compiz_is_running)
    *   [5.12 Compiz crashes when enabling the Gnome Compatibility plugin (GSettings backend)](#Compiz_crashes_when_enabling_the_Gnome_Compatibility_plugin_.28GSettings_backend.29)
    *   [5.13 Windows lose focus when unminimised](#Windows_lose_focus_when_unminimised)
    *   [5.14 Popout windows are offset when Compiz is running](#Popout_windows_are_offset_when_Compiz_is_running)
    *   [5.15 Alt-Tab switcher has no background (Emerald)](#Alt-Tab_switcher_has_no_background_.28Emerald.29)
*   [6 Known issues](#Known_issues)
    *   [6.1 Plugins in Compiz 0.8 are not present in Compiz 0.9](#Plugins_in_Compiz_0.8_are_not_present_in_Compiz_0.9)
    *   [6.2 Xfce panel window buttons are not refreshed when a window changes viewport](#Xfce_panel_window_buttons_are_not_refreshed_when_a_window_changes_viewport)
    *   [6.3 Compiz crashes when enabling the D-Bus plugin](#Compiz_crashes_when_enabling_the_D-Bus_plugin)
    *   [6.4 Workspace pager and window buttons issues](#Workspace_pager_and_window_buttons_issues)
    *   [6.5 Xfce workspace switcher has wrong aspect ratio](#Xfce_workspace_switcher_has_wrong_aspect_ratio)
*   [7 See also](#See_also)

## Installation

As of May 2013, Compiz is [no longer available](https://mailman.archlinux.org/pipermail/arch-dev-public/2013-May/024956.html) in the [official repositories](/index.php/Official_repositories "Official repositories"). Packages for installing both the 0.9 and 0.8 series are available in the [AUR](/index.php/AUR "AUR"). The two series are **not parallel installable.**

### Installing the 0.9 series

**Note:**

*   From Compiz 0.9.8 onwards, all Compiz components are developed and distributed as a single project. This means that a single package can provide all of the Compiz components.
*   To have *emerald-themes* with *emerald0.9*, first install [emerald0.9](https://aur.archlinux.org/packages/emerald0.9/) and then install [emerald-themes](https://aur.archlinux.org/packages/emerald-themes/). Doing the opposite will resolve the wrong dependencies and cause conflicts.

Required:

*   **Compiz** — OpenGL compositing window manager with CCSM, Plugins and GTK Window Decorator.

	[https://launchpad.net/compiz](https://launchpad.net/compiz) || [compiz](https://aur.archlinux.org/packages/compiz/)

Optional:

*   **Emerald** — A standalone window decorator for Compiz.

	[http://www.compiz.org/](http://www.compiz.org/) || [emerald0.9](https://aur.archlinux.org/packages/emerald0.9/)

*   **Emerald Themes** — Extra themes for the Emerald window decorator.

	[http://www.northfield.ws/projects/compiz/](http://www.northfield.ws/projects/compiz/) || [emerald-themes](https://aur.archlinux.org/packages/emerald-themes/)

*   **Fusion Icon** — A tray applet for starting Compiz and switching window managers and decorators on the fly.

	[https://github.com/kozec/fusion-icon-gtk3](https://github.com/kozec/fusion-icon-gtk3) || [fusion-icon0.9](https://aur.archlinux.org/packages/fusion-icon0.9/)

### Installing the 0.8 series

**Note:** The [compiz-core](https://aur.archlinux.org/packages/compiz-core/) package does not provide the GTK Window Decorator by default. Users of this package should use [emerald](https://aur.archlinux.org/packages/emerald/) for [#Window decoration](#Window_decoration). Alternatively, use [compiz-gtk](https://aur.archlinux.org/packages/compiz-gtk/) for a Compiz Core package that also provides GTK Window Decorator.

Required:

*   **Compiz Core** — OpenGL compositing window manager.

	[https://github.com/compiz-reloaded/compiz/](https://github.com/compiz-reloaded/compiz/) || [compiz-core](https://aur.archlinux.org/packages/compiz-core/), [compiz-gtk](https://aur.archlinux.org/packages/compiz-gtk/)

Highly recommended:

*   **CompizConfig Settings Manager** — Graphical settings manager for Compiz.

	[https://github.com/compiz-reloaded/ccsm](https://github.com/compiz-reloaded/ccsm) || [ccsm](https://aur.archlinux.org/packages/ccsm/)

*   **Compiz Fusion Plugins Main** — Main plugins collection for Compiz.

	[https://github.com/compiz-reloaded/compiz-plugins-main](https://github.com/compiz-reloaded/compiz-plugins-main) || [compiz-fusion-plugins-main](https://aur.archlinux.org/packages/compiz-fusion-plugins-main/)

*   **Compiz Fusion Plugins Extra** — Extra plugins collection for Compiz.

	[https://github.com/compiz-reloaded/compiz-plugins-extra](https://github.com/compiz-reloaded/compiz-plugins-extra) || [compiz-fusion-plugins-extra](https://aur.archlinux.org/packages/compiz-fusion-plugins-extra/)

Optional:

*   **Compiz Fusion Plugins Experimental** — Experimental Compiz plugins.

	[https://github.com/compiz-reloaded/compiz-plugins-experimental](https://github.com/compiz-reloaded/compiz-plugins-experimental) || [compiz-fusion-plugins-experimental](https://aur.archlinux.org/packages/compiz-fusion-plugins-experimental/)

*   **Emerald** — A standalone window decorator for Compiz.

	[https://github.com/compiz-reloaded/emerald](https://github.com/compiz-reloaded/emerald) || [emerald](https://aur.archlinux.org/packages/emerald/)

*   **Emerald Themes** — Extra themes for the Emerald window decorator.

	[https://github.com/compiz-reloaded/emerald-themes](https://github.com/compiz-reloaded/emerald-themes) || [emerald-themes](https://aur.archlinux.org/packages/emerald-themes/)

*   **Fusion Icon** — A tray applet for starting Compiz and switching window managers and decorators on the fly.

	[https://github.com/compiz-reloaded/fusion-icon](https://github.com/compiz-reloaded/fusion-icon) || [fusion-icon](https://aur.archlinux.org/packages/fusion-icon/)

## Starting Compiz

### Enabling important plugins

**Tip:** Depending on which package you installed Compiz from, some of these plugins may already be activated.

Before starting Compiz, you should activate some plugins to provide basic window manager behaviour or else you will have no ability to drag, scale or close any windows. Important plugins are listed below:

*   Window Decoration - provides window borders, see [#Window decoration](#Window_decoration).
*   Move Window.
*   Resize Window.
*   Place Windows - configure window placement options.
*   Application Switcher - provides an `Alt+Tab` switcher - there are numerous alternative application switcher plugins, for example: Shift Switcher, Static Application Switcher and more. Not all of them use the `Alt+Tab` keybinding.

To be able to switch to different [viewports](/index.php/Compiz_configuration#Workspaces_and_Viewports "Compiz configuration") you will need to enable one of the following:

*   Desktop Cube & Rotate Cube - provides the spinning cube with each side being a different viewport.
*   Desktop Wall - viewports are arranged next to each other - the animation is similar to the workspace switching animation in [Cinnamon](/index.php/Cinnamon "Cinnamon") and [GNOME](/index.php/GNOME "GNOME") Shell.
*   Expo - creates a view of all viewports and windows when the mouse is moved into the top left corner - this plugin can be used on its own or in conjunction with either of the two previous plugins.

#### Window decoration

**Tip:** For information on selecting and managing themes, see: [Compiz configuration#Window decoration themes](/index.php/Compiz_configuration#Window_decoration_themes "Compiz configuration").

The window decorator is the program which provides windows with borders. Unlike window managers such as Kwin or [Xfwm](/index.php/Xfwm "Xfwm") which provide just one decorator, users of Compiz have a choice of three: GTK Window Decorator, KDE Window Decorator and Emerald. The GTK Window Decorator and the KDE Window Decorator are included in the Compiz source and can be optionally compiled whilst building Compiz. Emerald, on the other hand, is a separate, standalone decorator. The *Window Decoration* plugin in CCSM must be ticked otherwise no window decorator will be started.

	Choosing the decorator

The window decorator that will be started is specified under CCSM -> *Effects* -> *Window Decoration* -> *Command*. The command can be one of the following executables: *emerald*, *gtk-window-decorator*, *kde4-window-decorator*. Use the `--replace` switch, e.g. `emerald --replace`, if specifying the decorator executable on its own is not sufficient.

**Tip:** In Compiz 0.9, the decorator command is set to *compiz-decorator* by default. This is a script which will search for the *emerald*, *gtk-window-decorator* and *kde4-window-decorator* executables in that order and start the first one that it finds.

### Compiz startup

**Note:** Some Compiz versions may require you to manually load the CCP plugin on startup: `compiz --replace ccp` [[1]](http://blog.northfield.ws/compiz-release-announcement-0-8-12/)

You can start Compiz using the following command:

```
$ compiz --replace

```

See `compiz --help` for more options.

#### Fusion Icon

**Tip:** When [#Autostarting Compiz in a desktop environment](#Autostarting_Compiz_in_a_desktop_environment) *fusion-icon* can be set as the default command instead of *compiz*.

To start Compiz using Fusion Icon, execute the command below:

```
$ fusion-icon

```

To ensure that *fusion-icon* then starts Compiz, right click on the icon in the panel and go to *select window manager*. Choose *Compiz* if it is not selected already.

### Autostarting Compiz in a desktop environment

See [Desktop environment#Custom window manager](/index.php/Desktop_environment#Custom_window_manager "Desktop environment").

## Using Compiz as a standalone window manager

### Starting the session with a display manager

A standalone Compiz session can be started from a [display manager](/index.php/Display_manager "Display manager"). For most display manager's - [LightDM](/index.php/LightDM "LightDM") for example - all that is required is to create a `.desktop` file in `/usr/share/xsessions` that executes *compiz* (with command line options if needed) or *fusion-icon*. See the article for your display manager. See [Desktop entries](/index.php/Desktop_entries "Desktop entries") for information on creating a `.desktop` file.

#### Autostarting programs when using a display manager

One way in which you could start programs with your Compiz session, when it is started from a [display manager](/index.php/Display_manager "Display manager"), is to use an [xprofile](/index.php/Xprofile "Xprofile") file. Another option is for the `.desktop` file in `/usr/share/xsessions` to not execute *compiz* directly but to execute a script which starts the programs you wish to start and also starts Compiz.

### Starting the session with startx

A Compiz session can be started with *startx*. Define either *compiz* or *fusion-icon* in your `.xinitrc` file. See the [xinitrc](/index.php/Xinitrc "Xinitrc") article for more details.

### Add a root menu

To add a root menu similar to that in [Openbox](/index.php/Openbox "Openbox") and other standalone window managers install [compiz-boxmenu](https://aur.archlinux.org/packages/compiz-boxmenu/). This program is a fork of [compiz-deskmenu](https://aur.archlinux.org/packages/compiz-deskmenu/).

Then copy the config files to your home directory as shown below:

```
# cp -R /etc/xdg/compiz /home/*username*/.config
# chown -R *username*:*group* /home/*username*/.config/compiz

```

where `username` is your username and `group` is the primary group for your user.

Then, open CCSM, navigate to the *Commands* plugin and in *Command line 0* enter the command `compiz-boxmenu`. In the *Key Bindings* tab, set *Run command 0* to `Control+Space` or another key/mouse button combination of choice. Take care not to use a combination that is already used for other functionality.

Now navigate to the *Viewport Switcher* plugin and click on the *Desktop-based Viewport Switching* tab. Change the *Plugin for initiate action* to `core` and change *Action name for initiate* to `run_command0_key`.

You should now find that a menu appears when you click `Control+Space`. To launch a graphical menu editor, click on the *Edit* option or run `compiz-boxmenu-editor` in a terminal. If you would prefer to edit your menu manually, open the following file in your favourite editor: `~/.config/compiz/boxmenu/menu.xml`. For your changes to take effect, you must click the *Reload* option in your menu.

### Allow users to shutdown/reboot

An unprivileged user should be able to execute commands such as `systemctl poweroff` and `systemctl reboot`. You could assign a keyboard shortcut to one of these commands using the *Commands* plugin in CCSM. Alternatively, you could create a launcher for one of these commands in [compiz-boxmenu](https://aur.archlinux.org/packages/compiz-boxmenu/) - see above. For more detailed information on shutting down see the following article: [Allow users to shutdown](/index.php/Allow_users_to_shutdown "Allow users to shutdown").

## Tips and tricks

### Restoring the native window manager

You can switch back to your desktop environment's default window manager with the following command:

```
*wm_name* --replace

```

using *kwin*, *metacity* or *xfwm4* for example instead of *wm_name*.

### Enabling the Alt+F2 run dialog

	GNOME Panel

Enable the *Gnome Compatibility* plugin in CCSM.

	MATE Panel

There are two ways to enable MATE Panel's run dialog in Compiz. You can either:

*   Enable the *MATE Compatibility* plugin in CCSM (use the *Gnome Compatibility* plugin for older Compiz versions which lack the MATE plugin).
*   Map the command below to the `Alt+F2` key combination using the *Commands* plugin in CCSM.

```
mate-panel --run-dialog

```

	LXDE Panel

Map the command below to the `Alt+F2` key combination using the *Commands* plugin in CCSM.

```
lxpanelctl run

```

	Xfce Appfinder

When Compiz is used in an Xfce session, the run dialog (provided by [xfce4-appfinder](https://www.archlinux.org/packages/?name=xfce4-appfinder)) should work without intervention. If you are using Xfce Appfinder in a standalone Compiz session, map the command below to the `Alt+F2` key combination using the *Commands* plugin in CCSM.

```
xfce4-appfinder --collapsed

```

	Other run dialogs

Map the command for a [run dialog](/index.php/List_of_applications#Application_launchers "List of applications") of choice to the `Alt+F2` key combination using the *Commands* plugin in CCSM.

### Remove title bar from maximized windows

As mentioned [here](http://planetkris.com/2009/07/how-to-remove-the-title-bar-with-compiz-without-losing-3-hours-of-your-life/) , enter `ccsm` --> `Window Decoration` in Effects --> `Decoration Windows` : change `any` to `!state=maxvert`.

## Troubleshooting

### Missing GLX_EXT_texture_from_pixmaps

#### On ATI cards (first solution)

You may run into the following error when trying to run Compiz on an ATI card:

```
Missing GLX_EXT_texture_from_pixmap

```

This is because Compiz's binary was compiled against Mesa's OpenGL library rather than ATI's OpenGL library.

Firstly, copy the library into a directory to keep it because ATI's drivers will over write it:

```
$ install -Dm644 /usr/lib/libGL.so.1.2 /usr/lib/mesa/libGL.so.1.2

```

Then you can reinstall your fglrx drivers. Now start Compiz as shown below:

```
LD_PRELOAD=/usr/lib/mesa/libGL.so.1.2 compiz --replace &

```

#### On ATI cards (second solution)

Another possible problem with *GLX_EXT_texture_from_pixmap* on ATI cards is that the card can only render it indirectly. If so, you have to pass the option to your libgl as shown below:

```
LIBGL_ALWAYS_INDIRECT=1 compiz --replace &

```

This workaround was tested on the following card : ATI Technologies Inc Radeon R250 [Mobility FireGL 9000] (rev 02).

#### On Intel chips

Firstly, check that you're using the intel driver as opposed to i810\. Then, use the following command to start Compiz (this command must be used every time).

```
LIBGL_ALWAYS_INDIRECT=true compiz --replace --sm-disable &

```

### Compiz starts without window borders with NVIDIA binary drivers

Firstly, ensure that your window decorator settings are configured correctly - see [#Window decoration](#Window_decoration). If window borders still do not start try adding *Option "AddARGBGLXVisuals" "True"* and *Option "DisableGLXRootClipping" "True"* to your "Screen" section in `/etc/X11/xorg.conf.d/20-nvidia.conf`. If window borders still do not load and you have used other Options elsewhere in `/etc/X11/xorg.conf.d/` try commenting them out and using only the aformentioned ARGBGLXVisuals and GLXRootClipping Options.

### Blank screen on resume from suspend-to-ram with NVIDIA binary drivers

If you receive a blank screen with a responsive cursor upon resume, try disabling sync to vblank. To do so, open CCSM, navigate to the *OpenGL* plugin and untick the *Sync to VBlank* option.

### Poor performance from capable graphics cards

**NVIDIA and Intel chips**: If everything is configured correctly but you still have poor performance with some effects, try disabling *CCSM > General Options > Display Settings > Detect Refresh Rate* and instead choose a value manually.

**NVIDIA chips only**: The inadequate refresh rate with *Detect Refresh Rate* may be due to an option called *DynamicTwinView* being enabled by default which plays a factor in accurately reporting the maximum refresh rate that your card and display support. You can disable *DynamicTwinView* by adding the following line to the "Device" or "Screen" section of your `/etc/X11/xorg.conf.d/20-nvidia.conf`, and then restarting your computer:

```
Option "DynamicTwinView" "False"

```

### Screen flicks with NVIDIA card

To fix this behaviour create the file below:

 `/etc/modprobe.d/nvidia.conf`  `options nvidia NVreg_RegistryDwords="PerfLevelSrc=0x2222"` 

### Video tearing

If you experience video tearing when using Compiz, try enabling the *Workarounds* plugin in CCSM. Once enabled, ensure that the following options are enabled in Workarounds: *Force complete redraw on initial damage*, *Force full screen redraws (buffer swap) on repaint*.

If you are using [Intel graphics](/index.php/Intel_graphics "Intel graphics") and the workaround above does not fix the video tearing, see [Intel graphics#Tear-free video](/index.php/Intel_graphics#Tear-free_video "Intel graphics").

Also see, [#Poor performance from capable graphics cards](#Poor_performance_from_capable_graphics_cards).

### Compiz effects not working (GConf backend)

If you have installed the GTK Window Decorator, check if the GConf schema was correctly installed:

```
$ gconftool-2 -R /apps/compiz/plugins | grep plugins

```

Make sure that all plugins are listed. If they are not, try to install the Compiz schema manually (do **not** run this command as root):

```
$ gconftool-2 --install-schema-file=/usr/share/gconf/schemas/compiz-decorator-gtk.schemas

```

### Fusion Icon fails to start

If you get an output like this from the command line:

 `$ fusion-icon` 
```
* Detected Session: gnome
* Searching for installed applications...
Traceback (most recent call last):
  File "/usr/bin/fusion-icon", line 57, in <module>
    from FusionIcon.interface import choose_interface
  File "/usr/lib/python2.5/site-packages/FusionIcon/interface.py", line 23, in <module>
    import start
  File "/usr/lib/python2.5/site-packages/FusionIcon/start.py", line 36, in <module>
    config.check()
  File "/usr/lib/python2.5/site-packages/FusionIcon/util.py", line 362, in check
    os.makedirs(self.config_folder)
  File "/usr/lib/python2.5/os.py", line 172, in makedirs
    mkdir(name, mode)
OSError: [Errno 13] Permission denied: '/home/andy/.config/compiz'

```

the problem is with the permission on `~/.config/compiz/`. To fix it, use:

```
# chown -R *username* /home/*username*/.config/compiz/

```

### Alt+F4 keybinding not working (Xfce)

If Compiz replaces Xfwm4 at login, this can cause the `Alt+F4` keybinding to become non-functional. To avoid this issue, ensure that only Compiz is started at login - see [Xfce#Default window manager](/index.php/Xfce#Default_window_manager "Xfce").

### Emerald crashes when selecting a theme

You may find that Emerald crashes when selecting certain themes (especially themes that use the legacy engine). If this occurs, select another theme in Emerald Theme Manager and then run the command `emerald --replace`.

### No system bell when Compiz is running

You may find that the system bell (such as the drip sound played when pressing backspace at the beginning of a line in GNOME or MATE Terminal) will not sound if Compiz is running. See the following [upstream bug report](https://bugs.launchpad.net/ubuntu/+source/compiz/+bug/537703).

[PulseAudio](/index.php/PulseAudio "PulseAudio") users, as a workaround, can force PulseAudio to handle the system bell, see [PulseAudio#X11 Bell Events](/index.php/PulseAudio#X11_Bell_Events "PulseAudio").

### Compiz crashes when enabling the Gnome Compatibility plugin (GSettings backend)

If you are using the GSettings backend, you may find that Compiz crashes if you try to enable the *Gnome Compatibility* plugin. In order to enable this plugin whilst using the GSettings backend you need to open CCSM and navigate to *Preferences*. Under the header *Integration* untick the box labelled *Enable integration into the desktop environment*. After unticking this option, you should find it possible to enable the *Gnome Compatibility* plugin.

### Windows lose focus when unminimised

You may find that certain windows (such as a [Chromium](/index.php/Chromium "Chromium") window) will lose focus when unminimised. See the following [upstream bug report](https://bugs.launchpad.net/compiz/+bug/1328779). One possible solution is to enable the *Keep previews of minimized windows* option, located within the *Workarounds* plugin.

**Note:** If you use the Chrome/Chromium browser and you enable this workaround, you will need to ensure that the *Use system title bar and borders* option within Chrome is enabled. If Chrome's own titlebar is used with the *Keep previews of minimized windows* Compiz workaround then when Chrome is minimized, the desktop beneath will become unresponsive.

### Popout windows are offset when Compiz is running

You may find that popout windows for panels which are placed at the bottom of the screen are offset by a few pixels so that the window appears to float above the panel. This problem is known to affect Xfce and KDE and may affect other desktops as well. Listed below are a number of workarounds that might fix some cases.

*   Place the panel at the top of screen instead of the bottom - this should work in most cases.
*   Disable the *Place Windows* plugin - this works for the Xfce Whisker Menu plugin but may not work elsewhere.
*   Use fixed window placement to determine the window's position. This can be set from the *Place Windows* plugin. For instance, for the Whisker Menu, specify that the window with the title *Whisker Menu* should appear at (-1, -1).

For more information, see the following [upstream bug report](https://bugs.launchpad.net/compiz/+bug/1419346).

### Alt-Tab switcher has no background (Emerald)

You may find that the `Alt-Tab` switcher (provided by the staticswitcher or switcher plugins) has a completely transparent background when using Emerald as well. This can make it hard to differentiate window thumbnails from the desktop background behind them. As of Compiz 0.9.12 ([revision 3975](http://bazaar.launchpad.net/~compiz-team/compiz/0.9.12/revision/3975)) a workaround is available. In CCSM, navigate to *Application Switcher* or *Static Application Switcher* depending on which plugin you are using. For the former, the *Background* settings are located under *General* and for the latter the settings are located under *Appearance*. Once you have found the settings, ensure that the *Set background color* box is ticked. The default is a dark grey which can be optionally changed.

Alternatively, use GTK Window Decorator instead of Emerald or use a different window switcher altogether such as the shift switcher. Note that even if you are using the GTK Window Decorator, you can still change the background color as described above.

## Known issues

### Plugins in Compiz 0.8 are not present in Compiz 0.9

Many plugins that were popular in Compiz 0.8 (such as the Animations Add-On plugin) were disabled in Compiz versions 0.9.8 and above in order to complete [OpenGL ES](https://en.wikipedia.org/wiki/OpenGL_ES "wikipedia:OpenGL ES") support. Disabled plugins that receive patches for this issue may well be re-enabled in future releases. For more information, see the [Compiz 0.9.8 release notes](https://launchpad.net/compiz/0.9.8/0.9.8.0).

Likewise, Compiz Plugins Unsupported (a package which includes plugins such as *Atlantis*) is unavailable in recent versions of Compiz 0.9\. It has not been developed for the Compiz 0.9 series since Compiz 0.9.5 and no longer builds successfully.

### Xfce panel window buttons are not refreshed when a window changes viewport

You may find that if you right click on a window title and choose an option such as *Move to Workspace Right* then the window will move but the window button will still be visible in the viewport the window moved from until you switch viewports. This issue can be fixed by replacing [xfce4-panel](https://www.archlinux.org/packages/?name=xfce4-panel) with [xfce4-panel-compiz](https://aur.archlinux.org/packages/xfce4-panel-compiz/) which incorporates a patch for this issue. See the following [upstream bug report](https://bugzilla.xfce.org/show_bug.cgi?id=10908) for more information.

### Compiz crashes when enabling the D-Bus plugin

The *D-Bus* plugin will cause Compiz to crash if enabled in conjunction with certain other plugins such as the *Cube* plugin. See the following [upstream bug report](https://bugs.launchpad.net/compiz/+bug/959395).

### Workspace pager and window buttons issues

Only a few [panels and docks](/index.php/List_of_applications#Taskbars_.2F_panels_.2F_docks "List of applications") are compatible with Compiz's [viewports](/index.php/Compiz_configuration#Workspaces_and_Viewports "Compiz configuration"). Incompatible panels and docks may display issues such as showing all window buttons in all workspaces or the workspace pager may only show one workspace available. The panels listed below are known to be compatible:

*   [xfce4-panel](https://www.archlinux.org/packages/?name=xfce4-panel)
*   [mate-panel](https://www.archlinux.org/packages/?name=mate-panel)
*   [perlpanel](https://www.archlinux.org/packages/?name=perlpanel)
*   [gnome-panel](https://www.archlinux.org/packages/?name=gnome-panel)
*   [cairo-dock](https://www.archlinux.org/packages/?name=cairo-dock)

### Xfce workspace switcher has wrong aspect ratio

When Compiz is used with Xfce Panel 4.11 and above, the workspace pager will use the width of only one workspace but will divide this space into ever smaller bars, according to how many viewports Compiz will specify. This issue can be fixed by replacing [xfce4-panel](https://www.archlinux.org/packages/?name=xfce4-panel) with [xfce4-panel-compiz](https://aur.archlinux.org/packages/xfce4-panel-compiz/) which incorporates a patch for this issue. For more information, see the following [upstream bug report](https://bugzilla.xfce.org/show_bug.cgi?id=11697).

## See also

*   [Compiz in Launchpad](https://launchpad.net/compiz)
*   [Compiz Home](http://compiz.org), including wiki and forum (website and wiki are unmaintained)
*   [Troubleshooting - Compiz Wiki](http://wiki.compiz.org/Troubleshooting), (wiki is unmaintained)