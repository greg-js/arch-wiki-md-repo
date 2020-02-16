From [[1]](https://www.microsemi.com/product-directory/design-resources/1750-libero-soc#overview):

	Libero® SoC Design Suite offers high productivity with its comprehensive, easy-to-learn, easy-to-adopt development tools for designing with Microsemi's PolarFire, IGLOO2, SmartFusion2, RTG4, SmartFusion, IGLOO, ProASIC3 and Fusion families.

This article shows how to install the Microsemi Libero FPGA Design Toolchain on Arch Linux.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
    *   [1.1 Preparations](#Preparations)
        *   [1.1.1 Package installation](#Package_installation)
        *   [1.1.2 Qt5 32-bit dependencies](#Qt5_32-bit_dependencies)
    *   [1.2 Extract files](#Extract_files)
        *   [1.2.1 Silent installation](#Silent_installation)
    *   [1.3 Post-Installation](#Post-Installation)
*   [2 Launching Libero](#Launching_Libero)
    *   [2.1 Application menu entry](#Application_menu_entry)
*   [3 Using a FlashPro programmer](#Using_a_FlashPro_programmer)
    *   [3.1 Adding udev rules](#Adding_udev_rules)
    *   [3.2 Removing conflicting kernel module](#Removing_conflicting_kernel_module)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Libero crashes with SysXceptError](#Libero_crashes_with_SysXceptError)

## Installation

### Preparations

Libero needs about 45GiB free diskspace. **The size of the disk where Libero is installed must not exceed 2TB!**

#### Package installation

Libero depends on some 32-bit packages from multilib. In order to install multilib packages using [pacman](/index.php/Pacman "Pacman"), you need to enable the [multilib](/index.php/Multilib "Multilib") repository first (if not already done).

Install the following packages: [openmotif](https://www.archlinux.org/packages/?name=openmotif) [zlib](https://www.archlinux.org/packages/?name=zlib) [libjpeg6-turbo](https://www.archlinux.org/packages/?name=libjpeg6-turbo) [lib32-libxft](https://www.archlinux.org/packages/?name=lib32-libxft) [lib32-libpng12](https://www.archlinux.org/packages/?name=lib32-libpng12) [lib32-dbus](https://www.archlinux.org/packages/?name=lib32-dbus) [lib32-sqlite](https://www.archlinux.org/packages/?name=lib32-sqlite) [lib32-libpulse](https://www.archlinux.org/packages/?name=lib32-libpulse) [lib32-libxcomposite](https://www.archlinux.org/packages/?name=lib32-libxcomposite)

#### Qt5 32-bit dependencies

Parts of Liberos shared libraries also depend on 32-bit Qt5 libraries, namely `libQt5XcbQpa.so.5`, `libQt5Gui.so.5`, `libQt5DBus.so.5` and `libQt5Core.so.5`. Sadly they are not available from the [multilib](/index.php/Multilib "Multilib") repository so we have to add them manually.

Download the 32-bit installer of Qt at [Qt 32-bit online installer](https://www.qt.io/download-thank-you?os=linux32&hsLang=en) and execute it:

```
$ chmod u+x qt-unified-linux-x86-2.0.5-2-online.run
$ ./qt-unified-linux-x86-2.0.5-2-online.run

```

It should be sufficient to install "Qt 5.5" -> "Desktop gcc". Set a sane installation path e.g. `/home/*user*/lib/qt5_32` where *user* is your username.

### Extract files

The Installer unpacks its own Java Runtime and by default uses `/tmp` for temporary files even if it tells you differently. Thus make sure you have enough space available on `/tmp`! The default 8GB [tmpfs](/index.php/Tmpfs "Tmpfs") is not sufficient for the installation, you have to disable it for installation and reboot the system to apply the change:

```
# systemctl mask tmp.mount
# reboot

```

From [https://www.microsemi.com/product-directory/design-resources/1750-libero-soc#downloads](https://www.microsemi.com/product-directory/design-resources/1750-libero-soc#downloads) download the "Libero SoC v12.1 for Linux" install file (You need to create an account for that). Make it executable and run it:

```
$ chmod u+x Libero_SoC_v12.1_lin.bin
$ ./Libero_SoC_v12.1_lin.bin -i console

```

In the installer answer the questions and set a path to extract the files to, e.g. `/home/*user*/programs/microsemi/libero/v12.1/` and `/home/*user*/programs/microsemi/common`. There is a graphical installer available, just replace `console` with `gui` in the call above.

#### Silent installation

You can also pass the installation parameters to the script on the commandline rather than typing them in. Following an example for a default installation:

```
$ ./Libero_SoC_v12.1_lin.bin -i silent \
   -DUSER_INSTALL_DIR=/home/*user*/programs/microsemi/libero/v12.1/ \
   -DUSER_COMMON_DIR=/home/*user*/programs/microsemi/common \
   -DCHOSEN_FEATURE_LIST=Synplify,ModelSim,ModelsimPro,Identify,Libero \
   -DCHOSEN_INSTALL_FEATURE_LIST=Synplify,ModelSim,ModelsimPro,Identify,Libero \
   -DCHOSEN_INSTALL_SET=Libero

```

### Post-Installation

Reenable the [tmpfs](/index.php/Tmpfs "Tmpfs") after the installation with:

```
# systemctl unmask tmp.mount
# reboot

```

Some modifications have to be made for Libero to run on Arch Linux.

Libero tries to load an old version of the motif library. Modify the following files and change the 3 to a 4 in the `case `uname`` block:

 `/home/*user*/programs/microsemi/libero/v12.1/Libero/bin/actel_setup_vars and /home/*user*/programs/microsemi/libero/v12.1/Libero/bin64/actel_setup_vars` 
```
...
case `uname` in
  SunOS)
  	...
  Linux)
    arch=lin

    # X/Motif
    **MOTIF_LIB=libXm.so.4**
    ...
```

**Tip:** Alternatively you can create a symlink in the `/lib` directory:
```
# ln -s /lib/libXm.so.4 /lib/libXm.so.3

```
This is discouraged as it tampers with a directory preferably modified by [pacman](/index.php/Pacman "Pacman") when installing packages. However it might be useful when reinstalling Libero or installing a newer version of it because the manual modification of the files above can be skipped.

Furthermore the outdated `libz` version shipped by Microsemi does not work with the repository version of [lib32-libpng12](https://www.archlinux.org/packages/?name=lib32-libpng12). In `/home/*user*/programs/microsemi/libero/v12.1/Libero/lib` do the following to make Libero use your library installed by [pacman](/index.php/Pacman "Pacman"):

```
$ mv libz.so.1 libz.so.1.old
$ ln -s /lib/libz.so libz.so.1

```

Repeat the same two commands in `/home/*user*/programs/microsemi/libero/v12.1/Libero/libfp` to enable the FlashPro utilities.

By mistake the installer adds double quotes around the common path when defining the vault location. Thus Libero will create a folder called `""` in the working directory when it is called. To change that either manually edit the file `install.def` to remove the double quotes from the line where `VAULT_LOCATION` is defined:

 `/home/*user*/programs/microsemi/libero/v12.1/Libero/data/install.def` 
```
...
data VAULT_LOCATION '/home/*user*/programs/microsemi/common/vault' OVERRIDE
...
```

... or run the commands below to remove the quotes:

```
$ cd /home/*user*/programs/microsemi/libero/v12.1/Libero/data
$ sed 's/"//g' install.def > tmp.def
$ cp tmp.def install.def
$ rm tmp.def

```

## Launching Libero

When launching Libero some environment variables have to be set.

```
LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/home/*user*/lib/qt5_32/5.5/gcc/lib
LM_LICENSE_FILE="*port*@*domain.of.your.license.server*"
SNPSLMD_LICENSE_FILE="*port*@*domain.of.synopsys.license.server*"

```

The `$LD_LIBRARY_PATH` has to include the libraries from the 32-bit Qt installation, `$LM_LICENSE_FILE` reflects your Libero license server on which the license daemon runs on some *port* under some url *domain.of.your.license.server*. `$SNPSLMD_LICENSE_FILE` is needed for the Synopsys tools used in Libero, set this to a different server and port if you have multiple license daemons running or to `$LD_LIBRARY_PATH` if not.

With those variabled set Libero is ready to be launched with

```
$ /home/*user*/programs/microsemi/libero/v12.1/Libero/bin/libero

```

Probably you may want to create a launch script for that:

 `/home/*user*/scripts/launch_libero.sh` 
```
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/home/*user*/lib/qt5_32/5.5/gcc/lib
export LM_LICENSE_FILE="*port*@*domain.of.your.license.server*"
export SNPSLMD_LICENSE_FILE="*port*@*domain.of.synopsys.license.server*"
/home/*user*/programs/microsemi/libero/v12.1/Libero/bin/libero
```

Do not forget to make it executable:

```
$ chmod u+x /home/*user*/scripts/launch_libero.sh

```

### Application menu entry

A freedesktop.org application menu entry (which a lot of desktop environments and window managers follow) can be added to the system by creating a `libero.desktop` file in your `~/.local/share/applications` directory:

 `~/.local/share/applications/libero.desktop` 
```
[Desktop Entry]
Version=1.0
Name=Libero SoC Design Suite v12.1
Comment=Microsemi Design Software for Microsemi FPGAs and SoCs
Exec=/home/*user*/scripts/launch_libero.sh
Icon=/home/*user*/programs/microsemi/libero/v12.1/libero.xpm
Terminal=false
Type=Application
Categories=Development
```

## Using a FlashPro programmer

Using a programmer (e.g. the Microsemi FlashPro5) requires two steps: Adding rules to gain device permissions and unloading a conflicting kernel module.

### Adding udev rules

To add the correct permissions for your user to access the programmer add the following file to your [Udev](/index.php/Udev "Udev") ruleset as root:

 `/etc/udev/rules.d/70-microsemi.rules` 
```
SUBSYSTEM=="usb", ATTR{idVendor}=="1514", ATTR{idProduct}=="2008", MODE="0666", GROUP="microsemi-prog"
SUBSYSTEM=="usb", ATTR{idVendor}=="0403", ATTR{idProduct}=="6001", MODE="0666", GROUP="microsemi-prog"
```

The group `microsemi-prog` is just an example, you may replace it by any group your user is in or add a new group and put your User *user* into it:

```
# groupadd microsemi-prog
# usermod -aG microsemi-prog *user*

```

You have to log out and in to apply the new group for the session. In a single terminal some can also apply the new group with `newgrp microsemi-prog`. To list your groups type `id` or `groups`.

### Removing conflicting kernel module

When plugging in the programmer it identifies as an FTDI serial device and loads the corresponding kernel driver. Liberos software does not work with that kernel driver so we have to unload it:

```
# rmmod ftdi_sio

```

To permanently unload the driver you may add it to your [Blacklist](/index.php/Blacklist "Blacklist"):

 `/etc/modprobe.d/blacklist-ftdi.conf`  `blacklist ftdi_sio` 

## Troubleshooting

### Libero crashes with SysXceptError

Libero till version 12.1 does not work on disks larger than 2TB of size. Neither the Libero binaries nor the vault nor your home-folder nor any project may reside on a partition larger than that size. If you cannot change the size of the partition where your home-folder is located start Libero with a different path for your home on a smaller disk:

```
$ HOME=/path/to/fake/home libero

```

Some may add that to the startup-script to apply it on start. The install and vault locations have to be set on installation or may be edited in `/home/*user*/programs/microsemi/libero/v12.1/Libero/data/install.def` when moving the files afterwards.