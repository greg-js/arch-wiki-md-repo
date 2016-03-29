**Note:** Currently the base Trinity packages can be built and installed on Arch using the PKGBUILD files on [https://github.com/michael-manley/Trinity_ArchLinux_PKGBUILD](https://github.com/michael-manley/Trinity_ArchLinux_PKGBUILD). Most components seem to work fine except arts is a bit bugged (least on VMWare) but is a work in progress. Binary packages are available for x86_64 at the moment but will provide i686 as built (See [Unofficial user repositories#trinity](/index.php/Unofficial_user_repositories#trinity "Unofficial user repositories")). You are all welcome to improve the PKGBUILD files.

**Note:** Michael's PKGBUILD files were added 2016 March 23, after a long time without any Trinity package repository being available. They seem to build successfully on a system with the [plasma](https://www.archlinux.org/groups/x86_64/plasma/) package group installed, despite the warning below about building without [KDE4](/index.php/KDE4 "KDE4") being present. Michael's PKGBUILD files include the ten "required" Trinity core packages described in [How_to_Build_TDE_Core_Modules#Suggested_Build_Order](https://wiki.trinitydesktop.org/How_to_Build_TDE_Core_Modules#Suggested_Build_Order), and also tdeaccessibility, tdebindings, and tdeutils. Please contribute additional Trinity core package PKGBUILD files if you are able. Also note, these Trinity applications and applets can be run just fine under other Desktop Environments, including KDE Plasma5.

The [Trinity Desktop Environment](http://trinitydesktop.org/) (TDE) project is a feature rich desktop environment for Unix-like operating systems with a primary goal of retaining the overall KDE 3.5 computing style. TDE is a fast, stable and mature desktop for Linux.

## Contents

*   [1 About TDE](#About_TDE)
*   [2 Build from source](#Build_from_source)
*   [3 Building with Michael's PKGBUILD files](#Building_with_Michael.27s_PKGBUILD_files)
*   [4 Start and configuration](#Start_and_configuration)
    *   [4.1 Enable tdm.service in systemd to start tdm at boot](#Enable_tdm.service_in_systemd_to_start_tdm_at_boot)
    *   [4.2 Configure to work with startx](#Configure_to_work_with_startx)
*   [5 Refusing to give up the Trinity "Kicker" panel](#Refusing_to_give_up_the_Trinity_.22Kicker.22_panel)
*   [6 See also](#See_also)

## About TDE

The current stable release of TDE (14.0.3) was released 2016 February 28\. Current development is on 14.1.0\.

Trinity is an independent fork of KDE 3.5 using a separate developer community. Continued development by the Trinity Project has polished off many rough edges that were present in the final release of KDE 3.5.10\. Many new and useful features have been added to keep the environment up-to-date.

R14 is intended to be a true TDE release with all branding, artwork, and graphics changed and updated for this project rather than using holdover KDE3 stock images. The significant improvements and changes to the R14 codebase have been backported to 3.5.13-sru. The desktop functions on current graphics libs, systemd, libusbx, udisk2 and other newly implemented hardware paradigms.

## Build from source

As of July, 2015, there are no Arch LInux Trinity packages, so you will need to create your own. See [Creating packages](/index.php/Creating_packages "Creating packages") for more information on how to create Arch packages.

To download the R14 source tarballs, follow the Download Source Tarballs link near the bottom of the [Trinity R14.0.0 Release](https://www.trinitydesktop.org/releases/R14.0.0/) page.

The sources are in a git repo. More info on cloning it is at their [GIT information](https://wiki.trinitydesktop.org/Project_GIT_Information#Using_GIT) page.

The suggested build order is specified in the [How to Build TDE](https://wiki.trinitydesktop.org/How_to_Build_TDE) page.

## Building with Michael's PKGBUILD files

**Note:** See [DeveloperWiki:Building in a Clean Chroot](/index.php/DeveloperWiki:Building_in_a_Clean_Chroot "DeveloperWiki:Building in a Clean Chroot") to build the packages in a chroot.

[Build](/index.php/Makepkg "Makepkg") the packages in the following order, for example:

```
#!/bin/sh
git clone https://github.com/michael-manley/Trinity_ArchLinux_PKGBUILD.git trinity
cd trinity/R14.0.3
dir=$PWD

for pkg in tqt3 tqtinterface arts dbus-tqt dbus-1-tqt tqca-tls libart-lgpl avahi-tqt tdelibs tdebase tdebindings tdeaccessibility tdeutils; do
  cd "$dir"/tde-"$pkg"
  makepkg -Lsci
done
```

In TDE R14.0.3, the tdebindings package will not build with the current [ruby](https://www.archlinux.org/packages/?name=ruby) 2.3 package installed on the system, or even with the [ruby2.2](https://aur.archlinux.org/packages/ruby2.2/) package, despite the [R14.0.3 Release Notes](https://wiki.trinitydesktop.org/Release_Notes_For_R14.0.3) claim to have "Added ruby 2.2 support". In particular `tdebindings/qtruby/rubylib/qtruby/Qt.cpp` seems to not be compatible with either package. Remove the ruby package while building tdebindings and re-install afterwards.

Then also, consider your preference for path ordering, whether `/opt/trinity/bin` should come before or after `/usr/bin`. This will give priority to one or the other of the KDE applications available through both Trinity and KDE/Plasma, if KDE/Plasma is also installed. The PATH environment variable may need to be modified in `~/.bash_profile` and/or `/etc/profile.d/trinity.sh`.

**Warning:** If Trinity is installed alongside another Qt-based Desktop Environment, such as [LXQt](/index.php/LXQt "LXQt") or [KDE](/index.php/KDE "KDE"), then move, modify, or in some way disable `/etc/profile.d/tqt3.sh` and `/etc/profile.d/trinity.sh`. Otherwise the alternative Desktop will fail horribly when the "QT" and "XDG" environment variables are redefined in these files!

Both these files can be selectively enabled by wrapping their content with:

```
if ps -C starttde,starttrinity &>/dev/null ;then
...
fi
```

## Start and configuration

After a successful install of TDE, the tdm desktop manager can be used to start TDE (and all other desktops) in the same manner kdm is used to start KDE Plasma. The init script for the display manager has been renamed from `kdm` to `tdm` to avoid conflicts. TDE includes a tdm.service file allowing systemd to start tdm at boot. TDE can also be started from the command line by including the path to starttde in your ~/.xinitrc. Either way launching tdm or TDE is straightforward.

### Enable tdm.service in systemd to start tdm at boot

If systemd is configured to boot the default `multi-user.target` (default), all that is required is to configure tdm to start at boot is to [enable](/index.php/Enable "Enable") `tdm.service`.

If you encounter any problem, the `default.target` may have manually configured. See [Display manager#Loading the display manager](/index.php/Display_manager#Loading_the_display_manager "Display manager") for resolution.

### Configure to work with startx

Trinity provides a normal `starttde`. If you've followed the Arch packaging guidelines, it will be in `/usr/bin`. The easiest way to start Trinity is to simply add `starttde` at the end of `~/.xinitrc`. If you do not presently have `~/.xinitrc`, then simply copy it from `/etc/skel` or create it with the following entry:

 `~/.xinitrc`  `exec starttde` 

Then from the command line, just type `startx`. More about [xinitrc](/index.php/Xinitrc "Xinitrc").

## Refusing to give up the Trinity "Kicker" panel

If you simply must have the Trinity "kicker" Desktop Panel and Applets while running Plasma5 or some other Desktop Environment, create this script and activate it. For Plasma5, use "System Settings -> Startup and Shutdown -> Autostart -> Add Script".

 `panelstart` 
```
#!/bin/bash
/opt/trinity/bin/tdeinit
/opt/trinity/bin/kicker
/opt/trinity/bin/tdebuildsycoca --noincremental

```

and

```
# chmod 755 panelstart

```

Yum!

## See also

*   Getting Involved with Trinity Development [https://trinitydesktop.org/helpwanted.php](https://trinitydesktop.org/helpwanted.php)
*   Main Project Site: [http://trinitydesktop.org](http://trinitydesktop.org/)
*   TDE GIT Repository: [http://git.trinitydesktop.org/cgit/](http://git.trinitydesktop.org/cgit/)
*   Bug Reporting: [http://bugs.trinitydesktop.org](http://bugs.trinitydesktop.org/)
*   Mailing Lists: [http://trinitydesktop.org/mailinglist.php](http://trinitydesktop.org/mailinglist.php)
*   Developers Web: [https://wiki.trinitydesktop.org/Category:Developers](https://wiki.trinitydesktop.org/Category:Developers)
*   QT and TQT Tutorials and Documentation: [https://wiki.trinitydesktop.org/Category:Developers#Tutorials_and_Documentation_for_QT_and_TQT](https://wiki.trinitydesktop.org/Category:Developers#Tutorials_and_Documentation_for_QT_and_TQT)
*   How To Build: [https://wiki.trinitydesktop.org/Category:Developers#Building_and_Distributing_Trinity](https://wiki.trinitydesktop.org/Category:Developers#Building_and_Distributing_Trinity)