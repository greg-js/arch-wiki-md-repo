KDE is a software project currently comprising of a [desktop environment](/index.php/Desktop_environment "Desktop environment") known as Plasma (or Plasma Workspaces), a collection of libraries and frameworks (KDE Frameworks) and several applications (KDE Applications) as well. KDE upstream has a well maintained [UserBase wiki](http://userbase.kde.org/). Detailed information about most KDE applications can be found there.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Plasma Desktop](#Plasma_Desktop)
    *   [1.2 Upgrading from Plasma 4 to 5](#Upgrading_from_Plasma_4_to_5)
    *   [1.3 KDE applications and language packs](#KDE_applications_and_language_packs)
*   [2 Starting Plasma](#Starting_Plasma)
    *   [2.1 Wayland](#Wayland)
*   [3 Configuration](#Configuration)
    *   [3.1 Personalization](#Personalization)
        *   [3.1.1 Plasma desktop](#Plasma_desktop_2)
            *   [3.1.1.1 Themes](#Themes)
                *   [3.1.1.1.1 Qt and GTK+ Applications Appearance](#Qt_and_GTK.2B_Applications_Appearance)
            *   [3.1.1.2 Widgets](#Widgets)
            *   [3.1.1.3 Sound applet in the system tray](#Sound_applet_in_the_system_tray)
            *   [3.1.1.4 Disable panel shadow](#Disable_panel_shadow)
        *   [3.1.2 Window decorations](#Window_decorations)
        *   [3.1.3 Icon themes](#Icon_themes)
        *   [3.1.4 Fonts](#Fonts)
            *   [3.1.4.1 Fonts in a Plasma session look poor](#Fonts_in_a_Plasma_session_look_poor)
            *   [3.1.4.2 Fonts are huge or seem disproportional](#Fonts_are_huge_or_seem_disproportional)
        *   [3.1.5 Space efficiency](#Space_efficiency)
    *   [3.2 Printing](#Printing)
    *   [3.3 Samba/Windows support](#Samba.2FWindows_support)
    *   [3.4 KDE Desktop activities](#KDE_Desktop_activities)
    *   [3.5 Power saving](#Power_saving)
    *   [3.6 Autostarting applications](#Autostarting_applications)
*   [4 System administration](#System_administration)
    *   [4.1 Terminate Xorg server through KDE System Settings](#Terminate_Xorg_server_through_KDE_System_Settings)
    *   [4.2 KCM](#KCM)
*   [5 Desktop search](#Desktop_search)
    *   [5.1 Baloo](#Baloo)
        *   [5.1.1 Using and configuring Baloo](#Using_and_configuring_Baloo)
        *   [5.1.2 How do I index a removable device?](#How_do_I_index_a_removable_device.3F)
    *   [5.2 Web browsers](#Web_browsers)
        *   [5.2.1 Konqueror and Rekonq](#Konqueror_and_Rekonq)
        *   [5.2.2 Chromium and Chrome](#Chromium_and_Chrome)
        *   [5.2.3 Firefox](#Firefox)
        *   [5.2.4 Qupzilla](#Qupzilla)
*   [6 PIM](#PIM)
    *   [6.1 Akonadi](#Akonadi)
        *   [6.1.1 Installation](#Installation_2)
        *   [6.1.2 Disabling Akonadi](#Disabling_Akonadi)
        *   [6.1.3 Database configuration](#Database_configuration)
            *   [6.1.3.1 MariaDB/MySQL](#MariaDB.2FMySQL)
                *   [6.1.3.1.1 Using ZFS](#Using_ZFS)
            *   [6.1.3.2 PostgreSQL](#PostgreSQL)
            *   [6.1.3.3 SQLite](#SQLite)
*   [7 Phonon](#Phonon)
    *   [7.1 Which backend should I choose?](#Which_backend_should_I_choose.3F)
*   [8 Useful applications](#Useful_applications)
    *   [8.1 Yakuake](#Yakuake)
    *   [8.2 KDE Telepathy](#KDE_Telepathy)
        *   [8.2.1 Use Telegram with KDE Telepathy](#Use_Telegram_with_KDE_Telepathy)
*   [9 Tips and tricks](#Tips_and_tricks)
    *   [9.1 Using an alternative window manager](#Using_an_alternative_window_manager)
        *   [9.1.1 KDE/Openbox session](#KDE.2FOpenbox_session)
        *   [9.1.2 Compiz custom](#Compiz_custom)
        *   [9.1.3 Re-enabling compositing effects](#Re-enabling_compositing_effects)
    *   [9.2 Integrate Android](#Integrate_Android)
    *   [9.3 Configure KWin to use OpenGL ES](#Configure_KWin_to_use_OpenGL_ES)
    *   [9.4 Speed up application startup](#Speed_up_application_startup)
    *   [9.5 Configuring monitor resolution / multiple monitors](#Configuring_monitor_resolution_.2F_multiple_monitors)
    *   [9.6 Open application launcher with Super key (Windows key)](#Open_application_launcher_with_Super_key_.28Windows_key.29)
    *   [9.7 Enabling touchpad tap to click on plasma wayland session](#Enabling_touchpad_tap_to_click_on_plasma_wayland_session)
*   [10 Troubleshooting](#Troubleshooting)
    *   [10.1 Configuration related](#Configuration_related)
        *   [10.1.1 Plasma desktop behaves strangely](#Plasma_desktop_behaves_strangely)
        *   [10.1.2 Clean cache to resolve upgrade problems](#Clean_cache_to_resolve_upgrade_problems)
    *   [10.2 Clean akonadi configuration to fix KMail](#Clean_akonadi_configuration_to_fix_KMail)
    *   [10.3 Fix empty IMAP inbox](#Fix_empty_IMAP_inbox)
    *   [10.4 Getting current state of KWin for support and debug purposes](#Getting_current_state_of_KWin_for_support_and_debug_purposes)
    *   [10.5 KDE and Qt programs look bad when in a different window manager](#KDE_and_Qt_programs_look_bad_when_in_a_different_window_manager)
    *   [10.6 KF5/Qt5 applications don't display icons in i3/fvwm/awesome](#KF5.2FQt5_applications_don.27t_display_icons_in_i3.2Ffvwm.2Fawesome)
    *   [10.7 Graphical related problems](#Graphical_related_problems)
        *   [10.7.1 Plasma keeps crashing with legacy Nvidia](#Plasma_keeps_crashing_with_legacy_Nvidia)
        *   [10.7.2 Applications don't refresh properly](#Applications_don.27t_refresh_properly)
        *   [10.7.3 Low 2D desktop performance (or) artifacts appear when on 2D](#Low_2D_desktop_performance_.28or.29_artifacts_appear_when_on_2D)
            *   [10.7.3.1 GPU driver problem](#GPU_driver_problem)
            *   [10.7.3.2 The Raster engine workaround](#The_Raster_engine_workaround)
        *   [10.7.4 Low 3D desktop performance](#Low_3D_desktop_performance)
        *   [10.7.5 Desktop compositing is disabled on my system with a modern Nvidia GPU](#Desktop_compositing_is_disabled_on_my_system_with_a_modern_Nvidia_GPU)
        *   [10.7.6 Flickering in fullscreen when compositing is enabled](#Flickering_in_fullscreen_when_compositing_is_enabled)
        *   [10.7.7 Display settings lost on reboot (multiple monitors)](#Display_settings_lost_on_reboot_.28multiple_monitors.29)
    *   [10.8 Sound problems under KDE](#Sound_problems_under_KDE)
        *   [10.8.1 ALSA related problems](#ALSA_related_problems)
            *   [10.8.1.1 "Falling back to default" messages when trying to listen to any sound in KDE](#.22Falling_back_to_default.22_messages_when_trying_to_listen_to_any_sound_in_KDE)
            *   [10.8.1.2 MP3 files cannot be played when using the GStreamer Phonon backend](#MP3_files_cannot_be_played_when_using_the_GStreamer_Phonon_backend)
    *   [10.9 Inotify folder watch limit](#Inotify_folder_watch_limit)
    *   [10.10 Freezes when using Automount on a NFS volume](#Freezes_when_using_Automount_on_a_NFS_volume)
    *   [10.11 Locale warning when installing packages in Konsole](#Locale_warning_when_installing_packages_in_Konsole)
    *   [10.12 Multi-monitor issues](#Multi-monitor_issues)
*   [11 Unstable releases](#Unstable_releases)
*   [12 See also](#See_also)

## Installation

### Plasma Desktop

**Note:**

*   Plasma 5 is not co-installable with Plasma 4.
*   The Plasma 4 desktop is unmaintained since August 2015.[[1]](https://www.kde.org/announcements/announce-applications-15.08.0.php) It is no longer in the official repositories since December 2015.[[2]](https://www.archlinux.org/news/dropping-plasma-4/)
*   [KDM](/index.php/KDM "KDM") is no longer available for Plasma 5\. KDE upstream [recommends](http://blog.davidedmundson.co.uk/blog/display_managers_finale) using the [SDDM](/index.php/SDDM "SDDM") display manager as it provides integration with the Plasma 5 theme.

Before installing Plasma, make sure you have a working [Xorg](/index.php/Xorg "Xorg") installation on your system.

Install the [plasma-meta](https://www.archlinux.org/packages/?name=plasma-meta) meta-package or the [plasma](https://www.archlinux.org/groups/x86_64/plasma/) group. For differences between [plasma-meta](https://www.archlinux.org/packages/?name=plasma-meta) and [plasma](https://www.archlinux.org/groups/x86_64/plasma/) reference [Creating packages#Meta packages and groups](/index.php/Creating_packages#Meta_packages_and_groups "Creating packages"). Alternatively, for a more minimal Plasma installation, install the [plasma-desktop](https://www.archlinux.org/packages/?name=plasma-desktop) package.

### Upgrading from Plasma 4 to 5

1.  Isolate `multi-user.target`: `# systemctl isolate multi-user.target` 
2.  If you use KDM as display manager, [disable](/index.php/Disable "Disable") the `kdm.service` systemd unit.
3.  [Uninstall](/index.php/Install "Install") the [kdebase-workspace](https://aur.archlinux.org/packages/kdebase-workspace/) package.
4.  [Install](/index.php/Install "Install") the [plasma-meta](https://www.archlinux.org/packages/?name=plasma-meta) package or the [plasma](https://www.archlinux.org/groups/x86_64/plasma/) group.
5.  [Enable](/index.php/Enable "Enable") the `sddm.service` systemd unit, or install and enable any other [display manager](/index.php/Display_manager "Display manager").
6.  Reboot or simply [start](/index.php/Start "Start") the systemd `sddm.service` unit.

**Note:** The Plasma 4 configuration is not automatically migrated to Plasma 5, so you will have to configure your desktop from scratch.

### KDE applications and language packs

To install the full set of KDE Applications, install the [kde-applications](https://www.archlinux.org/groups/x86_64/kde-applications/) group or the [kde-applications-meta](https://www.archlinux.org/packages/?name=kde-applications-meta) meta-package. Note that this will only install applications, it will not install any version of the Plasma Desktop.

If you need language files, install `kde-l10n-**yourlanguagehere**` (e.g. [kde-l10n-de](https://www.archlinux.org/packages/?name=kde-l10n-de) for the German language). For a full list of available languages see [this link](https://www.archlinux.org/packages/extra/any/kde-l10n/).

## Starting Plasma

**Tip:** To better integrate SDDM with Plasma, it is recommended to edit `/etc/sddm.conf` to use the breeze theme. Refer to [SDDM#Theme settings](/index.php/SDDM#Theme_settings "SDDM") for instructions.

To launch a Plasma 5 session, choose *Plasma* in your [display manager](/index.php/Display_manager "Display manager") menu.

Alternatively, to start Plasma with *startx*, append `exec startkde` to your `.xinitrc` file. If you want to start Xorg at login, please see [Start X at login](/index.php/Start_X_at_login "Start X at login").

### Wayland

As of Plasma 5.8, Plasma on [Wayland](/index.php/Wayland "Wayland") should be usable, although there are a [few known problems](https://community.kde.org/Plasma/5.8_Errata#Wayland).

*   To start a Plasma on Wayland session from a display manager, install the [plasma-wayland-session](https://www.archlinux.org/packages/?name=plasma-wayland-session) package and *Plasma* should show up in the display manager.
*   To start a Plasma on Wayland session from a console, run `startplasmacompositor`.

## Configuration

Most settings for KDE applications are stored in `~/.config`, but some older applications may use `~/.kde4`. However, configuring KDE is primarily done through the **System Settings** application. It can be started from a terminal by executing *systemsettings5*.

Frameworks 5 applications can use KDE 4 configuration however they expect the configuration files to be located in different places. To allow Frameworks 5 applications running in KDE 4 to share the same configurations they may be moved to the new locations and symlinked back to the old. Examples are:

*   Konsole profiles from `~/.kde4/share/apps/konsole` to `~/.local/share/konsole/`
*   Application appearance from `~/.kde4/share/config/kdeglobals` to `~/.config/kdeglobals`

### Personalization

#### Plasma desktop

##### Themes

**Note:** If the Plasma cursor theme is incorrect in some instances, see the following [forum post](https://bbs.archlinux.org/viewtopic.php?pid=1533071#p1533071) for a workaround.

[Plasma themes](http://kde-look.org/index.php?xcontentmode=76) define the look of panels and plasmoids. For easy system-wide installation, some such themes are available in both the official repositories and the [AUR](https://aur.archlinux.org/packages.php?O=0&K=plasmatheme&do_Search=Go).

The easiest way to install themes is by going through the Desktop Settings control panel:

```
 Workspace Theme > Desktop Theme > Get new Themes

```

This will present a nice frontend for [kde-look.org](http://www.kde-look.org/) that allows you to install, uninstall, or update third-party plasmoid scripts with literally just one click.

Splash and Lock screens are currently unavailable so to customize these screens you have to modify the original theme found in `/usr/share/plasma/look-and-feel/`. See [this thread](https://www.kubuntuforums.net/showthread.php?67599-Plasma-5-background-images&s=59832dc20e5bfc2948dbb591d8453f61) on the Kubuntu forums.

Note that the [SDDM](/index.php/SDDM "SDDM") login screen is not part of this theme.

###### Qt and GTK+ Applications Appearance

**Tip:** For Qt and GTK theme consistency, see [Uniform look for Qt and GTK applications](/index.php/Uniform_look_for_Qt_and_GTK_applications "Uniform look for Qt and GTK applications").

	Qt4

For Qt4 applications to have a consistent appearance, there are two options: Install [breeze-kde4](https://www.archlinux.org/packages/?name=breeze-kde4) and then pick Breeze as GUI Style in `qtconfig-qt4`; or install [breeze-gtk](https://www.archlinux.org/packages/?name=breeze-gtk) and pick GTK+ as GUI Style.

	GTK+

The recommended theme for a pleasant appearance in GTK+ applications is [breeze-gtk](https://www.archlinux.org/packages/?name=breeze-gtk) or [gnome-breeze-git](https://aur.archlinux.org/packages/gnome-breeze-git/), a GTK+ theme designed to mimic the appearance of Plasma 5 Breeze. Install [kde-gtk-config](https://www.archlinux.org/packages/?name=kde-gtk-config) and select the installed GTK-theme for GTK2/GTK3-Theme in *System Settings > Application Style > GNOME Application Style*.

In some themes, tooltips in GTK+ applications have white text on white backgrounds making it difficult to read. To change the colors in GTK2 applications, find the section for tooltips in the gtkrc file and change it. For GTK3 application two files need to be changed, gtk.css and settings.ini.

##### Widgets

Plasmoids are little scripted (plasmoid scripts) or coded (plasmoid binaries) KDE applications designed to enhance the functionality of your desktop.

The easiest way to install plasmoid scripts is by right-clicking onto a panel or the desktop and choosing *Add Widgets > Get new Widgets > Download Widgets*. This will present a nice frontend for [kde-look.org](http://www.kde-look.org/) that allows you to install, uninstall, or update third-party plasmoid scripts with literally just one click.

Many Plasmoid binaries are [available from the AUR](https://aur.archlinux.org/packages.php?O=0&K=plasmoid&do_Search=Go&PP=25&SO=d&SB=v).

##### Sound applet in the system tray

[Install](/index.php/Install "Install") [plasma-pa](https://www.archlinux.org/packages/?name=plasma-pa) or [kmix](https://www.archlinux.org/packages/?name=kmix) (start Kmix from the Application Launcher).

**Note:** To adjust the [step size of volume increments/decrements](https://bugs.kde.org/show_bug.cgi?id=313579#c28), add e.g. `VolumePercentageStep=1` in the `[Global]` section of `~/.kde4/share/config/kmixrc`

##### Disable panel shadow

As the plasma panel is on top of other windows, its shadow is drawn over them. [[3]](https://bbs.archlinux.org/viewtopic.php?pid=1228394#p1228394) To disable this behaviour without impacting other shadows, [install](/index.php/Install "Install") [xorg-xprop](https://www.archlinux.org/packages/?name=xorg-xprop) and run:

```
$ xprop -remove _KDE_NET_WM_SHADOW

```

then select the panel with the plus-sized cursor. [[4]](https://forum.kde.org/viewtopic.php?f=285&t=121592) For automation, install [xorg-xwininfo](https://www.archlinux.org/packages/?name=xorg-xwininfo) and create the following script:

 `/usr/local/bin/kde-no-shadow` 
```
#!/bin/bash
for WID in $(xwininfo -root -tree | sed '/"Plasma": ("plasmashell" "plasmashell")/!d; s/^  *\([^ ]*\) .*/\1/g'); do
   xprop -id $WID -remove _KDE_NET_WM_SHADOW
done

```

The script can be run on login with *Add Script* in *Autostart*:

```
$ kcmshell5 autostart

```

#### Window decorations

[Window decorations](http://kde-look.org/index.php?xcontentmode=75) can be changed in *System Settings > Workspace Appearance > Window Decorations*.

There you can also directly download and install more themes with one click, and some are available in the [AUR](https://aur.archlinux.org/packages.php?O=0&K=kdestyle&do_Search=Go&PP=25&SO=d&SB=v).

#### Icon themes

Icon themes can be installed and changed on *System Settings > Icons*.

**Note:** Although all modern Linux desktops share the same icon theme format, desktops like [GNOME](/index.php/GNOME "GNOME") use fewer icons (esp. in menus and toolbars). Themes developed for such desktops usually lack icons required by Plasma 5 and KDE apps.
It is recommended to install Plasma compatible icon themes instead.

#### Fonts

##### Fonts in a Plasma session look poor

Try installing the [ttf-dejavu](https://www.archlinux.org/packages/?name=ttf-dejavu) and [ttf-liberation](https://www.archlinux.org/packages/?name=ttf-liberation) packages.

After the installation, be sure to log out and back in. You should not have to modify anything in *System Settings > Fonts*.

If you have personally set up how your [Fonts](/index.php/Fonts "Fonts") render, be aware that System Settings may alter their appearance. When you go *System Settings > Appearance > Fonts* System Settings will likely alter your font configuration file (`fonts.conf`).

There is no way to prevent this, but, if you set the values to match your `fonts.conf` file, the expected font rendering will return (it will require you to restart your application or in a few cases restart your desktop). Note that Gnome's Font Preferences also does this.

##### Fonts are huge or seem disproportional

Try to force font DPI to **96** in *System Settings > Application Appearance > Fonts*.

If that does not work, try setting the DPI directly in your Xorg configuration as documented [here](/index.php/Xorg#Setting_DPI_manually "Xorg").

#### Space efficiency

The Plasma Netbook shell has been dropped from Plasma 5, see the following [KDE forum post](https://forum.kde.org/viewtopic.php?f=289&t=126631&p=335947&hilit=plasma+netbook#p335899) However, you can achieve something similar by editing the file `~/.config/kwinrc` adding `BorderlessMaximizedWindows=true` in the `[Windows]` section.

### Printing

**Tip:** Use the [CUPS](/index.php/CUPS "CUPS") web interface for faster configuration. Printers configured in this way can be used in KDE applications.

You can also configure printers in *System Settings > Printer Configuration*. To use this method, you must first install [print-manager](https://www.archlinux.org/packages/?name=print-manager) and [cups](https://www.archlinux.org/packages/?name=cups).

The `avahi-daemon.service` and `org.cups.cupsd.service` daemons must be started first; otherwise, you will get the following error:

```
The service 'Printer Configuration' does not provide an interface 'KCModule'
with keyword 'system-config- printer-kde/system-config-printer-kde.py'
The factory does not support creating components of the specified type.

```

If you are getting the following error, you need to give your user the right to manage printers.

```
There was an error during CUPS operation: 'cups-authorization-canceled'

```

For CUPS, this is set in `/etc/cups/cups-files.conf`.

Adding `lpadmin` to `/etc/group` and then to the `SystemGroup` directive in `/etc/cups/cups-files.conf` allows anyone in the `lpadmin` group to configure printers. Do *not* add the `lp` group to the `SystemGroup` directive, or printing will fail.

```
# groupadd -g107 lpadmin

```
 `/etc/cups/cups-files.conf` 
```
# Administrator user group...
SystemGroup sys root lpadmin
```

**Tip:** Read [CUPS#Configuration](/index.php/CUPS#Configuration "CUPS") to get more details on how to configure CUPS.

### Samba/Windows support

If you want to have access to Windows services, install [Samba](/index.php/Samba "Samba") (package [samba](https://www.archlinux.org/packages/?name=samba)).

The Dolphin share functionality requires the package [kdenetwork-filesharing](https://www.archlinux.org/packages/?name=kdenetwork-filesharing) and usershares, which the stock smb.conf does not have enabled. Instructions to add them are in [Samba#Creating usershare path](/index.php/Samba#Creating_usershare_path "Samba"), after which sharing in Dolphin should work out of the box after restarting Samba.

### KDE Desktop activities

KDE Desktop Activities are Plasma-based virtual-desktop-like sets of Plasma Widgets where you can independently configure widgets as if you have more than one screen or desktop.

On your desktop, click the Cashew Plasmoid and, on the pop-up window, press "Activities".

A plasma bar presenting you the current existing Plasma Desktop Activities will appear at the bottom of the screen. You can navigate between them by pressing the correspondent icons.

### Power saving

Plasma has an integrated power saving service called "**Powerdevil Power Management**" that may adjust the power saving profile of the system and/or the brightness of the screen (if supported).

**Note:** Powerdevil may not [inhibit](/index.php/Power_management#Power_managers "Power management") all logind settings (such as the lid close action for laptops). In these cases, the logind setting itself will need to be changed - see [Power management#Power management with systemd](/index.php/Power_management#Power_management_with_systemd "Power management").

### Autostarting applications

Plasma can autostart applications and run scripts on startup and shutdown. To autostart an application, start `systemsettings` and navigate to *Startup and Shutdown* -> *Autostart* and add the program or shell script of your choice. For applications, a `.desktop` file will be created, for shell scripts, a symlink will be created.

**Note:**

*   Programs can be autostarted on login only, whilst shell scripts can also be run on shutdown or even before Plasma itself starts.
*   Shell scripts will only be run if they are marked executable.

Place [Desktop entries](/index.php/Desktop_entries "Desktop entries") (i.e. `.desktop` files) here:

	`~/.config/autostart`

	for starting applications at login.

Place or symlink shell scripts in one of the following directories:

	`~/.config/plasma-workspace/env`

	for executing scripts at login before launching Plasma.

	`~/.config/autostart-scripts`

	for executing scripts at login.

	`~/.config/plasma-workspace/shutdown`

	for executing scripts on shutdown.

## System administration

### Terminate Xorg server through KDE System Settings

Navigate to the submenu *System Settings > Input Devices > Keyboard > Advanced (tab) > "Key Sequence to kill the X server"* and ensure that the checkbox is ticked.

### KCM

KCM stands for **KC**onfig **M**odule. KCMs can help you configure your system by providing interfaces in System Settings, or through the command line with *kcmshell5*.

**Configuration for look and feel of GTK applications.**

*   [kde-gtk-config](https://www.archlinux.org/packages/?name=kde-gtk-config)
*   [kcm-gtk](https://aur.archlinux.org/packages/kcm-gtk/)
*   [kcm-qt-graphicssystem](https://aur.archlinux.org/packages/kcm-qt-graphicssystem/)

**Configuration for the GRUB bootloader.**

*   [grub2-editor](https://aur.archlinux.org/packages/grub2-editor/)

**Configuration for the [Uncomplicated Firewall](/index.php/Uncomplicated_Firewall "Uncomplicated Firewall") (UFW)**

*   [kcm-ufw](https://aur.archlinux.org/packages/kcm-ufw/)

**Configuration for [PolicyKit](/index.php/PolicyKit "PolicyKit")**

*   [kcm-polkit-kde-git](https://aur.archlinux.org/packages/kcm-polkit-kde-git/)

**Configuration for Wacom tablets**

*   [kcm-wacomtablet](https://aur.archlinux.org/packages/kcm-wacomtablet/)

**Configuration for systemd**

*   [systemd-kcm](https://www.archlinux.org/packages/?name=systemd-kcm)

More KCMs can be found at [kde-apps.org](http://kde-apps.org/index.php?xcontentmode=273).

## Desktop search

KDE implements desktop search with a software called Baloo, a file indexing and searching solution.

### Baloo

#### Using and configuring Baloo

In order to search using Baloo on the KDE Plasma Desktop, press `ALT+F2` and type in your query. Within Dolphin press `CTRL+F`.

By default the Desktop Search KCM exposes only two options: A panel to blacklist folders and a way to disable it with one click.

Alternatively you can edit your `~/.config/baloofilerc` file ([info](https://community.kde.org/Baloo/Configuration)). Additionally the `balooctl` process can also be used. In order to disable Baloo run `balooctl disable`.

Once you added additional folders to the blacklist or disabled Baloo entirely, a process named `baloo_file_cleaner` removes all unneeded index files automatically. They are stored under `~/.local/share/baloo/`.

More advanced configuration options are available through [kcm_baloo_advanced](https://aur.archlinux.org/packages/kcm_baloo_advanced/).

#### How do I index a removable device?

By default every removable device is blacklisted. You just have to remove your device from the blacklist in the KCM panel.

### Web browsers

#### Konqueror and Rekonq

Konqueror supports two rendering engines – KHTML and QtWebKit (via the [kwebkitpart](https://www.archlinux.org/packages/?name=kwebkitpart) package) – Rekonq supports only QtWebKit. KHTML development was halted after Qt shipped WebKit but was kept for compatibility reasons. QtWebKit, in turn, has since been [deprecated](https://www.mail-archive.com/development@qt-project.org/msg18866.html) by the Qt Project and replaced by [Chromium](/index.php/Chromium "Chromium")-based Qt WebEngine which is currently not supported by either Konqueror or Rekonq. There is a [community continuation](http://qtwebkit.blogspot.com/2016/08/qtwebkit-im-back.html) of QtWebKit.

A successor named Fiber is currently in development, which will use Chromium's engine.

#### Chromium and Chrome

[Chromium](/index.php/Chromium "Chromium") and its proprietary variant Google Chrome have limited Plasma integration. [They can use KWallet](/index.php/KDE_Wallet#KDE_Wallet_for_Chrome_and_Chromium "KDE Wallet") and KDE Open/Save windows.

#### Firefox

Firefox can be configured to better integrate with Plasma. See [Firefox KDE integration](/index.php/Firefox#KDE_integration "Firefox") for details.

#### Qupzilla

Qupzilla ([qupzilla](https://www.archlinux.org/packages/?name=qupzilla)) is a Qt web browser with Plasma integration features. Qupzilla 2.0 uses Qt WebEngine instead of WebKit. The WebKit variant is also available as [qupzilla-qtwebkit-git](https://aur.archlinux.org/packages/qupzilla-qtwebkit-git/).

## PIM

KDE offers its own stack for personal information management. This includes emails, contacts, calendar, etc.

### Akonadi

Akonadi is a system meant to act as a local cache for PIM data, regardless of its origin, which can be then used by other applications. This includes the user's emails, contacts, calendars, events, journals, alarms, notes, and so on.

Akonadi does not store any data by itself: the storage format depends on the nature of the data (for example, contacts may be stored in vCard format).

#### Installation

Install [akonadi](https://www.archlinux.org/packages/?name=akonadi). For additional addons, install [kdepim-addons](https://www.archlinux.org/packages/?name=kdepim-addons). For EWS support, install [akonadi-ews-git](https://aur.archlinux.org/packages/akonadi-ews-git/).

**Note:** If you wish to use a database engine other than MariaDB/MySQL, then when installing the [akonadi](https://www.archlinux.org/packages/?name=akonadi) package, use the following command to skip installing the [mariadb](https://www.archlinux.org/packages/?name=mariadb) dependencies:
```
pacman -S akonadi --assume-installed mariadb

```

#### Disabling Akonadi

See this [section in the KDE userbase](http://userbase.kde.org/Akonadi#Disabling_the_Akonadi_subsystem).

#### Database configuration

##### MariaDB/MySQL

###### Using ZFS

If your home directory is on a ZFS pool, you will need to create `~/.config/akonadi/mysql-local.conf` with the following contents:

```
[mysqld]
innodb_use_native_aio = 0

```

Otherwise you will get the [OS error 22](/index.php/MySQL#OS_error_22_when_running_on_ZFS "MySQL")

##### PostgreSQL

1.  Install and setup PostgreSQL (see [PostgreSQL](/index.php/PostgreSQL "PostgreSQL"))
    *   Enable the `postgresql` [systemd](/index.php/Systemd "Systemd") service: `systemctl enable postgresql.service`.
2.  Create the `~/.config/akonadi/akonadiserverrc` file if it does not exist.
3.  Edit `~/.config/akonadi/akonadiserverrc` file so that it has the following contents:
    ```
    [General]
    Driver=QPSQL

    [QPSQL]
    Host=/run/postgresql/
    InitDbPath=/usr/bin/initdb
    Name=akonadi
    Options=
    Password=
    Port=5432
    ServerPath=/usr/bin/pg_ctl
    StartServer=true
    User=postgres

    ```

    **Note:** If your PostgreSQL database username, password, and port differ from `postgres`, (nothing), and `5432`, then make sure you respectively change the configuration options, `User=`, `Password=`, and `Port=`.

4.  Start Akonadi: `akonadictl start`, and check its status: `akonadictl status`.

##### SQLite

Edit `~/.config/akonadi/akonadiserverrc` to match the configuration below:

```
[General]
Driver=QSQLITE3

[QSQLITE3]
Name=/home/username/.local/akonadi/akonadi.db

```

## Phonon

From [Wikipedia](https://en.wikipedia.org/wiki/Phonon_(software) "wikipedia:Phonon (software)"):

	*“Phonon is the multimedia API provided by KDE and is the standard abstraction for handling multimedia streams within KDE software and also used by several Qt applications.*

Phonon was originally created to allow KDE and Qt software to be independent of any single multimedia framework such as GStreamer or xine and to provide a stable API for a major version's lifetime.”

**Phonon** is being widely used within KDE, for both audio (e.g., the System notifications or KDE audio apps) and video (e.g., the Dolphin video thumbnails).

### Which backend should I choose?

You can choose between backends based on [GStreamer](/index.php/GStreamer "GStreamer") and [VLC](/index.php/VLC "VLC") – each available in versions for Qt4 applications and Qt5 applications ([phonon-qt4-gstreamer](https://www.archlinux.org/packages/?name=phonon-qt4-gstreamer), [phonon-qt5-gstreamer](https://www.archlinux.org/packages/?name=phonon-qt5-gstreamer) – [phonon-qt4-vlc](https://www.archlinux.org/packages/?name=phonon-qt4-vlc), [phonon-qt5-vlc](https://www.archlinux.org/packages/?name=phonon-qt5-vlc)).

[Upstream prefers VLC](https://www.phoronix.com/scan.php?page=news_item&px=MTUwNDM) but prominent Linux distributions (Kubuntu and Fedora-KDE for example) prefer GStreamer because that allows them to easily leave out patented MPEG codecs from the default installation. Both backends have a slightly different [features set](http://community.kde.org/Phonon/FeatureMatrix).

In the past other backends were developed as well but are no longer maintained and their AUR packages have been deleted.

**Note:**

*   Multiple backends can be installed at once and prioritized at *System Settings > Multimedia > Phonon > Backend*. For Plasma 5 this would be *System Settings > Multimedia > Backend*.
*   According to the [KDE forums](https://forum.kde.org/viewtopic.php?f=250&t=126476&p=335080), the VLC backend lacks support for [ReplayGain](https://en.wikipedia.org/wiki/ReplayGain "wikipedia:ReplayGain").

**Note:**

*   If you choose the vlc backend, you may experience crashes every time kde wants to send you a audible warning (and in quite a number of other cases as well, see [[6]](https://forum.kde.org/viewtopic.php?f=289&t=135956))
*   A possible fix is to run

 `# /usr/lib/vlc/vlc-cache-gen -f /usr/lib/vlc/plugins` 

## Useful applications

The official set of KDE applications may be found [here](http://www.kde.org/applications/).

### Yakuake

[Yakuake](/index.php/Yakuake "Yakuake") provides a Quake-like terminal emulator whose visibility is toggled by the F12 key. It also has support for multiple tabs. Yakuake is available in the package [yakuake](https://www.archlinux.org/packages/?name=yakuake).

### KDE Telepathy

[KDE Telepathy](http://community.kde.org/KTp) is a project with the goal to closely integrate Instant Messaging with the KDE desktop. It utilizes the Telepathy framework as a backend and is intended to replace Kopete.

To install all Telepathy protocols, install the [telepathy](https://www.archlinux.org/groups/x86_64/telepathy/) group. To use the KDE Telepathy client, install the [telepathy-kde-meta](https://www.archlinux.org/packages/?name=telepathy-kde-meta) package that includes all the packages contained in the [telepathy-kde](https://www.archlinux.org/groups/x86_64/telepathy-kde/) group.

#### Use Telegram with KDE Telepathy

Telegram protocol is available using [telepathy-haze](https://www.archlinux.org/packages/?name=telepathy-haze), installing [telegram-purple](https://aur.archlinux.org/packages/telegram-purple/) or [telegram-purple-git](https://aur.archlinux.org/packages/telegram-purple-git/) and [telepathy-morse-git](https://aur.archlinux.org/packages/telepathy-morse-git/). The username is the Telegram account telephone number (complete with the national prefix '+xx', e.g. '+49' for Germany). The configuration through the GUI may be tricky: if the phone number is not accepted when configuring a new account in the KDE Telepathy client (with an error message complaining about an invalid parameter which prevents the account creation), insert it between single quotes and then remove the quotes manually from the configuration file (`~/.local/share/telepathy/mission-control/accounts.cfg`) after the account creation (if the quotes are not removed after, an authentication error should rise). Note that the configuration file should be edited manually when KDE Telepathy is not running, e.g. when there is no KDE desktop session active, otherwise manual changes may be overwritten by the software.

## Tips and tricks

### Using an alternative window manager

There may be reasons you want to use another window manager than KWin, for example to work around the DRI bug that causes [black screen with PRIME](/index.php/PRIME#Black_screen_with_GL-based_compositors "PRIME").

To use an alternative [window manager](/index.php/Window_manager "Window manager") with Plasma open the *System Settings* panel, navigate to *(Default) Applications > Window Manager > Use a different window manager* and select the window manager you wish to use from the list.

**Note:** The component chooser settings in plasma 5 doesn't allow changing the window manager anymore. [[7]](https://github.com/KDE/plasma-desktop/commit/2f83a4434a888cd17b03af1f9925cbb054256ade)

In order to change the window manager used you need to set the `KDEWM` [environment variable](/index.php/Environment_variable "Environment variable") before KDE startup. [[8]](https://wiki.haskell.org/Xmonad/Using_xmonad_in_KDE) To do that you can create a script called `set_window_manager.sh` in `~/.config/plasma-workspace/env` and export the `KDEWM` variable there. For example to use the i3 window manager :

 `~/.config/plasma-workspace/env/set_window_manager.sh`  `export KDEWM=/usr/bin/i3` 

And then make it executable :

 `$ chmod +x ~/.config/plasma-workspace/env/set_window_manager.sh` 

#### KDE/Openbox session

The [openbox](https://www.archlinux.org/packages/?name=openbox) package provides a session for using KDE with [Openbox](/index.php/Openbox "Openbox"). To make use of this session, select *KDE/Openbox* from the [display manager](/index.php/Display_manager "Display manager") menu.

For those starting the session manually, add the following line to your `.xinitrc` file:

```
exec openbox-kde-session

```

#### Compiz custom

If you need to run Compiz with custom options and switches select *Compiz custom* and then create a script called `compiz-kde-launcher` and add to it the commands you wish to use to start Compiz. See the example below:

 `/usr/local/bin/compiz-kde-launcher` 
```
#!/bin/bash
LIBGL_ALWAYS_INDIRECT=1
compiz --replace &
wait

```

Then make it executable:

```
$ chmod +x /usr/local/bin/compiz-kde-launcher

```

#### Re-enabling compositing effects

When replacing Kwin with a window manager which does not provide a Compositor (such as Openbox), any desktop compositing effects e.g. transparency will be lost. In this case, install and run a separate Composite manager to provide the effects such as [Xcompmgr](/index.php/Xcompmgr "Xcompmgr") or [Compton](/index.php/Compton "Compton").

### Integrate Android

KDE Connect provides several features for you:

*   Share files and URLs to/from KDE from/to any app, without wires.
*   Touchpad emulation: Use your phone screen as your computer's touchpad.
*   Notifications sync (4.3+): Read your Android notifications from the desktop.
*   Shared clipboard: copy and paste between your phone and your computer.
*   Multimedia remote control: Use your phone as a remote for Linux media players.
*   WiFi connection: no usb wire or bluetooth needed.
*   RSA Encryption: your information is safe.

You will need to install KDE Connect both on your computer and on your Android. For PC side, install [kdeconnect](https://www.archlinux.org/packages/?name=kdeconnect) package. For Android side, install `KDE Connect` from [Google Play](https://play.google.com/store/apps/details?id=org.kde.kdeconnect_tp) or from [F-Droid](https://f-droid.org/repository/browse/?fdid=org.kde.kdeconnect_tp).

### Configure KWin to use OpenGL ES

Set environment variable `KWIN_COMPOSE` to 'O2ES' to force the OpenGL ES backend. Please note that OpenGL ES is not supported by all drivers.

### Speed up application startup

User Rob described a "[magic trick](http://kdemonkey.blogspot.nl/2008/04/magic-trick.html)" on his blog to improve application start-up time by 50-150ms. To enable it, create this folder in your home:

```
$ mkdir ~/.compose-cache/

```

It can produce freezes under heavy io. To avoid this, also do:

```
$ ln -sfv /run/user/$UID/ /home/$USER/.compose-cache

```

**Note:** For those curious about what is going on here, this enables an optimization which Lubos (of general KDE speediness fame) came up with some time ago and was then rewritten and integrated into libx11\. Ordinarily, on startup, applications read input method information from `/usr/share/X11/locale/*your locale*/Compose`. This file is quite long (>5000 lines for the en_US.UTF-8 one) and takes some time to process. libX11 can create a cache of the parsed information which is much quicker to read subsequently, but it will only re-use an existing cache or create a new one in `~/.compose-cache` if the directory already exists.

### Configuring monitor resolution / multiple monitors

To enable display resolution management and multiple monitors in Plasma 5, install [kscreen](https://www.archlinux.org/packages/?name=kscreen). This adds the additional options to System Settings/Display and Monitor.

### Open application launcher with Super key (Windows key)

**Note:** Since plasma 5.8 release, this workaround is no longer needed. Pressing `Super` key launches kickstart application launcher as if `Alt+F1` keys are pressed.

Install and start [ksuperkey](https://aur.archlinux.org/packages/ksuperkey/). Now assign `Alt+F1` as hot key. The `Super` key will now open the application launcher. You can add ksuperkey to the autostart if you don't want to start it manually.

### Enabling touchpad tap to click on plasma wayland session

Currently, it's not possible to [configure tap to click via systemsettings](https://bugs.kde.org/show_bug.cgi?id=363109) on plasma wayland session. [A workaround](https://bugs.kde.org/show_bug.cgi?id=366605#c4) is provided to configure tap to click on plasma wayland session via dbus.

Here are simplified steps to get touchpad tap to click enabled on plasma wayland session.

Identify on which libinput recognizes the touchpad device.

 `# libinput-list-devices` 
```
Device:           ETPS/2 Elantech Touchpad
Kernel:           /dev/input/event14
Group:            7
Seat:             seat0, default
Size:             78.28x38.78mm
Capabilities:     pointer
Tap-to-click:     disabled
Tap-and-drag:     enabled
Tap drag lock:    disabled
Left-handed:      disabled
Nat.scrolling:    disabled
Middle emulation: n/a
Calibration:      n/a
Scroll methods:   *two-finger edge
Click methods:    none
Disable-w-typing: enabled
Accel profiles:   none
Rotation:         n/a

```

In this case, the touchpad is identified as `event14`

Check whether KDE Dbus recognizes the touchpad. Replace `event14` with the touchpad identifier found from `libinput-list-devices`.

 `$ qdbus org.kde.KWin.InputDevice /org/kde/KWin/InputDevice/event14 org.freedesktop.DBus.Properties.Get org.kde.KWin.InputDevice name` 
```
ETPS/2 Elantech Touchpad

```

Check the current value of `tapToClick`.

 `$ qdbus org.kde.KWin.InputDevice /org/kde/KWin/InputDevice/event14 org.freedesktop.DBus.Properties.Get org.kde.KWin.InputDevice tapToClick` 
```
false

```

Now set the `tapToClick` value to `true`.

```
$ qdbus org.kde.KWin.InputDevice /org/kde/KWin/InputDevice/event14 org.freedesktop.DBus.Properties.Set org.kde.KWin.InputDevice tapToClick true

```

Confirm that `tapToClick` value is `true`.

 `$ qdbus org.kde.KWin.InputDevice /org/kde/KWin/InputDevice/event14 org.freedesktop.DBus.Properties.Get org.kde.KWin.InputDevice tapToClick` 
```
true

```

After these steps performed, tap to click should work as expected.

## Troubleshooting

### Configuration related

Many problems in KDE are related to configuration.

#### Plasma desktop behaves strangely

Plasma problems are usually caused by unstable **Plasma widgets** (colloquially called *plasmoids*) or **Plasma themes**. First, find which was the last widget or theme you had installed and disable it or uninstall it.

So, if your desktop suddenly exhibits "locking up", this is likely caused by a faulty installed widget. If you cannot remember which widget you installed before the problem began (sometimes it can be an irregular problem), try to track it down by removing each widget until the problem ceases. Then you can uninstall the widget, and file a bug report (bugs.kde.org) **only if it is an official widget**. If it is not, it is recommended you find the entry on kde-look.org and inform the developer of that widget about the problem (detailing steps to reproduce, etc).

If you cannot find the problem, but you do not want *all* the settings to be lost, navigate to `~/.config`:

```
$ for j in plasma*; do mv -- "$j" "${j%}.bak"; done

```

This command will **rename all Plasma related configs** to *.bak (e.g. `plasmarc.bak`) of your user and when you will relogin into Plasma, you will have the **default** settings back. To undo that action, remove the .bak file extension. If you already have *.bak files, rename, move, or delete them first. It is highly recommended that you create regular backups anyway. See [Synchronization and backup programs](/index.php/Synchronization_and_backup_programs "Synchronization and backup programs") for a list of possible solutions.

#### Clean cache to resolve upgrade problems

The [problem](https://bbs.archlinux.org/viewtopic.php?id=135301) may be caused by old cache. Sometimes after an upgrade, the old cache might introduce strange, hard to debug behaviour such as unkillable shells, hangs when changing various settings and several other problems such as ark being unable to unrar or unzip or amarok not recognizing any of your music. This solution can also resolve problems with KDE and Qt programmes looking bad following upgrade.

Rebuild your cache with the following commands:

```
$ rm ~/.config/Trolltech.conf
$ kbuildsycoca4 --noincremental

```

Hopefully, your problems are now fixed.

### Clean akonadi configuration to fix KMail

First, make sure that KMail is not running. Then backup configuration:

```
$ mv ~/.local/share/akonadi ~/.local/share/akonadi-old
$ mv ~/.config/akonadi ~/.config/akonadi-old

```

Start *SystemSettings > Personal* and remove all the resources. Go back to Dolphin and remove the original `~/.local/share/akonadi` and `~/.config/akonadi` - the copies you made ensure that you can back-track if necessary.

Now go back to the System Settings page and carefully add the necessary resources. You should see the resource reading in your mail folders. Then start Kontact/KMail to see if it work properly.

### Fix empty IMAP inbox

For some IMAP accounts, kmail will show the inbox as a container with all other folders of this account inside. Kmail does not show messages in the inbox container but in all other subfolders [[9]](https://bugs.kde.org/show_bug.cgi?id=284172). To solve this problem simply disable the server side subscribition in the kmail account settings.

### Getting current state of KWin for support and debug purposes

This command prints out a wonderful summary of the current state of KWin including used options, used compositing backend and relevant OpenGL driver capabilities. See more on [Martin's blog](http://blog.martin-graesslin.com/blog/2012/03/on-getting-help-for-kwin-and-helping-kwin/).

```
$ qdbus org.kde.KWin /KWin supportInformation

```

### KDE and Qt programs look bad when in a different window manager

If you are using KDE or Qt programs but not in a full Plasma session (specifically, you did not run `startkde`), then as of Plasma 4.6.1 you will need to tell Qt how to find KDE's styles (Oxygen, QtCurve etc.)

You just need to set the environment variable `QT_PLUGIN_PATH`. E.g. put:

```
export QT_PLUGIN_PATH=$HOME/.kde4/lib/kde4/plugins/:/usr/lib/kde4/plugins/

```

into your `/etc/profile` (or `~/.profile` if you do not have root access). `qtconfig-qt4` should then be able to find your KDE styles and everything should look nice again!

Alternatively, you can symlink the Qt styles directory to the KDE styles one:

```
# ln -s /usr/lib/kde4/plugins/styles/ /usr/lib/qt4/pluginlib32-libdbusmenu-glibs/styles

```

Under Gnome you can try to install the package libgnomeui.

### KF5/Qt5 applications don't display icons in i3/fvwm/awesome

See [Qt#Configuration of Qt5 apps under environments other than KDE](/index.php/Qt#Configuration_of_Qt5_apps_under_environments_other_than_KDE "Qt").

### Graphical related problems

#### Plasma keeps crashing with legacy Nvidia

This is caused by a [bug in Plasma](https://bugs.kde.org/show_bug.cgi?id=348753) when using the Nvidia-304xx driver. Rather than disabling compositing, create a file `kwin.sh` in `~/.config/plasma-workspace/env/` with the following contents:

```
#!/bin/sh
export KWIN_EXPLICIT_SYNC=0

```

Then go to *system-settings > Startup and Shutdown > Autostart* and *Check/Add* the script as a pre-KDE startup file.

#### Applications don't refresh properly

If you use 3D-accelerated composition with [Intel](/index.php/Intel "Intel"), you might find that the Plasma panel and other applications don't refresh properly (stay frozen). Some Intel drivers have [problems with EGL](https://bugzilla.redhat.com/show_bug.cgi?id=1259475). Go to System Settings under *Display and Monitor* -> *Compositor*. Set *OpenGL interface* to OpenGL 3.1\. If that does not work, see [Intel graphics#SNA issues](/index.php/Intel_graphics#SNA_issues "Intel graphics") for alternative solutions.

#### Low 2D desktop performance (or) artifacts appear when on 2D

##### GPU driver problem

Make sure you have the proper driver for your card installed, so that your desktop is at least 2D accelerated. Follow these articles for more information: [ATI](/index.php/ATI "ATI"), [NVIDIA](/index.php/NVIDIA "NVIDIA"), [Intel](/index.php/Intel "Intel") for more information, in order to make sure that everything is all right. The open-source ATI and Intel drivers and the proprietary (binary) Nvidia driver should theoretically provide the best 2D and 3D acceleration.

##### The Raster engine workaround

If this does not solve your problems, your driver may not provide a good **XRender** acceleration which the current Qt painter engine relies on by default.

You can change the painter engine to software based only by invoking the application with the `-graphicssystem raster` command line. This rendering engine can be set as the default one by recompiling Qt with the same as configure option, `-graphicssystem raster`.

The raster paint engine enables the CPU to do the majority of the painting, as opposed to the GPU. You may get better performance, depending on your system. This is basically a work-around for the terrible Linux driver stack, since the CPU should obviously not be doing graphical computations since it is designed for fewer threads of greater complexity, as opposed to the GPU which is many threads but lesser computational strength. So, only use Raster engine if you are having problems or your GPU is much slower than you CPU, otherwise is better to use XRender.

Since Qt 4.7+, recompiling Qt is not needed. Simply export `QT_GRAPHICSSYSTEM=raster`, or `opengl`, or `native` (for the default). Raster depends on the CPU, OpenGL depends on the GPU and high driver support, and Native is just using the X11 rendering (mixture, usually).

**The best and automatic way to do that** is to install [kcm-qt-graphicssystem](https://aur.archlinux.org/packages/kcm-qt-graphicssystem/) from AUR and configure this particular Qt setting through *System Settings > Qt Graphics System*.

For more information, consult this [KDE Developer blog entry](http://apachelog.wordpress.com/2010/09/05/qt-graphics-system-kcm/) and/or this [Qt Developer blog entry](https://web.archive.org/web/20100430183745/http://labs.trolltech.com/blogs/2009/12/18/qt-graphics-and-performance-the-raster-engine).

#### Low 3D desktop performance

KDE begins with desktop effects enabled. Older cards may be insufficient for 3D desktop acceleration. You can disable desktop effects in *System Settings > Desktop Effects* and you can toggle desktop effects with `Alt+Shift+F12`.

**Note:** You may encounter such problems with 3D desktop performance even when using a more powerful graphics card. Make sure the GPU driver and it's components has been successfully installed.

#### Desktop compositing is disabled on my system with a modern Nvidia GPU

Sometimes, KWin may have settings in its configuration file (`kwinrc`) that *may* cause a problem on re-activating the 3D desktop `OpenGL` compositing. That could be caused randomly (for example, due to a sudden Xorg crash or restart, and it gets corrupted), so, in case that happens, delete your `~/.kde4/share/config/kwinrc` file and relogin. The KWin settings will turn to the KDE default ones and the problem should be probably gone.

#### Flickering in fullscreen when compositing is enabled

As of KDE SC 4.6.0, there is an option in *Sytem Settings > Desktop Effect > Advanced > Suspend desktop effects for fullscreen windows*. Uncheck it would tell kwin to disable unredirect fullscren.

#### Display settings lost on reboot (multiple monitors)

There is a [bug](https://bugs.kde.org/show_bug.cgi?id=346961) in kscreen that makes it forget dual screen settings after reboot with certain displays. A possible workaround is to uninstall [kscreen](https://www.archlinux.org/packages/?name=kscreen) and specify your screen setup in a xorg.conf file instead:

*   See [Multihead#RandR](/index.php/Multihead#RandR "Multihead") for using the [RandR](https://en.wikipedia.org/wiki/RandR "wikipedia:RandR") [X Window System](https://en.wikipedia.org/wiki/X_Window_System "wikipedia:X Window System") extension.
*   For Nouveau you can use the template at [Nouveau#Dual Head](/index.php/Nouveau#Dual_Head "Nouveau"), just edit it to suit your setup.
*   For the proprietary nvidia driver you can use the [nvidia-settings](/index.php/NVIDIA#Using_NVIDIA_Settings "NVIDIA") utility as root to write the config file.

### Sound problems under KDE

#### ALSA related problems

**Note:** First make sure you have [alsa-lib](https://www.archlinux.org/packages/?name=alsa-lib) and [alsa-utils](https://www.archlinux.org/packages/?name=alsa-utils) installed.

##### "Falling back to default" messages when trying to listen to any sound in KDE

When you encounter such messages:

```
The audio playback device *name_of_the_sound_device* does not work.
Falling back to default

```

Go to *System Settings > Multimedia > Phonon* and set the device named `default` above all the other devices in each box you see.

##### MP3 files cannot be played when using the GStreamer Phonon backend

This can be solved by installing the GStreamer libav plugin (package [gst-libav](https://www.archlinux.org/packages/?name=gst-libav)). If you still encounter problems, you can try changing the Phonon backend used by installing another such as [phonon-qt4-vlc](https://www.archlinux.org/packages/?name=phonon-qt4-vlc) or [phonon-qt5-vlc](https://www.archlinux.org/packages/?name=phonon-qt5-vlc). Then, make sure the backend is preferred via *System Settings > Multimedia > Phonon > Backend (tab)*.

### Inotify folder watch limit

If you get the following error:

```
KDE Baloo Filewatch service reached the inotify folder watch limit. File changes may be ignored.

```

Then you will need to increase the inotify folder watch limit:

```
# echo 10000 > /proc/sys/fs/inotify/max_user_watches

```

To make changes permanent, create `/etc/sysctl.d/90-inotify.conf` with

```
#increase inotify watch limit
fs.inotify.max_user_watches = 10000

```

### Freezes when using Automount on a NFS volume

Using [Fstab#Automount with systemd](/index.php/Fstab#Automount_with_systemd "Fstab") on a [NFS](/index.php/NFS "NFS") volume may cause freezes, see [bug report upstream](https://bugs.kde.org/show_bug.cgi?id=354137).

### Locale warning when installing packages in Konsole

```
 mandb: can't set the locale; make sure $lc_* and $lang are correct

```

By default, Konsole sets $LANG to en_US.US-ASCII. If you haven't generated that locale, then mandb can't use it. In your Konsole profile settings, click "Environment" and then add a line for LANG=en_US.UTF-8 or whatever your locale should be.

### Multi-monitor issues

The current release of KDE Plasma has several issues with multi-monitor setups, which can make Plasma unusable. See [KDE Bug 356225](https://bugs.kde.org/show_bug.cgi?id=356225).

These bugs have been resolved in the upstream/git KDE Plasma builds, which can be installed from [plasma-desktop-git](https://aur.archlinux.org/packages/plasma-desktop-git/) or [plasma-git-meta](https://aur.archlinux.org/packages/plasma-git-meta/) - bear in mind that all packages will conflict with current versions - it is recommended to [remove](/index.php/Remove "Remove") them first.

## Unstable releases

See [Official repositories#kde-unstable](/index.php/Official_repositories#kde-unstable "Official repositories")

## See also

*   [KDE homepage](http://www.kde.org)
*   [KDE bug tracker](https://bugs.kde.org)
*   [KDE Projects](https://projects.kde.org)
*   [Martin Graesslin's blog](http://blog.martin-graesslin.com/blog/kategorien/kde/)