[Haiku](http://www.haiku-os.org/) is a free and open source operating system compatible with [BeOS](http://en.wikipedia.org/wiki/BeOS). It is in active development.

## Contents

*   [1 Using Haiku](#Using_Haiku)
*   [2 Adding Haiku To The GRUB Boot Menu](#Adding_Haiku_To_The_GRUB_Boot_Menu)
    *   [2.1 GRUB Legacy](#GRUB_Legacy)
    *   [2.2 GRUB 2](#GRUB_2)
*   [3 Sharing Files Between Operating Systems](#Sharing_Files_Between_Operating_Systems)
*   [4 Optional Packages](#Optional_Packages)
*   [5 Software](#Software)
*   [6 Haiku Ports](#Haiku_Ports)
*   [7 Links](#Links)

## Using Haiku

You can use Haiku in different ways:

*   Install Haiku in [VirtualBox](/index.php/VirtualBox "VirtualBox"). For instructions please see [Emulating Haiku In VirtualBox](http://haiku-os.org/guides/virtualizing/virtualbox).
*   Boot Haiku and either run it as a "live desktop" or install it. If you would like to build your own copy of Haiku using the latest source code, please see [Building Haiku](http://haiku-os.org/guides/building).

Since Haiku is in active development, the [nightly builds](http://haiku-files.org/haiku/development/) are recommended over the previous "official" release.

Please keep in mind that, even though there is a lot of hardware that is supported by Haiku, there is a lot more that is not supported yet.

## Adding Haiku To The GRUB Boot Menu

If you choose to install Haiku, you can add it to the list of operating systems in the GRUB boot menu.

### GRUB Legacy

In Linux, edit the `"/boot/grub/menu.lst"` file. Add this section:

```
 title        Haiku
 rootnoverify (hd0,0)  # WARNING: Replace these numbers with your own drive and partition numbers
 chainloader  +1

```

### GRUB 2

Edit `/etc/grub.d/40_custom` to add:

```
menuentry "Haiku OS" {
  set root=(hdX,Y)
  chainloader +1
}

```

Replace X and Y for the appropriate hdd and partition numbers, respectively.

Then reinstall [GRUB](/index.php/GRUB "GRUB"):

```
 # grub-install /dev/sdX  # WARNING: Replace "/dev/sdX" with your own primary drive name

```

## Sharing Files Between Operating Systems

Haiku can mount and read EXT3 file systems. In Haiku, click on the deskbar "leaf" menu and select "Mount".

Conversely, Linux can mount the [Be File System](http://en.wikipedia.org/wiki/Be_File_System).

```
 # mount -t befs /dev/sda1 /mnt # Replace the drive name and number with your BFS drive

```

**Note:** Linux refers to the BFS as "befs" to avoid confusion with the UnixWare Boot File System.

## Optional Packages

Optional packages are packages that are packaged by the Haiku developers but are not maintained by them. You can install them when using Haiku with the `"installoptionalpackage"` command.

```
$ installoptionalpackage -l # List optional packages
$ installoptionalpackage -a pkgname # Install a package

```

Here is the list of the current [optional packages](http://cgit.haiku-os.org/haiku/tree/build/jam/OptionalPackages).

## Software

This section is just to give you a simple idea of "what to do next", after you finish booting into Haiku. All of this software can be installed with the official `installoptionalpackage` command.

*   Web Browser
    *   WebPositive
    *   BeZillaBrowser (an old Mozilla build, very stable)
*   Media Player
    *   MediaPlayer (comes with Haiku, plays music and videos, includes playlist support)
*   IRC
    *   Vision (the Haiku developers use #haiku on Freenode)
*   Text Editor
    *   Pe (comes with Haiku, programmer's editor)
    *   Vim
*   Bittorrent
    *   Transmission (CLI)
*   Image Editting
    *   WonderBrush
*   Scripting
    *   The Terminal application uses BASH.
    *   Perl
    *   Python

## Haiku Ports

"Haiku Ports" is an effort to port software from the BSD ports tree to Haiku. It is very easy to install and use. Installation instructions are here:

[http://ports.haiku-files.org/wiki/Installation](http://ports.haiku-files.org/wiki/Installation)

And a list of packages can be found here:

*   [http://ports.haiku-files.org/wiki/PortLog](http://ports.haiku-files.org/wiki/PortLog)
*   [http://ports.haiku-files.org/svn/haikuports/trunk/](http://ports.haiku-files.org/svn/haikuports/trunk/)

Please keep in mind that, even though a lot of software is listed on Haiku Ports, some of it is a work in progress and is not fully functional yet.

## Links

*   [The official Haiku website](http://www.haiku-os.org/)
*   [The official Haiku download page](http://www.haiku-files.org/)
*   [HaikuWare](http://www.haikuware.com/) BeOS and Haiku software (sometimes out of date)
*   [OsDrawer](http://dev.osdrawer.net/), a development hosting site specifically for native Haiku software.