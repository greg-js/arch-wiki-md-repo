From [[1]](https://www.microsemi.com/product-directory/design-resources/1750-libero-soc#overview):

	Libero® SoC Design Suite offers high productivity with its comprehensive, easy-to-learn, easy-to-adopt development tools for designing with Microsemi's PolarFire, IGLOO2, SmartFusion2, RTG4, SmartFusion, IGLOO, ProASIC3 and Fusion families.

This article shows how to install the Microsemi Libero Toolchain on Arch Linux.

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

## Installation

### Preparations

Libero needs about 45GiB free diskspace.

#### Package installation

Libero depends on some 32-bit packages from multilib. In order to install multilib packages using [pacman](/index.php/Pacman "Pacman"), you need to enable the [multilib](/index.php/Multilib "Multilib") repository first (if not already done).

Install the following packages: [openmotif](https://www.archlinux.org/packages/?name=openmotif) [zlib](https://www.archlinux.org/packages/?name=zlib) [lib32-libxft](https://www.archlinux.org/packages/?name=lib32-libxft) [lib32-libpng12](https://www.archlinux.org/packages/?name=lib32-libpng12) [lib32-dbus](https://www.archlinux.org/packages/?name=lib32-dbus) [lib32-sqlite](https://www.archlinux.org/packages/?name=lib32-sqlite) [lib32-libpulse](https://www.archlinux.org/packages/?name=lib32-libpulse)

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

Libero tries to load an old version of the motif library. Modify the following file and change the 3 to a 4 in the `case `uname`` block:

 `/home/*user*/programs/microsemi/libero/v12.1/Libero/bin/actel_setup_vars` 
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
This is discouraged as it tampers with a directory preferably modified by [pacman](/index.php/Pacman "Pacman") when installing packages. However it might be useful when reinstalling Libero or installing a newer version of it because the manual modification of the file above can be skipped.

Furthermore the outdated `libz` version shipped by Microsemi does not work with the repository version of [lib32-libpng12](https://www.archlinux.org/packages/?name=lib32-libpng12). In `/home/*user*/programs/microsemi/libero/v12.1/Libero/lib` do the following:

```
$ mv libz.so.1 libz.so.1.old
$ ln -s /lib/libz.so libz.so.1

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
LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/home/*user*/lib/qt5_32/5.5/gcc/lib
LM_LICENSE_FILE="*port*@*domain.of.your.license.server*"
SNPSLMD_LICENSE_FILE="*port*@*domain.of.synopsys.license.server*"
/home/*user*/programs/microsemi/libero/v12.1//Libero/bin/libero
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