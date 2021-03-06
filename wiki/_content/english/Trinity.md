The [Trinity Desktop Environment](http://trinitydesktop.org/) (TDE) project is a fork of [KDE](/index.php/KDE "KDE") 3.5 aiming to retain the traditional desktop style.

TDE still depends on an old version of Qt, which they now maintain themselves, since it is deprecated. The Trinity applications and applets should also work with other desktop environments.

## Contents

*   [1 Install binary packages](#Install_binary_packages)
*   [2 Build from source](#Build_from_source)
*   [3 Building with Michael's PKGBUILD files](#Building_with_Michael's_PKGBUILD_files)
*   [4 Start and configuration](#Start_and_configuration)
    *   [4.1 Enable tdm.service in systemd to start tdm at boot](#Enable_tdm.service_in_systemd_to_start_tdm_at_boot)
    *   [4.2 Configure to work with startx](#Configure_to_work_with_startx)
*   [5 Trinity "Kicker" panel with other desktop environments](#Trinity_"Kicker"_panel_with_other_desktop_environments)
*   [6 See also](#See_also)

## Install binary packages

As of June 29, 2017 binary packages for 14.0.4 are on the NasuTek Contrib Repos. Only x86_64 is provided since i686 is being depreciated. See [Unofficial user repositories#trinity](/index.php/Unofficial_user_repositories#trinity "Unofficial user repositories") on how to connect to this repo.

## Build from source

[Michael's PKGBUILD repository](https://github.com/michael-manley/Trinity_ArchLinux_PKGBUILD) contains PKGBUILD files for most Trinity packages.

The sources are in a git repo. More info on cloning it is at their [GIT information](https://wiki.trinitydesktop.org/Project_GIT_Information#Using_GIT) page.

The suggested build order is specified in the [How to Build TDE](https://wiki.trinitydesktop.org/How_to_Build_TDE) page.

## Building with Michael's PKGBUILD files

**Note:** See [DeveloperWiki:Building in a clean chroot](/index.php/DeveloperWiki:Building_in_a_clean_chroot "DeveloperWiki:Building in a clean chroot") to build the packages in a chroot.

[Build](/index.php/Makepkg "Makepkg") the packages in the following order, for example:

```
#!/bin/sh
git clone https://github.com/michael-manley/Trinity_ArchLinux_PKGBUILD.git trinity
cd trinity/R14.0.4
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

## Trinity "Kicker" panel with other desktop environments

To use the Trinity "kicker" Desktop Panel and Applets with another desktop environment, create this script and make it [executable](/index.php/Executable "Executable"). For Plasma5, use *System Settings > Startup and Shutdown > Autostart > Add Script*.

```
#!/bin/bash
/opt/trinity/bin/tdeinit
/opt/trinity/bin/kicker
/opt/trinity/bin/tdebuildsycoca --noincremental

```

## See also

*   [TDE Git repositories](http://git.trinitydesktop.org/cgit/)
*   [TDE Bugzilla](http://bugs.trinitydesktop.org/)
*   [Mailing Lists](http://trinitydesktop.org/mailinglist.php)
*   [Developers Web](https://wiki.trinitydesktop.org/Category:Developers)
*   [QT and TQT Tutorials and Documentation](https://wiki.trinitydesktop.org/Category:Developers#Tutorials_and_Documentation_for_QT_and_TQT)
*   [How To Build](https://wiki.trinitydesktop.org/Category:Developers#Building_and_Distributing_Trinity)