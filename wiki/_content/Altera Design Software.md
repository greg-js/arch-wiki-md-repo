# Altera Design Software

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

This tutorial shows how to download, install, and configure the following software from Altera:

*   Quartus II Subscription Edition v15.0
    *   USB-Blaster (I and II) Download Cable Driver
*   ModelSim-Altera Edition 10.3d (As included with Quartus II Subscription Edition v15.0)

**Note:** The following tutorial works for older Quartus II and ModelSim versions, including both Subscription Editions and Web Editions, from at-least v13.0 through v15.0.

## Contents

*   [1 Quartus II Subscription Edition](#Quartus_II_Subscription_Edition)
    *   [1.1 Get Quartus II](#Get_Quartus_II)
    *   [1.2 Install dependencies](#Install_dependencies)
    *   [1.3 Installing](#Installing)
    *   [1.4 Launching Quartus II](#Launching_Quartus_II)
    *   [1.5 Integrating Quartus II with the system](#Integrating_Quartus_II_with_the_system)
        *   [1.5.1 PATH variable](#PATH_variable)
        *   [1.5.2 Application menu entry - Quartus II](#Application_menu_entry_-_Quartus_II)
    *   [1.6 Subscription Edition License Validation](#Subscription_Edition_License_Validation)
    *   [1.7 USB-Blaster Download Cable Driver](#USB-Blaster_Download_Cable_Driver)
*   [2 ModelSim-Altera Edition](#ModelSim-Altera_Edition)
    *   [2.1 Install](#Install)
    *   [2.2 Compatibility with Archlinux](#Compatibility_with_Archlinux)
        *   [2.2.1 With the kernel 4.x and Upwards](#With_the_kernel_4.x_and_Upwards)
        *   [2.2.2 With freetype2 2.5.0.1-1](#With_freetype2_2.5.0.1-1)
        *   [2.2.3 With ncurses 5.9](#With_ncurses_5.9)
        *   [2.2.4 Install libraries](#Install_libraries)
    *   [2.3 Application Menu Entry - ModelSim-Altera Edition](#Application_Menu_Entry_-_ModelSim-Altera_Edition)
    *   [2.4 Resolving the "ModelSim Failed to access library 'work'" error](#Resolving_the_.22ModelSim_Failed_to_access_library_.27work.27.22_error)

## Quartus II Subscription Edition

The following procedure shows how to download, install, and configure Altera Quartus II Subscription Edition v15.0 for Arch Linux.

**Note:** The following tutorial works for older Quartus II and ModelSim versions, including both Subscription Editions and Web Editions, from at-least v13.0 through v15.0.

Quartus II is Altera's design software collection to design and interact with all their FPGAs/CPLDs/etc. products.

The procedure focuses on Arch Linux 64-bit systems, although 32-bit installations should work fine too.

Quartus II Subscription Edition v15.0 is [officially supported](http://www.altera.com/download/os-support/oss-index.html) for RHEL 5 and RHEL 6, but since it is one of those huge collections of proprietary software that does not interact so much with the distribution, it is fairly easy to install on Arch Linux.

### Get Quartus II

In [Altera's Downloads section](http://dl.altera.com/?edition=subscription), select Linux as the operating system and get the _Combined Files_ tar archive (something like `Quartus-15.0.0.145-linux-complete.tar`).

### Install dependencies

Although the main Quartus II software is 64-bit, lots of Altera tools shipped with Quartus II are still 32-bit softwares. Those include the Nios II EDS and Qsys, for example. This is why we need to install lots of `lib32-` libraries and other programs from the Arch Linux Multilib repo. Obviously, if you have a 32-bit Arch Linux system, you do not need the Multilib versions.

In order to install Multilib packages using [pacman](/index.php/Pacman "Pacman"), you need to enable the [multilib](/index.php/Multilib "Multilib") repository first (if not already done).

All the packages required below are taken from [Altera Software Installation and Licensing](http://www.altera.com/literature/manual/quartus_install.pdf) (sect. 1-4).

Let us first install the native versions of the required packages: [expat](https://www.archlinux.org/packages/?name=expat) [fontconfig](https://www.archlinux.org/packages/?name=fontconfig) [freetype2](https://www.archlinux.org/packages/?name=freetype2) [xorg-fonts-type1](https://www.archlinux.org/packages/?name=xorg-fonts-type1) [glibc](https://www.archlinux.org/packages/?name=glibc) [gtk2](https://www.archlinux.org/packages/?name=gtk2) [libcanberra](https://www.archlinux.org/packages/?name=libcanberra) [libpng](https://www.archlinux.org/packages/?name=libpng) [libpng12](https://aur.archlinux.org/packages/libpng12/)<sup><small>AUR</small></sup> [libice](https://www.archlinux.org/packages/?name=libice) [libsm](https://www.archlinux.org/packages/?name=libsm) [util-linux](https://www.archlinux.org/packages/?name=util-linux) [ncurses](https://www.archlinux.org/packages/?name=ncurses) [tcl](https://www.archlinux.org/packages/?name=tcl) [tcllib](https://www.archlinux.org/packages/?name=tcllib) [zlib](https://www.archlinux.org/packages/?name=zlib) [libx11](https://www.archlinux.org/packages/?name=libx11) [libxau](https://www.archlinux.org/packages/?name=libxau) [libxdmcp](https://www.archlinux.org/packages/?name=libxdmcp) [libxext](https://www.archlinux.org/packages/?name=libxext) [libxft](https://www.archlinux.org/packages/?name=libxft) [libxrender](https://www.archlinux.org/packages/?name=libxrender) [libxt](https://www.archlinux.org/packages/?name=libxt) [libxtst](https://www.archlinux.org/packages/?name=libxtst).

And the Multilib versions: [lib32-expat](https://www.archlinux.org/packages/?name=lib32-expat) [lib32-fontconfig](https://www.archlinux.org/packages/?name=lib32-fontconfig) [lib32-freetype2](https://www.archlinux.org/packages/?name=lib32-freetype2) [lib32-glibc](https://www.archlinux.org/packages/?name=lib32-glibc) [lib32-gtk2](https://www.archlinux.org/packages/?name=lib32-gtk2) [lib32-libcanberra](https://www.archlinux.org/packages/?name=lib32-libcanberra) [lib32-libpng](https://www.archlinux.org/packages/?name=lib32-libpng) [lib32-libpng12](https://aur.archlinux.org/packages/lib32-libpng12/)<sup><small>AUR</small></sup> [lib32-libice](https://www.archlinux.org/packages/?name=lib32-libice) [lib32-libsm](https://www.archlinux.org/packages/?name=lib32-libsm) [lib32-util-linux](https://www.archlinux.org/packages/?name=lib32-util-linux) [lib32-ncurses](https://www.archlinux.org/packages/?name=lib32-ncurses) [lib32-zlib](https://www.archlinux.org/packages/?name=lib32-zlib) [lib32-libx11](https://www.archlinux.org/packages/?name=lib32-libx11) [lib32-libxau](https://www.archlinux.org/packages/?name=lib32-libxau) [lib32-libxdmcp](https://www.archlinux.org/packages/?name=lib32-libxdmcp) [lib32-libxext](https://www.archlinux.org/packages/?name=lib32-libxext) [lib32-libxft](https://www.archlinux.org/packages/?name=lib32-libxft) [lib32-libxrender](https://www.archlinux.org/packages/?name=lib32-libxrender) [lib32-libxt](https://www.archlinux.org/packages/?name=lib32-libxt) [lib32-libxtst](https://www.archlinux.org/packages/?name=lib32-libxtst).

You are now ready to install and launch Quartus II.

### Installing

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

**This article or section needs language, wiki syntax or style improvements.**

**Reason:** The installation should be handled with pacman through a [PKGBUILD](/index.php/PKGBUILD "PKGBUILD"). (Discuss in [Talk:Altera Design Software#](https://wiki.archlinux.org/index.php/Talk:Altera_Design_Software))

To install, first extract the downloaded tar archive:

```
$ tar -xvf Quartus-15.0.0.145-linux-complete.tar

```

and launch `setup.sh`. If you are going to install Quartus II anywhere outside your home directory, run it as root:

```
# ./setup.sh

```

You will probably get a GUI install wizard if you installed all the aforementioned packages. You might also get a command-line interactive install wizard, which will do the same.

The default install path is `/root/altera/15.0`, but some prefer `/opt/altera/15.0`, which we assume for the rest of this document.

**Make sure to include** the 64-bit option of Quartus II when installing.

### Launching Quartus II

Assuming you installed Quartus II in `/opt/altera/15.0`, Quartus II binaries are located into `/opt/altera/15.0/quartus/bin`. Run Quartus II (64-bit version):

```
$ /opt/altera/15.0/quartus/bin/quartus --64bit

```

or the 32-bit version:

```
$ /opt/altera/15.0/quartus/bin/quartus

```

All other Altera tools, like Qsys, the Nios II EDS, Chip Planner and SignalTap II may be launched without any problem from the _Tools_ menu of Quartus II.

### Integrating Quartus II with the system

Quartus II can be integrated with the system in several ways, but those are optional.

#### `PATH` variable

Let us now add the Quartus `bin` folder to the `PATH` variable so it can be executed without specifying its absolute path. Create a `quartus.sh` file in the `/etc/profile.d` directory

```
/etc/profile.d/quartus.sh

```

```
export PATH=$PATH:/opt/altera/15.0/quartus/bin

```

Also, make sure it can be executed:

```
# chmod +x /etc/profile.d/quartus.sh

```

Please note that those `profile.d` files are loaded at each _login_. In the mean time, simply source that file in Bash:

```
$ source /etc/profile.d/quartus.sh

```

Other environment variables related to Quartus can be found in [the official installation manual](http://www.altera.com/literature/manual/quartus_install.pdf).

Even if `quartus` is now a command known by Bash, you still need to add the `--64bit` argument in order to launch the 64-bit version. A shell alias, like `quartus64`, is a great solution to avoid typing it each time.

#### Application menu entry - Quartus II

A freedesktop.org application menu entry (which a lot of desktop environments and window managers follow) can be added to the system by creating a `quartus.desktop` file in your `~/.local/share/applications` directory:

```
~/.local/share/applications/quartus.desktop

```

```
[Desktop Entry]
Version=1.0
Name=Quartus II Subscription Edition v15.0
Comment=Quartus II design software for Altera FPGA's
Exec=/opt/altera/15.0/quartus/bin/quartus --64bit
Icon=/opt/altera/15.0/quartus/adm/quartusii.png
Terminal=false
Type=Application
Categories=Development

```

### Subscription Edition License Validation

Configuring the path to your Quartus II Subscription Edition license file from the Quartus II settings interface is not enough for successful license validation. The license validation routine looks for your MAC address on device `eth0`. This was the legacy name for your ethernet controller; now `systemd` dynamically allocates a name to your device on boot - this can be different from machine to machine. We need to rename that device back to the expected `eth0`.

Create a new udev rule:

```
/etc/udev/rules.d/10-network.rules

```

```
SUBSYSTEM=="net", ACTION=="add", ATTR{address}=="xx:xx:xx:xx:xx:xx", NAME="eth0"

```

where `xx:xx:xx:xx:xx:xx` is your networking device's IP address. Then, _reload_ that file using `udevadm`:

```
# udevadm control --reload

```

The Quartus II Subscription Edition license validation routine also uses the deprecated networking tool `ifconfig` to validate your networking devices MAC address as per your Quartus II license. The deprecated networking package `net-tools` contains the `ifconfig` tool. Thus one must also install the `net-tools` package for Quartus II Subscription Edition licensing validation success.

### USB-Blaster Download Cable Driver

The USB-Blaster (I and II) Download Cable is a cable that allows you to download configuration data from your computer to your FPGA, CPLD or EEPROM configuration device. However, Altera only provides official support for RHEL, SUSE Entreprise and CentOS, so we are required to do a little bit of work to make it work with Arch Linux. If you want some more detail about this cable, please refer to the [USB-Blaster Download Cable User Guide](http://www.altera.com/literature/ug/ug_usb_blstr.pdf).

Create a new udev rule:

```
/etc/udev/rules.d/51-altera-usb-blaster.rules

```

```
SUBSYSTEM=="usb", ATTR{idVendor}=="09fb", ATTR{idProduct}=="6001", MODE="0666"
SUBSYSTEM=="usb", ATTR{idVendor}=="09fb", ATTR{idProduct}=="6002", MODE="0666"
SUBSYSTEM=="usb", ATTR{idVendor}=="09fb", ATTR{idProduct}=="6003", MODE="0666"
SUBSYSTEM=="usb", ATTR{idVendor}=="09fb", ATTR{idProduct}=="6010", MODE="0666"
SUBSYSTEM=="usb", ATTR{idVendor}=="09fb", ATTR{idProduct}=="6810", MODE="0666"

```

Then, _reload_ that file using `udevadm` (disconnect any Altera device from port USB port before this command):

```
# udevadm control --reload

```

To check that everything is working, plug your FPGA or CPLD board using your USB-Blaster Download Cable and run:

```
$ /opt/altera/15.0/quartus/bin/jtagconfig

```

You should have an output similar to this one

```
1) USB-Blaster [USB 1-1.1]
  020B30DD   EP2C15/20

```

If jtagconfig output does not contain board name, you might have problems with launching nios2 tools. In order to workaround this issue, you should copy jtagd settings to /etc/jtagd:

```
# mkdir /etc/jtagd
# cp /opt/altera/15.0/quartus/linux/pgm_parts.txt /etc/jtagd/jtagd.pgm_parts

```

and restart jtagd:

```
$ jtagconfig
1) USB-Blaster [2-4]
020F30DD 
$ killall jtagd
$ jtagd
$ jtagconfig
1) USB-Blaster [2-4]
020F30DD EP3C25/EP4CE22

```

If there seems to be an error message about "linux64" and you did not install the 64-bit version of Quartus II, create a symlink from `linux` to `linux64` in `/opt/altera/15.0/quartus`:

```
# ln -s /opt/altera/15.0/quartus/linux /opt/altera/15.0/quartus/linux64

```

## ModelSim-Altera Edition

### Install

ModelSim-Altera Edition 10.3d is downloaded and installed from the _Combined Files_ tar archive `Quartus-15.0.0.145-linux-complete.tar` as part of the Quartus II installation procedure above.

### Compatibility with Archlinux

#### With the kernel 4.x and Upwards

**Note:** ModelSim Starter Edition installation uses the path `/opt/altera/15.0/modelsim_ase/` where ModelSim Subscription Edition installation uses the path `/opt/altera/15.0/modelsim_ae/`; the following assumes the ModelSim Subcription Edition installation.

Modelsim has a problem with version 4 of the linux kernel. You need to edit the `vsim` script to make it compatible. This file may be be read only, so temporarily give yourself write permissions and:

change

```
/opt/altera/15.0/modelsim_ae/bin/vsim line 206

```

```
 *)                vco="linux_rh60" ;;

```

to

```
/opt/altera/15.0/modelsim_ae/bin/vsim line 206

```

```
 *)                vco="linux" ;;

```

#### With freetype2 2.5.0.1-1

The upgrade from freetype2 version 2.5.0.1-1 to 2.5.0.1-2 (October 2013[[1]](https://projects.archlinux.org/svntogit/packages.git/commit/?h=packages/freetype2&id=f2903d2374daf5becc931b010efb2f613eaaae18)) causes the following error in ModelSim:

```
$ vsim
Error in startup script:
Initialization problem, exiting.
Initialization problem, exiting.
Initialization problem, exiting.
   while executing
"EnvHistory::Reset"
   (procedure "PropertiesInit" line 3)
   invoked from within
"PropertiesInit"
   invoked from within
"ncFyP12 -+"
   (file "/opt/questasim/linux_x86_64/../tcl/vsim/vsim" line 1)
** Fatal: Read failure in vlm process (0,0)

```

There are two solutions to solve this problem. The first involves downgrading the Package (probably via the [Arch Linux Archive](/index.php/Arch_Linux_Archive "Arch Linux Archive")). The second and more elegant solution involves replacing the old freetype version for ModelSim only without withholding updates on the whole system (originally proposed at the now-dead link [http://communities.mentor.com/mgcx/message/46770](http://communities.mentor.com/mgcx/message/46770)):

*   Copy the freetype library and symlinks somewhere in the altera folder, eg: `$HOME/altera/xx.x/lib32/`

```
libfreetype.so
libfreetype.so.6
libfreetype.so.6.10.2
```

*   Edit the ModelSim script in `/opt/altera/15.0/modelsim_ae/bin/vsim` and add near the top (after the `#!/bin/sh`)

```
export LD_LIBRARY_PATH=/home/user/altera/xx.x/lib32

```

**Note:** The quartus script will need to have write permissions added to it.

When ModelSim is launched directly from Quartus the error may persist. In this case, add the same line to `quartus/bin/quartus_sh`.

#### With ncurses 5.9

The upgrade from ncurses version 5.9-7 to 6.0-1 (and later) (September 2015[[2]](https://projects.archlinux.org/svntogit/packages.git/commit/trunk?h=packages/ncurses&id=ddb1abecfe25260321c9cb0ef24f29351f28ecb3)) causes the following error in ModelSim:

```
$ vsim
vish: error while loading shared libraries: libncurses.so.5: cannot open shared object file: No such file or directory
[1]  + exit 127   vsim

```

There are two solutions to this problem. One is to use [ncurses5-compat-libs](https://aur.archlinux.org/packages/ncurses5-compat-libs/)<sup><small>AUR</small></sup> and tweak the PKGBUILD to compile a 32-bit version of the library. This will provide the latest version of ncurses with an ncurses5-compatible ABI.

The other solution is to download the ncurses 5.9 source, compile it, and copy the generated libraries and symlinks to the same directory as the freetype2 libraries.

Compiling ncurses 5.9 may lead to problems using GCC 5.x. It is also possible to get a precompiled library, using the [Arch Linux Archive](/index.php/Arch_Linux_Archive "Arch Linux Archive"). The package can be found at [http://ala.seblu.net/packages/l/lib32-ncurses/](http://ala.seblu.net/packages/l/lib32-ncurses/).

#### Install libraries

Install library _libxft_ and _ncurses_: [libxft](https://www.archlinux.org/packages/?name=libxft), [ncurses](https://www.archlinux.org/packages/?name=ncurses), [libxext](https://www.archlinux.org/packages/?name=libxext).

For 64 bit edition, install these library from [multilib](/index.php/Multilib "Multilib") repository: [lib32-libxft](https://www.archlinux.org/packages/?name=lib32-libxft), [lib32-ncurses](https://www.archlinux.org/packages/?name=lib32-ncurses), [lib32-libxext](https://www.archlinux.org/packages/?name=lib32-libxext).

### Application Menu Entry - ModelSim-Altera Edition

You can add Modelsim to your system application menu by creating a `modelsim.desktop` file in your `~/.local/share/applications` directory

```
~/.local/share/applications/modelsim.desktop

```

```
[Desktop Entry]
Version=1.0
Name=ModelSim-Altera Edition 10.3d
Comment=ModelSim simulation software for Altera FPGA's
Exec=/opt/altera/15.0/modelsim_ae/bin/vsim
Icon=/opt/altera/15.0/modelsim_ae/modesim.gif
Terminal=true
Type=Application
Categories=Development

```

### Resolving the "ModelSim Failed to access library 'work'" error

The solution was originally documented here: [http://jackeyblog.blogspot.com/2005/07/note-myself-modelsim-failed-to-access.html](http://jackeyblog.blogspot.com/2005/07/note-myself-modelsim-failed-to-access.html)

If you receive the error:

```
Error: (vcom-19) Failed to access library 'work' at "work". 

```

when running a simulation in a new directory, you must create a new `work` directory. Execute the following in the ModelSim console:

```
ModelSim> vlib work

```

Retrieved from "[https://wiki.archlinux.org/index.php?title=Altera_Design_Software&oldid=409237](https://wiki.archlinux.org/index.php?title=Altera_Design_Software&oldid=409237)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [Development](/index.php/Category:Development "Category:Development")
*   [Mathematics and science](/index.php/Category:Mathematics_and_science "Category:Mathematics and science")