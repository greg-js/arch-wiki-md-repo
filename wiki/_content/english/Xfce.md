Related articles

*   [Desktop environment](/index.php/Desktop_environment "Desktop environment")
*   [Window manager](/index.php/Window_manager "Window manager")
*   [Xfwm](/index.php/Xfwm "Xfwm")
*   [Thunar](/index.php/Thunar "Thunar")
*   [LXDE](/index.php/LXDE "LXDE")
*   [GNOME](/index.php/GNOME "GNOME")

[Xfce](http://www.xfce.org) is a lightweight and modular [desktop environment](/index.php/Desktop_environment "Desktop environment") currently based on both GTK 2 and GTK 3\. To provide a complete user experience, it includes a window manager, a file manager, desktop and panel.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Starting](#Starting)
*   [3 Configuration](#Configuration)
    *   [3.1 Menu](#Menu)
        *   [3.1.1 Whisker menu](#Whisker_menu)
        *   [3.1.2 Edit entries](#Edit_entries)
    *   [3.2 Desktop](#Desktop)
        *   [3.2.1 Transparent background for icon titles](#Transparent_background_for_icon_titles)
        *   [3.2.2 Remove desktop icons](#Remove_desktop_icons)
        *   [3.2.3 One wallpaper across multihead](#One_wallpaper_across_multihead)
        *   [3.2.4 Kill window shortcut](#Kill_window_shortcut)
    *   [3.3 Session](#Session)
        *   [3.3.1 Autostart](#Autostart)
        *   [3.3.2 Lock the screen](#Lock_the_screen)
        *   [3.3.3 Suspend](#Suspend)
        *   [3.3.4 Disable saved sessions](#Disable_saved_sessions)
        *   [3.3.5 Use a different window manager](#Use_a_different_window_manager)
    *   [3.4 Theming](#Theming)
    *   [3.5 Sound](#Sound)
        *   [3.5.1 Sound themes](#Sound_themes)
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
    *   [4.5 Open URLs by middle mouse in terminal](#Open_URLs_by_middle_mouse_in_terminal)
    *   [4.6 Colour management](#Colour_management)
    *   [4.7 Multiple monitors](#Multiple_monitors)
    *   [4.8 SSH agents](#SSH_agents)
    *   [4.9 Scroll a background window without shifting focus on it](#Scroll_a_background_window_without_shifting_focus_on_it)
    *   [4.10 Mouse button modifier](#Mouse_button_modifier)
    *   [4.11 Set the two fingers click to middle click for a touchpad](#Set_the_two_fingers_click_to_middle_click_for_a_touchpad)
    *   [4.12 Limit the minimum brightness of the brightness-slider](#Limit_the_minimum_brightness_of_the_brightness-slider)
    *   [4.13 Adding profile pictures](#Adding_profile_pictures)
    *   [4.14 Power manager plugin label](#Power_manager_plugin_label)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 Desktop icons rearrange themselves](#Desktop_icons_rearrange_themselves)
    *   [5.2 GTK themes not working with multiple monitors](#GTK_themes_not_working_with_multiple_monitors)
    *   [5.3 Icons do not appear in right-click menus](#Icons_do_not_appear_in_right-click_menus)
    *   [5.4 NVIDIA and xfce4-sensors-plugin](#NVIDIA_and_xfce4-sensors-plugin)
    *   [5.5 Black screens at boot with NVIDIA and multiple monitors](#Black_screens_at_boot_with_NVIDIA_and_multiple_monitors)
    *   [5.6 Panel applets keep being aligned on the left](#Panel_applets_keep_being_aligned_on_the_left)
    *   [5.7 Preferred Applications preferences have no effect](#Preferred_Applications_preferences_have_no_effect)
    *   [5.8 Restore default settings](#Restore_default_settings)
    *   [5.9 Session failure](#Session_failure)
    *   [5.10 Fonts in window title crashing xfce4-title](#Fonts_in_window_title_crashing_xfce4-title)
    *   [5.11 Laptop lid settings ignored](#Laptop_lid_settings_ignored)
    *   [5.12 User switching action button is greyed out](#User_switching_action_button_is_greyed_out)
    *   [5.13 Macros in .Xresources not working](#Macros_in_.Xresources_not_working)
    *   [5.14 Cursor theme doesn't change on login](#Cursor_theme_doesn't_change_on_login)
*   [6 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [xfce4](https://www.archlinux.org/groups/x86_64/xfce4/) group. You may also wish to install the [xfce4-goodies](https://www.archlinux.org/groups/x86_64/xfce4-goodies/) group which includes extra plugins and a number of useful utilities such as the [mousepad](https://www.archlinux.org/packages/?name=mousepad) editor. Xfce uses the [Xfwm](/index.php/Xfwm "Xfwm") window manager by default.

## Starting

Choose *Xfce Session* from the menu in a [display manager](/index.php/Display_manager "Display manager") of choice, or add `exec startxfce4` to [Xinitrc](/index.php/Xinitrc "Xinitrc").

**Note:** Do not call the `xfce4-session` executable directly; `startxfce4` is the correct command which, in turn, calls the former when appropriate.

## Configuration

Xfce stores configuration options in [Xfconf](http://docs.xfce.org/xfce/xfconf/start). There are several ways to modify these options:

*   In the main menu, select [Settings](http://docs.xfce.org/xfce/xfce4-settings/start) and the category you want to customize. Categories are programs usually located in `/usr/bin/xfce4-*` and `/usr/bin/xfdesktop-settings`.
*   `xfce4-settings-editor` can see and modify all settings. Options modified here will take effect immediately. Use `xfconf-query` to change settings from the commandline; see [the documentation](http://docs.xfce.org/xfce/xfconf/xfconf-query) for details.
*   Settings are stored in XML files in `~/.config/xfce4/xfconf/xfce-perchannel-xml/` which can be edited by hand. However, changes made here will *not* take effect immediately.

### Menu

See [Xdg-menu](/index.php/Xdg-menu "Xdg-menu") for more info on using the Free Desktop menu system.

#### Whisker menu

[xfce4-whiskermenu-plugin](https://www.archlinux.org/packages/?name=xfce4-whiskermenu-plugin) (also part of [xfce4-goodies](https://www.archlinux.org/groups/x86_64/xfce4-goodies/)) is an alternative application launcher. It shows a list of favorites, browses through all installed applications through category buttons, and supports fuzzy searching. After package being installed, it can replace *Applications Menu* as first item in Panel 1 (in *Settings > Panel > Items* add *Whisker Menu*).

#### Edit entries

A number of graphical tools are available for this task:

*   **MenuLibre** — An advanced menu editor that provides modern features in a clean, easy-to-use interface.

	[https://launchpad.net/menulibre](https://launchpad.net/menulibre) || [menulibre](https://aur.archlinux.org/packages/menulibre/).

*   **Alacarte** — Menu editor for GNOME

	[http://www.gnome.org/](http://www.gnome.org/) || [alacarte](https://www.archlinux.org/packages/?name=alacarte)

*   **XAME (XFCE Applications Menu Editor)** — GUI tool written in Gambas designed specifically for editing menu entries in Xfce, it will not work in other environments. (Discontinued)

	[http://redsquirrel87.altervista.org/doku.php/xfce-applications-menu-editor](http://redsquirrel87.altervista.org/doku.php/xfce-applications-menu-editor) || [xame](https://aur.archlinux.org/packages/xame/)

Alternatively, create the file `~/.config/menus/xfce-applications.menu` manually. See the example configuration below:

```
<!DOCTYPE Menu PUBLIC "-//freedesktop//DTD Menu 1.0//EN"
  "[http://www.freedesktop.org/standards/menu-spec/1.0/menu.dtd](http://www.freedesktop.org/standards/menu-spec/1.0/menu.dtd)">

<Menu>
    <Name>Xfce</Name>
    <MergeFile type="parent">/etc/xdg/menus/xfce-applications.menu</MergeFile>

    <Exclude>
        <Filename>xfce4-run.desktop</Filename>
        <Filename>exo-terminal-emulator.desktop</Filename>
        <Filename>exo-file-manager.desktop</Filename>
        <Filename>exo-mail-reader.desktop</Filename>
        <Filename>exo-web-browser.desktop</Filename>
        <Filename>xfce4-about.desktop</Filename>
        <Filename>xfhelp4.desktop</Filename>
    </Exclude>

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

#### Remove desktop icons

Issue the following command:

```
$ xfconf-query -c xfce4-desktop -v --create -p /desktop-icons/style -t int -s 0

```

To reinstate icons on the desktop, issue the same command with a value of 2.

#### One wallpaper across multihead

Open `xfce4-settings-editor` and create a new property with the following settings:

```
Property: /backdrop/screen0/xinerama-stretch
Type: Boolean
Value: TRUE|1|Enabled

```

#### Kill window shortcut

Xfce does not have a shortcut to kill a window, for example when a program freezes.

With [xorg-xkill](https://www.archlinux.org/packages/?name=xorg-xkill), use `xkill` to interactively kill a window. For the currently active window, use [xdotool](https://www.archlinux.org/packages/?name=xdotool):

```
$ xdotool getwindowfocus windowkill

```

Alternatively:

```
$ sh -c "xkill -id $(xprop -root -notype | sed -n '/^_NET_ACTIVE_WINDOW/ s/^.*# *\|\,.*$//g p')"

```

To add the shortcut, use *Settings > Keyboard* or an application like [xbindkeys](https://www.archlinux.org/packages/?name=xbindkeys).

### Session

#### Autostart

To launch custom applications when Xfce starts up, click the *Applications Menu > Settings > Settings Manager* and then choose the *Session and Startup* option and click the tab *Application Autostart*. You will see a list of programs that get launched on startup. To add an entry, click the *Add* button and fill out the form, specifying the path to an executable you want to run.

Autostart applications are stored as `*name*.desktop` in `~/.config/autostart/`.

Alternatively, add the commands you wish to run (including setting environment variables) to [xinitrc](/index.php/Xinitrc "Xinitrc") (or [xprofile](/index.php/Xprofile "Xprofile") when a [display manager](/index.php/Display_manager "Display manager") is being used).

**Tip:** Sometimes it might be useful to **delay the startup of an application**. Note that specifying under *Application > Autostart* a command such as `sleep 3 && *command*` does not work; a workaround is to use the syntax `sh -c "sleep 3 && *command*"`

#### Lock the screen

*xflock4* is the reference Bash script which is used to lock an Xfce session.

It tries to lock the screen with either [xscreensaver](https://www.archlinux.org/packages/?name=xscreensaver), [gnome-screensaver](https://www.archlinux.org/packages/?name=gnome-screensaver), [slock](https://www.archlinux.org/packages/?name=slock) or [xlockmore](https://www.archlinux.org/packages/?name=xlockmore). It consecutively looks for the corresponding binary or exits with return code 1 if it fails to find any of these four.

The [List of applications/Security#Screen lockers](/index.php/List_of_applications/Security#Screen_lockers "List of applications/Security") contains a short description of these four screen lockers together with other popular applications. There is in this list an alternative locker, [light-locker](https://www.archlinux.org/packages/?name=light-locker), which integrates particularly well with [xfce4-power-manager](https://www.archlinux.org/packages/?name=xfce4-power-manager). Once it is installed, Xfce Power Manager's setting gains an additional *Security* tab to configure *light-locker* and the existing *Lock screen when system is going for sleep* setting is relocated under this tab. In this new GUI it is possible to set whether the session should be locked upon screensaver activity or whenever the system goes to sleep.

To have *xflock4* run *light-locker* or any custom session locker, not among the four cited above, one must set `LockCommand` in the session's xfconf channel to the command line to be used (the command inside the quotes in the following example can be adapted accordingly for other screen lockers):

 `$ xfconf-query -c xfce4-session -p /general/LockCommand -s "*light-locker-command --lock*" --create -t string` 

The panel lock button in the *Action Buttons* panel simply executes `/usr/bin/xflock4`. It should work as expected as long as *xflock4* is functioning i.e. one of the native lockers is installed or a custom locker is configured to integrate with it as proposed above.

#### Suspend

Whenever asked to suspend, Xfce executes the [xfce4-session-logout(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/xfce4-session-logout.1) command with the `suspend` option:

```
$ xfce4-session-logout --suspend

```

Whether or not the session is systematically locked on *suspend* can be configured through the xfconf properties or from the GUI.

To control this state using the CLI: there are two settings that are used, `LockScreen` and `lock-screen-suspend-hibernate`, in respectively the session and the power manager xfconf channels. To prevent locking on suspend, turn them to `false`:

```
$ xfconf-query -c xfce4-session -p /shutdown/LockScreen -s **false**
$ xfconf-query -c xfce4-power-manager -p /xfce4-power-manager/lock-screen-suspend-hibernate -s **false**

```

Similarly, turn them to `true` to lock the session on suspend.

The setting can also be controlled from the GUI: open the *Session and Startup* application and turn the flag *Advanced > Lock screen before sleep* on or off.

Whenever the suspend keyboard button is pressed, it can be handled by either Xfce's power manager or by *systemd-logind*. To give precedence to logind, the following xfconf setting must be set to `true`:

```
$ xfconf-query -c xfce4-power-manager -p /xfce4-power-manager/logind-handle-suspend-key -n -t bool -s **true**

```

**Note:** To check how *systemd-logind* handles events whenever it has precedence over Xfce, check [logind.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/logind.conf.5)

#### Disable saved sessions

Per user, saved sessions can be disabled by executing the following:

```
$ xfconf-query -c xfce4-session -p /general/SaveOnExit -s false

```

Then navigate to *Applications > Settings > Session and Startup > Sessions* and press the *Clear saved sessions* button to remove all previously saved sessions.

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

#### Use a different window manager

**Note:** For the changes to take effect, you will need to clear the saved sessions and ensure that session saving is disabled when logging out for the first time. Once the window manager of choice is running, session saving can be enabled again.

The files specifying the default window manager are found in the following locations:

*   `~/.config/xfce4/xfconf/xfce-perchannel-xml/xfce4-session.xml` - per user
*   `/etc/xdg/xfce4/xfconf/xfce-perchannel-xml/xfce4-session.xml` - systemwide

The default window manager for the user can be set easily using *xfconf-query*:

```
$ xfconf-query -c xfce4-session -p /sessions/Failsafe/Client0_Command -t string -sa *wm_name*

```

If you want to start the window manager with command line options, see the command below:

```
$ xfconf-query -c xfce4-session -p /sessions/Failsafe/Client0_Command -t string -t string -s *wm_name* -s *--wm-option*

```

If you need more command line options, simply add more `-t string` and `-s *--wm-option*` arguments to the command.

If you want to change the default window manager systemwide, edit the file specified above manually, changing *xfwm4* to the preferred window manager and adding more `<value type="string" value="*--wm-option*"/>` lines for extra command line options if needed.

You can also change the window manager by autostarting `*wm_name* --replace` using the autostart facility or by running `*wm_name* --replace &` in a terminal and making sure the session is saved on logout. Be aware though that this method does not truly change the default manager, it merely replaces it at login. Note that if you are using the autostart facility, you should disable saved sessions as this could lead to the new window manager being started twice after the default window manager.

### Theming

XFCE themes are available at [xfce-look.org](http://www.xfce-look.org). *Xfwm* themes are stored in `/usr/share/themes/xfce4`, and set in *Settings > Window Manager*. [GTK](/index.php/GTK "GTK") themes are set in *Settings > Appearance*.

To achieve a uniform look for all applications, see [Uniform look for Qt and GTK applications](/index.php/Uniform_look_for_Qt_and_GTK_applications "Uniform look for Qt and GTK applications").

See also [Cursor themes](/index.php/Cursor_themes "Cursor themes"), [Icons](/index.php/Icons "Icons"), and [Font configuration](/index.php/Font_configuration "Font configuration").

### Sound

#### Sound themes

XFCE4 supports [freedesktop system sounds](https://www.freedesktop.org/wiki/Specifications/sound-theme-spec/), but it is not configured out of the box.

To enable a sound theme:

1.  Install [libcanberra](https://www.archlinux.org/packages/?name=libcanberra) and [libcanberra-pulse](https://www.archlinux.org/packages/?name=libcanberra-pulse) for [PulseAudio](/index.php/PulseAudio "PulseAudio") support;
2.  "canberra-gtk-module" should be in the GTK_MODULES environment variable (re-login may be required);
3.  Check "Enable event sounds" in Settings Manager → Appearance → Settings tab;
4.  In the Settings Editor set "xsettings/Net/SoundThemeName" to a sound theme located in `/usr/share/sounds/`;
5.  Turn on "System Sounds" in audio mixer (e.g. pavucontrol).

[sound-theme-freedesktop](https://www.archlinux.org/packages/?name=sound-theme-freedesktop) provides a compatible sound theme, but it lacks many required events. A better choice is [sound-theme-smooth](https://aur.archlinux.org/packages/sound-theme-smooth/) (SoundThemeName should be "Smooth").

#### Keyboard volume buttons

[xfce4-pulseaudio-plugin](https://www.archlinux.org/packages/?name=xfce4-pulseaudio-plugin) provides a panel applet which has support for keyboard volume control and volume notifications. As an alternative, you can install [xfce4-volumed-pulse](https://aur.archlinux.org/packages/xfce4-volumed-pulse/), which also provides keybinding and notification control, but without an icon sitting in the panel. This is handy, for example, when using [pasystray](https://www.archlinux.org/packages/?name=pasystray) at the same time for a finer control.

Alternatively, [xfce4-mixer](https://aur.archlinux.org/packages/xfce4-mixer/) also provides a panel applet and keyboard shortcuts which supports Alsa as well. Note however, that it is based on a feature of GStreamer 0.10 which has been abandoned in 1.0.

For non desktop environment specific alternatives, see [List of applications/Multimedia#Volume control](/index.php/List_of_applications/Multimedia#Volume_control "List of applications/Multimedia").

##### Shortcuts

If you are not using an applet or daemon that controls the volume keys, you can map volume control commands to your volume keys manually using Xfce's keyboard settings. For the sound system you are using, see the sections linked to below for the appropriate commands.

*   ALSA: see [Advanced Linux Sound Architecture#Keyboard volume control](/index.php/Advanced_Linux_Sound_Architecture#Keyboard_volume_control "Advanced Linux Sound Architecture").
*   PulseAudio: see [PulseAudio#Keyboard volume control](/index.php/PulseAudio#Keyboard_volume_control "PulseAudio")
*   OSS: see [OSS#Using multimedia keys with OSS](/index.php/OSS#Using_multimedia_keys_with_OSS "OSS").

### Keyboard Shortcuts

Keyboard shortcuts are defined in two places: *Settings > Window Manager > Keyboard*, and *Settings > Keyboard > Shortcuts*.

### Polkit Authentication Agent

The [polkit-gnome](https://www.archlinux.org/packages/?name=polkit-gnome) agent will be installed along with [xfce4-session](https://www.archlinux.org/packages/?name=xfce4-session) and autostarted automatically; no user intervention is required. For more information, see [Polkit#Authentication agents](/index.php/Polkit#Authentication_agents "Polkit").

A third party polkit authentication agent for Xfce is also available, see [xfce-polkit](https://aur.archlinux.org/packages/xfce-polkit/) or [xfce-polkit-git](https://aur.archlinux.org/packages/xfce-polkit-git/).

### Display blanking

Some programs that are commonly used with Xfce will control monitor blanking and [DPMS](/index.php/DPMS "DPMS") (monitor powersaving) settings. They are discussed below.

	Xfce Power Manager

*Xfce Power Manager* controls blanking and DPMS settings. These settings can be configured in the *Power Manager* GUI within the *Display* tab.

Note that when *Display power management* is turned off, DPMS is fully disabled, it does not mean that *Power Manager* will simply stop controlling DPMS. It does not disable screen blanking either. To disable both blanking and DPMS, right click on the power manager system tray icon or left click on the panel applet and make sure that the option labelled *Presentation mode* is ticked.

	XScreenSaver

If [xscreensaver](https://www.archlinux.org/packages/?name=xscreensaver) is installed and runs alongside Xfce Power Manager, it may not be clear which application is in control of blanking and DPMS as both are competing for control of the same settings. Therefore, in a situation where it is important that the monitor not be blanked (when watching a video for instance), it is advisable to disable blanking and DPMS through both applications. To know more about *XScreenSaver* options, see [XScreenSaver#DPMS and blanking settings](/index.php/XScreenSaver#DPMS_and_blanking_settings "XScreenSaver").

	xset

If neither of the above applications are running, then blanking and DPMS settings can be controlled using the *xset* command, see [DPMS#Modify DPMS and screensaver settings with a command](/index.php/DPMS#Modify_DPMS_and_screensaver_settings_with_a_command "DPMS").

**Note:** There are some issues associated with blanking and resuming from blanking in some configurations. See [[1]](https://bbs.archlinux.org/viewtopic.php?id=194313&p=2)[[2]](https://bugzilla.xfce.org/show_bug.cgi?id=11107).

## Tips and tricks

### Hide partitions from thunar and xfdesktop

If your installation partitions are shown as mounted devices on the desktop and in Thunar, try to install [gvfs](https://www.archlinux.org/packages/?name=gvfs). See [Udisks#Hide selected partitions](/index.php/Udisks#Hide_selected_partitions "Udisks") for more advanced configuration options.

### Screenshots

Xfce has its own screenshot tool, [xfce4-screenshooter](https://www.archlinux.org/packages/?name=xfce4-screenshooter). It is part of the [xfce4-goodies](https://www.archlinux.org/groups/x86_64/xfce4-goodies/) group.

Go to *Applications > Settings > Keyboard*, *Application Shortcuts*. Add the `xfce4-screenshooter -f` (or `-w` for the active window) command to use the `Print` key in order to take fullscreen screenshots. See screenshooter's man page for other optional arguments.

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

Xfce's `extra/terminal` package comes with a darker colour palette. To change this, append the following in your terminalrc file for a lighter color theme, that is always visible in darker Terminal backgrounds.

 `~/.config/xfce4/terminal/terminalrc` 
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

### Open URLs by middle mouse in terminal

On update to version 0.8 open URL with middle mouse turned off by default and just paste clip to cursor. To enable old behavior fix next option in `${XDG_CONFIG_HOME}/xfce4/terminal/terminalrc` (`XDG_CONFIG_HOME=${HOME}/.config` by default)

 `${XDG_CONFIG_HOME}/xfce4/terminal/terminalrc` 
```
[Configuration]
MiscMiddleClickOpensUri=TRUE
```

### Colour management

Xfce has no native support for colour management. [[3]](https://bugzilla.xfce.org/show_bug.cgi?id=8559) See [ICC profiles](/index.php/ICC_profiles "ICC profiles") for alternatives.

### Multiple monitors

Xfce has support for multiple monitors. Settings can be configured in the *Applications > Settings > Display* dialog. For more information, see the [display](http://docs.xfce.org/xfce/xfce4-settings/display) article from the Xfce documentation.

XFCE's display configuration is not persistent so you may find yourself needing to use the display tool a lot, especially if you use multiple displays. One workaround for this is to use [arandr](https://www.archlinux.org/packages/?name=arandr) to easily configure your display configurations in the form of xrandr commands which you can assign to be executed as XFCE keyboard shortcuts.

### SSH agents

By default Xfce 4.10 will try to load gpg-agent or ssh-agent in that order during session initialization. To disable this, create an xfconf key using the following command:

```
xfconf-query -c xfce4-session -p /startup/ssh-agent/enabled -n -t bool -s false

```

To force using ssh-agent even if gpg-agent is installed, run the following instead:

```
xfconf-query -c xfce4-session -p /startup/ssh-agent/type -n -t string -s ssh-agent

```

To use [GNOME Keyring](/index.php/GNOME_Keyring "GNOME Keyring"), simply tick the checkbox *Launch GNOME services on startup* in the *Advanced* tab of *Session and Startup* in Xfce's settings. This will also disable gpg-agent and ssh-agent.

Source: [http://docs.xfce.org/xfce/xfce4-session/advanced](http://docs.xfce.org/xfce/xfce4-session/advanced)

### Scroll a background window without shifting focus on it

Go to *Main Menu > Settings > Window Manager Tweaks > Accessibility* tab. Uncheck *Raise windows when any mouse button is pressed*.

### Mouse button modifier

By default, the mouse button modifier in Xfce is set to `Alt`. This can be changed with *xfconf-query*. For instance, the following command will set the `Super` key as the mouse button modifier:

```
$ xfconf-query -c xfwm4 -p /general/easy_click -n -t string -s "Super"

```

Strictly speaking, using multiple modifiers is not supported. However, as a workaround, multiple modifiers can be specified if the key names are separated with `><`. For instance, to set `Ctrl+Alt` as the mouse button modifier, you can use the following command:

```
$ xfconf-query -c xfwm4 -p /general/easy_click -n -t string -s "Ctrl><Alt"

```

### Set the two fingers click to middle click for a touchpad

If you want the 2 finger click on the touchpad to do a middle click, create or edit the following file:

 `~/.config/xfce4/xfconf/xfce-perchannel-xml/pointers.xml` 
```
<channel name="pointers" version="1.0">
  <property name="SynPS2_Synaptics_TouchPad" type="empty">
    <property name="Properties" type="empty">
      <property name="Synaptics_Tap_Action" type="array">
        <value type="int" value="0"/>
        <value type="int" value="0"/>
        <value type="int" value="0"/>
        <value type="int" value="0"/>
        <value type="int" value="1"/>
        <value type="int" value="2"/>
        <value type="int" value="3"/>
      </property>
    </property>
  </property>
</channel>

```

The 2 in the array is the middle click.

### Limit the minimum brightness of the brightness-slider

Limiting the minimum brightness can be useful for displays which turn off backlight on a brightness level of 0\. In `xfce4-power-manager 1.3.2` a new hidden option had been introduced to set a minimum brightness value with a xfconf4-property. Add `brightness-slider-min-level` as an int property in xfconf4\. Adjust the int value to get a suitable minimum brightness level.

### Adding profile pictures

To add profile pictures for each user to be displayed in the whisker-menu, simply place a 96x96 PNG file in the respective user's home directory with the name `.face`. For example the PNG file `/home/*bob*/.face` for user *bob*.

Image editing programs like [GIMP](/index.php/GIMP "GIMP") can be used to convert and scale your favourite images down to 96x96.

### Power manager plugin label

The xfconf option `show-panel-label` of type `int` controls the label of the power manager, it can be configured for different label formats: it can be set to 0 (no label), 1 (percentage), 2 (remaining time) or 3 (both).

It is also accessible through the power manager plugin GUI in *Properties > Show label*

## Troubleshooting

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

Some configuration tools may corrupt displays.xml, which results in GTK themes under *Applications Menu > Settings > Appearance* ceasing to work. To fix the issue, delete `~/.config/xfce4/xfconf/xfce-perchannel-xml/displays.xml` and reconfigure your screens.

### Icons do not appear in right-click menus

**Note:** Despite the deprecation of GConf, this method does still work.

Users may find that icons do not appear when right-clicking options within some applications, including those made with [Qt](/index.php/Qt "Qt"). This problem only appears to happen within Xfce. Run these two commands:

```
$ gconftool-2 --type boolean --set /desktop/gnome/interface/buttons_have_icons true
$ gconftool-2 --type boolean --set /desktop/gnome/interface/menus_have_icons true

```

### NVIDIA and xfce4-sensors-plugin

To detect and use sensors of nvidia gpu you need to install [libxnvctrl](https://www.archlinux.org/packages/?name=libxnvctrl) and then rebuild [xfce4-sensors-plugin](https://www.archlinux.org/packages/?name=xfce4-sensors-plugin) with [ABS](/index.php/ABS "ABS"). You also have the option of using [xfce4-sensors-plugin-nvidia](https://aur.archlinux.org/packages/xfce4-sensors-plugin-nvidia/) which replaces [xfce4-sensors-plugin](https://www.archlinux.org/packages/?name=xfce4-sensors-plugin).

### Black screens at boot with NVIDIA and multiple monitors

Using [NVIDIA](/index.php/NVIDIA "NVIDIA"), multiple monitors and [NVIDIA/Troubleshooting#Avoid screen tearing](/index.php/NVIDIA/Troubleshooting#Avoid_screen_tearing "NVIDIA/Troubleshooting") may result as a black screen when booting Xfce. The screens' position conflict into the files `/etc/X11/xorg.conf` and `~/.config/xfce4/xfconf/xfce-perchannel-xml/displays.xml`. Deleting the `displays.xml` file fixes the behavior.

```
$ rm ~/.config/xfce4/xfconf/xfce-perchannel-xml/displays.xml

```

### Panel applets keep being aligned on the left

Add a separator someplace before the right end and set its "expand" property. [[4]](https://forums.linuxmint.com/viewtopic.php?f=110&t=155602})

### Preferred Applications preferences have no effect

Most applications rely on [xdg-open](/index.php/Xdg-open "Xdg-open") for opening a preferred application for a given file or URL.

In order for xdg-open and xdg-settings to detect and integrate with the Xfce desktop environment correctly, you need to [install](/index.php/Install "Install") the [xorg-xprop](https://www.archlinux.org/packages/?name=xorg-xprop) package.

If you do not do that, your preferred applications preferences (set by exo-preferred-applications) will not be obeyed. Installing the package and allowing *xdg-open* to detect that you are running Xfce makes it forward all calls to *exo-open* instead, which correctly uses all your preferred applications preferences.

To make sure xdg-open integration is working correctly, ask *xdg-settings* for the default web browser and see what the result is:

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

Relogin for changes to take effect. If you get `Unable to load a failsafe session` upon login, see the [#Session failure](#Session_failure) section.

### Session failure

Symptoms include:

*   The mouse is an X and/or does not appear at all;
*   Window decorations have disappeared and windows cannot be closed;
*   (`xfwm4-settings`) will not start, reporting `These settings cannot work with your current window manager (unknown)`;
*   Errors reported by a [display manager](/index.php/Display_manager "Display manager") such as `No window manager registered on screen 0`.
*   Unable to load a failsafe session:

```
Unable to load a failsafe session.
Unable to determine failsafe session name.  Possible causes: xfconfd isn't running (D-Bus setup problem); environment variable $XDG_CONFIG_DIRS is set incorrectly (must include "/etc"), or xfce4-session is installed incorrectly. 

```

Restarting Xfce or rebooting your system may solve the problem, but a corrupt session could also be the cause. Delete the session folder:

```
$ rm -r ~/.cache/sessions/

```

Also make sure that the relevant folders in `$HOME` are owned by the user starting `xfce4`. See [Chown](/index.php/Chown "Chown").

### Fonts in window title crashing xfce4-title

Install [ttf-droid](https://www.archlinux.org/packages/?name=ttf-droid) and [ttf-dejavu](https://www.archlinux.org/packages/?name=ttf-dejavu). See also [FS#44382](https://bugs.archlinux.org/task/44382).

### Laptop lid settings ignored

You may find that the lid close settings in Xfce4 Power Manager are ignored, meaning that the laptop will always suspend on lid close, no matter what settings are chosen in the power manager. This is because the power manager is not set to handle lid close events by default. Instead, *systemd-logind* handles the lid close event. To change this behavior so that the power manager handles lid close events, execute the following command:

```
$ xfconf-query -c xfce4-power-manager -p /xfce4-power-manager/logind-handle-lid-switch -s false

```

**Note:** Under some circumstances, the `logind-handle-lid-switch` setting will get set to true when changes are made to the laptop lid actions or the lock on suspend setting. See [[5]](https://bugzilla.xfce.org/show_bug.cgi?id=12756#c2). In this case, you will need to toggle `logind-handle-lid-switch` to false again.

### User switching action button is greyed out

The *Switch User* action button assumes that the *gdmflexiserver* executable (provided by [GDM](/index.php/GDM "GDM")) exists. Thus, if GDM is not being used then the button will be greyed out. See the [upstream bug report](https://bugzilla.xfce.org/show_bug.cgi?id=9307).

A possible workaround is to create an executable script called *gdmflexiserver* in `/usr/bin` or `/usr/local/bin` which calls the greeter switch command provided by the [display manager](/index.php/Display_manager "Display manager") which is being used.

*   For LXDM - [LXDM#Simultaneous users and switching users](/index.php/LXDM#Simultaneous_users_and_switching_users "LXDM").
*   For LightDM - [LightDM#User switching](/index.php/LightDM#User_switching "LightDM").

### Macros in .Xresources not working

Xfce loads `$HOME/.Xresources` file using `xrdb`, but with `-nocpp` option to skip preprocessing. For macros to work properly, copy `/etc/xdg/xfce4/xinitrc` to `$HOME/.config/xfce4` directory and remove `-nocpp` option to `xrdb` from the resulting file. See [this thread](https://bbs.archlinux.org/profile.php?id=104121).

### Cursor theme doesn't change on login

Ensure the systemwide XDG cursor is set to your desired cursor theme - see [Cursor themes#XDG specification](/index.php/Cursor_themes#XDG_specification "Cursor themes").

## See also

*   [Xfce - Documentation](http://docs.xfce.org/)
*   [Xfce - Wiki](http://wiki.xfce.org)
*   [Xfce - About](http://www.xfce.org/about/)
*   [Xfce - Tour](https://xfce.org/about/tour)
*   [Wikipedia:Xfce](https://en.wikipedia.org/wiki/Xfce "wikipedia:Xfce")
*   [Xfce-Look](http://www.xfce-look.org/) - Themes, wallpapers, and more.
*   [Xfce Wikia](http://xfce.wikia.com/wiki/Main_Page)