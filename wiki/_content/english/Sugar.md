A product of the [OLPC](https://en.wikipedia.org/wiki/One_Laptop_per_Child is a Desktop Environment akin to [KDE](/index.php/KDE "KDE") and [GNOME](/index.php/GNOME "GNOME"), but geared towards children and education.

Sugar has a special [Taxonomy](http://wiki.sugarlabs.org/go/Taxonomy) to name the parts of its system. The graphical interface itself constitute the **Glucose** group. This is the core system can reasonably expect to be present when installing Sugar. But to really use the environment, you need activities (some sort of applications). Base activities are part of **Fructose**. Then, **Sucrose** is constituted by both Glucose and Fructose and represents what should be distributed as a basic sugar desktop environment. Extra activities are part of **Honey**. Note that Ribose (the underlaying operating system) is here replaced by Arch.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
    *   [1.1 From Activity Library](#From_Activity_Library)
*   [2 Starting Sugar](#Starting_Sugar)
*   [3 See also](#See_also)

## Installation

With the upcoming python2 deprecation, python3-based packages have been released in an AUR. Namely the packages *sugar* and *sugar3* distinguish between python2 and python3 packages. However, the user is free to choose between the two of them.

Python 3:

*   For the minimal requirements to run sugar3, consider installing all the four packages, viz., [sugar3](https://aur.archlinux.org/packages/sugar3/), [sugar3-toolkit-gtk3](https://aur.archlinux.org/packages/sugar3-toolkit-gtk3/), [sugar3-datastore](https://aur.archlinux.org/packages/sugar3-datastore/), [sugar3-artwork](https://aur.archlinux.org/packages/sugar3-artwork/)
*   The Sugar Python3 Activities have not been added to the sugar3 repository. You can request it at [[sugar-arch-repository](https://github.com/srevinsaju/sugar-arch)]
*   For using sugar-runner on arch, install [sugar-runner](https://www.archlinux.org/packages/?name=sugar-runner)

Python 2:

*   For the core system (*Glucose*), install [sugar](https://www.archlinux.org/packages/?name=sugar). It provides the graphical interface and a desktop session, but not very useful on its own.
*   The [sugar-fructose](https://www.archlinux.org/groups/x86_64/sugar-fructose/) group contains the base activities (*Fructose*) including a web browser, a text editor, a media player and a terminal emulator.
*   The [sugar-runner](https://www.archlinux.org/packages/?name=sugar-runner) package provides a helper script that makes it possible to launch Sugar within another desktop environment, or from the command line directly.

### From Activity Library

The [Sugar Activity Library](http://wiki.sugarlabs.org/go/Activity_Library) provides many [Activity Bundles](http://wiki.sugarlabs.org/go/Development_Team/Almanac/Activity_Bundles) packaged as zip files with the ".xo" extension. These bundles can be downloaded and installed to the user's directory from Sugar, but the installation does not ensure that the dependencies are satisfied. Therefore it is not the recommended way to install activities, because they likely fail to start due missing dependencies. Commonly used dependencies:

*   For web activities, install [webkit2gtk](https://www.archlinux.org/packages/?name=webkit2gtk) from the official repositories.
*   For GTK 2 based activities, install [sugar-toolkit-gtk2](https://aur.archlinux.org/packages/sugar-toolkit-gtk2/) from AUR.

In order to check why the activity fails to start, look at the log file located at `~/.sugar/default/logs/[app_id]-1.log`.

## Starting Sugar

Sugar can be started either graphically, using a [display manager](/index.php/Display_manager "Display manager"), or manually from the console.

**Graphically**

Select the session *Sugar* from the display manager's session menu.

**Manually**

If [sugar-runner](https://www.archlinux.org/packages/?name=sugar-runner) installed, Sugar can be launched with the `sugar-runner` command.

Alternative method is to add `exec sugar` to the `~/.xinitrc` file. After that, Sugar can be launched with the `startx` command (see [xinitrc](/index.php/Xinitrc "Xinitrc") for additional details). After setting up the `~/.xinitrc` file, it can also be arranged to [Start X at login](/index.php/Start_X_at_login "Start X at login").

## See also

*   [The Official Website of Sugar](http://sugarlabs.org/)
*   [Activities for Sugar](http://activities.sugarlabs.org/)