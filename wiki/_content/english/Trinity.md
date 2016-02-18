The [Trinity Desktop Environment](http://trinitydesktop.org/) (TDE) project is a feature rich desktop environment for Unix-like operating systems with a primary goal of retaining the overall KDE 3.5 computing style. TDE is a fast, stable and mature desktop for Linux.

## Contents

*   [1 About TDE](#About_TDE)
*   [2 Build from source](#Build_from_source)
    *   [2.1 Building on Arch](#Building_on_Arch)
*   [3 Start and configuration](#Start_and_configuration)
    *   [3.1 Enable tdm.service in systemd to start tdm at boot](#Enable_tdm.service_in_systemd_to_start_tdm_at_boot)
    *   [3.2 Configure to work with startx](#Configure_to_work_with_startx)
*   [4 See also](#See_also)

## About TDE

The current stable release of TDE (14.0.0) was released December 16 2014\. Current development is on 14.1.0\.

Trinity is an independent fork of KDE 3.5 using a separate developer community. Continued development by the Trinity Project has polished off many rough edges that were present in the final release of KDE 3.5.10\. Many new and useful features have been added to keep the environment up-to-date.

R14 is intended to be a true TDE release with all branding, artwork, and graphics changed and updated for this project rather than using holdover KDE3 stock images. The significant improvements and changes to the R14 codebase have been backported to 3.5.13-sru. The desktop functions on current graphics libs, systemd, libusbx, udisk2 and other newly implemented hardware paradigms.

## Build from source

As of July, 2015, there are no Arch LInux Trinity packages, so you will need to create your own. See [Creating packages](/index.php/Creating_packages "Creating packages") for more information on how to create Arch packages.

To download the R14 source tarballs, follow the Download Source Tarballs link near the bottom of the [Trinity R14.0.0 Release](https://www.trinitydesktop.org/releases/R14.0.0/) page.

The sources are in a git repo. More info on cloning it is at their [GIT information](https://wiki.trinitydesktop.org/Project_GIT_Information#Using_GIT) page.

The suggested build order is specified in the [How to Build TDE](https://wiki.trinitydesktop.org/How_to_Build_TDE) page.

### Building on Arch

**Warning:** Trinity on Arch must be built in a clean environment without [KDE4](/index.php/KDE4 "KDE4") present.

Set up your chroot for building by referencing [DeveloperWiki:Building in a Clean Chroot](/index.php/DeveloperWiki:Building_in_a_Clean_Chroot "DeveloperWiki:Building in a Clean Chroot"). Make sure you configure your `local` repository in `$CHROOT/root/repo` and add each package built to the repository as outlined in the [DeveloperWiki](/index.php/DeveloperWiki "DeveloperWiki").

 `Example` 
```
 # mkarchroot -u $CHROOT/root
 # makechrootpkg -c -r $CHROOT
 # makechrootpkg -r $CHROOT    

```

Which means respectively:

1.  update the chroot
2.  build first package with the -c option
3.  build remaining packages without update

## Start and configuration

After a successful install of TDE, the tdm desktop manager can be used to start TDE (and all other desktops) in the same manner kdm is used to start KDE Plasma. The init script for the display manager has been renamed from `kdm` to `tdm` to avoid conflicts. TDE includes a tdm.service file allowing systemd to start tdm at boot. TDE can also be started from the command line by including the path to starttde in your ~/.xinitrc. Either way launching tdm or TDE is straightforward.

### Enable tdm.service in systemd to start tdm at boot

If systemd is configured to boot the default `multi-user.target` (default), all that is required is to configure tdm to start at boot is to [enable](/index.php/Enable "Enable") `tdm.service`.

If you encounter any problem, the `default.target` may have manually configured. See [Display manager#Loading the display manager](/index.php/Display_manager#Loading_the_display_manager "Display manager") for resolution.

### Configure to work with startx

Trinity provides a normal `starttde`. If you've followed the Arch packaging guidelines, it will be in `/usr/bin`. The easiest way to start Trinity is to simply add `starttde` at the end of `~/.xinitrc`. If you do not presently have `~/.xinitrc`, then simply copy it from `/etc/skel` or create it with the following entry:

 `~/.xinitrc`  `exec starttde` 

Then from the command line, just type `startx`. More about [xinitrc](/index.php/Xinitrc "Xinitrc").

## See also

*   Getting Involved with Trinity Development [https://trinitydesktop.org/helpwanted.php](https://trinitydesktop.org/helpwanted.php)
*   Main Project Site: [http://trinitydesktop.org](http://trinitydesktop.org/)
*   TDE GIT Repository: [http://git.trinitydesktop.org/cgit/](http://git.trinitydesktop.org/cgit/)
*   Bug Reporting: [http://bugs.trinitydesktop.org](http://bugs.trinitydesktop.org/)
*   Mailing Lists: [http://trinitydesktop.org/mailinglist.php](http://trinitydesktop.org/mailinglist.php)
*   Developers Web: [https://wiki.trinitydesktop.org/Category:Developers](https://wiki.trinitydesktop.org/Category:Developers)
*   QT and TQT Tutorials and Documentation: [https://wiki.trinitydesktop.org/Category:Developers#Tutorials_and_Documentation_for_QT_and_TQT](https://wiki.trinitydesktop.org/Category:Developers#Tutorials_and_Documentation_for_QT_and_TQT)
*   How To Build: [https://wiki.trinitydesktop.org/Category:Developers#Building_and_Distributing_Trinity](https://wiki.trinitydesktop.org/Category:Developers#Building_and_Distributing_Trinity)