# Logitech Gaming Keyboards

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Some Logitech Gaming Keyboards can work on Linux through Unofficial drivers. The options are the python based [Gnome15 project](http://www.gnome15.org) and the C based [g15daemon project](http://sourceforge.net/projects/g15daemon/).

## Install

[g15daemon](https://www.archlinux.org/packages/?name=g15daemon) and its dependencies are available in the community repository. G15daemon drivers still work for the keyboards they supported, but their development was mostly dropped in 2008, the source is still available for anyone to pick up and continue their development, there are a few bugs in them that were never solved. These drivers use the [g15macro](https://aur.archlinux.org/packages/g15macro/)<sup><small>AUR</small></sup> to interact with the G keys. There is also a [g15stats](https://aur.archlinux.org/packages/g15stats/)<sup><small>AUR</small></sup> plugin to show system information on the LCD display.

[gnome15](https://aur.archlinux.org/packages/gnome15/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/gnome15)]</sup> is available in AUR.

**Note:** The source site has been down since mid November 2014\. The AUR package cannot be built. The new Maintainer is actively working on providing all existing packages.

### Supported Models

**g15daemon** supports:

*   G15 (Orange and Blue)
*   G11
*   Gamepad
*   G510 (Requires Patching; Read below)

[Gnome15](http://gnome15.org/) has a list of supported devices on its front page. The keyboards are:

*   G19
*   G19s
*   G15 (Orange and Blue)
*   G13
*   G110
*   G510 and G510s (Partial)

## G510 on g15daemon

[Forum Thread](https://bbs.archlinux.org/viewtopic.php?pid=1421825) (This thread has more detailed instructions and might be helpful for readers from other distributions or less advanced users, it also contains a list of known issues.)

**Note:** This has not been tested with the G510s, if you want to try then find line 23 and 24 in the libg15.patch linked below and replace the device ID with the appropriate values for G510s which can be found with **lsusb** command from the [usbutils](https://www.archlinux.org/packages/?name=usbutils) package

A patch was written to make the G510 keyboard fully compatible with the g15daemon drivers. It is however not compatible with g15macro and as such an alternative approach was needed (which involved heavy modifications of the original code) the result yields much better performance for than using the gnome15 drivers which can currently result in severe input lag for this keyboard.

To apply the patch you must download the g15daemon and libg15 sources with [abs](https://www.archlinux.org/packages/?name=abs) and edit their PKGBUILDs.

**Note:** I would recommend that you instead follow the forum thread linked to at the start of this section, it is going to be a lot easier.

To download the sources to a folder directory called "community" (the folder will be dropped into whichever directory the terminal is in) run the two following commands:

```
ABSROOT=. abs community/g15daemon
ABSROOT=. abs community/libg15

```

Now enter the folders and fetch the sources for them. (Make sure to remember to download the soures for both of them)

```
makepkg -S

```

The patch already applies the patches from the arch community repository, so remove all patches that came with g15daemon by running:

```
rm community/g15daemon/*.patch

```

Then download the [libg15](http://pastebin.com/5VQixu64) and [g15daemon](http://pastebin.com/0HBfp7XY) patches and modify to your will. The color profiles per M-Led settings are hard coded into the libg15 patch at line 341, 344, 347 and 350 in R,G,B color code.

Then place the files (libg15.patch and g15daemon.patch) into the folders that your packages were downloaded into, after this you must replace the PKGBUILDS with the new ones: [g15daemon](http://pastebin.com/Ff2vAEkd), [libg15](http://pastebin.com/56a3cHhf) These new PKGBUILDS refer to local sources only, this means they do not fetch sources from the net if they are not present so make sure you hold on to your tar.bz2 files. If you want them to fetch these from the net you can refer to the original PKGBUILDs.

Now install the packages, libg15 comes first, [libg15render](https://www.archlinux.org/packages/?name=libg15render) is required as well before you install g15daemon.

```
makepkg -fic

```

This will compile, install and clean up the extracted sources afterwards to avoid cluttering the folder. I also recommend installing [g15stats](https://aur.archlinux.org/packages/g15stats/) from AUR next. For fluff.

After the installation you need to [download](http://www.mediafire.com/download/s24d6gjnzm4w34w/macros..rar) or create the macro script files, and place them into /usr/share/g15daemon/macros. If you want to create them yourself the files need to be executable and the filenames are corresponding to the label on each key (so for the G1 key use /usr/share/g15daemon/macros/G1). Normally these files should use the bash script syntax.

**Note:** You will need to have sudo installed and configure it so that g15daemon can be run without a password. The sleep command is to give g15daemon time to launch before g15stats is loaded into it

For commands on the G keys to work with graphical applications g15daemon must be started after the X11 session. To do this you must add these commands to your autostart/xinitrc.

```
sudo g15daemon && sleep 3 && g15stats

```

And congratulations! you have a working G510 keyboard on Linux :) With a few issues of course (known issues are in the forum thread linked to at the start of this section)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Logitech_Gaming_Keyboards&oldid=399630](https://wiki.archlinux.org/index.php?title=Logitech_Gaming_Keyboards&oldid=399630)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Keyboards](/index.php/Category:Keyboards "Category:Keyboards")