# KDE

Related articles

*   [Desktop environment](/index.php/Desktop_environment "Desktop environment")
*   [Display manager](/index.php/Display_manager "Display manager")
*   [Dolphin](/index.php/Dolphin "Dolphin")
*   [Window manager](/index.php/Window_manager "Window manager")
*   [Qt](/index.php/Qt "Qt")
*   [KDM](/index.php/KDM "KDM")
*   [KDevelop 4](/index.php/KDevelop_4 "KDevelop 4")
*   [Trinity](/index.php/Trinity "Trinity")
*   [Uniform Look for Qt and GTK Applications](/index.php/Uniform_Look_for_Qt_and_GTK_Applications "Uniform Look for Qt and GTK Applications")

KDE is a software project currently comprising of a [desktop environment](/index.php/Desktop_environment "Desktop environment") known as Plasma (or Plasma Workspaces), a collection of libraries and frameworks (KDE Frameworks) and several applications (KDE Applications) as well. KDE upstream has a well maintained [UserBase wiki](http://userbase.kde.org/). Detailed information about most KDE applications can be found there.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Plasma Desktop](#Plasma_Desktop)
    *   [1.2 Upgrading from Plasma 4 to 5](#Upgrading_from_Plasma_4_to_5)
    *   [1.3 KDE applications and language packs](#KDE_applications_and_language_packs)
*   [2 Starting Plasma](#Starting_Plasma)
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
    *   [3.6 Monitoring changes on local files and directories](#Monitoring_changes_on_local_files_and_directories)
    *   [3.7 Autostarting applications](#Autostarting_applications)
*   [4 System administration](#System_administration)
    *   [4.1 Terminate Xorg server through KDE System Settings](#Terminate_Xorg_server_through_KDE_System_Settings)
    *   [4.2 KCM](#KCM)
*   [5 Desktop search](#Desktop_search)
    *   [5.1 Baloo](#Baloo)
        *   [5.1.1 Using and configuring Baloo](#Using_and_configuring_Baloo)
        *   [5.1.2 How do I index a removable device?](#How_do_I_index_a_removable_device.3F)
    *   [5.2 Web browsers](#Web_browsers)
        *   [5.2.1 Konqueror and Rekonq](#Konqueror_and_Rekonq)
        *   [5.2.2 Firefox](#Firefox)
        *   [5.2.3 Qupzilla](#Qupzilla)
*   [6 PIM](#PIM)
    *   [6.1 Akonadi](#Akonadi)
        *   [6.1.1 Disabling Akonadi](#Disabling_Akonadi)
        *   [6.1.2 Database configuration](#Database_configuration)
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
*   [10 Troubleshooting](#Troubleshooting)
    *   [10.1 Graphics card related](#Graphics_card_related)
        *   [10.1.1 Intel](#Intel)
        *   [10.1.2 Plasma keeps crashing with legacy Nvidia](#Plasma_keeps_crashing_with_legacy_Nvidia)
    *   [10.2 Configuration related](#Configuration_related)
        *   [10.2.1 Plasma desktop behaves strangely](#Plasma_desktop_behaves_strangely)
        *   [10.2.2 Clean cache to resolve upgrade problems](#Clean_cache_to_resolve_upgrade_problems)
    *   [10.3 Clean akonadi configuration to fix KMail](#Clean_akonadi_configuration_to_fix_KMail)
    *   [10.4 Getting current state of KWin for support and debug purposes](#Getting_current_state_of_KWin_for_support_and_debug_purposes)
    *   [10.5 KDE and Qt programs look bad when in a different window manager](#KDE_and_Qt_programs_look_bad_when_in_a_different_window_manager)
    *   [10.6 KF5/Qt5 applications don't display icons in i3/fvwm/awesome](#KF5.2FQt5_applications_don.27t_display_icons_in_i3.2Ffvwm.2Fawesome)
    *   [10.7 Graphical related problems](#Graphical_related_problems)
        *   [10.7.1 Low 2D desktop performance (or) artifacts appear when on 2D](#Low_2D_desktop_performance_.28or.29_artifacts_appear_when_on_2D)
            *   [10.7.1.1 GPU driver problem](#GPU_driver_problem)
            *   [10.7.1.2 The Raster engine workaround](#The_Raster_engine_workaround)
        *   [10.7.2 Low 3D desktop performance](#Low_3D_desktop_performance)
        *   [10.7.3 Desktop compositing is disabled on my system with a modern Nvidia GPU](#Desktop_compositing_is_disabled_on_my_system_with_a_modern_Nvidia_GPU)
        *   [10.7.4 Flickering in fullscreen when compositing is enabled](#Flickering_in_fullscreen_when_compositing_is_enabled)
        *   [10.7.5 Display settings lost on reboot (multiple monitors)](#Display_settings_lost_on_reboot_.28multiple_monitors.29)
    *   [10.8 Sound problems under KDE](#Sound_problems_under_KDE)
        *   [10.8.1 ALSA related problems](#ALSA_related_problems)
            *   [10.8.1.1 "Falling back to default" messages when trying to listen to any sound in KDE](#.22Falling_back_to_default.22_messages_when_trying_to_listen_to_any_sound_in_KDE)
            *   [10.8.1.2 MP3 files cannot be played when using the GStreamer Phonon backend](#MP3_files_cannot_be_played_when_using_the_GStreamer_Phonon_backend)
    *   [10.9 Konsole does not save commands' history](#Konsole_does_not_save_commands.27_history)
    *   [10.10 Inotify folder watch limit](#Inotify_folder_watch_limit)
    *   [10.11 Freezes when using Automount on a NFS volume](#Freezes_when_using_Automount_on_a_NFS_volume)
*   [11 Unstable releases](#Unstable_releases)
*   [12 Bugs](#Bugs)
*   [13 See also](#See_also)

## Installation

### Plasma Desktop

**Note:**

*   Plasma 5 is not co-installable with Plasma 4.
*   The Plasma 4 desktop is unmaintained since August 2015.[[1]](https://www.kde.org/announcements/announce-applications-15.08.0.php) It is no longer in the official repositories since December 2015.[[2]](https://www.archlinux.org/news/dropping-plasma-4/)
*   [KDM](/index.php/KDM "KDM") is no longer available for Plasma 5\. KDE upstream [recommends](http://blog.davidedmundson.co.uk/blog/display_managers_finale) using the [SDDM](/index.php/SDDM "SDDM") display manager as it provides integration with the Plasma 5 theme.

Before installing Plasma, make sure you have a working [Xorg](/index.php/Xorg "Xorg") installation on your system.

Install the [plasma-meta](https://www.archlinux.org/packages/?name=plasma-meta) meta-package or the [plasma](https://www.archlinux.org/groups/x86_64/plasma/) group. For differences between [plasma-meta](https://www.archlinux.org/packages/?name=plasma-meta) and [plasma](https://www.archlinux.org/groups/x86_64/plasma/) reference [Creating packages#Meta packages and groups](/index.php/Creating_packages#Meta_packages_and_groups "Creating packages"). Alternatively, for a more minimal Plasma installation, install the [plasma-desktop](https://www.archlinux.org/packages/?name=plasma-desktop) package.

### Upgrading from Plasma 4 to 5

1.  Isolate `multi-user.target` `# systemctl isolate multi-user.target` 
2.  If you use KDM as display manager, disable it `# systemctl disable kdm` 
3.  [Uninstall](/index.php/Pacman "Pacman") the kdebase-workspace package `# pacman -Rc kdebase-workspace` 
4.  [Install](/index.php/Install "Install") the [plasma-meta](https://www.archlinux.org/packages/?name=plasma-meta) package or the [plasma](https://www.archlinux.org/groups/x86_64/plasma/) group.
5.  Enable [SDDM](/index.php/SDDM "SDDM") `# systemctl enable sddm` or install and enable any other [display manager](/index.php/Display_manager "Display manager").
6.  Reboot or simply run `# systemctl start sddm` 

**Note:** The Plasma 4 configuration is not automatically migrated to Plasma 5, so you will have to configure your desktop from scratch.

### KDE applications and language packs

To install the full set of KDE Applications, install the [kde-applications](https://www.archlinux.org/groups/x86_64/kde-applications/) group or the [kde-applications-meta](https://www.archlinux.org/packages/?name=kde-applications-meta) meta-packages to install specific modules. Note that this will only install applications, it will not install any version of the Plasma Desktop.

If you need language files, install `kde-l10n-**yourlanguagehere**` (e.g. [kde-l10n-de](https://www.archlinux.org/packages/?name=kde-l10n-de) for the German language). For a full list of available languages see [this link](https://www.archlinux.org/packages/extra/any/kde-l10n/).

## Starting Plasma

**Tip:** To better integrate SDDM with Plasma, it is recommended to edit `/etc/sddm.conf` to use the breeze theme. Refer to [SDDM#Theme settings](/index.php/SDDM#Theme_settings "SDDM") for instructions.

**Note:** The Plasma 4 configuration is not automatically migrated to Plasma 5, so you will have to configure your desktop from scratch.

To launch a Plasma 5 session, choose _Plasma_ in your [display manager](/index.php/Display_manager "Display manager") menu.

Alternatively, to start Plasma with _startx_, append `exec startkde` to your `.xinitrc` file. If you want to start Xorg at login, please see [Start X at login](/index.php/Start_X_at_login "Start X at login").

## Configuration

Most settings for KDE applications are stored in `~/.config`, but some older applications may use `~/.kde4`. However, configuring KDE is primarily done through the **System Settings** application. It can be started from a terminal by executing _systemsettings5_.

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

The recommended theme for a pleasant appearance in GTK+ applications is [breeze-gtk](https://www.archlinux.org/packages/?name=breeze-gtk) or [gnome-breeze-git](https://aur.archlinux.org/packages/gnome-breeze-git/)<sup><small>AUR</small></sup>, a GTK+ theme designed to mimic the appearance of Plasma 5 Breeze. Install [kde-gtk-config](https://www.archlinux.org/packages/?name=kde-gtk-config) and select the installed GTK-theme for GTK2/GTK3-Theme in _System Settings > Application Style > GNOME Application Style_.

##### Widgets

Plasmoids are little scripted (plasmoid scripts) or coded (plasmoid binaries) KDE applications designed to enhance the functionality of your desktop.

Plasmoid binaries can be installed using PKGBUILDs from [AUR](https://aur.archlinux.org/packages.php?O=0&K=plasmoid&do_Search=Go&PP=25&SO=d&SB=v), or you can write your own PKGBUILD.

The easiest way to install plasmoid scripts is by right-clicking onto a panel or the desktop and choosing _Add Widgets > Get new Widgets > Download Widgets_.

This will present a nice frontend for [kde-look.org](http://www.kde-look.org/) that allows you to install, uninstall, or update third-party plasmoid scripts with literally just one click.

Most plasmoids are not created officially by KDE developers. You can also try installing Mac OS X widgets, Microsoft Windows Vista/7 widgets, Google Widgets, and even SuperKaramba widgets.

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

The script can be run on login with _Add Script_ in _Autostart_:

```
$ kcmshell5 autostart

```

#### Window decorations

[Window decorations](http://kde-look.org/index.php?xcontentmode=75) can be changed in _System Settings > Workspace Appearance > Window Decorations_.

There you can also directly download and install more themes with one click, and some are available in the [AUR](https://aur.archlinux.org/packages.php?O=0&K=kdestyle&do_Search=Go&PP=25&SO=d&SB=v).

#### Icon themes

Icon-themes can be installed and changed on _System Settings > Icons_.

**Note:** [GNOME](/index.php/GNOME "GNOME") and KDE4 installed icon-themes may not be (fully) compatible with Plasma. It's recommended to install Plasma compatible icon-themes instead.

#### Fonts

##### Fonts in a Plasma session look poor

Try installing the [ttf-dejavu](https://www.archlinux.org/packages/?name=ttf-dejavu) and [ttf-liberation](https://www.archlinux.org/packages/?name=ttf-liberation) packages.

After the installation, be sure to log out and back in. You should not have to modify anything in _System Settings > Fonts_.

If you have personally set up how your [Fonts](/index.php/Fonts "Fonts") render, be aware that System Settings may alter their appearance. When you go _System Settings > Appearance > Fonts_ System Settings will likely alter your font configuration file (`fonts.conf`).

There is no way to prevent this, but, if you set the values to match your `fonts.conf` file, the expected font rendering will return (it will require you to restart your application or in a few cases restart your desktop). Note that Gnome's Font Preferences also does this.

##### Fonts are huge or seem disproportional

Try to force font DPI to **96** in _System Settings > Application Appearance > Fonts_.

If that does not work, try setting the DPI directly in your Xorg configuration as documented [here](/index.php/Xorg#Setting_DPI_manually "Xorg").

#### Space efficiency

The Plasma Netbook shell has been dropped from Plasma 5, see the following [KDE forum post](https://forum.kde.org/viewtopic.php?f=289&t=126631&p=335947&hilit=plasma+netbook#p335899) However, you can achieve something similar by editing the file `~/.config/kwinrc` adding `BorderlessMaximizedWindows=true` in the `[Windows]` section.

### Printing

**Tip:** Use the [CUPS](/index.php/CUPS "CUPS") web interface for faster configuration. Printers configured in this way can be used in KDE applications.

You can also configure printers in _System Settings > Printer Configuration_. To use this method, you must first install [print-manager](https://www.archlinux.org/packages/?name=print-manager) and [cups](https://www.archlinux.org/packages/?name=cups).

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

Adding `lpadmin` to `/etc/group` and then to the `SystemGroup` directive in `/etc/cups/cups-files.conf` allows anyone in the `lpadmin` group to configure printers. Do _not_ add the `lp` group to the `SystemGroup` directive, or printing will fail.

```
# groupadd -g107 lpadmin

```

 `/etc/cups/cups-files.conf` 

```
# Administrator user group...
SystemGroup sys root lpadmin
```

**Tip:** Read [CUPS#Administration](/index.php/CUPS#Administration "CUPS") to get more details on how to configure CUPS.

### Samba/Windows support

If you want to have access to Windows services, install [Samba](/index.php/Samba "Samba") (package [samba](https://www.archlinux.org/packages/?name=samba)).

The Dolphin share functionality requires usershares, which the stock smb.conf does not have enabled. Instructions to add them are in [Samba#Creating usershare path](/index.php/Samba#Creating_usershare_path "Samba"), after which sharing in Dolphin should work out of the box after restarting Samba.

### KDE Desktop activities

KDE Desktop Activities are Plasma-based virtual-desktop-like sets of Plasma Widgets where you can independently configure widgets as if you have more than one screen or desktop.

On your desktop, click the Cashew Plasmoid and, on the pop-up window, press "Activities".

A plasma bar presenting you the current existing Plasma Desktop Activities will appear at the bottom of the screen. You can navigate between them by pressing the correspondent icons.

### Power saving

Plasma has an integrated power saving service called "**Powerdevil Power Management**" that may adjust the power saving profile of the system and/or the brightness of the screen (if supported).

### Monitoring changes on local files and directories

KDE now uses **inotify** directly from the kernel with **kdirwatch** (included in kdelibs), so Gamin or FAM are no longer needed. You may want to install this [kdirwatch](https://aur.archlinux.org/packages/kdirwatch/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/kdirwatch)]</sup> from AUR which is a GUI frontend for kdirwatch.

### Autostarting applications

Plasma can autostart applications and run scripts on startup and shutdown. To autostart an application, start `systemsettings` and navigate to _Startup and Shutdown_ -> _Autostart_ and add the program or shell script of your choice. Note that programs can be autostarted on login only, whilst shell scripts can also be run on shutdown or even before Plasma itself starts. For applications, a `.desktop` file will be created in the `~/.config/autostart` directory. For shell scripts, a symlink will be created in one the following directories:

*   `~/.config/autostart-scripts` - for starting at login.
*   `~/.config/plasma-workspace/shutdown` - for starting on shutdown.
*   `~/.config/plasma-workspace/env` - for starting prior to login.

## System administration

### Terminate Xorg server through KDE System Settings

Navigate to the submenu _System Settings > Input Devices > Keyboard > Advanced (tab) > "Key Sequence to kill the X server"_ and ensure that the checkbox is ticked.

### KCM

KCM stands for **KC**onfig **M**odule. KCMs can help you configure your system by providing interfaces in System Settings, or through the command line with _kcmshell5_.

**Configuration for look and feel of GTK applications.**

*   [kde-gtk-config](https://www.archlinux.org/packages/?name=kde-gtk-config)
*   [kcm-gtk](https://aur.archlinux.org/packages/kcm-gtk/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/kcm-gtk)]</sup>
*   [kcm-qt-graphicssystem](https://aur.archlinux.org/packages/kcm-qt-graphicssystem/)<sup><small>AUR</small></sup>

**Configuration for the GRUB bootloader.**

*   [grub2-editor](https://aur.archlinux.org/packages/grub2-editor/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/grub2-editor)]</sup>

**Configuration for the [Uncomplicated Firewall](/index.php/Uncomplicated_Firewall "Uncomplicated Firewall") (UFW)**

*   [kcm-ufw](https://aur.archlinux.org/packages/kcm-ufw/)<sup><small>AUR</small></sup>

**Configuration for [PolicyKit](/index.php/PolicyKit "PolicyKit")**

*   [kcm-polkit-kde-git](https://aur.archlinux.org/packages/kcm-polkit-kde-git/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/kcm-polkit-kde-git)]</sup>

**Configuration for Wacom tablets**

*   [kcm-wacomtablet](https://aur.archlinux.org/packages/kcm-wacomtablet/)<sup><small>AUR</small></sup>

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

More advanced configuration options are available through [kcm_baloo_advanced](https://aur.archlinux.org/packages/kcm_baloo_advanced/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/kcm_baloo_advanced)]</sup>.

#### How do I index a removable device?

By default every removable device is blacklisted. You just have to remove your device from the blacklist in the KCM panel.

### Web browsers

#### Konqueror and Rekonq

Konqueror supports two rendering engines – KHTML and QtWebKit (via the [kwebkitpart](https://www.archlinux.org/packages/?name=kwebkitpart) package) – Rekonq supports only QtWebKit. KHTML development was halted after Qt shipped WebKit but was kept for compatibility reasons. QtWebKit, in turn, has since been [deprecated](https://www.mail-archive.com/development@qt-project.org/msg18866.html) by the Qt Project and replaced by [Chromium](/index.php/Chromium "Chromium")-based Qt WebEngine which is currently not supported by either Konqueror or Rekonq.

A successor named Fiber is currently in development, which will use Chromium's engine.

#### Firefox

Firefox can be configured to better integrate with Plasma. See [Firefox KDE integration](/index.php/Firefox#KDE_integration "Firefox") for details.

#### Qupzilla

Qupzilla ([qupzilla](https://www.archlinux.org/packages/?name=qupzilla)) is a Qt web browser with Plasma integration features. Qupzilla 2.0 will use Qt WebEngine intead of WebKit.

## PIM

KDE offers its own stack for personal information management. This includes emails, contacts, calendar, etc.

### Akonadi

Akonadi is a system meant to act as a local cache for PIM data, regardless of its origin, which can be then used by other applications. This includes the user's emails, contacts, calendars, events, journals, alarms, notes, and so on.

Akonadi does not store any data by itself: the storage format depends on the nature of the data (for example, contacts may be stored in vCard format).

#### Disabling Akonadi

See this [section in the KDE userbase](http://userbase.kde.org/Akonadi#Disabling_the_Akonadi_subsystem).

#### Database configuration

Start `akonaditray` from package [kdepim-runtime](https://www.archlinux.org/packages/?name=kdepim-runtime). Right click on it and select **configure**. In the Akonadi server configure tab, you can:

*   Configuring Akonadi to use MySQL/MariaDB Server
    *   If your home directory is on a ZFS pool, you will need to create `~/.config/akonadi/mysql-local.conf` with the following contents:

```
[mysqld]
innodb_use_native_aio = 0

```

Otherwise you will get the [OS error 22](/index.php/MySQL#OS_error_22_when_running_on_ZFS "MySQL")

*   Configuring Akonadi to use PostgreSQL Server
*   Configuring Akonadi to use SQLite
    *   Edit `~/.config/akonadi/akonadiserverrc` to match the below

```
[General]
Driver=QSQLITE3

[QSQLITE3]
Name=/home/username/.local/akonadi/akonadi.db

```

## Phonon

From [Wikipedia](https://en.wikipedia.org/wiki/Phonon_(software) "wikipedia:Phonon (software)"):

	_“Phonon is the multimedia API provided by KDE and is the standard abstraction for handling multimedia streams within KDE software and also used by several Qt applications._

Phonon was originally created to allow KDE and Qt software to be independent of any single multimedia framework such as GStreamer or xine and to provide a stable API for a major version's lifetime.”

**Phonon** is being widely used within KDE, for both audio (e.g., the System notifications or KDE audio apps) and video (e.g., the Dolphin video thumbnails).

### Which backend should I choose?

You can choose between backends based on [GStreamer](/index.php/GStreamer "GStreamer") and [VLC](/index.php/VLC "VLC") – each available in versions for Qt4 applications and Qt5 applications ([phonon-qt4-gstreamer](https://www.archlinux.org/packages/?name=phonon-qt4-gstreamer), [phonon-qt5-gstreamer](https://www.archlinux.org/packages/?name=phonon-qt5-gstreamer) – [phonon-qt4-vlc](https://www.archlinux.org/packages/?name=phonon-qt4-vlc), [phonon-qt5-vlc](https://www.archlinux.org/packages/?name=phonon-qt5-vlc)).

[Upstream prefers VLC](https://www.phoronix.com/scan.php?page=news_item&px=MTUwNDM) but prominent Linux distributions (Kubuntu and Fedora-KDE for example) prefer GStreamer because that allows them to easily leave out patented MPEG codecs from the default installation. Both backends have a slightly different [features set.](http://community.kde.org/Phonon/FeatureMatrix)

In the past other backends were developed as well but are no longer maintained and their AUR packages have been deleted.

**Note:**

*   Multiple backends can be installed at once and prioritized at _System Settings > Multimedia > Phonon > Backend_. For Plasma 5 this would be _System Settings > Multimedia > Backend_.
*   According to the [KDE forums](https://forum.kde.org/viewtopic.php?f=250&t=126476&p=335080), the VLC backend lacks support for [ReplayGain](https://en.wikipedia.org/wiki/ReplayGain "wikipedia:ReplayGain").

## Useful applications

The official set of KDE applications may be found [here](http://www.kde.org/applications/).

### Yakuake

[Yakuake](/index.php/Yakuake "Yakuake") provides a Quake-like terminal emulator whose visibility is toggled by the F12 key. It also has support for multiple tabs. Yakuake is available in the package [yakuake](https://www.archlinux.org/packages/?name=yakuake).

### KDE Telepathy

[KDE Telepathy](http://community.kde.org/KTp) is a project with the goal to closely integrate Instant Messaging with the KDE desktop. It utilizes the Telepathy framework as a backend and is intended to replace Kopete.

To install all Telepathy protocols, install the [telepathy](https://www.archlinux.org/groups/x86_64/telepathy/) group. To use the KDE Telepathy client, install the [telepathy-kde-meta](https://www.archlinux.org/packages/?name=telepathy-kde-meta) package that includes all the packages contained in the [telepathy-kde](https://www.archlinux.org/groups/x86_64/telepathy-kde/) group.

#### Use Telegram with KDE Telepathy

Telegram protocol is available using [telepathy-haze](https://www.archlinux.org/packages/?name=telepathy-haze), installing [telegram-purple](https://aur.archlinux.org/packages/telegram-purple/)<sup><small>AUR</small></sup> or [telegram-purple-git](https://aur.archlinux.org/packages/telegram-purple-git/)<sup><small>AUR</small></sup> and [telepathy-morse-git](https://aur.archlinux.org/packages/telepathy-morse-git/)<sup><small>AUR</small></sup>. The username is the Telegram account telephone number (complete with the national prefix '+xx', e.g. '+49' for Germany). The configuration through the GUI may be tricky: if the phone number is not accepted when configuring a new account in the KDE Telepathy client (with an error message complaining about an invalid parameter which prevents the account creation), insert it between single quotes and then remove the quotes manually from the configuration file (`~/.local/share/telepathy/mission-control/accounts.cfg`) after the account creation (if the quotes are not removed after, an authentication error should rise). Note that the configuration file should be edited manually when KDE Telepathy is not running, e.g. when there is no KDE desktop session active, otherwise manual changes may be overwritten by the software.

## Tips and tricks

### Using an alternative window manager

There may be reasons you want to use another window manager than KWin, for example to work around the DRI bug that causes [black screen with PRIME](/index.php/PRIME#Black_screen_with_GL-based_compositors "PRIME").

To use an alternative [window manager](/index.php/Window_manager "Window manager") with Plasma open the _System Settings_ panel, navigate to _(Default) Applications > Window Manager > Use a different window manager_ and select the window manager you wish to use from the list.

#### KDE/Openbox session

The [openbox](https://www.archlinux.org/packages/?name=openbox) package provides a session for using KDE with [Openbox](/index.php/Openbox "Openbox"). To make use of this session, select _KDE/Openbox_ from the [display manager](/index.php/Display_manager "Display manager") menu.

For those starting the session manually, add the following line to your `.xinitrc` file:

```
exec openbox-kde-session

```

#### Compiz custom

If you need to run Compiz with custom options and switches select _Compiz custom_ and then create a script called `compiz-kde-launcher` and add to it the commands you wish to use to start Compiz. See the example below:

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

**Note:** For those curious about what is going on here, this enables an optimization which Lubos (of general KDE speediness fame) came up with some time ago and was then rewritten and integrated into libx11\. Ordinarily, on startup, applications read input method information from `/usr/share/X11/locale/_your locale_/Compose`. This file is quite long (>5000 lines for the en_US.UTF-8 one) and takes some time to process. libX11 can create a cache of the parsed information which is much quicker to read subsequently, but it will only re-use an existing cache or create a new one in `~/.compose-cache` if the directory already exists.

### Configuring monitor resolution / multiple monitors

To enable display resolution management and multiple monitors in Plasma 5, install [kscreen](https://www.archlinux.org/packages/?name=kscreen). This adds the additional options to System Settings/Display and Monitor.

### Open application launcher with Super key (Windows key)

Install and start [ksuperkey](https://www.archlinux.org/packages/?name=ksuperkey). Now assign Alt + F1 as hot key. The Super Key will now open the application launcher. You can add ksuperkey to the autostart if you don't want to start it manually.

## Troubleshooting

### Graphics card related

#### Intel

If you use 3D-accelerated composition with Intel, you might find that the Plasma panel and other applications don't refresh properly (stay frozen). Some Intel drivers have [problems with EGL](https://bugzilla.redhat.com/show_bug.cgi?id=1259475). Try to set Plasma 5's _OpenGL interface_ setting to GLX instead (in System Settings under _Display and Monitor_ -> _Compositor_. If that does not work, see [Intel graphics#SNA issues](/index.php/Intel_graphics#SNA_issues "Intel graphics") for alternative solutions.

#### Plasma keeps crashing with legacy Nvidia

This is caused by a [bug in Plasma](https://bugs.kde.org/show_bug.cgi?id=348753) when using the Nvidia-304xx driver. Rather than disabling compositing, create a file `kwin.sh` in `~/.config/plasma-workspace/env/` with the following contents:

```
#!/bin/sh
export KWIN_EXPLICIT_SYNC=0

```

Then go to _system-settings > Startup and Shutdown > Autostart_ and _Check/Add_ the script as a pre-KDE startup file.

### Configuration related

Many problems in KDE are related to configuration.

#### Plasma desktop behaves strangely

Plasma problems are usually caused by unstable **Plasma widgets** (colloquially called _plasmoids_) or **Plasma themes**. First, find which was the last widget or theme you had installed and disable it or uninstall it.

So, if your desktop suddenly exhibits "locking up", this is likely caused by a faulty installed widget. If you cannot remember which widget you installed before the problem began (sometimes it can be an irregular problem), try to track it down by removing each widget until the problem ceases. Then you can uninstall the widget, and file a bug report (bugs.kde.org) **only if it is an official widget**. If it is not, it is recommended you find the entry on kde-look.org and inform the developer of that widget about the problem (detailing steps to reproduce, etc).

If you cannot find the problem, but you do not want _all_ the settings to be lost, navigate to `~/.config`:

```
$ for j in plasma*; do mv -- "$j" "${j%}.bak"; done

```

This command will **rename all Plasma related configs** to *.bak (e.g. `plasmarc.bak`) of your user and when you will relogin into Plasma, you will have the **default** settings back. To undo that action, remove the .bak file extension. If you already have *.bak files, rename, move, or delete them first. It is highly recommended that you create regular backups anyway. See [backup programs](/index.php/Backup_programs "Backup programs") for a list of possible solutions.

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

Start _SystemSettings > Personal_ and remove all the resources. Go back to Dolphin and remove the original `~/.local/share/akonadi` and `~/.config/akonadi` - the copies you made ensure that you can back-track if necessary.

Now go back to the System Settings page and carefully add the necessary resources. You should see the resource reading in your mail folders. Then start Kontact/KMail to see if it work properly.

### Getting current state of KWin for support and debug purposes

This command prints out a wonderful summary of the current state of KWin including used options, used compositing backend and relevant OpenGL driver capabilities. See more on [Martin's blog](http://blog.martin-graesslin.com/blog/2012/03/on-getting-help-for-kwin-and-helping-kwin/).

```
$ qdbus org.kde.kwin /KWin supportInformation

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

See [Qt#Configuration of Qt apps under environments other than KDE](/index.php/Qt#Configuration_of_Qt_apps_under_environments_other_than_KDE "Qt").

### Graphical related problems

#### Low 2D desktop performance (or) artifacts appear when on 2D

##### GPU driver problem

Make sure you have the proper driver for your card installed, so that your desktop is at least 2D accelerated. Follow these articles for more information: [ATI](/index.php/ATI "ATI"), [NVIDIA](/index.php/NVIDIA "NVIDIA"), [Intel](/index.php/Intel "Intel") for more information, in order to make sure that everything is all right. The open-source ATI and Intel drivers and the proprietary (binary) Nvidia driver should theoretically provide the best 2D and 3D acceleration.

##### The Raster engine workaround

If this does not solve your problems, your driver may not provide a good **XRender** acceleration which the current Qt painter engine relies on by default.

You can change the painter engine to software based only by invoking the application with the `-graphicssystem raster` command line. This rendering engine can be set as the default one by recompiling Qt with the same as configure option, `-graphicssystem raster`.

The raster paint engine enables the CPU to do the majority of the painting, as opposed to the GPU. You may get better performance, depending on your system. This is basically a work-around for the terrible Linux driver stack, since the CPU should obviously not be doing graphical computations since it is designed for fewer threads of greater complexity, as opposed to the GPU which is many threads but lesser computational strength. So, only use Raster engine if you are having problems or your GPU is much slower than you CPU, otherwise is better to use XRender.

Since Qt 4.7+, recompiling Qt is not needed. Simply export `QT_GRAPHICSSYSTEM=raster`, or `opengl`, or `native` (for the default). Raster depends on the CPU, OpenGL depends on the GPU and high driver support, and Native is just using the X11 rendering (mixture, usually).

**The best and automatic way to do that** is to install [kcm-qt-graphicssystem](https://aur.archlinux.org/packages/kcm-qt-graphicssystem/)<sup><small>AUR</small></sup> from AUR and configure this particular Qt setting through _System Settings > Qt Graphics System_.

For more information, consult this [KDE Developer blog entry](http://apachelog.wordpress.com/2010/09/05/qt-graphics-system-kcm/) and/or this [Qt Developer blog entry](http://labs.trolltech.com/blogs/2009/12/18/qt-graphics-and-performance-the-raster-engine/).

#### Low 3D desktop performance

KDE begins with desktop effects enabled. Older cards may be insufficient for 3D desktop acceleration. You can disable desktop effects in _System Settings > Desktop Effects_ and you can toggle desktop effects with `Alt+Shift+F12`.

**Note:** You may encounter such problems with 3D desktop performance even when using a more powerful graphics card, especially the catalyst proprietary driver (`fglrx`). This driver is known for having problems with 3D acceleration. Visit [the ATI Wiki page](/index.php/ATI "ATI") for more troubleshooting.

#### Desktop compositing is disabled on my system with a modern Nvidia GPU

Sometimes, KWin may have settings in its configuration file (`kwinrc`) that _may_ cause a problem on re-activating the 3D desktop `OpenGL` compositing. That could be caused randomly (for example, due to a sudden Xorg crash or restart, and it gets corrupted), so, in case that happens, delete your `~/.kde4/share/config/kwinrc` file and relogin. The KWin settings will turn to the KDE default ones and the problem should be probably gone.

#### Flickering in fullscreen when compositing is enabled

As of KDE SC 4.6.0, there is an option in _Sytem Settings > Desktop Effect > Advanced > Suspend desktop effects for fullscreen windows_. Uncheck it would tell kwin to disable unredirect fullscren.

#### Display settings lost on reboot (multiple monitors)

There is a [bug](https://bugs.kde.org/show_bug.cgi?id=346961) in kscreen that makes it forget dual screen settings after reboot with certain displays. A possible workaround is to delete kscreen and make sure that your screen resolution is specified in a xorg.conf file:

*   For Nouveau you can use the template at [Nouveau#Dual Head](/index.php/Nouveau#Dual_Head "Nouveau"), just edit it to suit your setup.
*   For the proprietary nvidia driver you can use the [nvidia-settings](/index.php/NVIDIA#Using_NVIDIA_Settings "NVIDIA") utility as root to write the config file.

### Sound problems under KDE

#### ALSA related problems

**Note:** First make sure you have [alsa-lib](https://www.archlinux.org/packages/?name=alsa-lib) and [alsa-utils](https://www.archlinux.org/packages/?name=alsa-utils) installed.

##### "Falling back to default" messages when trying to listen to any sound in KDE

When you encounter such messages:

```
The audio playback device _name_of_the_sound_device_ does not work.
Falling back to default

```

Go to _System Settings > Multimedia > Phonon_ and set the device named `default` above all the other devices in each box you see.

##### MP3 files cannot be played when using the GStreamer Phonon backend

This can be solved by installing the GStreamer libav plugin (package [gst-libav](https://www.archlinux.org/packages/?name=gst-libav)). If you still encounter problems, you can try changing the Phonon backend used by installing another such as [phonon-qt4-vlc](https://www.archlinux.org/packages/?name=phonon-qt4-vlc) or [phonon-qt5-vlc](https://www.archlinux.org/packages/?name=phonon-qt5-vlc). Then, make sure the backend is preferred via _System Settings > Multimedia > Phonon > Backend (tab)_.

### Konsole does not save commands' history

By default console command history is saved only when you type 'exit' in console. When you close Konsole with 'x' in the corner it does not happen. To enable autosaving after every command execution:

 `~/.bashrc` 

```
shopt -s histappend
[[ "${PROMPT_COMMAND}" ]] && PROMPT_COMMAND="$PROMPT_COMMAND;history -a" || PROMPT_COMMAND="history -a"

```

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

## Unstable releases

When KDE is reaching beta or RC milestone, KDE "unstable" packages are uploaded to the _kde-unstable_ repository. They stay there until KDE is declared stable and passes to the _extra_ repository.

You can add _kde-unstable_ with:

 `/etc/pacman.conf` 

```
[kde-unstable]
Include = /etc/pacman.d/mirrorlist
```

**Warning:** Make sure to add these lines **before** the _extra_ repository. Adding the section after _extra_ will cause [pacman](/index.php/Pacman "Pacman") to prefer the older packages in the extra repository. `pacman -Syu` will not install them, and will warn that they are "too new" if installed manually. Also, some of the libraries will stay at the older versions, which may cause file conflicts and/or instability!

1.  _kde-unstable_ is based upon _testing_. Therefore, you need to enable the repositories in the following order: _kde-unstable_, _testing_, _core_, _extra_, _community-testing_, _community_.
2.  To update from a previous KDE installation, run: `# pacman -Syu` or `# pacman -S kde-unstable/kde`
3.  If you do not have KDE installed, you might have difficulties to install it by using groups (limitation of pacman)
4.  **Subscribe and read the [arch-dev-public](https://mailman.archlinux.org/pipermail/arch-dev-public/) mailing list**
5.  Make sure [you make bug reports](#Bugs) if you find any problems.

## Bugs

It is preferable that if you find a minor or serious bug, you should visit [the Arch Bug Tracker](https://bugs.archlinux.org) or/and [KDE Bug Tracker](http://bugs.kde.org) in order to report that. Make sure that you are clear about what you want to report.

If you have any problem and you write about in on the Arch forums, first make sure that you have **fully** updated your system using a good sync mirror (check [here](https://www.archlinux.de/?page=MirrorStatus)) or try [Reflector](/index.php/Reflector "Reflector").

## See also

*   [KDE homepage](http://www.kde.org)
*   [KDE bug tracker](https://bugs.kde.org)
*   [KDE Projects](https://projects.kde.org)
*   [Martin Graesslin's blog](http://blog.martin-graesslin.com/blog/kategorien/kde/)

Retrieved from "[https://wiki.archlinux.org/index.php?title=KDE&oldid=413672](https://wiki.archlinux.org/index.php?title=KDE&oldid=413672)"