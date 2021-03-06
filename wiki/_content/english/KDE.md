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

KDE is a software project currently comprising a [desktop environment](/index.php/Desktop_environment "Desktop environment") known as Plasma, a collection of libraries and frameworks (KDE Frameworks) and several applications (KDE Applications) as well. KDE upstream has a well maintained [UserBase wiki](https://userbase.kde.org/). Detailed information about most KDE applications can be found there.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

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
                *   [3.1.1.1.1 Qt and GTK Applications Appearance](#Qt_and_GTK_Applications_Appearance)
            *   [3.1.1.2 Faces](#Faces)
            *   [3.1.1.3 Widgets](#Widgets)
            *   [3.1.1.4 Sound applet in the system tray](#Sound_applet_in_the_system_tray)
            *   [3.1.1.5 Disable panel shadow](#Disable_panel_shadow)
        *   [3.1.2 Window decorations](#Window_decorations)
        *   [3.1.3 Icon themes](#Icon_themes)
        *   [3.1.4 Space efficiency](#Space_efficiency)
        *   [3.1.5 Thumbnail generation](#Thumbnail_generation)
    *   [3.2 Printing](#Printing)
    *   [3.3 Samba/Windows support](#Samba/Windows_support)
    *   [3.4 KDE Desktop activities](#KDE_Desktop_activities)
    *   [3.5 Power management](#Power_management)
    *   [3.6 Autostart](#Autostart)
    *   [3.7 Phonon](#Phonon)
        *   [3.7.1 Which backend should I choose?](#Which_backend_should_I_choose?)
*   [4 Applications](#Applications)
    *   [4.1 System administration](#System_administration)
        *   [4.1.1 Terminate Xorg server through KDE System Settings](#Terminate_Xorg_server_through_KDE_System_Settings)
        *   [4.1.2 KCM](#KCM)
    *   [4.2 Desktop search](#Desktop_search)
    *   [4.3 Web browsers](#Web_browsers)
    *   [4.4 PIM](#PIM)
        *   [4.4.1 Akonadi](#Akonadi)
            *   [4.4.1.1 MySQL](#MySQL)
                *   [4.4.1.1.1 System-wide MySQL instance](#System-wide_MySQL_instance)
            *   [4.4.1.2 PostgreSQL](#PostgreSQL)
                *   [4.4.1.2.1 Per-user PostgreSQL instance](#Per-user_PostgreSQL_instance)
                *   [4.4.1.2.2 System-wide PostgreSQL instance](#System-wide_PostgreSQL_instance)
            *   [4.4.1.3 SQLite](#SQLite)
            *   [4.4.1.4 Disabling Akonadi](#Disabling_Akonadi)
    *   [4.5 KDE Telepathy](#KDE_Telepathy)
        *   [4.5.1 Use Telegram with KDE Telepathy](#Use_Telegram_with_KDE_Telepathy)
    *   [4.6 KDE Connect](#KDE_Connect)
*   [5 Tips and tricks](#Tips_and_tricks)
    *   [5.1 Use a different window manager](#Use_a_different_window_manager)
        *   [5.1.1 KDE/Openbox session](#KDE/Openbox_session)
        *   [5.1.2 Re-enabling compositing effects](#Re-enabling_compositing_effects)
    *   [5.2 Configuring monitor resolution / multiple monitors](#Configuring_monitor_resolution_/_multiple_monitors)
    *   [5.3 KWin-lowlatency](#KWin-lowlatency)
    *   [5.4 Configuring ICC profiles](#Configuring_ICC_profiles)
    *   [5.5 Disable opening application launcher with Super key (Windows key)](#Disable_opening_application_launcher_with_Super_key_(Windows_key))
    *   [5.6 Disable bookmarks showing in application menu](#Disable_bookmarks_showing_in_application_menu)
*   [6 Troubleshooting](#Troubleshooting)
    *   [6.1 Fonts](#Fonts)
        *   [6.1.1 Fonts in a Plasma session look poor](#Fonts_in_a_Plasma_session_look_poor)
        *   [6.1.2 Fonts are huge or seem disproportional](#Fonts_are_huge_or_seem_disproportional)
    *   [6.2 Configuration related](#Configuration_related)
        *   [6.2.1 Plasma desktop behaves strangely](#Plasma_desktop_behaves_strangely)
        *   [6.2.2 Clean cache to resolve upgrade problems](#Clean_cache_to_resolve_upgrade_problems)
        *   [6.2.3 Volume control, notifications or multimedia keys do not work](#Volume_control,_notifications_or_multimedia_keys_do_not_work)
        *   [6.2.4 Login Screen KCM does not sync cursor settings to SDDM](#Login_Screen_KCM_does_not_sync_cursor_settings_to_SDDM)
    *   [6.3 Graphical problems](#Graphical_problems)
        *   [6.3.1 Getting current state of KWin for support and debug purposes](#Getting_current_state_of_KWin_for_support_and_debug_purposes)
        *   [6.3.2 Disable desktop effects manually or automatically for defined applications](#Disable_desktop_effects_manually_or_automatically_for_defined_applications)
        *   [6.3.3 Enable transparency](#Enable_transparency)
        *   [6.3.4 Disable compositing](#Disable_compositing)
        *   [6.3.5 Flickering in fullscreen when compositing is enabled](#Flickering_in_fullscreen_when_compositing_is_enabled)
        *   [6.3.6 Screen tearing with NVIDIA](#Screen_tearing_with_NVIDIA)
        *   [6.3.7 Plasma cursor sometimes shown incorrectly](#Plasma_cursor_sometimes_shown_incorrectly)
        *   [6.3.8 Unusable screen resolution set](#Unusable_screen_resolution_set)
        *   [6.3.9 Blurry icons in System tray](#Blurry_icons_in_System_tray)
    *   [6.4 Sound problems](#Sound_problems)
        *   [6.4.1 No sound after suspend](#No_sound_after_suspend)
        *   [6.4.2 MP3 files cannot be played when using the GStreamer Phonon backend](#MP3_files_cannot_be_played_when_using_the_GStreamer_Phonon_backend)
    *   [6.5 Power management](#Power_management_2)
        *   [6.5.1 No Suspend/Hibernate options](#No_Suspend/Hibernate_options)
    *   [6.6 KMail](#KMail)
        *   [6.6.1 Clean Akonadi configuration to fix KMail](#Clean_Akonadi_configuration_to_fix_KMail)
        *   [6.6.2 Empty IMAP inbox in KMail](#Empty_IMAP_inbox_in_KMail)
        *   [6.6.3 Authorization error for EWS account in KMail](#Authorization_error_for_EWS_account_in_KMail)
    *   [6.7 Networking](#Networking)
        *   [6.7.1 Freezes when using Automount on a NFS volume](#Freezes_when_using_Automount_on_a_NFS_volume)
    *   [6.8 Aggressive QXcbConnection journal logging](#Aggressive_QXcbConnection_journal_logging)
    *   [6.9 KF5/Qt 5 applications do not display icons in i3/FVWM/awesome](#KF5/Qt_5_applications_do_not_display_icons_in_i3/FVWM/awesome)
    *   [6.10 Problems with saving credentials and persistently occurring KWallet dialogs](#Problems_with_saving_credentials_and_persistently_occurring_KWallet_dialogs)
    *   [6.11 Discover does not show any applications](#Discover_does_not_show_any_applications)
    *   [6.12 High CPU usage of kscreenlocker_greet with NVIDIA drivers](#High_CPU_usage_of_kscreenlocker_greet_with_NVIDIA_drivers)
    *   [6.13 OS error 22 when running Akonadi on ZFS](#OS_error_22_when_running_Akonadi_on_ZFS)
    *   [6.14 Some programs are unable to scroll when their windows are inactive](#Some_programs_are_unable_to_scroll_when_their_windows_are_inactive)
    *   [6.15 TeamViewer behaves slowly](#TeamViewer_behaves_slowly)
*   [7 See also](#See_also)

## Installation

### Plasma

Before installing Plasma, make sure you have a working [Xorg](/index.php/Xorg "Xorg") installation on your system.

[Install](/index.php/Install "Install") the [plasma-meta](https://www.archlinux.org/packages/?name=plasma-meta) meta-package or the [plasma](https://www.archlinux.org/groups/x86_64/plasma/) group. For differences between [plasma-meta](https://www.archlinux.org/packages/?name=plasma-meta) and [plasma](https://www.archlinux.org/groups/x86_64/plasma/) reference [Package group](/index.php/Package_group "Package group"). Alternatively, for a more minimal Plasma installation, install the [plasma-desktop](https://www.archlinux.org/packages/?name=plasma-desktop) package.

To enable support for [Wayland](/index.php/Wayland "Wayland") in Plasma, also install the [plasma-wayland-session](https://www.archlinux.org/packages/?name=plasma-wayland-session) package.

### KDE applications

To install the full set of KDE Applications, install the [kde-applications](https://www.archlinux.org/groups/x86_64/kde-applications/) group or the [kde-applications-meta](https://www.archlinux.org/packages/?name=kde-applications-meta) meta-package. Note that this will only install applications, it will not install any version of Plasma.

### Unstable releases

See [Official repositories#kde-unstable](/index.php/Official_repositories#kde-unstable "Official repositories")

## Starting Plasma

**Note:** Although it is possible to launch Plasma under [Wayland](/index.php/Wayland "Wayland"), there are some missing features and known problems. See [Wayland Showstoppers](https://community.kde.org/Plasma/Wayland_Showstoppers) for a list of issues and the [Plasma on Wayland workboard](https://phabricator.kde.org/project/board/99/) for the current state of development. Use [Xorg](/index.php/Xorg "Xorg") for the most complete and stable experience.

Plasma can be started either using a [display manager](/index.php/Display_manager "Display manager"), or from the console.

### Using a display manager

*   Select *Plasma* to launch a new session in [Xorg](/index.php/Xorg "Xorg").
*   [Install](/index.php/Install "Install") [plasma-wayland-session](https://www.archlinux.org/packages/?name=plasma-wayland-session) and select *Plasma (Wayland)* to launch a new session in [Wayland](/index.php/Wayland "Wayland").

### From the console

*   To start Plasma with [xinit/startx](/index.php/Xinit "Xinit"), append `exec startplasma-x11` to your `.xinitrc` file. If you want to start Xorg at login, please see [Start X at login](/index.php/Start_X_at_login "Start X at login").
*   To start a Plasma on Wayland session from a console, run `XDG_SESSION_TYPE=wayland dbus-run-session startplasma-wayland`.[[1]](https://community.kde.org/KWin/Wayland#Start_a_Plasma_session_on_Wayland)

## Configuration

Most settings for KDE applications are stored in `~/.config/`. However, configuring KDE is primarily done through the **System Settings** application. It can be started from a terminal by executing `systemsettings5`.

### Personalization

#### Plasma desktop

##### Themes

[Plasma themes](https://store.kde.org/browse/cat/104/) define the look of panels and Plasma widgets. For easy system-wide installation, some themes are available in both the official repositories and the [AUR](https://aur.archlinux.org/packages.php?K=plasma+theme).

Plasma themes can also be installed through *System Settings > Global Theme > Get New Global Themes...*.

The [KDE Store](https://store.kde.org/) offers more Plasma customization's, like [SDDM](/index.php/SDDM "SDDM") themes and splash-screens.

###### Qt and GTK Applications Appearance

**Tip:** For Qt and GTK theme consistency, see [Uniform look for Qt and GTK applications](/index.php/Uniform_look_for_Qt_and_GTK_applications "Uniform look for Qt and GTK applications").

	Qt4

Breeze is not directly available for Qt4 since it cannot be built without KDE 4 packages, which have been dropped from the extra repository in August 2018 ([FS#59784](https://bugs.archlinux.org/task/59784)). However you can install [breeze-gtk](https://www.archlinux.org/packages/?name=breeze-gtk) and pick GTK as GUI Style by running `qtconfig-qt4`.

	GTK

The recommended theme for a pleasant appearance in GTK applications is [breeze-gtk](https://www.archlinux.org/packages/?name=breeze-gtk), a GTK theme designed to mimic the appearance of Plasma's Breeze theme. Install [kde-gtk-config](https://www.archlinux.org/packages/?name=kde-gtk-config) (part of the [plasma](https://www.archlinux.org/groups/x86_64/plasma/) group) and select `Breeze` or `Breeze-Dark` as the GTK2/GTK3 theme in *System Settings > Application Style > Configure GNOME/GTK Application Style...*.

In some themes, tooltips in GTK applications have white text on white backgrounds making it difficult to read. To change the colors in GTK2 applications, find the section for tooltips in the `.gtkrc-2.0` file and change it. For GTK3 application two files need to be changed, `gtk.css` and `settings.ini`.

Some GTK2 programs like [vuescan-bin](https://aur.archlinux.org/packages/vuescan-bin/) still look hardly usable due to invisible checkboxes with the Breeze or Adwaita skin in a Plasma session. To workaround this, install and select e.g. the Numix-Frost-Light skin of the [numix-frost-themes](https://aur.archlinux.org/packages/numix-frost-themes/) under *System Settings* > *Application Style* > *Configure GNOME/GTK Application Style...* > *GTK2 theme:*. Numix-Frost-Light looks similar to Breeze.

##### Faces

Plasma and [SDDM](/index.php/SDDM "SDDM") will both use a PNG file found at `~/.face.icon` as a user's avatar. To configure with a graphical interface, you can use *System Settings > Accounts Details > User Manager*, which may first need to be [installed](/index.php/Install "Install") (see the [user-manager](https://www.archlinux.org/packages/?name=user-manager) package). The default icon can be found in `/usr/share/sddm/faces/`.

##### Widgets

Plasmoids are little scripted (plasmoid scripts) or coded (plasmoid binaries) KDE applications designed to enhance the functionality of your desktop.

The easiest way to install plasmoid scripts is by right-clicking onto a panel or the desktop and choosing *Add Widgets > Get New Widgets... > Download New Plasma Widgets*. This will present a nice frontend for [https://store.kde.org/](https://store.kde.org/) that allows you to install, uninstall, or update third-party plasmoid scripts with literally just one click.

Many Plasmoid binaries are available from the [AUR](https://aur.archlinux.org/packages.php?K=plasmoid).

##### Sound applet in the system tray

[Install](/index.php/Install "Install") [plasma-pa](https://www.archlinux.org/packages/?name=plasma-pa) or [kmix](https://www.archlinux.org/packages/?name=kmix) (start Kmix from the Application Launcher). [plasma-pa](https://www.archlinux.org/packages/?name=plasma-pa) is now installed by default with [plasma](https://www.archlinux.org/groups/x86_64/plasma/), no further configuration needed.

**Note:** To adjust the [step size of volume increments/decrements](https://bugs.kde.org/show_bug.cgi?id=313579#c28), add e.g. `VolumePercentageStep=1` in the `[Global]` section of `~/.config/kmixrc`.

##### Disable panel shadow

As the Plasma panel is on top of other windows, its shadow is drawn over them. [[2]](https://bbs.archlinux.org/viewtopic.php?pid=1228394#p1228394) To disable this behaviour without impacting other shadows, [install](/index.php/Install "Install") [xorg-xprop](https://www.archlinux.org/packages/?name=xorg-xprop) and run:

```
$ xprop -remove _KDE_NET_WM_SHADOW

```

then select the panel with the plus-sized cursor. [[3]](https://forum.kde.org/viewtopic.php?f=285&t=121592) For automation, install [xorg-xwininfo](https://www.archlinux.org/packages/?name=xorg-xwininfo) and create the following script:

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

There you can also directly download and install more themes with one click, and some are available in the [AUR](https://aur.archlinux.org/packages.php?K=kde+window+decoration).

#### Icon themes

Icon themes can be installed and changed on *System Settings > Icons*.

**Note:** Although all modern Linux desktops share the same icon theme format, desktops like [GNOME](/index.php/GNOME "GNOME") use fewer icons (esp. in menus and toolbars). Themes developed for such desktops usually lack icons required by Plasma and KDE apps. It is recommended to install Plasma compatible icon themes instead.

**Tip:** Since some icon themes do not inherit from the default icon theme, some icons may be missing. To inherit from the Breeze, add `breeze` to the `Inherits=` array in `/usr/share/icon/*theme-name*/index.theme`, for example: `Inherits=breeze,hicolor`. You need to reapply this patch after every update to the icon theme, consider using [Pacman hooks](/index.php/Pacman_hooks "Pacman hooks") to automate the process.

#### Space efficiency

The Plasma Netbook shell has been dropped from Plasma 5, see the following [KDE forum post](https://forum.kde.org/viewtopic.php?f=289&t=126631&p=335947&hilit=plasma+netbook#p335899). However, you can achieve something similar by editing the file `~/.config/kwinrc` adding `BorderlessMaximizedWindows=true` in the `[Windows]` section.

#### Thumbnail generation

To allow thumbnail generation for media or document files on the desktop and in Dolphin, install [kdegraphics-thumbnailers](https://www.archlinux.org/packages/?name=kdegraphics-thumbnailers) and [ffmpegthumbs](https://www.archlinux.org/packages/?name=ffmpegthumbs).

Then enable the thumbnail categories for the desktop via *right click* on the *desktop background* > *Configure Desktop* > *Icons* > *Configure Preview Plugins...*.

In *Dolphin*, navigate to *Control* > *Configure Dolphin...* > *General* > *Previews*.

### Printing

**Tip:** Use the [CUPS](/index.php/CUPS "CUPS") web interface for faster configuration. Printers configured in this way can be used in KDE applications.

You can also configure printers in *System Settings > Printers*. To use this method, you must first install [print-manager](https://www.archlinux.org/packages/?name=print-manager) and [cups](https://www.archlinux.org/packages/?name=cups). See [CUPS#Configuration](/index.php/CUPS#Configuration "CUPS").

### Samba/Windows support

If you want to have access to Windows services, install [Samba](/index.php/Samba "Samba") (package [samba](https://www.archlinux.org/packages/?name=samba)).

The Dolphin share functionality requires the package [kdenetwork-filesharing](https://www.archlinux.org/packages/?name=kdenetwork-filesharing) and usershares, which the stock `smb.conf` does not have enabled. Instructions to add them are in [Samba#Enable Usershares](/index.php/Samba#Enable_Usershares "Samba"), after which sharing in Dolphin should work out of the box after restarting Samba.

**Tip:** Use `*` (asterisk) for both username and password when accessing a Windows share without authentication in Dolphin's prompt.

Unlike GTK file browsers which utilize GVfs also for the launched program, opening files from Samba shares in Dolphin via KIO makes Plasma copy the whole file to the local system first with most programs (VLC is an exception). To workaround this, you can use a GTK based file browser like [thunar](https://www.archlinux.org/packages/?name=thunar) with [gvfs](https://www.archlinux.org/packages/?name=gvfs) and [gvfs-smb](https://www.archlinux.org/packages/?name=gvfs-smb) (and [gnome-keyring](https://www.archlinux.org/packages/?name=gnome-keyring) for saving login credentials) to access SMB shares in a more able way.

Another possibility is to [mount](/index.php/Mount "Mount") a Samba share via [cifs-utils](https://www.archlinux.org/packages/?name=cifs-utils) to make it look to Plasma like if the SMB share was just a normal local folder and thus can be accessed normally. See [Samba#Manual mounting](/index.php/Samba#Manual_mounting "Samba") and [Samba#Automatic mounting](/index.php/Samba#Automatic_mounting "Samba").

An GUI solution is available with [samba-mounter-git](https://aur.archlinux.org/packages/samba-mounter-git/), which offers basically the same functionality via an easy to use option located at *System Settings* > *Network Drivers*. However, it might break with new KDE Plasma versions.

### KDE Desktop activities

[KDE Desktop Activities](https://userbase.kde.org/Plasma#Activities) are special workspaces where you can select specific settings for each activity that apply only when you are using said activity.

### Power management

[Install](/index.php/Install "Install") [powerdevil](https://www.archlinux.org/packages/?name=powerdevil) for an integrated Plasma power managing service. This service offers additional power saving features, monitor brightness control (if supported) and battery reporting including peripheral devices.

An alternative package without [NetworkManager](/index.php/NetworkManager "NetworkManager") and [Bluez](/index.php/Bluez "Bluez") dependencies is provided by [powerdevil-light](https://aur.archlinux.org/packages/powerdevil-light/).

**Note:** Powerdevil may not [inhibit](/index.php/Power_management#Power_managers "Power management") all logind settings (such as the lid close action for laptops). In these cases, the logind setting itself will need to be changed - see [Power management#Power management with systemd](/index.php/Power_management#Power_management_with_systemd "Power management").

### Autostart

Plasma can autostart applications and run scripts on startup and shutdown. To autostart an application, navigate to *System Settings > Startup and Shutdown > Autostart* and add the program or shell script of your choice. For applications, a *.desktop* file will be created, for shell scripts, a symlink will be created.

**Note:**

*   Programs can be autostarted on login only, whilst shell scripts can also be run on shutdown or even before Plasma itself starts.
*   Shell scripts will only be run if they are marked [executable](/index.php/Executable "Executable").

*   Place [Desktop entries](/index.php/Desktop_entries "Desktop entries") (i.e. *.desktop* files) in the appropriate [XDG Autostart](/index.php/XDG_Autostart "XDG Autostart") directory.

*   Place or symlink shell scripts in one of the following directories:

	`~/.config/plasma-workspace/env/`

	for executing scripts at login before launching Plasma.

	`~/.config/autostart-scripts/`

	for executing scripts at login.

	`~/.config/plasma-workspace/shutdown/`

	for executing scripts when Plasma exits.

### Phonon

From [Wikipedia](https://en.wikipedia.org/wiki/Phonon_(software) "wikipedia:Phonon (software)"):

	Phonon is the multimedia API provided by KDE and is the standard abstraction for handling multimedia streams within KDE software and also used by several Qt applications.

	Phonon was originally created to allow KDE and Qt software to be independent of any single multimedia framework such as GStreamer or xine and to provide a stable API for a major version's lifetime.

Phonon is being widely used within KDE, for both audio (e.g., the System notifications or KDE audio apps) and video (e.g., the [Dolphin](/index.php/Dolphin "Dolphin") video thumbnails).

#### Which backend should I choose?

You can choose between backends based on [GStreamer](/index.php/GStreamer "GStreamer") and [VLC](/index.php/VLC "VLC") – each available in versions for Qt4 applications and Qt5 applications ([phonon-qt4-gstreamer](https://aur.archlinux.org/packages/phonon-qt4-gstreamer/), [phonon-qt5-gstreamer](https://www.archlinux.org/packages/?name=phonon-qt5-gstreamer) – [phonon-qt4-vlc](https://aur.archlinux.org/packages/phonon-qt4-vlc/), [phonon-qt5-vlc](https://www.archlinux.org/packages/?name=phonon-qt5-vlc)).

[Upstream prefers VLC](https://www.phoronix.com/scan.php?page=news_item&px=MTUwNDM) but prominent Linux distributions (Kubuntu and Fedora-KDE for example) prefer GStreamer because that allows them to easily leave out patented MPEG codecs from the default installation. Both backends have a slightly different [features set](https://community.kde.org/Phonon/FeatureMatrix). The Gstreamer backend has some optional codec dependency, install them as needed:

*   [gst-libav](https://www.archlinux.org/packages/?name=gst-libav) — Libav codecs.
*   [gst-plugins-good](https://www.archlinux.org/packages/?name=gst-plugins-good) — PulseAudio support and additional codecs.
*   [gst-plugins-ugly](https://www.archlinux.org/packages/?name=gst-plugins-ugly) — additional codecs.
*   [gst-plugins-bad](https://www.archlinux.org/packages/?name=gst-plugins-bad) — additional codecs.

In the past other backends were developed as well but are no longer maintained and their AUR packages have been deleted.

**Note:**

*   Multiple backends can be installed at once and prioritized via the *phononsettings* application.
*   According to the [KDE forums](https://forum.kde.org/viewtopic.php?f=250&t=126476&p=335080), the VLC backend lacks support for [ReplayGain](https://en.wikipedia.org/wiki/ReplayGain "wikipedia:ReplayGain").
*   If using the VLC backend, you may experience crashes every time Plasma wants to send you an audible warning and in quite a number of other cases as well [[5]](https://forum.kde.org/viewtopic.php?f=289&t=135956). A possible fix is to rebuild the VLC plugins cache:

 `# /usr/lib/vlc/vlc-cache-gen /usr/lib/vlc/plugins` 

## Applications

The KDE project provides a suite of applications that integrate with the Plasma desktop. See the [kde-applications](https://www.archlinux.org/groups/x86_64/kde-applications/) group for a full listing of the available applications. Also see [Category:KDE](/index.php/Category:KDE "Category:KDE") for related KDE application pages.

Aside from the programs provided in KDE Applications, there are many other applications available that can complement the Plasma desktop. Some of these are discussed below.

### System administration

#### Terminate Xorg server through KDE System Settings

Navigate to the submenu *System Settings > Input Devices > Keyboard > Advanced (tab) > "Key Sequence to kill the X server"* and ensure that the checkbox is ticked.

#### KCM

KCM stands for **KC**onfig **M**odule. KCMs can help you configure your system by providing interfaces in System Settings, or through the command line with *kcmshell5*.

*   **sddm-kcm** — KDE Config Module for [SDDM](/index.php/SDDM "SDDM").

	[https://cgit.kde.org/sddm-kcm.git](https://cgit.kde.org/sddm-kcm.git) || [sddm-kcm](https://www.archlinux.org/packages/?name=sddm-kcm)

*   **kde-gtk-config** — GTK2 and GTK3 Configurator for KDE.

	[https://cgit.kde.org/kde-gtk-config.git](https://cgit.kde.org/kde-gtk-config.git) || [kde-gtk-config](https://www.archlinux.org/packages/?name=kde-gtk-config)

*   **System policies** — Set of configuration modules which allows administrator to change [PolicyKit](/index.php/PolicyKit "PolicyKit") settings.

	[https://cgit.kde.org/polkit-kde-kcmodules-1.git](https://cgit.kde.org/polkit-kde-kcmodules-1.git) || [kcm-polkit-kde-git](https://aur.archlinux.org/packages/kcm-polkit-kde-git/)

*   **wacom tablet** — KDE GUI for the Wacom Linux Drivers.

	[https://www.linux-apps.com/p/1127862/](https://www.linux-apps.com/p/1127862/) || [kcm-wacomtablet](https://www.archlinux.org/packages/?name=kcm-wacomtablet)

*   **Kcmsystemd** — systemd control module for KDE.

	[https://github.com/rthomsen/kcmsystemd](https://github.com/rthomsen/kcmsystemd) || [systemd-kcm](https://aur.archlinux.org/packages/systemd-kcm/)

More KCMs can be found at [linux-apps.com](https://www.linux-apps.com/search?projectSearchText=KCM).

### Desktop search

KDE implements desktop search with a software called [Baloo](/index.php/Baloo "Baloo"), a file indexing and searching solution.

### Web browsers

The following web browsers can integrate with Plasma:

*   **[Konqueror](https://en.wikipedia.org/wiki/Konqueror "wikipedia:Konqueror")** — Part of the KDE project, supports two rendering engines – KHTML and the [Chromium](/index.php/Chromium "Chromium")-based Qt WebEngine.

	[https://konqueror.org/](https://konqueror.org/) || [konqueror](https://www.archlinux.org/packages/?name=konqueror)

*   **[Falkon](https://en.wikipedia.org/wiki/Falkon "wikipedia:Falkon")** — A Qt web browser with Plasma integration features, previously known as Qupzilla. It uses Qt WebEngine.

	[https://userbase.kde.org/Falkon/](https://userbase.kde.org/Falkon/) || [falkon](https://www.archlinux.org/packages/?name=falkon)

*   **[Chromium](/index.php/Chromium "Chromium")** — Chromium and its proprietary variant Google Chrome have limited Plasma integration. [They can use KWallet](/index.php/KDE_Wallet#KDE_Wallet_for_Chrome_and_Chromium "KDE Wallet") and KDE Open/Save windows.

	[https://www.chromium.org/](https://www.chromium.org/) || [chromium](https://www.archlinux.org/packages/?name=chromium)

*   **[Firefox](/index.php/Firefox "Firefox")** — Firefox can be configured to better integrate with Plasma. See [Firefox KDE integration](/index.php/Firefox#KDE/GNOME_integration "Firefox") for details.

	[https://mozilla.org/firefox](https://mozilla.org/firefox) || [firefox](https://www.archlinux.org/packages/?name=firefox)

**Tip:** Starting from Plasma 5.13, one can integrate [Firefox](/index.php/Firefox "Firefox") or [Chrome](/index.php/Chrome "Chrome") with Plasma: providing media playback control from the Plasma tray, download notifications and find open tabs in KRunner. [Install](/index.php/Install "Install") [plasma-browser-integration](https://www.archlinux.org/packages/?name=plasma-browser-integration) and the corresponding browser add-on. Chrome/Chromium support should already be included, for Firefox add-on see [Firefox#KDE/GNOME integration](/index.php/Firefox#KDE/GNOME_integration "Firefox").

### PIM

KDE offers its own stack for [personal information management](https://en.wikipedia.org/wiki/Personal_information_management "wikipedia:Personal information management") (PIM). This includes emails, contacts, calendar, etc. To install all the PIM packages, you could use the [kdepim](https://www.archlinux.org/groups/x86_64/kdepim/) package group or the [kdepim-meta](https://www.archlinux.org/packages/?name=kdepim-meta) meta package.

#### Akonadi

Akonadi is a system meant to act as a local cache for PIM data, regardless of its origin, which can be then used by other applications. This includes the user's emails, contacts, calendars, events, journals, alarms, notes, and so on. Akonadi does not store any data by itself: the storage format depends on the nature of the data (for example, contacts may be stored in vCard format).

Install [akonadi](https://www.archlinux.org/packages/?name=akonadi). For additional addons, install [kdepim-addons](https://www.archlinux.org/packages/?name=kdepim-addons).

**Note:** If you wish to use a database engine other than [MariaDB](/index.php/MariaDB "MariaDB"), then when installing the [akonadi](https://www.archlinux.org/packages/?name=akonadi) package, use the following command to skip installing the [mariadb](https://www.archlinux.org/packages/?name=mariadb) dependencies:
```
# pacman -S akonadi --assume-installed mariadb

```

See also [FS#32878](https://bugs.archlinux.org/task/32878).

##### MySQL

By default Akonadi will use `/usr/bin/mysqld` ([MariaDB](/index.php/MariaDB "MariaDB") by default, see [MySQL](/index.php/MySQL "MySQL") for alternative providers) to run a managed MySQL instance with the database stored in `~/.local/share/akonadi/db_data/`.

###### System-wide MySQL instance

Akonadi supports using the system-wide [MySQL](/index.php/MySQL "MySQL") for its database.[[6]](https://techbase.kde.org/KDE_PIM/Akonadi#Can_Akonadi_use_a_normal_MySQL_server_running_on_my_system.3F)

 `~/.config/akonadi/akonadiserverrc` 
```
[%General]
Driver=QMYSQL

[QMYSQL]
Host=
Name=akonadi_*username*
Options="UNIX_SOCKET=/run/mysqld/mysqld.sock"
StartServer=false
```

##### PostgreSQL

Akonadi supports either using the existing system-wide [PostgreSQL](/index.php/PostgreSQL "PostgreSQL") instance, i.e. `postgresql.service`, or running a PostgreSQL instance with user privileges and the database in `~/.local/share/akonadi/db_data/`.

###### Per-user PostgreSQL instance

[Install](/index.php/Install "Install") [postgresql](https://www.archlinux.org/packages/?name=postgresql) and [postgresql-old-upgrade](https://www.archlinux.org/packages/?name=postgresql-old-upgrade).

Edit Akonadi configuration file so that it has the following contents:

 `~/.config/akonadi/akonadiserverrc` 
```
[%General]
Driver=QPSQL
```

**Note:**

*   When Akonadi starts, it will create the `[QPSQL]` section and set the appropriate variables in it.
*   The database will be stored in `~/.local/share/akonadi/db_data/`.

Start Akonadi with `akonadictl start`, and check its status: `akonadictl status`.

**Note:**

*   Starting with [akonadi](https://www.archlinux.org/packages/?name=akonadi) 19.08.0-1 the PostgreSQL database cluster in `~/.local/share/akonadi/db_data/` will get automatically upgraded when a major PostgreSQL version upgrade is detected.
*   For previous [akonadi](https://www.archlinux.org/packages/?name=akonadi) versions major PostgreSQL version upgrades will require a manual database upgrade. Follow the [update instructions on KDE UserBase Wiki](https://userbase.kde.org/Akonadi/Postgres_update). Make sure to adjust the paths to PostgreSQL binaries to those used by [postgresql](https://www.archlinux.org/packages/?name=postgresql) and [postgresql-old-upgrade](https://www.archlinux.org/packages/?name=postgresql-old-upgrade), see [PostgreSQL#Upgrading PostgreSQL](/index.php/PostgreSQL#Upgrading_PostgreSQL "PostgreSQL").

###### System-wide PostgreSQL instance

This requires an already configured and running [PostgreSQL](/index.php/PostgreSQL "PostgreSQL").

Create a PostgreSQL user account for your user:

```
[postgres]$ createuser *username*

```

Create a database for Akonadi:

```
[postgres]$ createdb -O *username* --locale=en_US.UTF-8 -T template0 akonadi-*username*

```

Configure Akonadi to use the system-wide PostgreSQL:

 `~/.config/akonadi/akonadiserverrc` 
```
[%General]
Driver=QPSQL

[QPSQL]
Host=/run/postgresql
Name=akonadi-*username*
StartServer=false
```

**Note:** Custom port, username and password can be specified with options `Port=`, `User=`, `Password=` in the `[QPSQL]` section.

Start Akonadi with `akonadictl start`, and check its status: `akonadictl status`.

##### SQLite

To use [SQLite](/index.php/SQLite "SQLite") edit Akonadi configuration file to match the configuration below:

 `~/.config/akonadi/akonadiserverrc` 
```
[%General]
Driver=QSQLITE3
```

**Note:**

*   When Akonadi starts, it will create the `[QSQLITE3]` section and set the appropriate variables in it.
*   The database will be stored as `~/.local/share/akonadi/akonadi.db`.

##### Disabling Akonadi

See this [section in the KDE userbase](https://userbase.kde.org/Akonadi#Disabling_the_Akonadi_subsystem).

### KDE Telepathy

[KDE Telepathy](https://community.kde.org/KTp) is a project with the goal to closely integrate Instant Messaging with the KDE desktop. It utilizes the Telepathy framework as a backend and is intended to replace Kopete.

To install all Telepathy protocols, install the [telepathy](https://www.archlinux.org/groups/x86_64/telepathy/) group. To use the KDE Telepathy client, install the [telepathy-kde-meta](https://www.archlinux.org/packages/?name=telepathy-kde-meta) package that includes all the packages contained in the [telepathy-kde](https://www.archlinux.org/groups/x86_64/telepathy-kde/) group.

#### Use Telegram with KDE Telepathy

[Telegram](/index.php/Telegram "Telegram") protocol is available using [telepathy-haze](https://www.archlinux.org/packages/?name=telepathy-haze), installing [telegram-purple](https://aur.archlinux.org/packages/telegram-purple/) or [telegram-purple-git](https://aur.archlinux.org/packages/telegram-purple-git/) and [telepathy-morse-git](https://aur.archlinux.org/packages/telepathy-morse-git/). The username is the Telegram account telephone number (complete with the national prefix `+*xx*`, e.g. `+49` for Germany).

The configuration through the GUI may be tricky: if the phone number is not accepted when configuring a new account in the KDE Telepathy client (with an error message complaining about an invalid parameter which prevents the account creation), insert it between single quotes and then remove the quotes manually from the configuration file (`~/.local/share/telepathy/mission-control/accounts.cfg`) after the account creation (if the quotes are not removed after, an authentication error should rise).

**Note:** The configuration file should be edited manually when KDE Telepathy is not running, e.g. when there is no KDE desktop session active, otherwise manual changes may be overwritten by the software.

### KDE Connect

[KDE Connect](https://community.kde.org/KDEConnect) provides several features to connect your [Android](/index.php/Android "Android") phone with your Linux desktop:

*   Share files and URLs to/from KDE from/to any app, without wires.
*   Touchpad emulation: Use your phone screen as your computer's touchpad.
*   Notifications sync (4.3+): Read your Android notifications from the desktop.
*   Shared clipboard: copy and paste between your phone and your computer.
*   Multimedia remote control: Use your phone as a remote for Linux media players.
*   WiFi connection: no usb wire or bluetooth needed.
*   RSA Encryption: your information is safe.

You will need to install KDE Connect both on your computer and on your Android. For PC side, [install](/index.php/Install "Install") [kdeconnect](https://www.archlinux.org/packages/?name=kdeconnect) package. For Android side, install KDE Connect from [Google Play](https://play.google.com/store/apps/details?id=org.kde.kdeconnect_tp) or from [F-Droid](https://f-droid.org/packages/org.kde.kdeconnect_tp/). If you want to browse your phone's filesystem, you need to [install](/index.php/Install "Install") [sshfs](https://www.archlinux.org/packages/?name=sshfs) as well and configure filesystem exposes in your Android app.

It is possible to use KDE Connect even if you do not use the Plasma desktop. For desktop environments that use AppIndicators, such as Unity, install [indicator-kdeconnect](https://aur.archlinux.org/packages/indicator-kdeconnect/) package as well. For GNOME users, better integration can be achieved by installing [gnome-shell-extension-gsconnect](https://aur.archlinux.org/packages/gnome-shell-extension-gsconnect/) instead of [kdeconnect](https://www.archlinux.org/packages/?name=kdeconnect). To start the KDE Connect daemon manually, execute `/usr/lib/kdeconnectd`.

If you use a [firewall](/index.php/Firewall "Firewall"), you need to open UDP and TCP ports `1714` through `1764`. See [https://community.kde.org/KDEConnect#Troubleshooting](https://community.kde.org/KDEConnect#Troubleshooting).

## Tips and tricks

### Use a different window manager

The component chooser settings in Plasma does not allow changing the window manager anymore. [[7]](https://github.com/KDE/plasma-desktop/commit/2f83a4434a888cd17b03af1f9925cbb054256ade) In order to change the window manager used you need to set the `KDEWM` [environment variable](/index.php/Environment_variable "Environment variable") before KDE startup. [[8]](https://wiki.haskell.org/Xmonad/Using_xmonad_in_KDE) To do that you can create a script called `set_window_manager.sh` in `~/.config/plasma-workspace/env/` and export the `KDEWM` variable there. For example to use the i3 window manager :

 `~/.config/plasma-workspace/env/set_window_manager.sh`  `export KDEWM=/usr/bin/i3` 

And then make it executable :

 `$ chmod +x ~/.config/plasma-workspace/env/set_window_manager.sh` 
**Note:** When using i3 window manager with Plasma, it may be necessary to manually set dialogs to open in floating mode in order for them to correctly appear. For more information, see [I3#Correct handling of floating dialogs](/index.php/I3#Correct_handling_of_floating_dialogs "I3").

#### KDE/Openbox session

The [openbox](https://www.archlinux.org/packages/?name=openbox) package provides a session for using KDE with [Openbox](/index.php/Openbox "Openbox"). To make use of this session, select *KDE/Openbox* from the [display manager](/index.php/Display_manager "Display manager") menu.

For those starting the session manually, add the following line to your [xinit](/index.php/Xinit "Xinit") configuration:

 `~/.xinitrc` 
```
exec openbox-kde-session

```

#### Re-enabling compositing effects

When replacing Kwin with a window manager which does not provide a Compositor (such as Openbox), any desktop compositing effects e.g. transparency will be lost. In this case, install and run a separate Composite manager to provide the effects such as [Xcompmgr](/index.php/Xcompmgr "Xcompmgr") or [Compton](/index.php/Compton "Compton").

### Configuring monitor resolution / multiple monitors

To enable display resolution management and multiple monitors in Plasma, install [kscreen](https://www.archlinux.org/packages/?name=kscreen). This provides additional options to *System Settings > Display and Monitor*.

### KWin-lowlatency

[KWin-lowlatency](https://github.com/tildearrow/kwin-lowlatency) is a attempt to reduce latency and stuttering in the popular KWin compositor and is available as [kwin-lowlatency](https://aur.archlinux.org/packages/kwin-lowlatency/).

### Configuring ICC profiles

To enable [ICC profiles](/index.php/ICC_profiles "ICC profiles") in Plasma, [install](/index.php/Install "Install") [colord-kde](https://www.archlinux.org/packages/?name=colord-kde). This provides additional options to *System Settings > Color Corrections*.

ICC profiles can be imported using *Add Profile*.

### Disable opening application launcher with Super key (Windows key)

To disable this feature you currently can run the following command:

```
$ kwriteconfig5 --file kwinrc --group ModifierOnlyShortcuts --key Meta ""

```

### Disable bookmarks showing in application menu

With Plasma Browser integration installed, KDE will show bookmarks in the application launcher.

To disable this feature you currently can run the following commands:

```
$ mkdir ~/.local/share/kservices5
$ sed 's/EnabledByDefault=true$/EnabledByDefault=false/' /usr/share/kservices5/plasma-runner-bookmarks.desktop > ~/.local/share/kservices5/plasma-runner-bookmarks.desktop

```

## Troubleshooting

### Fonts

#### Fonts in a Plasma session look poor

Try installing the [ttf-dejavu](https://www.archlinux.org/packages/?name=ttf-dejavu) and [ttf-liberation](https://www.archlinux.org/packages/?name=ttf-liberation) packages.

After the installation, be sure to log out and back in. You should not have to modify anything in *System Settings > Fonts*. If you are using [qt5ct](https://www.archlinux.org/packages/?name=qt5ct), the settings in Qt5 Configuration Tool may override the font settings in System Settings.

If you have personally set up how your [Fonts](/index.php/Fonts "Fonts") render, be aware that System Settings may alter their appearance. When you go *System Settings > Fonts* System Settings will likely alter your font configuration file (`fonts.conf`).

There is no way to prevent this, but, if you set the values to match your `fonts.conf` file, the expected font rendering will return (it will require you to restart your application or in a few cases restart your desktop). Note that Gnome's Font Preferences also does this.

#### Fonts are huge or seem disproportional

Try to force font DPI to `**96**` in *System Settings > Fonts*.

If that does not work, try setting the DPI directly in your Xorg configuration as documented in [Xorg#Setting DPI manually](/index.php/Xorg#Setting_DPI_manually "Xorg").

### Configuration related

Many problems in KDE are related to its configuration.

#### Plasma desktop behaves strangely

Plasma problems are usually caused by unstable *Plasma widgets* (colloquially called *plasmoids*) or *Plasma themes*. First, find which was the last widget or theme you had installed and disable or uninstall it.

So, if your desktop suddenly exhibits "locking up", this is likely caused by a faulty installed widget. If you cannot remember which widget you installed before the problem began (sometimes it can be an irregular problem), try to track it down by removing each widget until the problem ceases. Then you can uninstall the widget, and file a bug report on the [KDE bug tracker](https://bugs.kde.org/) **only if it is an official widget**. If it is not, it is recommended to find the entry on the [KDE Store](https://store.kde.org/) and inform the developer of that widget about the problem (detailing steps to reproduce, etc.).

If you cannot find the problem, but you do not want *all* the settings to be lost, navigate to `~/.config/` and run the following command:

```
$ for j in plasma*; do mv -- "$j" "${j%}.bak"; done

```

This command will rename **all** Plasma related configuration files to **.bak* (e.g. `plasmarc.bak`) of your user and when you will relogin into Plasma, you will have the default settings back. To undo that action, remove the *.bak* file extension. If you already have **.bak* files, rename, move, or delete them first. It is highly recommended that you create regular backups anyway. See [Synchronization and backup programs](/index.php/Synchronization_and_backup_programs "Synchronization and backup programs") for a list of possible solutions.

#### Clean cache to resolve upgrade problems

The [problem](https://bbs.archlinux.org/viewtopic.php?id=135301) may be caused by old cache. Sometimes, after an upgrade, the old cache might introduce strange, hard to debug behaviour such as unkillable shells, hangs when changing various settings, Ark being unable to extract archives or Amarok not recognizing any of your music. This solution can also resolve problems with KDE and Qt applications looking bad after an update.

Rebuild the cache using the following commands:

```
$ rm ~/.config/Trolltech.conf
$ kbuildsycoca5 --noincremental

```

Optionally, empty the `~/.cache/` folder contents, however, this will also clear the cache of other applications:

```
$ rm -rf ~/.cache/*

```

#### Volume control, notifications or multimedia keys do not work

Hiding certain items in the System Tray settings (e.g. Audio Volume, Media Player or Notifications) also disables related features. Hiding the *Audio Volume* disables volume control keys, *Media Player* disables multimedia keys (rewind, stop, pause) and hiding *Notifications* disables showing notifications.

#### Login Screen KCM does not sync cursor settings to SDDM

The Login Screen KCM reads your cursor settings from `~/.config/kcminputrc`, without this file no settings are synced. The easiest way to generate this file is to change your cursor theme in *System Settings > Cursors*, then change it back to your preferred cursor theme.

### Graphical problems

Make sure you have the proper driver for your GPU installed. See [Xorg#Driver installation](/index.php/Xorg#Driver_installation "Xorg") for more information. If you have an older card, it might help to [#Disable desktop effects manually or automatically for defined applications](#Disable_desktop_effects_manually_or_automatically_for_defined_applications) or [#Disable compositing](#Disable_compositing).

#### Getting current state of KWin for support and debug purposes

This command prints out a summary of the current state of KWin including used options, used compositing backend and relevant OpenGL driver capabilities. See more on [Martin's blog](https://blog.martin-graesslin.com/blog/2012/03/on-getting-help-for-kwin-and-helping-kwin/).

```
$ qdbus org.kde.KWin /KWin supportInformation

```

#### Disable desktop effects manually or automatically for defined applications

Plasma has desktop effects enabled by default and e.g. not every game will disable them automatically. You can disable desktop effects in *System Settings > Desktop Behavior > Desktop Effects* and you can toggle desktop effects with `Alt+Shift+F12`.

Additionally, you can create custom KWin rules to automatically disable/enable compositing when a certain application/window starts under *System Settings > Window Management > Window Rules*.

#### Enable transparency

If you use a transparent background without enabling the compositor, you will get the message:

```
This color scheme uses a transparent background which does not appear to be supported on your desktop

```

In *System Settings > Display and Monitor > Compositor*, check *Enable compositor on startup* and restart Plasma.

#### Disable compositing

In *System Settings > Display and Monitor > Compositor*, uncheck *Enable compositor on startup* and restart Plasma.

#### Flickering in fullscreen when compositing is enabled

In *System Settings > Display and Monitor > Compositor*, uncheck *Allow applications to block compositing*. This may harm performance.

#### Screen tearing with NVIDIA

See [NVIDIA/Troubleshooting#Avoid screen tearing in KDE (KWin)](/index.php/NVIDIA/Troubleshooting#Avoid_screen_tearing_in_KDE_(KWin) "NVIDIA/Troubleshooting").

#### Plasma cursor sometimes shown incorrectly

Create the directory `~/.icons/default` and inside a file named `index.theme` with the following contents:

 `~/.icons/default/index.theme` 
```
[Icon Theme]
Inherits=breeze_cursors
```

Execute the following command:

```
$ ln -s /usr/share/icons/breeze_cursors/cursors ~/.icons/default/cursors

```

#### Unusable screen resolution set

Your local configuration settings for kscreen can override those set in `xorg.conf`. Look for kscreen configuration files in `~/.local/share/kscreen/` and check if mode is being set to a resolution that is not supported by your monitor.

#### Blurry icons in System tray

In order to add icons to tray, applications often make use of the library appindicator. If your icons are blurry, check which version of libappindicator you have installed. If you only have [libappindicator-gtk2](https://www.archlinux.org/packages/?name=libappindicator-gtk2) installed, you can install [libappindicator-gtk3](https://www.archlinux.org/packages/?name=libappindicator-gtk3) or [libappindicator-sharp](https://www.archlinux.org/packages/?name=libappindicator-sharp) as an attempt to get clear icons.

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

#### MP3 files cannot be played when using the GStreamer Phonon backend

This can be solved by installing the GStreamer libav plugin (package [gst-libav](https://www.archlinux.org/packages/?name=gst-libav)). If you still encounter problems, you can try changing the Phonon backend used by installing another such as [phonon-qt4-vlc](https://aur.archlinux.org/packages/phonon-qt4-vlc/) or [phonon-qt5-vlc](https://www.archlinux.org/packages/?name=phonon-qt5-vlc).

Then, make sure the backend is preferred via *System Settings > Multimedia > Audio and Video > Backend*.

### Power management

#### No Suspend/Hibernate options

If your system is able to suspend or hibernate using [systemd](/index.php/Systemd "Systemd") but do not have these options shown in KDE, make sure [powerdevil](https://www.archlinux.org/packages/?name=powerdevil) is installed.

### KMail

#### Clean Akonadi configuration to fix KMail

See [this](https://docs.kde.org/trunk5/en/pim/kmail2/clean-start-after-a-failed-migration.html) document for detail.

If you want a backup, copy the following configuration directories:

```
$ cp -a ~/.local/share/akonadi ~/.local/share/akonadi-old
$ cp -a ~/.config/akonadi ~/.config/akonadi-old

```

#### Empty IMAP inbox in KMail

For some IMAP accounts KMail will show the inbox as a top-level container (so it will not be possible to read messages there) with all other folders of this account inside.[[9]](https://bugs.kde.org/show_bug.cgi?id=284172). To solve this problem simply disable the server-side subscriptions in the KMail account settings.

#### Authorization error for EWS account in KMail

While setting up EWS account in KMail, you may keep getting errors about failed authorization even for valid and fully working credentials. This is likely caused by broken communication between [KWallet](/index.php/KWallet "KWallet") and KMail. To workaround the issue set a passsword via qdbus:

```
$ qdbus org.freedesktop.Akonadi.Resource.akonadi_ews_resource_0 /Settings org.kde.Akonadi.Ews.Wallet.setPassword "XXX"

```

### Networking

#### Freezes when using Automount on a NFS volume

Using [Fstab#Automount with systemd](/index.php/Fstab#Automount_with_systemd "Fstab") on a [NFS](/index.php/NFS "NFS") volume may cause freezes, see [bug report upstream](https://bugs.kde.org/show_bug.cgi?id=354137).

### Aggressive QXcbConnection journal logging

See [Qt#Disable/Change Qt journal logging behaviour](/index.php/Qt#Disable/Change_Qt_journal_logging_behaviour "Qt").

### KF5/Qt 5 applications do not display icons in i3/FVWM/awesome

See [Qt#Configuration of Qt5 apps under environments other than KDE Plasma](/index.php/Qt#Configuration_of_Qt5_apps_under_environments_other_than_KDE_Plasma "Qt").

### Problems with saving credentials and persistently occurring KWallet dialogs

It is not recommended to turn off the [KWallet](/index.php/KWallet "KWallet") password saving system in the user settings as it is required to save encrypted credentials like WiFi passphrases for each user. Persistently occuring KWallet dialogs can be the consequence of turning it off.

In case you find the dialogs to unlock the wallet annoying when applications want to access it, you can let the [display managers](/index.php/Display_manager "Display manager") [SDDM](/index.php/SDDM "SDDM") and [LightDM](/index.php/LightDM "LightDM") unlock the wallet at login automatically, see [KDE Wallet#Unlock KDE Wallet automatically on login](/index.php/KDE_Wallet#Unlock_KDE_Wallet_automatically_on_login "KDE Wallet"). The first wallet needs to be generated by KWallet (and not user-generated) in order to be usable for system program credentials.

In case you want the wallet credentials not to be opened in memory for every application, you can restrict applications from accessing it with [kwalletmanager](https://www.archlinux.org/packages/?name=kwalletmanager) in the KWallet settings.

If you do not care for credential encryption at all, you can simply leave the password forms blank when KWallet asks for the password while creating a wallet. In this case, applications can access passwords without having to unlock the wallet first.

### Discover does not show any applications

This can be solved by installing [packagekit-qt5](https://www.archlinux.org/packages/?name=packagekit-qt5).

### High CPU usage of kscreenlocker_greet with NVIDIA drivers

As described in [KDE Bug 347772](https://bugs.kde.org/show_bug.cgi?id=347772) NVIDIA OpenGL drivers and QML may not play well together with Qt 5\. This may lead `kscreenlocker_greet` to high CPU usage after unlocking the session. To work around this issue, set the `QSG_RENDERER_LOOP` [environment variable](/index.php/Environment_variable "Environment variable") to `basic`.

Then kill previous instances of the greeter with `killall kscreenlocker_greet`.

### OS error 22 when running Akonadi on ZFS

If your home directory is on a [ZFS](/index.php/ZFS "ZFS") pool, create a `~/.config/akonadi/mysql-local.conf` file with the following contents:

```
[mysqld]
innodb_use_native_aio = 0

```

See [MariaDB#OS error 22 when running on ZFS](/index.php/MariaDB#OS_error_22_when_running_on_ZFS "MariaDB").

### Some programs are unable to scroll when their windows are inactive

This is caused by the problematic way of GTK3 handling mouse scroll events. A workaround for this is to set [environment variable](/index.php/Environment_variable "Environment variable") `GDK_CORE_DEVICE_EVENTS=1`. However, this workaround also breaks touchpad smooth scrolling and touchscreen scrolling.

### TeamViewer behaves slowly

When using TeamViewer, it may behave slowly if you use smooth animations (such as windows minimizing). See [#Disable compositing](#Disable_compositing) as a workaround.

## See also

*   [KDE homepage](https://www.kde.org/)
*   [KDE news](https://dot.kde.org/)
*   [KDE Blogs](https://planet.kde.org/)
*   [KDE Forums](https://forum.kde.org/)
*   [KDE Wikis](https://wiki.kde.org/)
*   [KDE bug tracker and reporter](https://bugs.kde.org/)
*   [Martin Graesslin's blog](https://blog.martin-graesslin.com/blog/kategorien/kde/)