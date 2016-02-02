# Xfce

[Xfce](http://www.xfce.org) is a lightweight and modular [Desktop environment](/index.php/Desktop_environment "Desktop environment") currently based on GTK+ 2\. To provide a complete user experience, it includes a window manager, a file manager, desktop and panel.

## Contents

*   [1 Installation](#Installation)
*   [2 Starting Xfce](#Starting_Xfce)
*   [3 Configuration](#Configuration)
    *   [3.1 Menu](#Menu)
        *   [3.1.1 Whisker menu](#Whisker_menu)
        *   [3.1.2 Edit entries](#Edit_entries)
    *   [3.2 Desktop](#Desktop)
        *   [3.2.1 Transparent background for icon titles](#Transparent_background_for_icon_titles)
        *   [3.2.2 Remove Thunar options from right-click menu](#Remove_Thunar_options_from_right-click_menu)
        *   [3.2.3 Kill window shortcut](#Kill_window_shortcut)
    *   [3.3 Session](#Session)
        *   [3.3.1 Startup applications](#Startup_applications)
            *   [3.3.1.1 Delay application startup](#Delay_application_startup)
        *   [3.3.2 Lock the screen](#Lock_the_screen)
        *   [3.3.3 User switching](#User_switching)
        *   [3.3.4 Disable saved sessions](#Disable_saved_sessions)
        *   [3.3.5 Default window manager](#Default_window_manager)
    *   [3.4 Theming](#Theming)
    *   [3.5 Sound](#Sound)
        *   [3.5.1 Xfce4 mixer](#Xfce4_mixer)
            *   [3.5.1.1 Change default sound card in Xfce4 Mixer](#Change_default_sound_card_in_Xfce4_Mixer)
        *   [3.5.2 Keyboard volume buttons](#Keyboard_volume_buttons)
            *   [3.5.2.1 Shortcuts](#Shortcuts)
    *   [3.6 Keyboard Shortcuts](#Keyboard_Shortcuts)
    *   [3.7 Polkit Authentication Agent](#Polkit_Authentication_Agent)
    *   [3.8 Display blanking](#Display_blanking)
*   [4 Tips and tricks](#Tips_and_tricks)
    *   [4.1 Hide partitions from thunar and xfdesktop](#Hide_partitions_from_thunar_and_xfdesktop)
    *   [4.2 Screenshots](#Screenshots)
    *   [4.3 Disable Terminal F1 and F11 shortcuts](#Disable_Terminal_F1_and_F11_shortcuts)
    *   [4.4 Terminal color themes or palettes](#Terminal_color_themes_or_palettes)
        *   [4.4.1 Changing default color theme](#Changing_default_color_theme)
        *   [4.4.2 Terminal tango color theme](#Terminal_tango_color_theme)
    *   [4.5 Colour management](#Colour_management)
    *   [4.6 Multiple monitors](#Multiple_monitors)
    *   [4.7 SSH agents](#SSH_agents)
    *   [4.8 Scroll a background window without shifting focus on it](#Scroll_a_background_window_without_shifting_focus_on_it)
    *   [4.9 Mouse button modifier](#Mouse_button_modifier)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 Action buttons are missing icons](#Action_buttons_are_missing_icons)
    *   [5.2 Desktop icons rearrange themselves](#Desktop_icons_rearrange_themselves)
    *   [5.3 GTK themes not working with multiple monitors](#GTK_themes_not_working_with_multiple_monitors)
    *   [5.4 Icons do not appear in right-click menus](#Icons_do_not_appear_in_right-click_menus)
    *   [5.5 Keyboard settings are not saved in xkb-plugin](#Keyboard_settings_are_not_saved_in_xkb-plugin)
    *   [5.6 NVIDIA and xfce4-sensors-plugin](#NVIDIA_and_xfce4-sensors-plugin)
    *   [5.7 Preferred Applications preferences have no effect](#Preferred_Applications_preferences_have_no_effect)
    *   [5.8 Restore default settings](#Restore_default_settings)
    *   [5.9 Session failure](#Session_failure)
    *   [5.10 Fonts in window title crashing xfce4-title](#Fonts_in_window_title_crashing_xfce4-title)
    *   [5.11 Laptop lid settings ignored](#Laptop_lid_settings_ignored)
*   [6 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [xfce4](https://www.archlinux.org/groups/x86_64/xfce4/) group. You may also wish to install the [xfce4-goodies](https://www.archlinux.org/groups/x86_64/xfce4-goodies/) group which includes extra plugins and a number of useful utilities such as the [mousepad](https://www.archlinux.org/packages/?name=mousepad) editor. Xfce uses the [Xfwm](/index.php/Xfwm "Xfwm") window manager by default.

## Starting Xfce

Choose _Xfce Session_ from the menu in a [display manager](/index.php/Display_manager "Display manager") of choice, or add `exec startxfce4` to [Xinitrc](/index.php/Xinitrc "Xinitrc").

**Note:** Do not call the `xfce4-session` executable directly; `startxfce4` is the correct command which, in turn, calls the former when appropriate.

## Configuration

Xfce stores configuration options in [Xfconf](http://docs.xfce.org/xfce/xfconf/start). There are several ways to modify these options:

*   In the main menu, select [Settings](http://docs.xfce.org/xfce/xfce4-settings/start) and the category you want to customize. Categories are programs usually located in `/usr/bin/xfce4-*` and `/usr/bin/xfdesktop-settings`.
*   `xfce4-settings-editor` can see and modify all settings. Options modified here will take effect immediately. Use `xfconf-query` to change settings from the commandline; see [the documentation](http://docs.xfce.org/xfce/xfconf/xfconf-query) for details.
*   Settings are stored in XML files in `~/.config/xfce4/xfconf/xfce-perchannel-xml/` which can be edited by hand. However, changes made here will _not_ take effect immediately.

### Menu

#### Whisker menu

[xfce4-whiskermenu-plugin](https://www.archlinux.org/packages/?name=xfce4-whiskermenu-plugin) is an alternate application launcher. It shows a list of favorites and browses through all installed applications through category buttons.

#### Edit entries

A number of graphical tools are available for this task:

*   **XAME** — GUI tool written in Gambas designed specifically for editing menu entries in Xfce, it will not work in other environments.

	[http://www.redsquirrel87.com/XAME.html](http://www.redsquirrel87.com/XAME.html) || [xame](https://aur.archlinux.org/packages/xame/)<sup><small>AUR</small></sup>

*   **MenuLibre** — An advanced menu editor that provides modern features in a clean, easy-to-use interface.

	[https://launchpad.net/menulibre](https://launchpad.net/menulibre) || [menulibre](https://aur.archlinux.org/packages/menulibre/)<sup><small>AUR</small></sup>.

*   **Alacarte** — Menu editor for GNOME

	[http://www.gnome.org/](http://www.gnome.org/) || [alacarte](https://www.archlinux.org/packages/?name=alacarte)

Alternatively, create the file `~/.config/menus/xfce-applications.menu` manually. See the example configuration below:

```
<!DOCTYPE Menu PUBLIC "-//freedesktop//DTD Menu 1.0//EN"
  "[http://www.freedesktop.org/standards/menu-spec/1.0/menu.dtd](http://www.freedesktop.org/standards/menu-spec/1.0/menu.dtd)">

```

```
<Menu>
    <Name>Xfce</Name>
    <MergeFile type="parent">/etc/xdg/menus/xfce-applications.menu</MergeFile>

```

```
    <Exclude>
        <Filename>xfce4-run.desktop</Filename>
        <Filename>exo-terminal-emulator.desktop</Filename>
        <Filename>exo-file-manager.desktop</Filename>
        <Filename>exo-mail-reader.desktop</Filename>
        <Filename>exo-web-browser.desktop</Filename>
        <Filename>xfce4-about.desktop</Filename>
        <Filename>xfhelp4.desktop</Filename>
    </Exclude>

```

```
    <Layout>
        <Merge type="all"/>
        <Separator/>
        <Menuname>Settings</Menuname>
        <Separator/>
        <Filename>xfce4-session-logout.desktop</Filename>
    </Layout>
</Menu>

```

The `<MergeFile>` tag includes the default Xfce menu.

The `<Exclude>` tag excludes applications which we do not want to appear in the menu. Here we excluded some Xfce default shortcuts, but you can exclude `firefox.desktop` or any other application.

The `<Layout>` tag defines the layout of the menu. The applications can be organized in folders or however we wish. For more details see the [Xfce wiki](http://wiki.xfce.org/howto/customize-menu).

You can also make changes to the Xfce menu by editing the `.desktop` files themselves. To hide entries, see [Desktop entries#Hide desktop entries](/index.php/Desktop_entries#Hide_desktop_entries "Desktop entries"). You can edit the application's category by modifying the `Categories=` line of the desktop entry, see [Desktop entries#File example](/index.php/Desktop_entries#File_example "Desktop entries").

### Desktop

#### Transparent background for icon titles

To change the default white background of desktop icon titles to something more suitable, create or edit `~/.gtkrc-2.0`:

```
style "xfdesktop-icon-view" {
    XfdesktopIconView::label-alpha = 10
    base[NORMAL] = "#000000"
    base[SELECTED] = "#71B9FF"
    base[ACTIVE] = "#71B9FF"
    fg[NORMAL] = "#fcfcfc"
    fg[SELECTED] = "#ffffff"
    fg[ACTIVE] = "#ffffff"
}
widget_class "*XfdesktopIconView*" style "xfdesktop-icon-view"

```

#### Remove Thunar options from right-click menu

Issue the following command:

```
$ xfconf-query -c xfce4-desktop -v --create -p /desktop-icons/style -t int -s 0

```

#### Kill window shortcut

Xfce does not have a shortcut to kill a window, for example when a program freezes.

With [xorg-xkill](https://www.archlinux.org/packages/?name=xorg-xkill), use `xkill` to interactively kill a window. For the currently active window, use [xdotool](https://www.archlinux.org/packages/?name=xdotool):

```
$ xdotool getwindowfocus windowkill

```

Alternatively:

```
$ xkill -id "$(xprop -root -notype | sed -n '/^_NET_ACTIVE_WINDOW/ s/^.*# *\|\,.*$//g p')"

```

To add the shortcut, use _Settings > Keyboard_ or an application like [xbindkeys](https://www.archlinux.org/packages/?name=xbindkeys).

### Session

#### Startup applications

To launch custom applications when Xfce starts up, click the _Applications Menu > Settings > Settings Manager_ and then choose the _Session and Startup_ option and click the tab _Application Autostart_. You will see a list of programs that get launched on startup. To add an entry, click the _Add_ button and fill out the form, specifying the path to an executable you want to run.

Alternatively, add the commands you wish to run (including setting environment variables) to [xinitrc](/index.php/Xinitrc "Xinitrc") (or [xprofile](/index.php/Xprofile "Xprofile") when a [display manager](/index.php/Display_manager "Display manager") is being used).

##### Delay application startup

Sometimes it might be useful to delay the startup of an application. Specifying a command such as `sleep 3 && command` under _Application Autostart_ does not work. As a workaround, one can use the following syntax instead:

```
sh -c "sleep 3 && command"

```

#### Lock the screen

To lock an Xfce4 session through the _xflock4_ script one of [xscreensaver](https://www.archlinux.org/packages/?name=xscreensaver), [gnome-screensaver](https://www.archlinux.org/packages/?name=gnome-screensaver), [slock](https://www.archlinux.org/packages/?name=slock) or [xlockmore](https://www.archlinux.org/packages/?name=xlockmore) packages needs to be installed. If you are using the Whisker Menu and your screen locker is not specified in _xflock4_, you can change the lock command using _Properties > Behavior > Lock Screen_.

Bear in mind that if you want Xfce Power Manager to lock the screen on events such as lid close or suspend, your screen locker must be specified in _xflock4_. If it is not, you can create a local copy of _xflock4_, for example `/usr/local/bin/xflock4`, which specifies another screen locker of choice.

See [List of applications/Security#Screen lockers](/index.php/List_of_applications/Security#Screen_lockers "List of applications/Security") for a comprehensive list of screen lockers.

**Tip:** The [light-locker](https://www.archlinux.org/packages/?name=light-locker) session locker integrates with [xfce4-power-manager](https://www.archlinux.org/packages/?name=xfce4-power-manager). If light-locker is installed, a _Security_ tab is added to the power manager settings and the existing _Lock screen when system is going for sleep_ setting is relocated under the _Security_ tab.

#### User switching

**Note:** For the User Switch action button to work without GDM, a workaround is required:

*   For LXDM - [LXDM#Simultaneous users and switching users](/index.php/LXDM#Simultaneous_users_and_switching_users "LXDM").
*   For LightDM - [LightDM#User switching under Xfce4](/index.php/LightDM#User_switching_under_Xfce4 "LightDM").

Xfce4 has support for user switching when used with a [Display manager](/index.php/Display_manager "Display manager") that has this functionality - examples being [LightDM](/index.php/LightDM "LightDM") and [GDM](/index.php/GDM "GDM"). Please consult your display manager's wiki page for more information. When you have a display manager installed and configured correctly you can switch users from the 'action buttons' menu item in the panel.

#### Disable saved sessions

Per user, saved sessions can be disabled by executing the following:

```
$ xfconf-query -c xfce4-session -p /general/SaveOnExit -s false

```

Then navigate to _Applications_ -> _Settings_ -> _Session and Startup_ -> _Sessions_ and click the _Clear saved sessions_ button.

**Tip:** If the command above does not change the setting persistently, use the following command instead: `xfconf-query -c xfce4-session -p /general/SaveOnExit -n -t bool -s false`

Alternatively, Xfce [kiosk mode](https://wiki.xfce.org/howto/kiosk_mode) can be used to disable the saving of sessions systemwide. To disable sessions, create or edit the file `/etc/xdg/xfce4/kiosk/kioskrc` and add the following:

```
[xfce4-session]
SaveSession=NONE

```

If kiosk mode is not working, the user can set read only permissions for the sessions directory:

```
$ rm ~/.cache/sessions/* && chmod 500 ~/.cache/sessions

```

This will prevent Xfce from saving any sessions despite any configuration that specifies otherwise.

#### Default window manager

**Note:** For the changes to take effect, you will need to clear the saved sessions and ensure that session saving is disabled when logging out for the first time. Once the window manager of choice is running, session saving can be enabled again.

The files specifying the default window manager are found in the following locations:

*   `~/.config/xfce4/xfconf/xfce-perchannel-xml/xfce4-session.xml` - per user
*   `/etc/xdg/xfce4/xfconf/xfce-perchannel-xml/xfce4-session.xml` - systemwide

The default window manager for the user can be set easily using _xfconf-query_:

```
$ xfconf-query -c xfce4-session -p /sessions/Failsafe/Client0_Command -t string -sa **wm_name**

```

If you want to start the window manager with command line options, see the command below:

```
$ xfconf-query -c xfce4-session -p /sessions/Failsafe/Client0_Command -t string -t string -s **wm_name** -s **--wm-option**

```

If you need more command line options, simply add more `-t string` and `-s **--wm-option**` arguments to the command.

If you want to change the default window manager systemwide, edit the file specified above manually, changing _xfwm4_ to the preferred window manager and adding more `<value type="string" value="**--wm-option**"/>` lines for extra command line options if needed.

You can also change the window manager by autostarting `**wm_name** --replace` using the autostart facility or by running `**wm_name** --replace &` in a terminal and making sure the session is saved on logout. Be aware though that this method does not truly change the default manager, it merely replaces it at login. Note that if you are using the autostart facility, you should disable saved sessions as this could lead to the new window manager being started twice after the default window manager.

### Theming

XFCE themes are available at [xfce-look.org](http://www.xfce-look.org). _Xfwm_ themes are stored in `/usr/share/themes/xfce4`, and set in _Settings > Window Manager_. [GTK+](/index.php/GTK%2B "GTK+") themes are set in _Settings > Appearance_.

To achieve a uniform look for all applications, see [Uniform look for Qt and GTK applications](/index.php/Uniform_look_for_Qt_and_GTK_applications "Uniform look for Qt and GTK applications").

See also [Cursor themes](/index.php/Cursor_themes "Cursor themes"), [Icons](/index.php/Icons "Icons"), and [Font configuration](/index.php/Font_configuration "Font configuration").

### Sound

#### Xfce4 mixer

**Note:** Xfce4 mixer and Xfce4 volumed are no longer being maintained upstream as they cannot be ported to GStreamer 1.0\. For more information, see the 4.12 [news post](http://www.xfce.org/about/news/?post=1425081600).

Xfce4 mixer, provided by [xfce4-mixer](https://www.archlinux.org/packages/?name=xfce4-mixer), is the GUI mixer app and panel plugin from the Xfce team. It is part of the xfce4 group. For [PulseAudio](/index.php/PulseAudio "PulseAudio") and [OSS](/index.php/OSS "OSS") support, you will need to install [gstreamer0.10-good-plugins](https://www.archlinux.org/packages/?name=gstreamer0.10-good-plugins) if it is not installed already.

You might need to change the default sound card for Xfce4 mixer to function correctly. For further details, such as how to set the default sound card, see [Advanced Linux Sound Architecture#Set the default sound card](/index.php/Advanced_Linux_Sound_Architecture#Set_the_default_sound_card "Advanced Linux Sound Architecture"). Alternatively you can use [PulseAudio](/index.php/PulseAudio "PulseAudio") together with [pavucontrol](https://www.archlinux.org/packages/?name=pavucontrol) or [OSS](/index.php/OSS "OSS"). For OSS, see [OSS#Applications that use GStreamer](/index.php/OSS#Applications_that_use_GStreamer "OSS").

If you did need to change the default soundcard, logout to ensure that the changes take effect.

##### Change default sound card in Xfce4 Mixer

In some cases (when using [PulseAudio](/index.php/PulseAudio "PulseAudio") or [xfce4-volumed](https://aur.archlinux.org/packages/xfce4-volumed/)<sup><small>AUR</small></sup> for instance) it might be necessary to change the default sound card in Xfce4 Mixer in order for volume control to work as expected. [[1]](http://grumbel.blogspot.co.uk/2011/10/fixing-volume-control-in-xfce4.html)

To change the default sound card, open _xfce4-settings-editor_ and navigate to **xfce4-mixer** and check the entries under **sound-cards**. Locate the correct entry for the card you are using and then replace the values of **sound-card** and **active-card** with the entry. If you are using PulseAudio then the entry will likely be similar to the following: **PlaybackInternalAudioAnalogStereoPulseAudioMixer**. Then logout for the changes to take effect.

#### Keyboard volume buttons

If the [xfce4-mixer](https://www.archlinux.org/packages/?name=xfce4-mixer) package is version `4.10.0-3` or greater, then the mixer panel applet provides the ability to control the volume using the keyboard. However, volume notifications will not be shown. Alternatively, [xfce4-volumed](https://aur.archlinux.org/packages/xfce4-volumed/)<sup><small>AUR</small></sup> maps volume keys to Xfce4 mixer, and displays notifications through Xfce4-notifyd. When using [PulseAudio](/index.php/PulseAudio "PulseAudio"), use [xfce4-volumed-pulse](https://aur.archlinux.org/packages/xfce4-volumed-pulse/)<sup><small>AUR</small></sup> instead.

If you are using PulseAudio and you do not wish to use Xfce4 Mixer at all, install [xfce4-pulseaudio-plugin](https://aur.archlinux.org/packages/xfce4-pulseaudio-plugin/)<sup><small>AUR</small></sup>. This provides a panel applet which has support for keyboard volume control and volume notifications.

For non desktop environment specific alternatives, see [List of applications#Volume managers](/index.php/List_of_applications#Volume_managers "List of applications").

##### Shortcuts

If you are not using an applet or daemon that controls the volume keys, you can map volume control commands to your volume keys manually using Xfce's keyboard settings. For the sound system you are using, see the sections linked to below for the appropriate commands.

*   ALSA: see [Advanced Linux Sound Architecture#Keyboard volume control](/index.php/Advanced_Linux_Sound_Architecture#Keyboard_volume_control "Advanced Linux Sound Architecture").
*   PulseAudio: see [PulseAudio#Keyboard volume control](/index.php/PulseAudio#Keyboard_volume_control "PulseAudio")
*   OSS: see [OSS#Using multimedia keys with OSS](/index.php/OSS#Using_multimedia_keys_with_OSS "OSS").

### Keyboard Shortcuts

Keyboard shortcuts are defined in two places: _Settings > Window Manager > Keyboard_, and _Settings > Keyboard > Shortcuts_.

### Polkit Authentication Agent

The [polkit-gnome](https://www.archlinux.org/packages/?name=polkit-gnome) agent will be installed along with [xfce4-session](https://www.archlinux.org/packages/?name=xfce4-session) and autostarted automatically; no user intervention is required. For more information, see [Polkit#Authentication agents](/index.php/Polkit#Authentication_agents "Polkit").

A third party polkit authentication agent for Xfce is also available, see [xfce-polkit-git](https://aur.archlinux.org/packages/xfce-polkit-git/)<sup><small>AUR</small></sup>.

### Display blanking

**Note:** There are some issues associated with blanking and resuming from blanking in some configurations. See [[2]](https://bbs.archlinux.org/viewtopic.php?id=194313&p=2)[[3]](https://bugzilla.xfce.org/show_bug.cgi?id=11107).

Some programs that are commonly used with Xfce will control monitor blanking and [DPMS](/index.php/DPMS "DPMS") (monitor powersaving) settings. They are discussed below.

	Xfce Power Manager

Xfce Power Manager will control blanking and DPMS settings. These settings can be configured by running _xfce4-power-manager-settings_ and clicking the _Display_ tab. Note that unticking the _Handle display power management_ option means that the Power Manager will disable DPMS - it does not mean that the Power Manager will relinquish control of DPMS. Also note that it will not disable screen blanking. To disable both blanking and DPMS, right click on the power manager system tray icon or left click on the panel applet and make sure that the option labelled _Presentation mode_ is ticked.

	XScreenSaver

See [XScreenSaver#DPMS and blanking settings](/index.php/XScreenSaver#DPMS_and_blanking_settings "XScreenSaver"). Note that if XScreenSaver is running alongside Xfce Power Manager, it may not be entirely clear which application is in control of blanking and DPMS as both applications are competing for control of the same settings. Therefore, in a situation where it is important that the monitor not be blanked (when watching a film for instance), it is advisable to disable blanking and DPMS through both applications.

	xset

If neither of the above applications are running, then blanking and DPMS settings can be controlled using the _xset_ command, see [DPMS#Modifying DPMS and screensaver settings using xset](/index.php/DPMS#Modifying_DPMS_and_screensaver_settings_using_xset "DPMS").

## Tips and tricks

### Hide partitions from thunar and xfdesktop

See [Udisks#Hide selected partitions](/index.php/Udisks#Hide_selected_partitions "Udisks").

### Screenshots

Xfce has its own screenshot tool, [xfce4-screenshooter](https://www.archlinux.org/packages/?name=xfce4-screenshooter). It is part of the [xfce4-goodies](https://www.archlinux.org/groups/x86_64/xfce4-goodies/) group.

Go to _Applications > Settings > Keyboard_, _Application Shortcuts_. Add the `xfce4-screenshooter -f` (or `-w` for the active window) command to use the `Print` key in order to take fullscreen screenshots. See screenshooter's man page for other optional arguments.

Alternatively, an independent screenshot program like [scrot](/index.php/Taking_a_screenshot#scrot "Taking a screenshot") can be used.

### Disable Terminal F1 and F11 shortcuts

The xfce terminal binds F1 and F11 to help and fullscreen, respectively, which can make using programs like htop difficult. To disable those shortcuts, create or edit its configuration file, then log out and log back in. F10 can disabled in the Preferences menu.

 `~/.config/xfce4/terminal/accels.scm` 

```
(gtk_accel_path "<Actions>/terminal-window/fullscreen" "")
(gtk_accel_path "<Actions>/terminal-window/contents" "")

```

### Terminal color themes or palettes

Terminal color themes or palettes can be changed in GUI under Appearance tab in Preferences. These are the colors that are available to most console applications like [Emacs](/index.php/Emacs "Emacs"), [Vi](/index.php/Vi "Vi") and so on. Their settings are stored individually for each system user in `~/.config/xfce4/terminal/terminalrc` file. There are also so many other themes to choose from. Check forum thread [Terminal Colour Scheme Screenshots](https://bbs.archlinux.org/viewtopic.php?id=51818) for hundreds of available choices and themes.

#### Changing default color theme

XFCE's `extra/terminal` package comes with a darker color palette. To change this, append the following in your terminalrc file for a lighter color theme, that is always visible in darker Terminal backgrounds.

```
~/.config/xfce4/terminal/terminalrc

```

```
ColorPalette5=#38d0fcaaf3a9
ColorPalette4=#e013a0a1612f
ColorPalette2=#d456a81b7b42
ColorPalette6=#ffff7062ffff
ColorPalette3=#7ffff7bd7fff
ColorPalette13=#82108210ffff

```

#### Terminal tango color theme

To switch to tango color theme, open with your favorite editor

```
~/.config/xfce4/terminal/terminalrc

```

And add(replace) these lines:

```
ColorForeground=White
ColorBackground=#323232323232
ColorPalette1=#2e2e34343636
ColorPalette2=#cccc00000000
ColorPalette3=#4e4e9a9a0606
ColorPalette4=#c4c4a0a00000
ColorPalette5=#34346565a4a4
ColorPalette6=#757550507b7b
ColorPalette7=#060698989a9a
ColorPalette8=#d3d3d7d7cfcf
ColorPalette9=#555557575353
ColorPalette10=#efef29292929
ColorPalette11=#8a8ae2e23434
ColorPalette12=#fcfce9e94f4f
ColorPalette13=#72729f9fcfcf
ColorPalette14=#adad7f7fa8a8
ColorPalette15=#3434e2e2e2e2
ColorPalette16=#eeeeeeeeecec

```

### Colour management

Xfce has no native support for colour management. [[4]](https://bugzilla.xfce.org/show_bug.cgi?id=8559) See [ICC profiles](/index.php/ICC_profiles "ICC profiles") for alternatives.

### Multiple monitors

As of [xfce4-settings](https://www.archlinux.org/packages/?name=xfce4-settings) version 4.11.4, Xfce has support for multiple monitors. Settings can be configured in the _Applications_ -> _Settings_ -> _Display_ dialog. For more information, see the [display](http://docs.xfce.org/xfce/xfce4-settings/display) article from the Xfce documentation.

### SSH agents

By default Xfce 4.10 will try to load gpg-agent or ssh-agent in that order during session initialization. To disable this, create an xfconf key using the following command:

```
xfconf-query -c xfce4-session -p /startup/ssh-agent/enabled -n -t bool -s false

```

To force using ssh-agent even if gpg-agent is installed, run the following instead:

```
xfconf-query -c xfce4-session -p /startup/ssh-agent/type -n -t string -s ssh-agent

```

To use [GNOME Keyring](/index.php/GNOME_Keyring "GNOME Keyring"), simply tick the checkbox _Launch GNOME services on startup_ in the _Advanced_ tab of _Session Manager_ in Xfce's settings. This will also disable gpg-agent and ssh-agent.

Source: [http://docs.xfce.org/xfce/xfce4-session/advanced](http://docs.xfce.org/xfce/xfce4-session/advanced)

### Scroll a background window without shifting focus on it

Go to _Main Menu > Settings > Window Manager Tweaks > Accessibility_ tab. Uncheck _Raise windows when any mouse button is pressed_.

### Mouse button modifier

By default, the mouse button modifier in Xfce is set to `Alt`. This can be changed with _xfconf-query_. For instance, the following command will set the `Super` key as the mouse button modifier:

```
$ xfconf-query -c xfwm4 -p /general/easy_click -n -t string -s "Super"

```

Strictly speaking, using multiple modifiers is not supported. However, as a workaround, multiple modifiers can be specified if the key names are separated with `><`. For instance, to set `Ctrl+Alt` as the mouse button modifier, you can use the following command:

```
$ xfconf-query -c xfwm4 -p /general/easy_click -n -t string -s "Ctrl><Alt"

```

## Troubleshooting

### Action buttons are missing icons

This happens if icons for some actions (Suspend, Hibernate) are missing from the icon theme, or do not have the expected names. To fix this, install an icon theme which has the necessary icons already added; see [Icons#Xfce icons](/index.php/Icons#Xfce_icons "Icons").

Then, you can switch to that icon theme using Applications -> Settings -> Appearance -> Icons.

Alternatively you can use the required icons provided by the icon theme you installed in your current icon theme. To do so, you first need to find out what the currently used icon theme is called. You can do so by using the command below:

```
$ xfconf-query -c xsettings -p /Net/IconThemeName

```

Then set the following variable:

```
$ icontheme=/usr/share/icons/_theme-name_

```

where _theme-name_ is the name of the current icon theme.

Then create symbolic links from the current icon theme into the icon theme providing the icons (this example assumes the icons are being provided by the [elementary-xfce-icons](https://aur.archlinux.org/packages/elementary-xfce-icons/)<sup><small>AUR</small></sup> theme.)

```
ln -s /usr/share/icons/elementary-xfce/apps/16/system-suspend.svg           ${icontheme}/16x16/actions/system-suspend.svg
ln -s /usr/share/icons/elementary-xfce/apps/16/system-suspend-hibernate.svg ${icontheme}/16x16/actions/system-hibernate.svg
ln -s /usr/share/icons/elementary-xfce/apps/22/system-suspend.svg           ${icontheme}/22x22/actions/system-suspend.svg
ln -s /usr/share/icons/elementary-xfce/apps/22/system-suspend-hibernate.svg ${icontheme}/22x22/actions/system-hibernate.svg
ln -s /usr/share/icons/elementary-xfce/apps/24/system-suspend.svg           ${icontheme}/24x24/actions/system-suspend.svg
ln -s /usr/share/icons/elementary-xfce/apps/24/system-suspend-hibernate.svg ${icontheme}/24x24/actions/system-hibernate.svg
ln -s /usr/share/icons/elementary-xfce/apps/48/system-suspend.svg           ${icontheme}/48x48/actions/system-suspend.svg
ln -s /usr/share/icons/elementary-xfce/apps/48/system-suspend-hibernate.svg ${icontheme}/48x48/actions/system-hibernate.svg

```

Log out and in again, and you should see icons for all actions.

### Desktop icons rearrange themselves

At certain events (such as opening the panel settings dialog) icons on the desktop rearrange themselves. This is because icon positions are determined by files in the `~/.config/xfce4/desktop/` directory. Each time a change is made to the desktop (icons are added or removed or change position) a new file is generated in this directory and these files can conflict.

To solve the problem, navigate to the directory and delete all the files other than the one which correctly defines the icon positions. You can determine which file defines the correct icon positions by opening it and examining the locations of the icons. The topmost row is defined as `row 0` and the leftmost column is defined by `col 0`. Therefore an entry of:

```
[Firefox]
row=3
col=0

```

means that the Firefox icon will be located on the 4th row of the leftmost column.

### GTK themes not working with multiple monitors

Some configuration tools may corrupt displays.xml, which results in GTK themes under _Applications Menu > Settings > Appearance_ ceasing to work. To fix the issue, delete `~/.config/xfce4/xfconf/xfce-perchannel-xml/displays.xml` and reconfigure your screens.

### Icons do not appear in right-click menus

**Note:** Despite the deprecation of GConf, this method does still work.

Users may find that icons do not appear when right-clicking options within some applications, including those made with [Qt](/index.php/Qt "Qt"). This problem only appears to happen within Xfce. Run these two commands:

```
$ gconftool-2 --type boolean --set /desktop/gnome/interface/buttons_have_icons true
$ gconftool-2 --type boolean --set /desktop/gnome/interface/menus_have_icons true

```

### Keyboard settings are not saved in xkb-plugin

There is a bug in [xfce4-xkb-plugin](https://www.archlinux.org/packages/?name=xfce4-xkb-plugin) _0.5.4.1-1_ which causes it to lose keyboard, layout switching and compose key settings. [[5]](https://bugzilla.xfce.org/show_bug.cgi?id=10226) As a workaround, enable _Use system defaults_ in `xfce4-keyboard-settings`, then reconfigure _xfce4-xkb-plugin_.

### NVIDIA and xfce4-sensors-plugin

To detect and use sensors of nvidia gpu you need to install [libxnvctrl](https://www.archlinux.org/packages/?name=libxnvctrl) and then rebuild [xfce4-sensors-plugin](https://www.archlinux.org/packages/?name=xfce4-sensors-plugin) with [ABS](/index.php/ABS "ABS"). You also have the option of using [xfce4-sensors-plugin-nvidia](https://aur.archlinux.org/packages/xfce4-sensors-plugin-nvidia/)<sup><small>AUR</small></sup> which replaces [xfce4-sensors-plugin](https://www.archlinux.org/packages/?name=xfce4-sensors-plugin).

### Preferred Applications preferences have no effect

Most applications rely on [xdg-open](/index.php/Xdg-open "Xdg-open") for opening a preferred application for a given file or URL.

In order for xdg-open and xdg-settings to detect and integrate with the Xfce desktop environment correctly, you need to [install](/index.php/Install "Install") the [xorg-xprop](https://www.archlinux.org/packages/?name=xorg-xprop) package.

If you do not do that, your preferred applications preferences (set by exo-preferred-applications) will not be obeyed. Installing the package and allowing _xdg-open_ to detect that you are running Xfce makes it forward all calls to _exo-open_ instead, which correctly uses all your preferred applications preferences.

To make sure xdg-open integration is working correctly, ask _xdg-settings_ for the default web browser and see what the result is:

```
# xdg-settings get default-web-browser

```

If it replies with:

```
xdg-settings: unknown desktop environment

```

it means that it has failed to detect Xfce as your desktop environment, which is likely due to a missing [xorg-xprop](https://www.archlinux.org/packages/?name=xorg-xprop) package.

### Restore default settings

If for any reason you need to revert back: to the default settings, rename `~/.config/xfce4-session/` and `~/.config/xfce4/`

```
$ mv ~/.config/xfce4-session/ ~/.config/xfce4-session-bak
$ mv ~/.config/xfce4/ ~/.config/xfce4-bak

```

Relogin for changes to take effect. If you get "Unable to load a failsafe session" upon login, see the [#Session failure](#Session_failure) section.

### Session failure

Symptoms include:

*   The mouse is an X and/or does not appear at all;
*   window decorations have disappeared and windows cannot be closed;
*   (`xfwm4-settings`) will not start, reporting `These settings cannot work with your current window manager (unknown)`;
*   errors reported by a [display manager](/index.php/Display_manager "Display manager") such as `No window manager registered on screen 0`.

Restarting xfce or rebooting your system may solve the problem, but a corrupt session is the likely cause. Delete the session folder:

```
$ rm -r ~/.cache/sessions/

```

### Fonts in window title crashing xfce4-title

[Install](/index.php/Install "Install") [ttf-droid](https://www.archlinux.org/packages/?name=ttf-droid) and [ttf-dejavu](https://www.archlinux.org/packages/?name=ttf-dejavu). See also [FS#44382](https://bugs.archlinux.org/task/44382).

### Laptop lid settings ignored

You may find that the lid close settings in Xfce4 Power Manager are ignored, meaning that the laptop will always suspend on lid close, no matter what settings are chosen in the power manager. This is because the power manager is not set to handle lid close events by default. Instead, logind handles the lid close event. To change this behavior so that the the power manager handles lid close events, execute the following command:

```
$ xfconf-query -c xfce4-power-manager -p /xfce4-power-manager/logind-handle-lid-switch -s false

```

Note that each time the laptop lid settings are changed in the power manager, this setting will be reset.

## See also

*   [Xfce - About](http://www.xfce.org/about/)
*   [http://docs.xfce.org/](http://docs.xfce.org/) - The complete documentation.
*   [Xfce-Look](http://www.xfce-look.org/) - Themes, wallpapers, and more.
*   [Xfce Wikia](http://xfce.wikia.com/wiki/Frequently_Asked_Questions) - How to edit the auto generated menu with the menu editor
*   [Xfce Wiki](http://wiki.xfce.org)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Xfce&oldid=415455](https://wiki.archlinux.org/index.php?title=Xfce&oldid=415455)"