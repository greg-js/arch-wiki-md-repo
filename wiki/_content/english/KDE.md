Related articles

*   [Desktop environment](/index.php/Desktop_environment "Desktop environment")
*   [Display manager](/index.php/Display_manager "Display manager")
*   [Window manager](/index.php/Window_manager "Window manager")
*   [Qt](/index.php/Qt "Qt")
*   [SDDM](/index.php/SDDM "SDDM")
*   [Dolphin](/index.php/Dolphin "Dolphin")
*   [KDE Wallet](/index.php/KDE_Wallet "KDE Wallet")
*   [KDevelop](/index.php/KDevelop "KDevelop")
*   [Trinity](/index.php/Trinity "Trinity")
*   [Uniform Look for Qt and GTK Applications](/index.php/Uniform_Look_for_Qt_and_GTK_Applications "Uniform Look for Qt and GTK Applications")

KDE is a software project currently comprising of a [desktop environment](/index.php/Desktop_environment "Desktop environment") known as Plasma, a collection of libraries and frameworks (KDE Frameworks) and several applications (KDE Applications) as well. KDE upstream has a well maintained [UserBase wiki](https://userbase.kde.org/). Detailed information about most KDE applications can be found there.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Plasma](#Plasma)
    *   [1.2 KDE applications](#KDE_applications)
    *   [1.3 Unstable releases](#Unstable_releases)
*   [2 Starting Plasma](#Starting_Plasma)
    *   [2.1 Using a display manager](#Using_a_display_manager)
    *   [2.2 From the console](#From_the_console)
*   [3 Configuration](#Configuration)
    *   [3.1 Personalization](#Personalization)
        *   [3.1.1 Plasma desktop](#Plasma_desktop)
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
        *   [3.1.6 Thumbnail generation](#Thumbnail_generation)
    *   [3.2 Printing](#Printing)
    *   [3.3 Samba/Windows support](#Samba.2FWindows_support)
    *   [3.4 KDE Desktop activities](#KDE_Desktop_activities)
    *   [3.5 Power saving](#Power_saving)
    *   [3.6 Autostarting applications](#Autostarting_applications)
    *   [3.7 Phonon](#Phonon)
        *   [3.7.1 Which backend should I choose?](#Which_backend_should_I_choose.3F)
*   [4 Applications](#Applications)
    *   [4.1 System administration](#System_administration)
        *   [4.1.1 Terminate Xorg server through KDE System Settings](#Terminate_Xorg_server_through_KDE_System_Settings)
        *   [4.1.2 KCM](#KCM)
    *   [4.2 Desktop search](#Desktop_search)
        *   [4.2.1 Baloo](#Baloo)
            *   [4.2.1.1 Using and configuring Baloo](#Using_and_configuring_Baloo)
            *   [4.2.1.2 How do I index a removable device?](#How_do_I_index_a_removable_device.3F)
    *   [4.3 Web browsers](#Web_browsers)
    *   [4.4 PIM](#PIM)
        *   [4.4.1 Akonadi](#Akonadi)
            *   [4.4.1.1 Installation](#Installation_2)
            *   [4.4.1.2 Disabling Akonadi](#Disabling_Akonadi)
            *   [4.4.1.3 Database configuration](#Database_configuration)
                *   [4.4.1.3.1 MariaDB/MySQL (using ZFS)](#MariaDB.2FMySQL_.28using_ZFS.29)
                *   [4.4.1.3.2 PostgreSQL](#PostgreSQL)
                *   [4.4.1.3.3 SQLite](#SQLite)
    *   [4.5 KDE Telepathy](#KDE_Telepathy)
        *   [4.5.1 Use Telegram with KDE Telepathy](#Use_Telegram_with_KDE_Telepathy)
    *   [4.6 Integrate Android](#Integrate_Android)
*   [5 Tips and tricks](#Tips_and_tricks)
    *   [5.1 Using an alternative window manager](#Using_an_alternative_window_manager)
        *   [5.1.1 KDE/Openbox session](#KDE.2FOpenbox_session)
        *   [5.1.2 Re-enabling compositing effects](#Re-enabling_compositing_effects)
    *   [5.2 Configuring monitor resolution / multiple monitors](#Configuring_monitor_resolution_.2F_multiple_monitors)
    *   [5.3 Disable opening application launcher with Super key (Windows key)](#Disable_opening_application_launcher_with_Super_key_.28Windows_key.29)
*   [6 Troubleshooting](#Troubleshooting)
    *   [6.1 Configuration related](#Configuration_related)
        *   [6.1.1 Plasma desktop behaves strangely](#Plasma_desktop_behaves_strangely)
        *   [6.1.2 Clean cache to resolve upgrade problems](#Clean_cache_to_resolve_upgrade_problems)
    *   [6.2 Graphical problems](#Graphical_problems)
        *   [6.2.1 Getting current state of KWin for support and debug purposes](#Getting_current_state_of_KWin_for_support_and_debug_purposes)
        *   [6.2.2 Disable desktop effects manually or automatically for defined applications](#Disable_desktop_effects_manually_or_automatically_for_defined_applications)
        *   [6.2.3 Disable compositing](#Disable_compositing)
        *   [6.2.4 Flickering in fullscreen when compositing is enabled](#Flickering_in_fullscreen_when_compositing_is_enabled)
        *   [6.2.5 Screen tearing with NVIDIA](#Screen_tearing_with_NVIDIA)
        *   [6.2.6 Plasma cursor sometimes shown incorrecty](#Plasma_cursor_sometimes_shown_incorrecty)
    *   [6.3 Sound problems](#Sound_problems)
        *   [6.3.1 No sound after suspend](#No_sound_after_suspend)
        *   [6.3.2 "Falling back to default" messages when trying to listen to any sound](#.22Falling_back_to_default.22_messages_when_trying_to_listen_to_any_sound)
        *   [6.3.3 MP3 files cannot be played when using the GStreamer Phonon backend](#MP3_files_cannot_be_played_when_using_the_GStreamer_Phonon_backend)
    *   [6.4 Power management](#Power_management)
        *   [6.4.1 No Suspend/Hibernate options](#No_Suspend.2FHibernate_options)
        *   [6.4.2 Backlight control hotkeys stopped working](#Backlight_control_hotkeys_stopped_working)
    *   [6.5 KMail](#KMail)
        *   [6.5.1 Clean akonadi configuration to fix KMail](#Clean_akonadi_configuration_to_fix_KMail)
        *   [6.5.2 Empty IMAP inbox in KMail](#Empty_IMAP_inbox_in_KMail)
    *   [6.6 Networking](#Networking)
        *   [6.6.1 Freezes when using Automount on a NFS volume](#Freezes_when_using_Automount_on_a_NFS_volume)
    *   [6.7 Aggressive QXcbConnection journal logging](#Aggressive_QXcbConnection_journal_logging)
    *   [6.8 KF5/Qt5 applications do not display icons in i3/fvwm/awesome](#KF5.2FQt5_applications_do_not_display_icons_in_i3.2Ffvwm.2Fawesome)
    *   [6.9 Problems with saving credentials and persistently occurring KWallet dialogs](#Problems_with_saving_credentials_and_persistently_occurring_KWallet_dialogs)
    *   [6.10 Weird "q" symbol in konsole](#Weird_.22q.22_symbol_in_konsole)
*   [7 See also](#See_also)

## Installation

### Plasma

Before installing Plasma, make sure you have a working [Xorg](/index.php/Xorg "Xorg") installation on your system.

[Install](/index.php/Install "Install") the [plasma-meta](https://www.archlinux.org/packages/?name=plasma-meta) meta-package or the [plasma](https://www.archlinux.org/groups/x86_64/plasma/) group. For differences between [plasma-meta](https://www.archlinux.org/packages/?name=plasma-meta) and [plasma](https://www.archlinux.org/groups/x86_64/plasma/) reference [Creating packages#Meta packages and groups](/index.php/Creating_packages#Meta_packages_and_groups "Creating packages"). Alternatively, for a more minimal Plasma installation, install the [plasma-desktop](https://www.archlinux.org/packages/?name=plasma-desktop) package.

To enable support for [Wayland](/index.php/Wayland "Wayland") in Plasma, also install the [plasma-wayland-session](https://www.archlinux.org/packages/?name=plasma-wayland-session) package.

### KDE applications

To install the full set of KDE Applications, install the [kde-applications](https://www.archlinux.org/groups/x86_64/kde-applications/) group or the [kde-applications-meta](https://www.archlinux.org/packages/?name=kde-applications-meta) meta-package. Note that this will only install applications, it will not install any version of Plasma.

### Unstable releases

See [Official repositories#kde-unstable](/index.php/Official_repositories#kde-unstable "Official repositories")

## Starting Plasma

**Note:** Although it is possible to launch Plasma under [Wayland](/index.php/Wayland "Wayland"), there are some missing features and known problems as of Plasma 5.12\. See the [Plasma 5.12 Errata](https://community.kde.org/Plasma/5.12_Errata#Wayland) for a list of issues and the [Plasma on Wayland workboard](https://phabricator.kde.org/project/board/99/) for the current state of development. Use [Xorg](/index.php/Xorg "Xorg") for the most complete and stable experience.

Plasma can be started either using a [display manager](/index.php/Display_manager "Display manager"), or from the console.

### Using a display manager

*   Select *Plasma* to launch a new session in [Xorg](/index.php/Xorg "Xorg").
*   [Install](/index.php/Install "Install") [plasma-wayland-session](https://www.archlinux.org/packages/?name=plasma-wayland-session) and select *Plasma (Wayland)* to launch a new session in [Wayland](/index.php/Wayland "Wayland").

**Note:** The [NVIDIA](/index.php/NVIDIA "NVIDIA") proprietary driver implementation for Wayland requires EGLStreams. KDE have not implemented EGLStreams in their Wayland [implementation](https://blog.martin-graesslin.com/blog/2016/09/to-eglstream-or-not). The following workarounds are available:

*   Using the [Nouveau](/index.php/Nouveau "Nouveau") driver.
*   Using the (default) Xorg session.

### From the console

To start Plasma with [xinit](/index.php/Xinit "Xinit")/*startx*, append `exec startkde` to your `.xinitrc` file. If you want to start Xorg at login, please see [Start X at login](/index.php/Start_X_at_login "Start X at login"). To start a Plasma on Wayland session from a console, run `startplasmacompositor`.

## Configuration

Most settings for KDE applications are stored in `~/.config`. However, configuring KDE is primarily done through the **System Settings** application. It can be started from a terminal by executing `systemsettings5`.

### Personalization

#### Plasma desktop

##### Themes

[Plasma themes](https://store.kde.org/browse/cat/104/) define the look of panels and plasmoids. For easy system-wide installation, some themes are available in both the official repositories and the [AUR](https://aur.archlinux.org/packages.php?O=0&K=plasmatheme&do_Search=Go).

The easiest way to install themes is by going through the *System Settings > Workspace Theme > Desktop Theme > Get new Themes*.

This will present a frontend for the [KDE-Store](https://store.kde.org/) that allows you to install, uninstall, or update third-party plasmoid scripts.

Splash and Lock screens are currently unavailable. To customize these screens, you have to modify the original theme found in `/usr/share/plasma/look-and-feel/`. See [this thread](https://www.kubuntuforums.net/showthread.php?67599-Plasma-5-background-images&s=59832dc20e5bfc2948dbb591d8453f61) on the Kubuntu forums.

Note that the [SDDM](/index.php/SDDM "SDDM") login screen is not part of this theme.

###### Qt and GTK+ Applications Appearance

**Tip:** For Qt and GTK theme consistency, see [Uniform look for Qt and GTK applications](/index.php/Uniform_look_for_Qt_and_GTK_applications "Uniform look for Qt and GTK applications").

	Qt4

For Qt4 applications to have a consistent appearance, there are two options:

Install [breeze-kde4](https://www.archlinux.org/packages/?name=breeze-kde4) and then pick Breeze as GUI Style in `qtconfig-qt4`; or install [breeze-gtk](https://www.archlinux.org/packages/?name=breeze-gtk) and pick GTK+ as GUI Style.

	GTK+

The recommended theme for a pleasant appearance in GTK+ applications is [breeze-gtk](https://www.archlinux.org/packages/?name=breeze-gtk) or [gnome-breeze-git](https://aur.archlinux.org/packages/gnome-breeze-git/), a GTK+ theme designed to mimic the appearance of Plasma's Breeze theme. Install [kde-gtk-config](https://www.archlinux.org/packages/?name=kde-gtk-config) and select the installed GTK-theme for GTK2/GTK3-Theme in *System Settings > Application Style > GNOME Application Style*.

In some themes, tooltips in GTK+ applications have white text on white backgrounds making it difficult to read. To change the colors in GTK2 applications, find the section for tooltips in the `.gtkrc-2.0` file and change it. For GTK3 application two files need to be changed, `gtk.css` and `settings.ini`. It might also help to uncheck the option to *Apply colors to non-Qt applications* under *System Settings* > *Colors*.

Some GTK2 programs like [vuescan-bin](https://aur.archlinux.org/packages/vuescan-bin/) still look hardly usable due to invisible checkboxes with the Breeze or Adwaita skin in a Plasma session. To workaround this, install and select e.g. the Numix-Frost-Light skin of the [numix-frost-themes](https://aur.archlinux.org/packages/numix-frost-themes/) under *System Settings* > *Application Style* > *GNOME Application Style (GTK)* > *Select a GTK2 Theme:*. Numix-Frost-Light looks similar to Breeze.

##### Widgets

Plasmoids are little scripted (plasmoid scripts) or coded (plasmoid binaries) KDE applications designed to enhance the functionality of your desktop.

The easiest way to install plasmoid scripts is by right-clicking onto a panel or the desktop and choosing *Add Widgets > Get new Widgets > Download Widgets*. This will present a nice frontend for [https://store.kde.org/](https://store.kde.org/) that allows you to install, uninstall, or update third-party plasmoid scripts with literally just one click.

Many Plasmoid binaries are available from the [AUR](https://aur.archlinux.org/packages.php?O=0&K=plasmoid&PP=50&SO=d&SB=v).

##### Sound applet in the system tray

[Install](/index.php/Install "Install") [plasma-pa](https://www.archlinux.org/packages/?name=plasma-pa) or [kmix](https://www.archlinux.org/packages/?name=kmix) (start Kmix from the Application Launcher). [plasma-pa](https://www.archlinux.org/packages/?name=plasma-pa) is now installed by default with [plasma](https://www.archlinux.org/groups/x86_64/plasma/), no further configuration needed.

**Note:** To adjust the [step size of volume increments/decrements](https://bugs.kde.org/show_bug.cgi?id=313579#c28), add e.g. `VolumePercentageStep=1` in the `[Global]` section of `~/.config/kmixrc`.

##### Disable panel shadow

As the Plasma panel is on top of other windows, its shadow is drawn over them. [[1]](https://bbs.archlinux.org/viewtopic.php?pid=1228394#p1228394) To disable this behaviour without impacting other shadows, [install](/index.php/Install "Install") [xorg-xprop](https://www.archlinux.org/packages/?name=xorg-xprop) and run:

```
$ xprop -remove _KDE_NET_WM_SHADOW

```

then select the panel with the plus-sized cursor. [[2]](https://forum.kde.org/viewtopic.php?f=285&t=121592) For automation, install [xorg-xwininfo](https://www.archlinux.org/packages/?name=xorg-xwininfo) and create the following script:

 `/usr/local/bin/kde-no-shadow` 
```
#!/bin/bash
for WID in $(xwininfo -root -tree | sed '/"Plasma": ("plasmashell" "plasmashell")/!d; s/^  *\([^ ]*\) .*/\1/g'); do
   xprop -id $WID -remove _KDE_NET_WM_SHADOW
done

```

Set execution permissions for the script:

```
# chmod 755 /usr/local/bin/kde-no-shadow

```

The script can be run on login with *Add Script* in *Autostart*:

```
$ kcmshell5 autostart

```

#### Window decorations

[Window decorations](https://store.kde.org/browse/cat/114/) can be changed in *System Settings > Application Style > Window Decorations*.

There you can also directly download and install more themes with one click, and some are available in the [AUR](https://aur.archlinux.org/packages.php?O=0&K=kdestyle&do_Search=Go&PP=25&SO=d&SB=v).

#### Icon themes

Icon themes can be installed and changed on *System Settings > Icons*.

**Note:** Although all modern Linux desktops share the same icon theme format, desktops like [GNOME](/index.php/GNOME "GNOME") use fewer icons (esp. in menus and toolbars). Themes developed for such desktops usually lack icons required by Plasma and KDE apps. It is recommended to install Plasma compatible icon themes instead.

#### Fonts

##### Fonts in a Plasma session look poor

Try installing the [ttf-dejavu](https://www.archlinux.org/packages/?name=ttf-dejavu) and [ttf-liberation](https://www.archlinux.org/packages/?name=ttf-liberation) packages.

After the installation, be sure to log out and back in. You should not have to modify anything in *System Settings > Fonts*. If you are using [qt5ct](https://www.archlinux.org/packages/?name=qt5ct), the settings in Qt5 Configuration Tool may override the font settings in System Settings.

If you have personally set up how your [Fonts](/index.php/Fonts "Fonts") render, be aware that System Settings may alter their appearance. When you go *System Settings > Fonts* System Settings will likely alter your font configuration file (`fonts.conf`).

There is no way to prevent this, but, if you set the values to match your `fonts.conf` file, the expected font rendering will return (it will require you to restart your application or in a few cases restart your desktop). Note that Gnome's Font Preferences also does this.

##### Fonts are huge or seem disproportional

Try to force font DPI to `**96**` in *System Settings > Fonts*.

If that does not work, try setting the DPI directly in your Xorg configuration as documented in [Xorg#Setting DPI manually](/index.php/Xorg#Setting_DPI_manually "Xorg").

#### Space efficiency

The Plasma Netbook shell has been dropped from Plasma 5, see the following [KDE forum post](https://forum.kde.org/viewtopic.php?f=289&t=126631&p=335947&hilit=plasma+netbook#p335899) However, you can achieve something similar by editing the file `~/.config/kwinrc` adding `BorderlessMaximizedWindows=true` in the `[Windows]` section.

#### Thumbnail generation

To allow thumbnail generation for media or document files on the desktop and in Dolphin, install [kdegraphics-thumbnailers](https://www.archlinux.org/packages/?name=kdegraphics-thumbnailers), [ffmpegthumbs](https://www.archlinux.org/packages/?name=ffmpegthumbs) and [kde-thumbnailer-odf](https://aur.archlinux.org/packages/kde-thumbnailer-odf/).

Then enable the thumbnail categories for the desktop via *right click* on the *desktop background* > *Configure Desktop* > *Icons* > *More Preview Options...*.

In *Dolphin*, navigate to *Control* > *General* > *Previews*.

### Printing

**Tip:** Use the [CUPS](/index.php/CUPS "CUPS") web interface for faster configuration. Printers configured in this way can be used in KDE applications.

You can also configure printers in *System Settings > Printers*. To use this method, you must first install [print-manager](https://www.archlinux.org/packages/?name=print-manager) and [cups](https://www.archlinux.org/packages/?name=cups). See [CUPS#Configuration](/index.php/CUPS#Configuration "CUPS").

### Samba/Windows support

If you want to have access to Windows services, install [Samba](/index.php/Samba "Samba") (package [samba](https://www.archlinux.org/packages/?name=samba)).

The Dolphin share functionality requires the package [kdenetwork-filesharing](https://www.archlinux.org/packages/?name=kdenetwork-filesharing) and usershares, which the stock `smb.conf` does not have enabled. Instructions to add them are in [Samba#Creating usershare path](/index.php/Samba#Creating_usershare_path "Samba"), after which sharing in Dolphin should work out of the box after restarting Samba.

Plasma's abilities to access SMB shares are limited, though. Writing to Windows shares is problematic and opening files from such shares, e.g. large videos, makes Plasma copying the whole file to the local system first. To workaround this, you can install a GTK based file browser like [thunar](https://www.archlinux.org/packages/?name=thunar) with [gvfs](https://www.archlinux.org/packages/?name=gvfs) and [gvfs-smb](https://www.archlinux.org/packages/?name=gvfs-smb) (and [gnome-keyring](https://www.archlinux.org/packages/?name=gnome-keyring) for saving login credentials) to access SMB shares in a more able way. Another possible workaround is to [mount](/index.php/Mount "Mount") a Samba share via [cifs-utils](https://www.archlinux.org/packages/?name=cifs-utils) to make it look to Plasma like if the SMB share was just a normal local folder and thus can be accessed normally. The mount command could look like the following for write access to a public share:

```
# mount -t cifs -o username=*,password=*,uid=1000,gid=1000,file_mode=0660,dir_mode=0770 //networkhost/share/ /home/user/localmountpoint/

```

Make it permanent:

 `/etc/fstab` 
```
//networkhost/share/ /home/user/localmountpoint/ cifs defaults,username=*,password=*,uid=1000,gid=1000,file_mode=0660,dir_mode=0770 0 2

```

It might be necessary to append `.local` to the hostname. For some NAS devices it might also be necessary to append `vers=1.0` to the argument line to enforce SMB 1.0 compatibility.

An easier solution is to use [samba-mounter-git](https://aur.archlinux.org/packages/samba-mounter-git/), which offers basically the same functionality via an easy to use option located at *System Settings* > *Network Drivers*.

### KDE Desktop activities

[KDE Desktop Activities](https://userbase.kde.org/Plasma#Activities) are special workspaces where you can select specific settings for each activity that apply only when you are using said activity.

### Power saving

[Install](/index.php/Install "Install") [powerdevil](https://www.archlinux.org/packages/?name=powerdevil) for an integrated power saving service called "**Powerdevil Power Management**", that may adjust the power saving profile of the system and/or the brightness of the screen (if supported).

**Note:** Powerdevil may not [inhibit](/index.php/Power_management#Power_managers "Power management") all logind settings (such as the lid close action for laptops). In these cases, the logind setting itself will need to be changed - see [Power management#Power management with systemd](/index.php/Power_management#Power_management_with_systemd "Power management").

### Autostarting applications

Plasma can autostart applications and run scripts on startup and shutdown. To autostart an application, navigate to *System Settings > Startup and Shutdown > Autostart* and add the program or shell script of your choice. For applications, a `.desktop` file will be created, for shell scripts, a symlink will be created.

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

### Phonon

From [Wikipedia](https://en.wikipedia.org/wiki/Phonon_(software) "wikipedia:Phonon (software)"):

	Phonon is the multimedia API provided by KDE and is the standard abstraction for handling multimedia streams within KDE software and also used by several Qt applications.

	Phonon was originally created to allow KDE and Qt software to be independent of any single multimedia framework such as GStreamer or xine and to provide a stable API for a major version's lifetime.

Phonon is being widely used within KDE, for both audio (e.g., the System notifications or KDE audio apps) and video (e.g., the [Dolphin](/index.php/Dolphin "Dolphin") video thumbnails).

#### Which backend should I choose?

You can choose between backends based on [GStreamer](/index.php/GStreamer "GStreamer") and [VLC](/index.php/VLC "VLC") – each available in versions for Qt4 applications and Qt5 applications ([phonon-qt4-gstreamer](https://www.archlinux.org/packages/?name=phonon-qt4-gstreamer), [phonon-qt5-gstreamer](https://www.archlinux.org/packages/?name=phonon-qt5-gstreamer) – [phonon-qt4-vlc](https://www.archlinux.org/packages/?name=phonon-qt4-vlc), [phonon-qt5-vlc](https://www.archlinux.org/packages/?name=phonon-qt5-vlc)).

[Upstream prefers VLC](https://www.phoronix.com/scan.php?page=news_item&px=MTUwNDM) but prominent Linux distributions (Kubuntu and Fedora-KDE for example) prefer GStreamer because that allows them to easily leave out patented MPEG codecs from the default installation. Both backends have a slightly different [features set](https://community.kde.org/Phonon/FeatureMatrix).

In the past other backends were developed as well but are no longer maintained and their AUR packages have been deleted.

**Note:**

*   Multiple backends can be installed at once and prioritized at *System Settings > Multimedia > Backend*.
*   According to the [KDE forums](https://forum.kde.org/viewtopic.php?f=250&t=126476&p=335080), the VLC backend lacks support for [ReplayGain](https://en.wikipedia.org/wiki/ReplayGain "wikipedia:ReplayGain").
*   If you choose the vlc backend, you may experience crashes every time kde wants to send you a audible warning (and in quite a number of other cases as well, see [[4]](https://forum.kde.org/viewtopic.php?f=289&t=135956))
*   A possible fix is to run

 `# /usr/lib/vlc/vlc-cache-gen -f /usr/lib/vlc/plugins` 

## Applications

The KDE project provides a suite of applications that integrate with the Plasma desktop. See the [kde-applications](https://www.archlinux.org/groups/x86_64/kde-applications/) group for a full listing of the available applications. Also see [Category:KDE](/index.php/Category:KDE "Category:KDE") for related KDE application pages.

Aside from the programs provided in KDE Applications, there are many other applications available that can complement the Plasma desktop. Some of these are discussed below.

### System administration

#### Terminate Xorg server through KDE System Settings

Navigate to the submenu *System Settings > Input Devices > Keyboard > Advanced (tab) > "Key Sequence to kill the X server"* and ensure that the checkbox is ticked.

#### KCM

KCM stands for **KC**onfig **M**odule. KCMs can help you configure your system by providing interfaces in System Settings, or through the command line with *kcmshell5*.

*   **kde-gtk-config** — GTK2 and GTK3 Configurator for KDE.

	[https://cgit.kde.org/kde-gtk-config.git](https://cgit.kde.org/kde-gtk-config.git) || [kde-gtk-config](https://www.archlinux.org/packages/?name=kde-gtk-config)

*   **KCM Qt Graphics System** — This KCM allows you to easily configure the standard Qt graphics system.

	[https://www.linux-apps.com/p/1127857/](https://www.linux-apps.com/p/1127857/) || [kcm-qt-graphicssystem](https://aur.archlinux.org/packages/kcm-qt-graphicssystem/)

*   **UFW KControl Module** — KDE4 control module for UFW ([Uncomplicated Firewall](/index.php/Uncomplicated_Firewall "Uncomplicated Firewall")).

	[https://www.linux-apps.com/p/1127851/](https://www.linux-apps.com/p/1127851/) || [kcm-ufw](https://aur.archlinux.org/packages/kcm-ufw/)

*   **System policies** — Set of configuration modules which allows administrator to change [PolicyKit](/index.php/PolicyKit "PolicyKit") settings.

	[https://cgit.kde.org/polkit-kde-kcmodules-1.git](https://cgit.kde.org/polkit-kde-kcmodules-1.git) || [kcm-polkit-kde-git](https://aur.archlinux.org/packages/kcm-polkit-kde-git/)

*   **wacom tablet** — KDE GUI for the Wacom Linux Drivers.

	[https://www.linux-apps.com/p/1127862/](https://www.linux-apps.com/p/1127862/) || [kcm-wacomtablet](https://aur.archlinux.org/packages/kcm-wacomtablet/)

*   **Kcmsystemd** — systemd control module for KDE.

	[https://github.com/rthomsen/kcmsystemd](https://github.com/rthomsen/kcmsystemd) || [systemd-kcm](https://www.archlinux.org/packages/?name=systemd-kcm)

More KCMs can be found at [linux-apps.com](https://www.linux-apps.com/search?projectSearchText=KCM).

### Desktop search

KDE implements desktop search with a software called Baloo, a file indexing and searching solution.

#### Baloo

##### Using and configuring Baloo

In order to search using Baloo on the Plasma desktop, start krunner (default keyboard shortcut `ALT+F2`) and type in your query. Within Dolphin press `CTRL+F`.

By default the Desktop Search KCM exposes only two options: A panel to blacklist folders and a way to disable it with one click.

Alternatively you can edit your `~/.config/baloofilerc` file ([info](https://community.kde.org/Baloo/Configuration)). Additionally the `balooctl` process can also be used. In order to disable Baloo run `balooctl stop` and `balooctl disable`.

Once you added additional folders to the blacklist or disabled Baloo entirely, a process named `baloo_file_cleaner` removes all unneeded index files automatically. They are stored under `~/.local/share/baloo/`.

##### How do I index a removable device?

By default every removable device is blacklisted. You just have to remove your device from the blacklist in the KCM panel.

### Web browsers

*   **[Konqueror](https://en.wikipedia.org/wiki/Konqueror "wikipedia:Konqueror")** — Part of the KDE project, supports two rendering engines – KHTML and the [Chromium](/index.php/Chromium "Chromium")-based Qt WebEngine.

	[https://konqueror.org/](https://konqueror.org/) || [konqueror](https://www.archlinux.org/packages/?name=konqueror)

*   **[QupZilla](https://en.wikipedia.org/wiki/QupZilla "wikipedia:QupZilla")** — A Qt web browser with Plasma integration features. It uses Qt WebEngine.

	[https://www.qupzilla.com/](https://www.qupzilla.com/) || [qupzilla](https://www.archlinux.org/packages/?name=qupzilla)

*   **[Chromium](/index.php/Chromium "Chromium")** — Chromium and its proprietary variant Google Chrome have limited Plasma integration. [They can use KWallet](/index.php/KDE_Wallet#KDE_Wallet_for_Chrome_and_Chromium "KDE Wallet") and KDE Open/Save windows.

	[https://www.chromium.org/](https://www.chromium.org/) || [chromium](https://www.archlinux.org/packages/?name=chromium)

*   **[Firefox](/index.php/Firefox "Firefox")** — Firefox can be configured to better integrate with Plasma. See [Firefox KDE integration](/index.php/Firefox#KDE.2FGNOME_integration "Firefox") for details.

	[https://mozilla.org/firefox](https://mozilla.org/firefox) || [firefox](https://www.archlinux.org/packages/?name=firefox)

### PIM

KDE offers its own stack for personal information management. This includes emails, contacts, calendar, etc. To install all the PIM packages, you could use the meta-package [kdepim-meta](https://www.archlinux.org/packages/?name=kdepim-meta).

#### Akonadi

Akonadi is a system meant to act as a local cache for PIM data, regardless of its origin, which can be then used by other applications. This includes the user's emails, contacts, calendars, events, journals, alarms, notes, and so on.

Akonadi does not store any data by itself: the storage format depends on the nature of the data (for example, contacts may be stored in vCard format).

##### Installation

Install [akonadi](https://www.archlinux.org/packages/?name=akonadi). For additional addons, install [kdepim-addons](https://www.archlinux.org/packages/?name=kdepim-addons).

**Note:** If you wish to use a database engine other than MariaDB/MySQL, then when installing the [akonadi](https://www.archlinux.org/packages/?name=akonadi) package, use the following command to skip installing the [mariadb](https://www.archlinux.org/packages/?name=mariadb) dependencies: `# pacman -S akonadi --assume-installed mariadb` 

##### Disabling Akonadi

See this [section in the KDE userbase](https://userbase.kde.org/Akonadi#Disabling_the_Akonadi_subsystem).

##### Database configuration

###### MariaDB/MySQL (using ZFS)

If your home directory is on a ZFS pool, you will need to create `~/.config/akonadi/mysql-local.conf` with the following contents:

```
[mysqld]
innodb_use_native_aio = 0

```

Otherwise you will get the [OS error 22](/index.php/MySQL#OS_error_22_when_running_on_ZFS "MySQL")

###### PostgreSQL

Install and setup [PostgreSQL](/index.php/PostgreSQL "PostgreSQL"). Make sure `postgresql.service` is [started](/index.php/Started "Started").

Edit Akonadi configuration file so that it has the following contents:

 `~/.config/akonadi/akonadiserverrc` 
```
[%General]
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

Start Akonadi with `akonadictl start`, and check its status: `akonadictl status`.

###### SQLite

Edit Akonadi configuration file to match the configuration below:

 `~/.config/akonadi/akonadiserverrc` 
```
[%General]
Driver=QSQLITE3

[QSQLITE3]
Name=/home/*username*/.local/share/akonadi/akonadi.db
```

### KDE Telepathy

[KDE Telepathy](https://community.kde.org/KTp) is a project with the goal to closely integrate Instant Messaging with the KDE desktop. It utilizes the Telepathy framework as a backend and is intended to replace Kopete.

To install all Telepathy protocols, install the [telepathy](https://www.archlinux.org/groups/x86_64/telepathy/) group. To use the KDE Telepathy client, install the [telepathy-kde-meta](https://www.archlinux.org/packages/?name=telepathy-kde-meta) package that includes all the packages contained in the [telepathy-kde](https://www.archlinux.org/groups/x86_64/telepathy-kde/) group.

#### Use Telegram with KDE Telepathy

[Telegram](/index.php/Telegram "Telegram") protocol is available using [telepathy-haze](https://www.archlinux.org/packages/?name=telepathy-haze), installing [telegram-purple](https://aur.archlinux.org/packages/telegram-purple/) or [telegram-purple-git](https://aur.archlinux.org/packages/telegram-purple-git/) and [telepathy-morse-git](https://aur.archlinux.org/packages/telepathy-morse-git/). The username is the Telegram account telephone number (complete with the national prefix `+*xx*`, e.g. `+49` for Germany).

The configuration through the GUI may be tricky: if the phone number is not accepted when configuring a new account in the KDE Telepathy client (with an error message complaining about an invalid parameter which prevents the account creation), insert it between single quotes and then remove the quotes manually from the configuration file (`~/.local/share/telepathy/mission-control/accounts.cfg`) after the account creation (if the quotes are not removed after, an authentication error should rise).

**Note:** The configuration file should be edited manually when KDE Telepathy is not running, e.g. when there is no KDE desktop session active, otherwise manual changes may be overwritten by the software.

### Integrate Android

[KDE Connect](https://community.kde.org/KDEConnect) provides several features for you:

*   Share files and URLs to/from KDE from/to any app, without wires.
*   Touchpad emulation: Use your phone screen as your computer's touchpad.
*   Notifications sync (4.3+): Read your Android notifications from the desktop.
*   Shared clipboard: copy and paste between your phone and your computer.
*   Multimedia remote control: Use your phone as a remote for Linux media players.
*   WiFi connection: no usb wire or bluetooth needed.
*   RSA Encryption: your information is safe.

You will need to install KDE Connect both on your computer and on your Android. For PC side, install [kdeconnect](https://www.archlinux.org/packages/?name=kdeconnect) package. For Android side, install `KDE Connect` from [Google Play](https://play.google.com/store/apps/details?id=org.kde.kdeconnect_tp) or from [F-Droid](https://f-droid.org/repository/browse/?fdid=org.kde.kdeconnect_tp).

It is possible to use KDE Connect even if you do not use the Plasma desktop. For desktop environments that use AppIndicators, such as Unity, install [indicator-kdeconnect](https://aur.archlinux.org/packages/indicator-kdeconnect/) package as well.

## Tips and tricks

### Using an alternative window manager

The component chooser settings in Plasma does not allow changing the window manager anymore. [[5]](https://github.com/KDE/plasma-desktop/commit/2f83a4434a888cd17b03af1f9925cbb054256ade) In order to change the window manager used you need to set the `KDEWM` [environment variable](/index.php/Environment_variable "Environment variable") before KDE startup. [[6]](https://wiki.haskell.org/Xmonad/Using_xmonad_in_KDE) To do that you can create a script called `set_window_manager.sh` in `~/.config/plasma-workspace/env` and export the `KDEWM` variable there. For example to use the i3 window manager :

 `~/.config/plasma-workspace/env/set_window_manager.sh`  `export KDEWM=/usr/bin/i3` 

And then make it executable :

 `$ chmod +x ~/.config/plasma-workspace/env/set_window_manager.sh` 

#### KDE/Openbox session

The [openbox](https://www.archlinux.org/packages/?name=openbox) package provides a session for using KDE with [Openbox](/index.php/Openbox "Openbox"). To make use of this session, select *KDE/Openbox* from the [display manager](/index.php/Display_manager "Display manager") menu.

For those starting the session manually, add the following line to your `.xinitrc` file:

```
exec openbox-kde-session

```

#### Re-enabling compositing effects

When replacing Kwin with a window manager which does not provide a Compositor (such as Openbox), any desktop compositing effects e.g. transparency will be lost. In this case, install and run a separate Composite manager to provide the effects such as [Xcompmgr](/index.php/Xcompmgr "Xcompmgr") or [Compton](/index.php/Compton "Compton").

### Configuring monitor resolution / multiple monitors

To enable display resolution management and multiple monitors in Plasma, install [kscreen](https://www.archlinux.org/packages/?name=kscreen). This adds the additional options to *Sytem Settings > Display and Monitor*.

### Disable opening application launcher with Super key (Windows key)

To disable this feature you currently can run the following command:

```
$ kwriteconfig5 --file kwinrc --group ModifierOnlyShortcuts --key Meta ""

```

## Troubleshooting

### Configuration related

Many problems in KDE are related to configuration.

#### Plasma desktop behaves strangely

Plasma problems are usually caused by unstable **Plasma widgets** (colloquially called *plasmoids*) or **Plasma themes**. First, find which was the last widget or theme you had installed and disable it or uninstall it.

So, if your desktop suddenly exhibits "locking up", this is likely caused by a faulty installed widget. If you cannot remember which widget you installed before the problem began (sometimes it can be an irregular problem), try to track it down by removing each widget until the problem ceases. Then you can uninstall the widget, and file a bug report ([https://bugs.kde.org/](https://bugs.kde.org/)) **only if it is an official widget**. If it is not, it is recommended you find the entry on [https://store.kde.org/](https://store.kde.org/) and inform the developer of that widget about the problem (detailing steps to reproduce, etc).

If you cannot find the problem, but you do not want *all* the settings to be lost, navigate to `~/.config`:

```
$ for j in plasma*; do mv -- "$j" "${j%}.bak"; done

```

This command will **rename all Plasma related configs** to *.bak (e.g. `plasmarc.bak`) of your user and when you will relogin into Plasma, you will have the **default** settings back. To undo that action, remove the .bak file extension. If you already have *.bak files, rename, move, or delete them first. It is highly recommended that you create regular backups anyway. See [Synchronization and backup programs](/index.php/Synchronization_and_backup_programs "Synchronization and backup programs") for a list of possible solutions.

#### Clean cache to resolve upgrade problems

The [problem](https://bbs.archlinux.org/viewtopic.php?id=135301) may be caused by old cache. Sometimes after an upgrade, the old cache might introduce strange, hard to debug behaviour such as unkillable shells, hangs when changing various settings and several other problems such as ark being unable to unrar or unzip or amarok not recognizing any of your music. This solution can also resolve problems with KDE and Qt programmes looking bad following upgrade.

Rebuild the cache use the following commands:

```
$ rm ~/.config/Trolltech.conf
$ kbuildsycoca5 --noincremental
$ kbuildsycoca4 --noincremental

```

Optional empty the `~/.cache` folder contents, **note** this also clears cache of other applications:

```
$ rm -rf ~/.cache/*

```

### Graphical problems

Make sure you have the proper driver for your GPU installed. See [Xorg#Driver installation](/index.php/Xorg#Driver_installation "Xorg") for more information. If you have an older card, it might help to [#Disable desktop effects manually or automatically for defined applications](#Disable_desktop_effects_manually_or_automatically_for_defined_applications) or [#Disable compositing](#Disable_compositing).

#### Getting current state of KWin for support and debug purposes

This command prints out a summary of the current state of KWin including used options, used compositing backend and relevant OpenGL driver capabilities. See more on [Martin's blog](https://blog.martin-graesslin.com/blog/2012/03/on-getting-help-for-kwin-and-helping-kwin/).

```
$ qdbus org.kde.KWin /KWin supportInformation

```

#### Disable desktop effects manually or automatically for defined applications

Plasma has desktop effects enabled by default and e.g. not every game will disable them automatically. You can disable desktop effects in *System Settings > Desktop Effects* and you can toggle desktop effects with `Alt+Shift+F12`. Additionally, you can create custom KWin rules to automatically disable/enable compositing when a certain application/window starts under *System Settings > Window Management > Window Rules*.

#### Disable compositing

In *Sytem Settings > Display and Monitor*, uncheck *Enable compositor on startup* and restart Plasma.

#### Flickering in fullscreen when compositing is enabled

In *Sytem Settings > Display and Monitor*, uncheck *Allow applications to block compositing*. This may harm performance.

#### Screen tearing with NVIDIA

See [NVIDIA/Troubleshooting#Avoid screen tearing in KDE (KWin)](/index.php/NVIDIA/Troubleshooting#Avoid_screen_tearing_in_KDE_.28KWin.29 "NVIDIA/Troubleshooting").

#### Plasma cursor sometimes shown incorrecty

Create the directory `~/.icons/default` and inside a file named `index.theme` with the following contents:

 `/home/*archie*/.icons/default/index.theme` 
```
[Icon Theme]
Inherits=breeze_cursors
```

Execute the following command:

```
$ ln -s /usr/share/icons/breeze_cursors/cursors ~/.icons/default/cursors

```

### Sound problems

**Note:** First make sure you have [alsa-utils](https://www.archlinux.org/packages/?name=alsa-utils) installed.

#### No sound after suspend

If there is no sound after suspending and if KMix does not show audio devices which should be there, restarting plasmashell and pulseaudio may help:

```
$ killall plasmashell
$ systemctl --user restart pulseaudio.service
$ plasmashell

```

Some applications may also need to be restarted in order for sound to play from them again.

#### "Falling back to default" messages when trying to listen to any sound

When you encounter such messages:

```
The audio playback device *name_of_the_sound_device* does not work.
Falling back to default

```

Go to *System Settings > Multimedia > Phonon* and set the device named `default` above all the other devices in each box you see.

#### MP3 files cannot be played when using the GStreamer Phonon backend

This can be solved by installing the GStreamer libav plugin (package [gst-libav](https://www.archlinux.org/packages/?name=gst-libav)). If you still encounter problems, you can try changing the Phonon backend used by installing another such as [phonon-qt4-vlc](https://www.archlinux.org/packages/?name=phonon-qt4-vlc) or [phonon-qt5-vlc](https://www.archlinux.org/packages/?name=phonon-qt5-vlc). Then, make sure the backend is preferred via *System Settings > Multimedia > Backend*.

### Power management

#### No Suspend/Hibernate options

If your system is able to suspend or hibernate using [systemd](/index.php/Systemd "Systemd") but do not have these options shown in KDE, make sure [powerdevil](https://www.archlinux.org/packages/?name=powerdevil) is installed.

#### Backlight control hotkeys stopped working

It may happen that backlight control hotkeys suddenly stop working (possibly after an update). This may be due to a shortcuts conflict between KDE Daemon and Power Management. If this is the case, go to *Settings > Shortcuts > Global shortcuts* and set the hotkeys shortcuts in the Power management section, overriding KDE daemons.

If this does not help, see [Backlight](/index.php/Backlight "Backlight").

### KMail

#### Clean akonadi configuration to fix KMail

First, make sure that KMail is not running. Then backup configuration:

```
$ cp -a ~/.local/share/akonadi ~/.local/share/akonadi-old
$ cp -a ~/.config/akonadi ~/.config/akonadi-old

```

Start *SystemSettings > Personal* and remove all the resources. Go back to Dolphin and remove the original `~/.local/share/akonadi` and `~/.config/akonadi` - the copies you made ensure that you can back-track if necessary.

Now go back to the System Settings page and carefully add the necessary resources. You should see the resource reading in your mail folders. Then start Kontact/KMail to see if it work properly.

#### Empty IMAP inbox in KMail

For some IMAP accounts, kmail will show the inbox as a container with all other folders of this account inside. Kmail does not show messages in the inbox container but in all other subfolders, see [KDE Bug 284172](https://bugs.kde.org/show_bug.cgi?id=284172). To solve this problem simply disable the server side subscription in the kmail account settings.

### Networking

#### Freezes when using Automount on a NFS volume

Using [Fstab#Automount with systemd](/index.php/Fstab#Automount_with_systemd "Fstab") on a [NFS](/index.php/NFS "NFS") volume may cause freezes, see [bug report upstream](https://bugs.kde.org/show_bug.cgi?id=354137).

### Aggressive QXcbConnection journal logging

See [Qt#Disable/Change Qt journal logging behaviour](/index.php/Qt#Disable.2FChange_Qt_journal_logging_behaviour "Qt").

### KF5/Qt5 applications do not display icons in i3/fvwm/awesome

See [Qt#Configuration of Qt5 apps under environments other than KDE Plasma](/index.php/Qt#Configuration_of_Qt5_apps_under_environments_other_than_KDE_Plasma "Qt").

### Problems with saving credentials and persistently occurring KWallet dialogs

It is not recommended to turn off the [KWallet](/index.php/KWallet "KWallet") password saving system in the user settings as it is required to save encrypted credentials like WiFi passphrases for each user. Persistently occuring KWallet dialogs can be the consequence of turning it off. In case you find the dialogs to unlock the wallet annoying when applications want to access it, you can let the login managers `SDDM` and `LightDM` unlock the wallet at login automatically, see [KDE Wallet](/index.php/KDE_Wallet#Unlock_KDE_Wallet_automatically_on_login "KDE Wallet"). The first wallet needs to be generated by KWallet (and not user-generated) in order to be usable for system program credentials. In case you want the wallet credentials not to be opened in memory for every application, you can restrict applications from accessing it with [kwalletmanager](https://www.archlinux.org/packages/?name=kwalletmanager) in the KWallet settings. If you do not care for credential encryption at all, you can simply leave the password forms blank when KWallet asks for the password while creating a wallet. In this case, applications can access passwords without having to unlock the wallet first.

### Weird "q" symbol in konsole

If you get a weird "q" symbols in programs such as vim[[7]](https://github.com/vim/vim/issues/2008) or neovim[[8]](https://github.com/neovim/neovim/issues/7002), it is because they use cursor shape changing escape sequences (DECSCUSR) which konsole does not support. See [KDE Bug 347323](https://bugs.kde.org/show_bug.cgi?id=347323).

You will need to disable these escape sequences in the programs that use them. See [neovim FAQ](https://github.com/neovim/neovim/wiki/FAQ#nvim-shows-weird-symbols-2-q-when-changing-modes) for a workaround for neovim.

## See also

*   [KDE homepage](https://www.kde.org/)
*   [KDE bug tracker](https://bugs.kde.org/)
*   [Martin Graesslin's blog](https://blog.martin-graesslin.com/blog/kategorien/kde/)