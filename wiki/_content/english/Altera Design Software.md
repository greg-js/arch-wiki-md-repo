From [altera.com Design Software - FPGA Design](https://www.altera.com/products/design-software/fpga-design.html):

	The Quartus® Prime design software is a multiplatform design environment that easily adapts to your specific needs in all phases of FPGA, CPLD, and SoC designs. The Quartus Prime software delivers the highest performance and productivity for Intel® FPGAs, CPLDs, and SoCs.

This tutorial shows how to download, install, and configure the following software from Altera:

*   Quartus Prime Standard Edition
    *   USB-Blaster (I and II) Download Cable Driver
*   ModelSim-Altera Edition (Included with Quartus Prime Standard Edition)

## Contents

*   [1 Quartus Prime Standard Edition](#Quartus_Prime_Standard_Edition)
    *   [1.1 Installation via AUR](#Installation_via_AUR)
    *   [1.2 Manual installation](#Manual_installation)
        *   [1.2.1 Get Quartus Prime](#Get_Quartus_Prime)
        *   [1.2.2 Install dependencies](#Install_dependencies)
        *   [1.2.3 Installing](#Installing)
        *   [1.2.4 Launching Quartus Prime](#Launching_Quartus_Prime)
        *   [1.2.5 Integrating Quartus Prime with the system](#Integrating_Quartus_Prime_with_the_system)
            *   [1.2.5.1 PATH variable](#PATH_variable)
            *   [1.2.5.2 Application menu entry - Quartus Prime](#Application_menu_entry_-_Quartus_Prime)
        *   [1.2.6 USB-Blaster Download Cable Driver](#USB-Blaster_Download_Cable_Driver)
    *   [1.3 Standard Edition License Validation](#Standard_Edition_License_Validation)
    *   [1.4 Troubleshooting](#Troubleshooting)
        *   [1.4.1 Empty (greyish) windows inside quartus (XMonad)](#Empty_(greyish)_windows_inside_quartus_(XMonad))
        *   [1.4.2 USB Blaster not working](#USB_Blaster_not_working)
            *   [1.4.2.1 JTAG chain broken](#JTAG_chain_broken)
            *   [1.4.2.2 Error when scanning hardware - Server error](#Error_when_scanning_hardware_-_Server_error)
        *   [1.4.3 Installation hangs when installing Quartus Prime Help and/or ModelSim](#Installation_hangs_when_installing_Quartus_Prime_Help_and/or_ModelSim)
*   [2 ModelSim-Altera Edition](#ModelSim-Altera_Edition)
    *   [2.1 Install](#Install)
    *   [2.2 Compatibility with Archlinux](#Compatibility_with_Archlinux)
        *   [2.2.1 With the kernel 4.x and Upwards](#With_the_kernel_4.x_and_Upwards)
        *   [2.2.2 With freetype2 2.5.0.1-1](#With_freetype2_2.5.0.1-1)
        *   [2.2.3 With fontconfig 2.12.6](#With_fontconfig_2.12.6)
        *   [2.2.4 With ncurses 5.9](#With_ncurses_5.9)
        *   [2.2.5 lib32-glibc 2.23-1](#lib32-glibc_2.23-1)
    *   [2.3 Application Menu Entry - ModelSim-Altera Edition](#Application_Menu_Entry_-_ModelSim-Altera_Edition)
    *   [2.4 Troubleshooting](#Troubleshooting_2)
        *   [2.4.1 Resolving the "ModelSim Failed to access library 'work'" error](#Resolving_the_"ModelSim_Failed_to_access_library_'work'"_error)
        *   [2.4.2 Crash with "Error: couldn't open socket: host is unreachable"](#Crash_with_"Error:_couldn't_open_socket:_host_is_unreachable")

## Quartus Prime Standard Edition

### Installation via AUR

To install the latest version of Quartus Prime and Modelsim install the package [quartus-free](https://aur.archlinux.org/packages/quartus-free/).

**Note:** This package will install all the devices supported by Quartus Prime. To do a minimal installation see the manual installation instruction.

To start Quartus Prime execute `quartus`.

To program a FPGA (via the USB-Blaster) the user needs to be part of the `plugdev` group.

### Manual installation

The following procedure shows how to download, install, and configure Altera Quartus Prime Standard Edition v15.1 for Arch Linux.

**Note:** The following tutorial works for older Quartus II and ModelSim versions, including both Subscription Editions and Web Editions, from at-least v13.0 through v15.0.

Quartus Prime is Altera's design software collection to design and interact with all their FPGAs/CPLDs/etc. products.

The procedure focuses on Arch Linux 64-bit systems, although 32-bit installations should work fine too.

Quartus Prime Standard Edition v15.1 is [officially supported](http://www.altera.com/download/os-support/oss-index.html) for RHEL 5 and RHEL 6, but since it is one of those huge collections of proprietary software that does not interact so much with the distribution, it is fairly easy to install on Arch Linux.

#### Get Quartus Prime

In [Altera's Downloads section](http://dl.altera.com/?edition=standard), select Linux as the operating system and get the *Combined Files* tar archive (something like `Quartus-15.1.2.193-linux-complete.tar`).

#### Install dependencies

Although the main Quartus Prime software is 64-bit, alot of Altera tools shipped with Quartus Prime are still 32-bit software. Those include the Nios II EDS and Qsys, for example. This is why we need to install lots of `lib32-` libraries and other programs from the Arch Linux multilib repo. Obviously, if you have a 32-bit Arch Linux system, you do not need the multilib versions.

In order to install multilib packages using [pacman](/index.php/Pacman "Pacman"), you need to enable the [multilib](/index.php/Multilib "Multilib") repository first (if not already done).

All the packages required below are taken from [Altera Software Installation and Licensing](http://www.altera.com/literature/manual/quartus_install.pdf) (sect. 1-4).

Let us first install the native versions of the required packages: [expat](https://www.archlinux.org/packages/?name=expat) [fontconfig](https://www.archlinux.org/packages/?name=fontconfig) [freetype2](https://www.archlinux.org/packages/?name=freetype2) [xorg-fonts-type1](https://www.archlinux.org/packages/?name=xorg-fonts-type1) [glibc](https://www.archlinux.org/packages/?name=glibc) [gtk2](https://www.archlinux.org/packages/?name=gtk2) [libcanberra](https://www.archlinux.org/packages/?name=libcanberra) [libpng](https://www.archlinux.org/packages/?name=libpng) [libpng12](https://www.archlinux.org/packages/?name=libpng12) [libice](https://www.archlinux.org/packages/?name=libice) [libsm](https://www.archlinux.org/packages/?name=libsm) [util-linux](https://www.archlinux.org/packages/?name=util-linux) [ncurses](https://www.archlinux.org/packages/?name=ncurses) [tcl](https://www.archlinux.org/packages/?name=tcl) [tcllib](https://aur.archlinux.org/packages/tcllib/) [zlib](https://www.archlinux.org/packages/?name=zlib) [libx11](https://www.archlinux.org/packages/?name=libx11) [libxau](https://www.archlinux.org/packages/?name=libxau) [libxdmcp](https://www.archlinux.org/packages/?name=libxdmcp) [libxext](https://www.archlinux.org/packages/?name=libxext) [libxft](https://www.archlinux.org/packages/?name=libxft) [libxrender](https://www.archlinux.org/packages/?name=libxrender) [libxt](https://www.archlinux.org/packages/?name=libxt) [libxtst](https://www.archlinux.org/packages/?name=libxtst) [ld-lsb](https://www.archlinux.org/packages/?name=ld-lsb).

And the multilib versions: [lib32-expat](https://www.archlinux.org/packages/?name=lib32-expat) [lib32-fontconfig](https://www.archlinux.org/packages/?name=lib32-fontconfig) [lib32-freetype2](https://www.archlinux.org/packages/?name=lib32-freetype2) [lib32-glibc](https://www.archlinux.org/packages/?name=lib32-glibc) [lib32-gtk2](https://www.archlinux.org/packages/?name=lib32-gtk2) [lib32-libcanberra](https://www.archlinux.org/packages/?name=lib32-libcanberra) [lib32-libpng](https://www.archlinux.org/packages/?name=lib32-libpng) [lib32-libpng12](https://www.archlinux.org/packages/?name=lib32-libpng12) [lib32-libice](https://www.archlinux.org/packages/?name=lib32-libice) [lib32-libsm](https://www.archlinux.org/packages/?name=lib32-libsm) [lib32-util-linux](https://www.archlinux.org/packages/?name=lib32-util-linux) [lib32-ncurses](https://www.archlinux.org/packages/?name=lib32-ncurses) [lib32-zlib](https://www.archlinux.org/packages/?name=lib32-zlib) [lib32-libx11](https://www.archlinux.org/packages/?name=lib32-libx11) [lib32-libxau](https://www.archlinux.org/packages/?name=lib32-libxau) [lib32-libxdmcp](https://www.archlinux.org/packages/?name=lib32-libxdmcp) [lib32-libxext](https://www.archlinux.org/packages/?name=lib32-libxext) [lib32-libxft](https://www.archlinux.org/packages/?name=lib32-libxft) [lib32-libxrender](https://www.archlinux.org/packages/?name=lib32-libxrender) [lib32-libxt](https://www.archlinux.org/packages/?name=lib32-libxt) [lib32-libxtst](https://www.archlinux.org/packages/?name=lib32-libxtst).

You are now ready to install and launch Quartus Prime.

#### Installing

To install, first extract the downloaded tar archive:

```
$ tar -xvf Quartus-15.1.2.193-linux-complete.tar

```

and launch `setup.sh`. If you are going to install Quartus Prime anywhere outside your home directory, run it as root:

```
# ./setup.sh

```

You will probably get a GUI install wizard if you installed all the aforementioned packages. You might also get a command-line interactive install wizard, which will do the same.

The default install path is `/root/altera/15.1`, but some prefer `/opt/altera/15.1`, which we assume for the rest of this document.

**Make sure to include** the 64-bit option of Quartus Prime when installing.

#### Launching Quartus Prime

Assuming you installed Quartus Prime in `/opt/altera/15.1`, Quartus Prime binaries are located into `/opt/altera/15.1/quartus/bin`. Run Quartus Prime (64-bit version):

```
$ /opt/altera/15.1/quartus/bin/quartus --64bit

```

or the 32-bit version:

```
$ /opt/altera/15.1/quartus/bin/quartus

```

All other Altera tools, like Qsys, the Nios II EDS, Chip Planner and SignalTap II may be launched without any problem from the *Tools* menu of Quartus Prime.

#### Integrating Quartus Prime with the system

Quartus Prime can be integrated with the system in several ways, but those are optional.

##### `PATH` variable

Let us now add the Quartus `bin` folder to the `PATH` variable so it can be executed without specifying its absolute path. Create a `quartus.sh` file in the `/etc/profile.d` directory

 `/etc/profile.d/quartus.sh`  `export PATH=$PATH:/opt/altera/15.1/quartus/bin` 

Also, make sure it can be executed:

```
# chmod +x /etc/profile.d/quartus.sh

```

Please note that those `profile.d` files are loaded at each *login*. In the mean time, simply `source` that file in Bash:

```
$ source /etc/profile.d/quartus.sh

```

Other environment variables related to Quartus can be found in [the official installation manual](http://www.altera.com/literature/manual/quartus_install.pdf).

Even if `quartus` is now a command known by Bash, you still need to add the `--64bit` argument in order to launch the 64-bit version. A shell alias, like `quartus64`, is a great solution to avoid typing it each time.

##### Application menu entry - Quartus Prime

A freedesktop.org application menu entry (which a lot of desktop environments and window managers follow) can be added to the system by creating a `quartus.desktop` file in your `~/.local/share/applications` directory:

 `~/.local/share/applications/quartus.desktop` 
```
[Desktop Entry]
Version=1.0
Name=Quartus Prime Standard Edition v15.1
Comment=Quartus Prime design software for Altera FPGA's
Exec=/opt/altera/15.1/quartus/bin/quartus --64bit
Icon=/opt/altera/15.1/quartus/adm/quartusii.png
Terminal=false
Type=Application
Categories=Development
```

#### USB-Blaster Download Cable Driver

The USB-Blaster (I and II) Download Cable is a cable that allows you to download configuration data from your computer to your FPGA, CPLD or EEPROM configuration device. However, Altera only provides official support for RHEL, SUSE Entreprise and CentOS, so we are required to do a little bit of work to make it work with Arch Linux. If you want some more detail about this cable, please refer to the [USB-Blaster Download Cable User Guide](http://www.altera.com/literature/ug/ug_usb_blstr.pdf).

Create a new udev rule:

 `/etc/udev/rules.d/51-altera-usb-blaster.rules` 
```
SUBSYSTEM=="usb", ATTR{idVendor}=="09fb", ATTR{idProduct}=="6001", MODE="0666"
SUBSYSTEM=="usb", ATTR{idVendor}=="09fb", ATTR{idProduct}=="6002", MODE="0666"
SUBSYSTEM=="usb", ATTR{idVendor}=="09fb", ATTR{idProduct}=="6003", MODE="0666"
SUBSYSTEM=="usb", ATTR{idVendor}=="09fb", ATTR{idProduct}=="6010", MODE="0666"
SUBSYSTEM=="usb", ATTR{idVendor}=="09fb", ATTR{idProduct}=="6810", MODE="0666"
```

Then, *reload* that file using `udevadm` (disconnect any Altera device from port USB port before this command):

```
# udevadm control --reload

```

To check that everything is working, plug your FPGA or CPLD board using your USB-Blaster Download Cable and run:

```
$ /opt/altera/15.1/quartus/bin/jtagconfig

```

You should have an output similar to this one

```
1) USB-Blaster [USB 1-1.1]
  020B30DD   EP2C15/20

```

If jtagconfig output does not contain board name, you might have problems with launching nios2 tools. In order to workaround this issue, you should copy jtagd settings to /etc/jtagd:

```
# mkdir /etc/jtagd
# cp /opt/altera/15.1/quartus/linux/pgm_parts.txt /etc/jtagd/jtagd.pgm_parts

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

If there seems to be an error message about "linux64" and you did not install the 64-bit version of Quartus Prime, create a symlink from `linux` to `linux64` in `/opt/altera/15.1/quartus`:

```
# ln -s /opt/altera/15.1/quartus/linux /opt/altera/15.1/quartus/linux64

```

### Standard Edition License Validation

Configuring the path to your Quartus Prime Standard Edition license file from the Quartus Prime settings interface is not enough for successful license validation. The license validation routine looks for your MAC address on device `eth0`. This was the legacy name for your ethernet controller; now `systemd` dynamically allocates a name to your device on boot - this can be different from machine to machine. We need to rename that device back to the expected `eth0`.

Create a new udev rule:

 `/etc/udev/rules.d/10-network.rules`  `SUBSYSTEM=="net", ACTION=="add", ATTR{address}=="xx:xx:xx:xx:xx:xx", NAME="eth0"` 

where `xx:xx:xx:xx:xx:xx` is your networking device's MAC address. Then, *reload* that file using `udevadm`:

```
# udevadm control --reload

```

Alternatively a dummy `eth0` network interface can be created by `systemd-networkd` daemon dynamically at boot. Create the file `25-dummy.netdev` in the `/etc/systemd/network/` directory

 `/etc/systemd/network/25-dummy.netdev` 
```
[Match]
Host=hostname

[NetDev]
Name=eth0
Kind=dummy
MACAddress=xx:xx:xx:xx:xx:xx
```

where `xx:xx:xx:xx:xx:xx` is the licensed networking device's MAC address and `hostname` is your machine's hostname. Finally ensure `systemd-networkd` service is [enabled](/index.php/Enable "Enable") and [started](/index.php/Start "Start").

The Quartus Prime Standard Edition license validation routine also uses the deprecated networking tool `ifconfig` to validate your networking devices MAC address as per your Quartus Prime license. The deprecated networking package `net-tools` contains the `ifconfig` tool. Thus one must also install the `net-tools` package for Quartus Prime Standard Edition licensing validation success.

### Troubleshooting

#### Empty (greyish) windows inside quartus (XMonad)

Some of the built-in editors in quartus such as ip editors and qsys only show a blank window. To workaround this issue change the name that is reported by your window manager to for example [`LG3D`](http://stackoverflow.com/questions/14486147/java-web-start-application-shows-empty-window-on-xmonad). To change the name reported by XMonad see the [documentation](http://xmonad.org/xmonad-docs/xmonad-contrib/XMonad-Hooks-SetWMName.html).

#### USB Blaster not working

Run:

```
 $ /opt/altera/quartus/bin/jtagconfig

```

Then depending on the output:

##### JTAG chain broken

```
 1) USB-Blaster [3-2]
   Unable to read device chain - JTAG chain broken

```

A possible cause can be a missing 32 bit version of libudev, install [lib32-libudev0-shim](https://www.archlinux.org/packages/?name=lib32-libudev0-shim) ([source](https://www-acc.gsi.de/wiki/Timing/QuartusInstallUbuntu1404.)).

##### Error when scanning hardware - Server error

```
 Connecting to server(s) [........          ]
 Error when scanning hardware - Server error

```

A workaround is to edit `/etc/jtagd.conf` or `$HOME/.jtagd.conf` (depending on whether you want to run jtagd as root or unprivileged user) to include the following line:

```
 Password = "changeme";

```

The second step is to add the server:

```
 $ /opt/altera/quartus/bin/jtagconfig --addserver 127.0.0.1 changeme

```

If you still have problems, try restarting `jtagd`:

```
 # killall -9 jtagd
 $ /opt/altera/quartus/bin/jtagd

```

#### Installation hangs when installing Quartus Prime Help and/or ModelSim

For Quartus Prime Lite 17.1, or probably other versions, the installation process hangs when installing Quartus Prime Help and ModelSim. One workaround is to uncheck them in the "Select Components" step and install them later manually from the components folder.

## ModelSim-Altera Edition

### Install

ModelSim-Altera Edition is downloaded and installed from the *Combined Files* tar archive `Quartus-15.1.2.193-linux-complete.tar` as part of the Quartus Prime installation procedure above.

### Compatibility with Archlinux

#### With the kernel 4.x and Upwards

**Note:** ModelSim Starter Edition installation uses the path `/opt/altera/15.1/modelsim_ase/` where ModelSim Subscription Edition installation uses the path `/opt/altera/15.1/modelsim_ae/`; the following assumes the ModelSim Subcription Edition installation.

Modelsim has a problem with version 4 of the linux kernel. You need to edit the `vsim` script to make it compatible. This file may be be read only, so temporarily give yourself write permissions and:

change

 `/opt/altera/15.1/modelsim_ae/vco line 206`  `*)                vco="linux_rh60" ;;` 

to

 `/opt/altera/15.1/modelsim_ae/vco line 206`  `*)                vco="linux" ;;` 

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

Another error message caused by the same problem:

```
$ vsim
Error in startup script:
Initialization problem, exiting.
Initialization problem, exiting.
    while executing
"InitializeINIFile quietly"
    invoked from within
"ncFyP12 -+"
    (file "/mtitcl/vsim/vsim" line 1)
** Fatal: Read failure in vlm process (0,0)

```

There are two solutions to solve this problem. The first involves downgrading the Package (probably via the [Arch Linux Archive](/index.php/Arch_Linux_Archive "Arch Linux Archive")). If you are using the 32-bit version, it is sufficient to downgrade [lib32-freetype2](https://www.archlinux.org/packages/?name=lib32-freetype2). The second and more elegant solution involves replacing the old freetype version for ModelSim only without withholding updates on the whole system (originally proposed at the now-dead link [http://communities.mentor.com/mgcx/message/46770](http://communities.mentor.com/mgcx/message/46770)):

*   Copy the lib32-freetype2 2.5.0.1-1 library and symlinks somewhere in the altera folder, eg: `$HOME/altera/xx.x/lib32/`

```
libfreetype.so
libfreetype.so.6
libfreetype.so.6.10.2
```

*   Edit the ModelSim script `/opt/altera/15.1/modelsim_ae/vco` and add after `dir=`dirname "$arg0"``

```
export LD_LIBRARY_PATH=${dir}/../lib32

```

**Note:** The quartus script will need to have write permissions added to it.

When ModelSim is launched directly from Quartus the error may persist. In this case, add the same line to `quartus/bin/quartus_sh`.

#### With fontconfig 2.12.6

Similar as the problem with freetype above, the upgrade from fontconfig 2.12.6+5+g665584a-1 to fontconfig 2.13.0+10+g58f5285 causes ModelSim to not start anymore because that fontconfig version would need a newer freetype version. It yields the following error message:

```
modelsim_ase/bin/../linux/vish: symbol lookup error: /usr/lib32/libfontconfig.so.1: undefined symbol: FT_Done_MM_Var

```

So, in addition to libfreetype, you also have to supply a downgraded version of libfontconfig to successfully start ModelSim.

#### With ncurses 5.9

The upgrade from ncurses version 5.9-7 to 6.0-1 (and later) (September 2015[[2]](https://projects.archlinux.org/svntogit/packages.git/commit/trunk?h=packages/ncurses&id=ddb1abecfe25260321c9cb0ef24f29351f28ecb3)) causes the following error in ModelSim:

```
$ vsim
vish: error while loading shared libraries: libncurses.so.5: cannot open shared object file: No such file or directory
[1]  + exit 127   vsim

```

There are two solutions to this problem. One is to use [ncurses5-compat-libs](https://aur.archlinux.org/packages/ncurses5-compat-libs/) and tweak the PKGBUILD to compile a 32-bit version of the library. (Or use [lib32-ncurses5-compat-libs](https://aur.archlinux.org/packages/lib32-ncurses5-compat-libs/)) This will provide the latest version of ncurses with an ncurses5-compatible ABI.

The other solution is to download the ncurses 5.9 source, compile it, and copy the generated libraries and symlinks to the same directory as the freetype2 libraries.

Compiling ncurses 5.9 may lead to problems using GCC 5.x. It is also possible to get a precompiled library, using the [Arch Linux Archive](/index.php/Arch_Linux_Archive "Arch Linux Archive"). The package can be found at [http://ala.seblu.net/packages/l/lib32-ncurses/](http://ala.seblu.net/packages/l/lib32-ncurses/).

#### lib32-glibc 2.23-1

Originally discussed here: [https://bbs.archlinux.org/viewtopic.php?id=212531](https://bbs.archlinux.org/viewtopic.php?id=212531)

The upgrade from lib32-glibc version 2.23-1 to later versions of lib32-glibc breaks FlexLM and prevents ModelSim from checking out a license. One workaround is to download the [archived lib32-glibc-2.23-1](https://archive.archlinux.org/packages/l/lib32-glibc/) and extract it to a directory such as `${HOME}/altera/xx.x/lib32/glibc223-1`. Then create or modify the `LD_LIBRARY_PATH` environment variable at the top of the `/opt/altera/xx.x/modelsim_ae/vco` script to include the new glibc223-1/usr/lib32 directory in the search path:

```
export LD_LIBRARY_PATH=${HOME}/altera/xx.x/lib32;${HOME}/altera/xx.x/lib32/glibc223-1/usr/lib32

```

### Application Menu Entry - ModelSim-Altera Edition

You can add Modelsim to your system application menu by creating a `modelsim.desktop` file in your `~/.local/share/applications` directory

 `~/.local/share/applications/modelsim.desktop` 
```
[Desktop Entry]
Version=1.0
Name=ModelSim-Altera Edition
Comment=ModelSim simulation software for Altera FPGA's
Exec=/opt/altera/15.1/modelsim_ae/bin/vsim
Icon=/opt/altera/15.1/modelsim_ae/modesim.gif
Terminal=true
Type=Application
Categories=Development
```

### Troubleshooting

#### Resolving the "ModelSim Failed to access library 'work'" error

The solution was originally documented here: [http://jackeyblog.blogspot.com/2005/07/note-myself-modelsim-failed-to-access.html](http://jackeyblog.blogspot.com/2005/07/note-myself-modelsim-failed-to-access.html)

If you receive the error:

```
Error: (vcom-19) Failed to access library 'work' at "work". 

```

when running a simulation in a new directory, you must create a new `work` directory. Execute the following in the ModelSim console:

```
ModelSim> vlib work

```

#### Crash with "Error: couldn't open socket: host is unreachable"

If ModelSilm crash while trying to start a simulation with the error:

```
Error: couldn't open socket: host is unreachable
Trouble making server.

```

then you may need to add an entry for `localhost` in your `/etc/hosts` file:

 `/etc/hosts` 
```
  #<ip-address>  <hostname.domain.org>  <hostname>
  ...
  127.0.0.1      localhost              *yourhostname*

```