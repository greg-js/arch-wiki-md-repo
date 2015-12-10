# pawm

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

This wiki page details installation and configuration of the PAWM window manager under Arch Linux.

**Note:** It's unmaintained. Latest released version is 2.3.0.

## Contents

*   [1 Introduction](#Introduction)
    *   [1.1 PAWM creation history](#PAWM_creation_history)
*   [2 Installation](#Installation)
*   [3 Start PAWM with X as default](#Start_PAWM_with_X_as_default)
*   [4 Configuration (making PAWM pretty)](#Configuration_.28making_PAWM_pretty.29)
    *   [4.1 Icons](#Icons)
*   [5 Application Launcher](#Application_Launcher)
    *   [5.1 Creating new Launcher files](#Creating_new_Launcher_files)
*   [6 Using PAWM](#Using_PAWM)
*   [7 PAWM Utilities](#PAWM_Utilities)

## Introduction

[PAWM](https://sites.google.com/site/pleyadestest/david/projects/pawm) is an X11 stacking window manager. It is a very small, fast, and simple window manager. It is based on Xlib and needs no other external libraries to compile it. It provides an initial windowing environment for minimalist desktops or for single use purposes such as:

*   A web browser terminal computer.
*   Testing gui based programs.

### PAWM creation history

PAWM was written by David Gómez and Raúl Núñez de Arenas Coronado. PAWM was written with the objective of creating a tiny window manager that would execute any X application, but still keep it simple and intuitive to use.

PAWM stands for _Puto Amo Window Manager'._

## Installation

[Install](/index.php/Install "Install") [pawm](https://www.archlinux.org/packages/?name=pawm).

## Start PAWM with X as default

In order to run PAWM as your default window manager, edit the file `~/.xinitrc` (See [xinitrc](/index.php/Xinitrc "Xinitrc")) so the final line is:

```
exec pawm

```

If you now type:

```
startx

```

at the command prompt, X will start using PAWM for its window manager.

If you would like to configure X (and PAWM) to start on boot (or when you login) read the wiki page [Start X at login](/index.php/Start_X_at_login "Start X at login") to find out how.

## Configuration (making PAWM pretty)

By default, PAWM looks blue, plain and kind of dated. By editing the file `/etc/pawm.conf` you can customize the scheme of your PAWM.

Colors are changed through hexadecimal values. Fonts can be changed either through core fonts[[1]](http://en.wikipedia.org/wiki/X_logical_font_description) or Xft fonts[[2]](http://www.x.org/archive/X11R6.8.2/doc/fonts.html).

You may also adjust adjust the behavior of pabar, paicons, pashut icon or any modules added.

### Icons

PAWM only supports [.xpm](http://en.wikipedia.org/wiki/X_PixMap) format. Programs like [GIMP](/index.php/GIMP#GIMP "GIMP") can convert images appropriately.

*   Window icons must be 20x20 pixels.
*   Pashut icons must be 20x20 pixels.
*   Paicon icons may be of any size.

Any icons used in PAWM **must** be put in `/usr/share/pawm/icons/`

## Application Launcher

First, create a directory `~/.pawm` . This allows each user to have a unique application set.

There are 3 ways to launch programs in PAWM.

*   Add it to the `~/.xinitrc` file.
*   Execute the program from console with the **`-display`** paramater.
*   Use the PAWM application launcher

This article covers the third option.

### Creating new Launcher files

Create a new file in the directory. For our example we will use the terminal emulator [Sakura](http://www.pleyades.net/david/sakura.php).

The filename must start with **app** with up to 20 characters after it.

```
appSakura

```

Then take your favorite file editor and open the file. The launcher apps have 4 lines that need editing.

1.  The name of the image you want to use.
2.  The initial icon screen position. As you move it, PAWM will edit the X Y coordinates accordingly.
3.  Icon text. This is optional.
4.  Application binary. This can be either relative or absolute path.

The finished file will look like this:

```
sakura.xpm
40 40
Sakura
sakura

```

When you next start PAWM your icons will be there. As well, any icon changes including position will be preserved.

## Using PAWM

As PAWM is minimalistic, the controls are as well.

*   Double clicking a titlebar scrolls the window up or down respectively.
*   There are Minimize, Restore/Maximize, Close buttons.
*   You can drag windows around.
*   You can drag Launcher icons around.
*   Clicking on open applications on the PABar will minimize and restore.
*   Alt+Tab switches between windows.
*   Clicking on a Launcher executes the program.
*   Clicking on the power button brings up a dialog to quit PAWM.
*   Reloading PAWM refreshes any changes made.

## PAWM Utilities

The following complementary packages can be found in the [AUR](/index.php/AUR "AUR").

*   [xsri](https://aur.archlinux.org/packages/xsri/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/xsri)]</sup> A program that can be used for fast image and gradient setting. Good for `~/.xinitrc`
*   [thinglaunch](https://aur.archlinux.org/packages/thinglaunch/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/thinglaunch)]</sup> is a launcher program for X. You can bind it to a key in your favorite window manager. When you want to start a program, just type its name. thinglaunch has a tiny footprint and depends only on Xlib.
*   [pawmIcons](https://aur.archlinux.org/packages/pawmIcons/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/pawmicons)]</sup> A simple python based utility for creating hassle free Launcher icons. It does not support custom icons.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Pawm&oldid=392560](https://wiki.archlinux.org/index.php?title=Pawm&oldid=392560)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Stacking WMs](/index.php/Category:Stacking_WMs "Category:Stacking WMs")