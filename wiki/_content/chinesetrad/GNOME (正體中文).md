## Contents

*   [1 GNOME是什麼?](#GNOME.E6.98.AF.E4.BB.80.E9.BA.BC.3F)
*   [2 如何安裝GNOME桌面](#.E5.A6.82.E4.BD.95.E5.AE.89.E8.A3.9DGNOME.E6.A1.8C.E9.9D.A2)
*   [3 Introduction](#Introduction)
*   [4 Upgrade from GNOME 2.32](#Upgrade_from_GNOME_2.32)
*   [5 Installing to a new system](#Installing_to_a_new_system)
    *   [5.1 Daemons and modules needed by GNOME](#Daemons_and_modules_needed_by_GNOME)
    *   [5.2 Running GNOME](#Running_GNOME)
*   [6 Using the shell](#Using_the_shell)
*   [7 Customization](#Customization)
    *   [7.1 Using Gnome-tweak-tool](#Using_Gnome-tweak-tool)
        *   [7.1.1 Wallpaper](#Wallpaper)
        *   [7.1.2 Turning off the sound](#Turning_off_the_sound)
        *   [7.1.3 Change GDM's keyboard layout](#Change_GDM.27s_keyboard_layout)
    *   [7.2 Changing the GTK3 theme using settings.ini](#Changing_the_GTK3_theme_using_settings.ini)
    *   [7.3 Resizing the massive title bar](#Resizing_the_massive_title_bar)
    *   [7.4 Setting an icon theme](#Setting_an_icon_theme)
    *   [7.5 Start program automatically after login to GNOME 3](#Start_program_automatically_after_login_to_GNOME_3)
    *   [7.6 Removing folders from the "Computer" section in Nautilus's Places sidebar](#Removing_folders_from_the_.22Computer.22_section_in_Nautilus.27s_Places_sidebar)
    *   [7.7 Setting the default terminal via console](#Setting_the_default_terminal_via_console)
    *   [7.8 Setting Nautilus to use location bar entry](#Setting_Nautilus_to_use_location_bar_entry)
    *   [7.9 Disable accessibility icon in panel](#Disable_accessibility_icon_in_panel)
    *   [7.10 Disable bluetooth icon in panel](#Disable_bluetooth_icon_in_panel)
    *   [7.11 Middle Mouse Button Emulation](#Middle_Mouse_Button_Emulation)
    *   [7.12 Battery icon](#Battery_icon)
    *   [7.13 Xmonad](#Xmonad)
*   [8 Enabling fallback mode](#Enabling_fallback_mode)
*   [9 Enabling hidden features](#Enabling_hidden_features)
    *   [9.1 Changing Hotkeys](#Changing_Hotkeys)
*   [10 How to shutdown through the Status menu](#How_to_shutdown_through_the_Status_menu)
*   [11 Enabling integrated messaging](#Enabling_integrated_messaging)
*   [12 Enabling extensions](#Enabling_extensions)
*   [13 Troubleshooting](#Troubleshooting)
    *   [13.1 My screen isn't locked after resume from suspend/hibernate](#My_screen_isn.27t_locked_after_resume_from_suspend.2Fhibernate)
    *   [13.2 My GTK2+ apps show segfaults and won't start](#My_GTK2.2B_apps_show_segfaults_and_won.27t_start)
    *   [13.3 I use the ATI Catalyst driver and I encounter glitches and artifacts while using GNOME Shell](#I_use_the_ATI_Catalyst_driver_and_I_encounter_glitches_and_artifacts_while_using_GNOME_Shell)
    *   [13.4 I have multiple monitors and the Dock extension appears stuck between them](#I_have_multiple_monitors_and_the_Dock_extension_appears_stuck_between_them)
    *   [13.5 There are no event sounds for Empathy and other programs](#There_are_no_event_sounds_for_Empathy_and_other_programs)
    *   [13.6 Editing hotkeys via can-change-accels fails](#Editing_hotkeys_via_can-change-accels_fails)
    *   [13.7 "Failed to load session 'gnome-fallback'" message](#.22Failed_to_load_session_.27gnome-fallback.27.22_message)
    *   [13.8 [fallback mode] Panels and applets don't respond to right click to remove, etc, as in GNOME 2](#.5Bfallback_mode.5D_Panels_and_applets_don.27t_respond_to_right_click_to_remove.2C_etc.2C_as_in_GNOME_2)
    *   [13.9 Show Desktop: ALT+STRG+D does not Work](#Show_Desktop:_ALT.2BSTRG.2BD_does_not_Work)

## GNOME是什麼?

[GNOME](http://www.gnome.org/)專案提供了兩樣東西: GNOME桌面環境，一個設計給終使用者的直覺、引人注目的桌面環境。和GNOME開發平台, 一個用來開發可整合進桌面環境的極具擴展性的框架。

## 如何安裝GNOME桌面

在安裝GNOME之前，請先利用以下指令更新你的pacman:

```
# pacman -Syu 
# pacman -Syy

```

這會幫你略過當安裝gnome-media套件時，所需的依賴gstreamer0.10-gconf不存在未更新的系統中的問題。安裝gnome前更新的你系統是必需的。

利用下列指令安裝GNOME桌面:

```
# pacman -S gnome

```

這裡有一個套件組(metapackage)，包含了一個群組的組件。你可以選擇安裝這個群組全部的套件或是部分的套件。全部的套件都可以被安全的安裝，此安裝是被高度建議的。但以下是一些可能不被需要的套件的列表

*   **Epiphany** GNOME的網頁瀏覽器。假設你預定要使用其它的網頁瀏覽器，如Firefox。那這個套件就是不必要的。但是仍建議你使用這個被Firefox遮住光環但還是非常棒的瀏覽器。

*   **Evolution** 一個GNOME中用來管理個人資訊的套件(e-mail,行程，聯絡人資訊...等)。假如你想要使用其它的個人資訊管理套件，如Thunderbird，或是網頁版的個人資訊管理套件，如google或yahoo。那麼這個套件就不是必需的。

*   **gnome-backgrounds** 是由GNOME社群為你挑選的桌面布景集合。假設你有自己的桌面背景圖案。那麼這個套件就可以不用安裝。

*   **gnome-screensaver** GNOME桌面的螢幕保護程式集合。假如你不使用螢幕保護程式，那麼這個套件就可以不用安裝。

*   **gnome-themes** GNOME布景主題的集合。假如你要使用自己的布景主題。那麼這個套件就可以不用安裝。

*   **gnome2-user-docs** 和 **yelp** 是GNOME的幫助文件和幫助文件的讀取器。假如你不是個會讀取幫助文件，而是傾向於在Google上找尋幫助的話。那麼這個套件就可以不用安裝。

For GNOME 3, the GNOME Project has started from scratch and created a completely new, modern desktop designed for today's users and technologies. In GNOME 3:

*   There is a new default modern visual theme and font
*   The Activities view which provides an easy way to access all your windows and applications
*   Built-in (integrated) messaging desktop services
*   A more subtle notifications system and a more discrete panel
*   A fast Activities search feature
*   A new System Settings application
*   ... and more features like: window tiling (Aero Snap like), an improved Nautilus etc.

[more details on the [GNOME3](http://www.gnome3.org/) website]

## Introduction

GNOME3 comes with **two** interfaces, **gnome-shell** (the new, standard layout) and **fallback** mode. gnome-session will automatically detect if your computer is capable of running gnome-shell and will start fallback mode if not.

**Fallback** mode is very similar to the GNOME 2.x layout (while using gnome-panel and metacity, instead of gnome-shell and Mutter).

If you are on fallback mode you can still change the window manager with your preferred one.

## Upgrade from GNOME 2.32

**Warning:** The session might crash during the update and it is recommended that you run the update command in a screen session, from another DE or WM, or from tty

```
# pacman -Syu 

```

**Important**: You will end up with a system that has GNOME 3.x **fallback** mode. To install the new shell:

```
# pacman -S gnome-shell

```

## Installing to a new system

GNOME 3 is in [extra]. You can install it by running the following command:

```
# pacman -Syu
# pacman -S gnome

```

For additional applications

```
# pacman -S gnome-extra

```

### Daemons and modules needed by GNOME

The GNOME desktop requires one daemon, **DBUS** for proper operation.

[Start the dbus daemon](/index.php/Daemon#Performing_daemon_actions_manually "Daemon") and add dbus to your [DAEMONS array](/index.php/Rc.conf#Daemons "Rc.conf") so it starts automatically on boot.

**GVFS** allows the mounting of virtual file systems (e.g. file systems over FTP or SMB) to be used by other applications, including the GNOME file manager Nautilus. This is done with the use of **FUSE**: a user space virtual file system layer kernel module.

To load the FUSE kernel module:

```
# modprobe fuse

```

Or add the module to the **MODULES** array in `/etc/rc.conf` so they will load at boot up, e.g.:

```
MODULES=(**fuse** usblp)

```

**Note:** FUSE is a kernel module, not a daemon.

### Running GNOME

For better desktop integration **GDM** is recommended (but other login managers, such as SLiM also work, see Policykit section).

```
# pacman -S gdm

```

Check out [Display manager](/index.php/Display_manager "Display manager") to learn how to start it correctly.

If you prefer to start it from the console, add the following line to your `~/.xinitrc` file, making sure it's the last line and the only one that starts with _exec_ (see [xinitrc](/index.php/Xinitrc "Xinitrc")):

```
exec gnome-session

```

Now GNOME will start when you enter the following command:

```
$ startx

```

## Using the shell

See [https://live.gnome.org/GnomeShell/CheatSheet](https://live.gnome.org/GnomeShell/CheatSheet)

## Customization

### Using Gnome-tweak-tool

```
# pacman -S gnome-tweak-tool

```

This tool can customize fonts, themes, minimize & maximize buttons and some other useful settings like what action is taken when the lid is closed.

A good customization tutorial is [http://blog.fpmurphy.com/2011/03/customizing-the-gnome-3-shell.html](http://blog.fpmurphy.com/2011/03/customizing-the-gnome-3-shell.html) which explores the power of gsettings.

Version 3.0.3 only works if gnome-shell is installed (OK if forced to fallback mode), bug: [https://bugzilla.gnome.org/show_bug.cgi?id=647132](https://bugzilla.gnome.org/show_bug.cgi?id=647132)

#### Wallpaper

```
$ GSETTINGS_BACKEND=dconf gsettings get org.gnome.desktop.background picture-uri
$ GSETTINGS_BACKEND=dconf gsettings set org.gnome.desktop.background picture-uri "file:///usr/share/backgrounds/gnome/SundownDunes.jpg"

```

You will need to point to a file where the gdm user has permission to read, not in your home directory.

#### Turning off the sound

```
$ GSETTINGS_BACKEND=dconf gsettings set org.gnome.desktop.sound event-sounds false

```

#### Change GDM's keyboard layout

Since GDM 3 does not care about your gnome keyboard settings, you have to set your layout to Xorg config. See here: [Beginners' guide#Non-US_keyboard](/index.php/Beginners%27_guide#Non-US_keyboard "Beginners' guide")

### Changing the GTK3 theme using settings.ini

Similar to `~/.gtkrc-2.0` for GTK2+ it is possible to set the GTK3 (GNOME 3) theme via `${XDG_CONFIG_HOME}/gtk-3.0/settings.ini`. By default `${XDG_CONFIG_HOME}` is interpreted as `~/.config`.

Only Adwaita theme exists in this moment for gtk3 and is available in [gnome-themes-standard](https://www.archlinux.org/packages/?name=gnome-themes-standard) package.

Example:

```
 [Settings]
 gtk-theme-name = Adwaita
 gtk-fallback-icon-theme = gnome
 # next option is applicable only if selected theme supports it
 gtk-application-prefer-dark-theme = true
 # set font name and dimension
 gtk-font-name = Sans 10

```

It may be necessary to restart one's DE or WM for the settings to be applied.

**Note:** More options can be find there: [GtkSettings documentation](http://developer.gnome.org/gtk3/3.0/GtkSettings.html#GtkSettings.properties)

### Resizing the massive title bar

```
# sed -i "/title_vertical_pad/s/value=\"[0-9]\{1,2\}\"/value=\"0\"/g" /usr/share/themes/Adwaita/metacity-1/metacity-theme-3.xml

```

Hit `Alt+F2` and type `restart` followed by `Enter`

This will change the title_vertical_pad from 14 to 0 giving a much sleeker look to windows.

To restore the original values:

```
sudo pacman -S gnome-themes-standard

```

### Setting an icon theme

**Note:** With gnome-tweak-tool version 3.0.3 and later, you can place icon theme you wish to use inside ~/.icons.

Usefully, Gnome 3 is able to use Gnome 2 icon themes, which means you're not stuck with the default set. To do this, simply copy your desired icon theme's directory to ~/.icons. For example:

```
$ cp -R /home/user/Desktop/my_new_icon_theme ~/.icons

```

The new icon theme 'my_new_icon_theme' will now be selectable using the gnome-tweak-tool (under 'Interface'), otherwise it can be set with no need of gnome-tweak-tool by adding the gtk-icon-theme-name entry inside ${XDG_CONFIG_HOME}/gtk-3.0/settings.ini.

 `${XDG_CONFIG_HOME}/gtk-3.0/settings.ini` 

```
.....
gtk-icon-theme-name = my_new_icon_theme
.....
```

### Start program automatically after login to GNOME 3

You can specify which programs to start automatically after login using the **gnome-session-properties** tool, which is a part of the **gnome-session** package.

```
$ gnome-session-properties

```

### Removing folders from the "Computer" section in Nautilus's Places sidebar

The displayed folders are specified in `~/.config/user-dirs.dirs` and can be altered with any editor. An execution of `xdg-user-dirs-update` will change them again, thus it may be advisable to set the file permissions to read-only.

### Setting the default terminal via console

`gsettings`, which replaces `gconftool-2` in Gnome 3, is used to set e. g. the default terminal manually. The setting is relevant for _nautilus-open-terminal_.

The commands for [urxvt](/index.php/Rxvt-unicode "Rxvt-unicode") run as daemon:

```
gsettings set org.gnome.desktop.default-applications.terminal exec urxvtc
gsettings set org.gnome.desktop.default-applications.terminal exec-arg "'-e'"

```

### Setting Nautilus to use location bar entry

If you want to enter path locations manually in Nautilus, you can press `Ctrl+l`. To make this persistent you can use gsettings.

```
gsettings set org.gnome.nautilus.preferences always-use-location-entry true

```

### Disable accessibility icon in panel

First deactivate it as startup-service: [GNOME_3#Start_program_automatically_after_login_to_GNOME_3](/index.php/GNOME_3#Start_program_automatically_after_login_to_GNOME_3 "GNOME 3")

After that create a folder named **noa11y.icon@panel.ui** in **$HOME/.local/share/gnome-shell/extensions**. In this folder create two files. The first one is named **extension.js** and has this content:

```
const Panel = imports.ui.panel;

function main() {
	Panel.STANDARD_TRAY_ICON_SHELL_IMPLEMENTATION['a11y'] = ''**_;_**
}

```

The second one is named **metadata.json** and has this content:

```
{
	"shell-version": ["3.0.1"],
	"uuid": "noa11y.icon@panel.ui",
	"name": "na11y",
	"description": "Turn off the ally icon in the panel"
}

```

Now restart the gnome-shell (press **ALT+F2**, type **r** and press **Enter**) and the icon is away. If this extensions stops working adjust the shell-version number in the metadata-file according to your version.

If the above method doesn't work, you can try disabling the accessibility icon system wide. Edit the file **/usr/share/gnome-shell/js/ui/panel.js**, find this line:

```
'a11y': imports.ui.status.accessibility.ATIndicator,

```

and comment it out e.g.:

```
/* 'a11y': imports.ui.status.accessibility.ATIndicator, */

```

Afterwards restart the shell.

### Disable bluetooth icon in panel

First deactivate it as startup-service: [GNOME_3#Start_program_automatically_after_login_to_GNOME_3](/index.php/GNOME_3#Start_program_automatically_after_login_to_GNOME_3 "GNOME 3")

After that create a folder named **nobluetooth.icon@panel.ui** in **$HOME/.local/share/gnome-shell/extensions**. In this folder create two files. The first one is named **extension.js** and has this content:

```
const Panel = imports.ui.panel;

function main() {
	Panel.STANDARD_TRAY_ICON_SHELL_IMPLEMENTATION['bluetooth'] = ''**_;_**
}

```

The second one is named **metadata.json** and has this content:

```
{
	"shell-version": ["3.0.1"],
	"uuid": "nobluetooth.icon@panel.ui",
	"name": "nbluetooth",
	"description": "Turn off the bluetooth icon in the panel"
}

```

Now restart the gnome-shell (press **ALT+F2**, type **r** and press **Enter**) and the icon is away. If this extensions stops working adjust the shell-version number in the metadata-file according to your version.

### Middle Mouse Button Emulation

By default, GNOME 3 disables middle mouse button emulation regardless of Xorg settings (**Emulate3Buttons**). To enable middle mouse button emulation use:

```
gsettings set org.gnome.settings-daemon.peripherals.mouse middle-button-enabled true

```

### Battery icon

To have battery tray icon, install gnome-power-manager package:

```
# pacman -S gnome-power-manager

```

### Xmonad

Upgrading to Gnome 3 will (most-likely) break your xmonad setup. You can use xmonad again by forcing fallback mode (see below) and creating the following two files:

 `/usr/share/gnome-session/sessions/xmonad.session` 

```
[GNOME Session]
Name=Xmonad session
RequiredComponents=gnome-panel;gnome-settings-daemon;
RequiredProviders=windowmanager;notifications;
DefaultProvider-windowmanager=xmonad
DefaultProvider-notifications=notification-daemon
```

 `/usr/share/xsessions/xmonad-gnome-session.desktop` 

```
[Desktop Entry]
Name=Xmonad GNOME
Comment=Tiling window manager
TryExec=/usr/bin/gnome-session
Exec=gnome-session --session=xmonad
Type=XSession
```

The next time you log in, you'll have the ability to choose _Xmonad GNOME_ as your session.

## Enabling fallback mode

Your session will automatically start in fallback mode if gnome-shell is not present or if your desktop cannot handle graphics acceleration (such as running in a Virtual Machine or on old hardware). If you want to enable it while having gnome-shell installed, open gnome-control-center. Open System Info > Graphics. Change _Forced Fallback Mode_ to _ON_.

## Enabling hidden features

Gnome 3.0 hides a lot of useful options which you can customize with **dconf-editor** or **gconf-editor** for settings not yet migrated to dconf.

### Changing Hotkeys

In **dconf-editor**, enable org.gnome.desktop.interface "can-change-accels".

An example of changing the delete hotkey: Open nautilus, select any file/directory, then click "Edit" from the menubar, and hover over the "Move to Trash" menuitem. While hovering, push **delete**, and default accel will be unset. Now push the key that you want to set as accel. i.e. Pushing again **delete**, will make the accel change to "del".

Make sure you have selected a file, else the "Move to Trash" menuitem will be greyed out. You should disable "can-change-accels" afterwards, to prevent accidental accel changes.

## How to shutdown through the Status menu

For now, the Shutdown option seems to be hidden if the user presses the Status menu on the upper right. If you want to shutdown your system through the Status menu, click on it and then press the **Alt** button. The "**Suspend**" option will instantly turn into "Power off...", as long as you are pressing the Alt button, which will allow you to properly shutdown your system.

You can also install the "Alternative Status Menu" extension (see the section on Enabling Extensions, below). This will put a permanent "Power Off" option in the Status menu below the usual suspend option.

## Enabling integrated messaging

Empathy, the engine behind the integrated messaging, and all of the system settings based on your messaging accounts will not show up unless the **telepathy** group of packages or at least one of the backends (**telepathy-gabble**, or **telepathy-haze**, for example) is installed. These are not included in the default Arch GNOME installs and the Empathy interface doesn't give a nice error message, it just fails to work silently. You can install them:

```
# pacman -S telepathy

```

## Enabling extensions

Gnome Shell can be customised to an extent with extensions that have been written by others. These provide functionality like having a dock that is always present, and being able to change the shell theme. More details on the functionality of currently available extensions is given [here](http://www.webupd8.org/2011/04/gnome-shell-extensions-additional.html) You can use the [gnome-shell-extensions-git](https://aur.archlinux.org/packages/gnome-shell-extensions-git/) package in the AUR to install them or [install them individually using the [extra](https://www.archlinux.org/packages/?sort=&q=gnome-shell-extension&maintainer=&last_update=&flagged=&limit=50) extensions' snapshots] . Restart Gnome to enable them.

If installing the extensions causes Gnome to stop working then you must remove the user-theme extension and and the auto-move-windows extension from their installation directory (could be in ~/.local/share/gnome-shell/extensions or /usr/share/gnome-shell/extensions or /usr/local/share/gnome-shell/extensions). Removing or adding extensions to these directories will remove or install them form the system. More details on Gnome Shell extensions are available [here](https://live.gnome.org/GnomeShell/Extensions).

## Troubleshooting

### My screen isn't locked after resume from suspend/hibernate

Screen lock does only work when you suspend through gnome status menu. If you suspend or hibernate with powerbutton/etc. you screen is not locked after resume. This problem occours because of an config failure in dconf, so just open dconf-editor and change lock-use screensaver to false (unchecked) in org/gnome/power-manager. Your screen will no be locked after resume, regardless whether you used gnome status menu or power button or key combination. For more information see bugreport: [Screen gets no more locked after suspend#Comment 8](https://bugzilla.redhat.com/show_bug.cgi?id=698135#c8)

### My GTK2+ apps show segfaults and won't start

That usually happens when **oxygen-gtk** is installed. That theme conflicts somehow with GNOME 3's or/and GTK3 settings and when it has been set as a GTK2 theme, the GTK2 apps segfault with errors like:

```
 (firefox-bin:14345): GLib-GObject-WARNING **: invalid (NULL) pointer instance

(firefox-bin:14345): GLib-GObject-CRITICAL **: g_signal_connect_data: assertion `G_TYPE_CHECK_INSTANCE (instance)' failed

(firefox-bin:14345): Gdk-CRITICAL **: IA__gdk_screen_get_default_colormap: assertion `GDK_IS_SCREEN (screen)' failed

(firefox-bin:14345): Gdk-CRITICAL **: IA__gdk_colormap_get_visual: assertion `GDK_IS_COLORMAP (colormap)' failed

(firefox-bin:14345): Gdk-CRITICAL **: IA__gdk_screen_get_default_colormap: assertion `GDK_IS_SCREEN (screen)' failed

(firefox-bin:14345): Gdk-CRITICAL **: IA__gdk_screen_get_root_window: assertion `GDK_IS_SCREEN (screen)' failed

(firefox-bin:14345): Gdk-CRITICAL **: IA__gdk_screen_get_root_window: assertion `GDK_IS_SCREEN (screen)' failed

(firefox-bin:14345): Gdk-CRITICAL **: IA__gdk_window_new: assertion `GDK_IS_WINDOW (parent)' failed
Segmentation fault

```

The current "workaround" is to **remove** **oxygen-gtk** from the system completely and set another theme for your apps.

### I use the ATI Catalyst driver and I encounter glitches and artifacts while using GNOME Shell

For the moment, Catalyst is not proposed to be used while running GNOME Shell. The opensource ATI driver, xf86-video-ati, however, seems to be working properly with the GNOME 3 composited desktop.

### I have multiple monitors and the Dock extension appears stuck between them

If you have multiple monitors configured using Nvidia Twinview, the dock extension may get sandwiched in-between the monitors. You can edit the source of this extension to reposition the dock to a position of your choosing.

Edit **/usr/share/gnome-shell/extensions/dock@gnome-shell-extensions.gnome.org/extension.js** and locate this line in the source:

```
this.actor.set_position(primary.width-this._item_size-this._spacing-2, (primary.height-height)/2);

```

The first parameter is the X position of the dock display, by subtracting 15 pixels as opposed to 2 pixels from this it correctly positioned on my primary monitor, you can play around with any X,Y coordinate pair to position it correctly.

```
this.actor.set_position(primary.width-this._item_size-this._spacing-15, (primary.height-height)/2);

```

### There are no event sounds for Empathy and other programs

The **sound-theme-freedesktop** package must be installed for the default event sounds:

```
 # pacman -S sound-theme-freedesktop

```

If you're using [OSS](/index.php/OSS "OSS"), you may want to install **libcanberra-oss** [from AUR](https://aur.archlinux.org/packages.php?ID=31163).

### Editing hotkeys via can-change-accels fails

It is also possible to manually change the keys via an application's so-called accel map file. Where it is to be found is up to the application: For instance, Thunar's is at `~/.config/Thunar/accels.scm`, whereas Nautilus's is located at `~/.gnome2/accels/nautilus`. The file should contain a list of possible hotkeys, each unchanged line commented out with a leading ";" that has to be removed for a change to become active.

### "Failed to load session 'gnome-fallback'" message

Check if **notification-daemon** is installed.

```
 # pacman -S notification-daemon

```

### [fallback mode] Panels and applets don't respond to right click to remove, etc, as in GNOME 2

Check Configuration Editor: /apps/metacity/general/mouse_button_modifier. This modifier key (<Alt>, <Super>, etc) used for normal windows is also used by panels and their applets.

### Show Desktop: ALT+STRG+D does not Work

The GNOME developers treated the corresponding binding as bug (see [https://bugzilla.gnome.org/show_bug.cgi?id=643609](https://bugzilla.gnome.org/show_bug.cgi?id=643609)) due to Minimization being deprecated. To show the desktop again assign ALT+STRG+D to the following setting:

```
System Settings --> Keyboard --> Shortcuts --> Windows --> Hide all normal windows

```