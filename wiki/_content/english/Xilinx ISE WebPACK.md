The Xilinx ISE WebPACK is a complete FPGA/CPLD programmable logic design suite providing:

*   Specification of programmable logic via schematic capture or Verilog/VHDL
*   Synthesis and Place & Route of specified logic for various Xilinx FPGAs and CPLDs
*   Functional (Behavioral) and Timing (post-Place & Route) simulation
*   Download of configuration data into target device via communications cable

The development of the ISE WebPACK has been stopped in favor of the [Vivado Suite](/index.php/Xilinx_Vivado "Xilinx Vivado"), but it is still useful to develop for older devices not supported by the new suite.

While Arch Linux is not one of the officially supported distributions, many features are known to work on Arch Linux.

## Contents

*   [1 Prerequisites](#Prerequisites)
    *   [1.1 Download ISE WebPACK](#Download_ISE_WebPACK)
    *   [1.2 Dependencies](#Dependencies)
    *   [1.3 Default Shell](#Default_Shell)
*   [2 Installation](#Installation)
    *   [2.1 Install from AUR](#Install_from_AUR)
    *   [2.2 Manual installation](#Manual_installation)
    *   [2.3 Launching the ISE design tools](#Launching_the_ISE_design_tools)
        *   [2.3.1 Launching via desktop icons](#Launching_via_desktop_icons)
    *   [2.4 License Installation](#License_Installation)
    *   [2.5 Node-Locked Licenses](#Node-Locked_Licenses)
*   [3 Post-Installation Fixes and Tweaks](#Post-Installation_Fixes_and_Tweaks)
    *   [3.1 Dynamic Library Fix (libstdc++.so)](#Dynamic_Library_Fix_(libstdc++.so))
    *   [3.2 Digilent USB-JTAG Drivers](#Digilent_USB-JTAG_Drivers)
    *   [3.3 Xilinx Platform Cable USB-JTAG Drivers](#Xilinx_Platform_Cable_USB-JTAG_Drivers)
    *   [3.4 Locale Issues](#Locale_Issues)
    *   [3.5 Segmentation Fault on PlanAhead](#Segmentation_Fault_on_PlanAhead)
    *   [3.6 GNU make](#GNU_make)
    *   [3.7 Running Xilinx tools from within KDE](#Running_Xilinx_tools_from_within_KDE)
    *   [3.8 CORE Generator fails to generate core](#CORE_Generator_fails_to_generate_core)

## Prerequisites

### Download ISE WebPACK

The Xilinx ISE WebPACK is a freeware software released under a proprietary license which does not allow redistribution. To obtain the install data visit [the official download page](http://www.xilinx.com/support/download/index.html/content/xilinx/en/downloadNav/design-tools.html).

### Dependencies

Several tools included in the ISE Webpack (and the installer itself) depends on [ncurses5-compat-libs](https://aur.archlinux.org/packages/ncurses5-compat-libs/). [Additionally](https://forums.xilinx.com/t5/General-Technical-Discussion/Xilinx-issues-on-Linux/td-p/194576) other tools (e.g. the FPGA editor) requires [libstdc++5](https://www.archlinux.org/packages/?name=libstdc%2B%2B5), [openmotif](https://www.archlinux.org/packages/?name=openmotif), [xorg-fonts-75dpi](https://www.archlinux.org/packages/?name=xorg-fonts-75dpi) and [xorg-fonts-100dpi](https://www.archlinux.org/packages/?name=xorg-fonts-100dpi).

If you plan to develop software for an embedded ARM core (e.g. for Xilinx Zynq SoC devices), you will want to install the GCC cross-compiler bundled included with the Xilinx Embedded Development Kit (EDK). This compiler requires the [lib32-glibc](https://www.archlinux.org/packages/?name=lib32-glibc) package from the [multilib](/index.php/Multilib "Multilib") repository and [lib32-ncurses5-compat-libs](https://aur.archlinux.org/packages/lib32-ncurses5-compat-libs/) from the [AUR](/index.php/AUR "AUR").

### Default Shell

During the installation, the Mentor CodeSourcery toolchains for embedded processors can be installed along with the Xilinx tools. This installation silently fails when the default shell is set to [dash](/index.php/Dash "Dash"). Make sure `/usr/bin/sh` points to `/usr/bin/bash`.

This can be checked by running this command:

```
$ ls -l /usr/bin/sh

```

If the output looks like this:

```
`lrwxrwxrwx 1 root root 15 13 Mar 06:47 /usr/bin/sh -> bash`

```

then `/usr/bin/sh` already points to `/usr/bin/bash`. (the default in Arch Linux).

If not, link `/usr/bin/sh` to bash:

```
# ln -sfT bash /usr/bin/sh

```

## Installation

### Install from AUR

Install the package [xilinx-ise](https://aur.archlinux.org/packages/xilinx-ise/), you will have to place the tarball with the installation data in the same folder of the `PKGBUILD` before starting the building process.

### Manual installation

**Note:** The installation is last known to work with Xilinx ISE 14.7, requiring the dynamic library fix described below.

Extract the tarball containing the installation data:

```
$ tar -xvf Xilinx_ISE_DS_Lin_14.7_1015_1.tar

```

The ISE design tools installer is a Qt application. If you are running the KDE desktop environment, the installer may try to load the "Oxygen" widget theme, which will fail due to the older Qt framework bundled with the Xilinx ISE design tools. You need to remove the `QT_PLUGIN_PATH` environment variable before executing the installer:

```
$ unset QT_PLUGIN_PATH

```

Then, install the ISE Design Tools:

```
$ cd Xilinx_ISE_DS_Lin_14.7_1015_1
$ ./xsetup

```

Follow the instructions to install the ISE. By default, the whole application is installed to `/opt/Xilinx/`, so make sure the user running the installer has permissions to write to this directory.

During installation, uncheck the "Install Cable Drivers" option. Leaving it checked will cause errors during the installation.

### Launching the ISE design tools

The ISE design tools include a shell script that modifies the environment variables (mostly `PATH` and `LD_LIBRARY_PATH`). This script must be sourced before starting the ISE tools:

```
$ source /opt/Xilinx/14.7/ISE_DS/settings64.sh

```

or, for a 32-bit installation:

```
$ source /opt/Xilinx/14.7/ISE_DS/settings32.sh

```

Then, the ISE design tools will be found in your `PATH` and can be started by typing their name in the terminal (e.g. `ise`, `planAhead`, `xsdk`, ...)

#### Launching via desktop icons

You can also create a [desktop entry](/index.php/Desktop_entry "Desktop entry") at `/usr/share/applications/`

 `/usr/share/applications/ise.desktop` 
```
#!/usr/bin/env xdg-open
[Desktop Entry]
Version=1.0
Type=Application
Name=Xilinx ISE
Exec=sh -c "unset LANG && unset QT_PLUGIN_PATH && source /opt/Xilinx/14.7/ISE_DS/settings64.sh && ise"
Icon=/opt/Xilinx/14.7/ISE_DS/ISE/data/images/pn-ise.png
Categories=Development;
Comment=Xilinx ISE
StartupWMClass=_pn
```

After that you can copy this file to the `~/Desktop` folder and launch ISE tools from the desktop.

### License Installation

After requesting a WebPACK license from Xilinx using their [Licensing Site](http://www.xilinx.com/getlicense/), you will be e-mailed a license file. This file can be imported with the Xilinx License Manager (run `xlcm -manage` from the terminal).

Another way to import the license is to simply copy it to the `~/.Xilinx` or `/opt/Xilinx/14.7/ISE_DS/ISE/coregen/core_licenses` directory.

### Node-Locked Licenses

Arch Linux by default uses systemd's [Predictable Network Interface Names](/index.php/Network_configuration#Device_names "Network configuration"). This means that your system will most likely not have its network interfaces named "eth0", "eth1" and so forth.

However, the Xilinx License Manager looks for these names to find out the system's MAC addresses, which are used for node-locked licenses. If you want to use node-locked licenses, you will have to manually assign to your interface a name in the format expected by the License Manager. The [change device name](/index.php/Network_configuration#Change_device_name "Network configuration") article subsection explain how to write an [udev](/index.php/Udev "Udev") rule to do so. If your machine does not have a wired ethernet adapter, then it is possible to use the systemd and the `dummy` kernel module to create a virtual ethernet adapter with the proper MAC address. To do this, create

 `/etc/systemd/network/25-dummy.netdev` 
```
[Match]

[NetDev]
Name=eth0
Kind=dummy
MACAddress=00:11:22:33:44:55:66
```

and restart systemd-networkd.

## Post-Installation Fixes and Tweaks

After installation, a few manual fixes are required to work around problems caused by running the Xilinx tools on a Linux distribution that is not officially supported by Xilinx. Some of these fixes are taken from [this forum post.](http://zedboard.org/content/ise-142-bug-reports)

### Dynamic Library Fix (libstdc++.so)

**Note:** This workaround is already applied in the AUR package

The ISE tools supply an outdated version of the libstdc++.so library, which may cause segfaults when using the Xilinx Microprocessor Debugger and prevents the usage of the oxygen-gtk theme. This outdated version is located in two directories within the installation tree: `/opt/Xilinx/14.7/ISE_DS/ISE/lib/lin64/` and `/opt/Xilinx/14.7/ISE_DS/common/lib/lin64`. To use Arch's newer version of libstdc++, rename or delete the original files and replace them with symlinks:

```
$ cd /opt/Xilinx/14.7/ISE_DS/ISE/lib/lin64/
$ mv libstdc++.so libstdc++.so.bak
$ mv libstdc++.so.6 libstdc++.so.6.bak
$ mv libstdc++.so.6.0.8 libstdc++.so.6.0.8.bak
$ ln -s /usr/lib/libstdc++.so
$ ln -s libstdc++.so libstdc++.so.6
$ ln -s libstdc++.so libstdc++.so.6.0.8

```

Then, repeat this process in the `/opt/Xilinx/14.7/ISE_DS/common/lib/lin64` directory.

### Digilent USB-JTAG Drivers

To use Digilent Adept USB-JTAG adapters (e.g. the onboard JTAG adapter on the [ZedBoard](http://www.zedboard.org)) from within the Xilinx design tools, you need to install the Digilent [Adept Runtime](http://store.digilentinc.com/digilent-adept-2-download-only/) and [Plugin](http://store.digilentinc.com/digilent-plugin-for-xilinx-tools-download-only/).

Make sure you have installed [fxload](https://aur.archlinux.org/packages/fxload/) from the [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository") .

To install the Digilent Adept Runtime, it is recommended to install [digilent.adept.runtime](https://aur.archlinux.org/packages/digilent.adept.runtime/) from the [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository").

In addition, installing [digilent.adept.utilities](https://aur.archlinux.org/packages/digilent.adept.utilities/) may do good to configuring your board.

To install the Digilent plugin, you have to copy two files to the ISE plugin directory. Run the following commands as root:

```
$ mkdir -p /opt/Xilinx/14.7/ISE_DS/ISE/lib/lin64/plugins/Digilent/libCseDigilent
$ cd /opt/Xilinx/14.7/ISE_DS/ISE/bin/lin64/digilent/libCseDigilent_2.4.4-x86_64/lin64/14.1/libCseDigilent
$ cp libCseDigilent.{so,xml} /opt/Xilinx/14.7/ISE_DS/ISE/lib/lin64/plugins/Digilent/libCseDigilent
$ chmod -x /opt/Xilinx/14.7/ISE_DS/ISE/lib/lin64/plugins/Digilent/libCseDigilent/libCseDigilent.xml

```

Finally, add every user that should have access to the Digilent USB-JTAG adapter to the "uucp" group.

To grant access to the usb driver for normal users you may have to add the USB Vendor/Product IDs of your JTAG adapter which can be found with

```
$ lsusb | grep Xilinx

```

to the udev rules in `/etc/udev/rules.d/20-digilent.rules`:

```
SUBSYSTEM=="usb", ATTRS{idVendor}=="xxxx", ATTRS{idProduct}=="xxxx", GROUP="users", MODE="666"

```

If it still doesn't work, you can make further reading in [Xilinx_JTAG_Linux](http://www.george-smart.co.uk/wiki/Xilinx_JTAG_Linux). The magic git repo there may be help.

### Xilinx Platform Cable USB-JTAG Drivers

Make sure you have installed [fxload](https://aur.archlinux.org/packages/fxload/) or [fxload-libusb](https://aur.archlinux.org/packages/fxload-libusb/) from the [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository") . We need to build driver from source (git and some make stuff need to be installed, make will say what programs or libraries are missed):

```
$ cd /opt/Xilinx
$ sudo git clone [git://git.zerfleddert.de/usb-driver](git://git.zerfleddert.de/usb-driver)
$ cd usb-driver/
$ sudo make

```

If you using 32-bit version of ISE on 64-bit system, pass "lib32" to make:

```
$ sudo make lib32

```

And install driver (replace 14.7 to your version):

```
$ ./setup_pcusb /opt/Xilinx/14.7/ISE_DS/ISE

```

Or in older versions:

```
$ ./setup_pcusb /opt/Xilinx/10.x/ISE

```

For the new fxload version: [fxload-libusb](https://aur.archlinux.org/packages/fxload-libusb/), the file /etc/udev/rules.d/xusbdfwu.rules needs to be changed to:

 `$ /etc/udev/rules.d/xusbdfwu.rules` 
```
ACTION=="add", SUBSYSTEM=="usb", ATTRS{idVendor}=="03fd", ATTRS{idProduct}=="0008", MODE="666"
ACTION=="add", SUBSYSTEM=="usb", ATTRS{idVendor}=="03fd", ATTRS{idProduct}=="0007", RUN+="/usr/bin/fxload-libusb -t fx2 -I /usr/share/xusbdfwu.hex -d 03fd:0007"
ACTION=="add", SUBSYSTEM=="usb", ATTRS{idVendor}=="03fd", ATTRS{idProduct}=="0009", RUN+="/usr/bin/fxload-libusb -t fx2 -I /usr/share/xusb_xup.hex -d 03fd:0009"
ACTION=="add", SUBSYSTEM=="usb", ATTRS{idVendor}=="03fd", ATTRS{idProduct}=="000d", RUN+="/usr/bin/fxload-libusb -t fx2 -I /usr/share/xusb_emb.hex -d 03fd:000d"
ACTION=="add", SUBSYSTEM=="usb", ATTRS{idVendor}=="03fd", ATTRS{idProduct}=="000f", RUN+="/usr/bin/fxload-libusb -t fx2 -I /usr/share/xusb_xlp.hex -d 03fd:000f"
ACTION=="add", SUBSYSTEM=="usb", ATTRS{idVendor}=="03fd", ATTRS{idProduct}=="0013", RUN+="/usr/bin/fxload-libusb -t fx2 -I /usr/share/xusb_xp2.hex -d 03fd:0013"
ACTION=="add", SUBSYSTEM=="usb", ATTRS{idVendor}=="03fd", ATTRS{idProduct}=="0015", RUN+="/usr/bin/fxload-libusb -t fx2 -I /usr/share/xusb_xse.hex -d 03fd:0015"

```

When performing this command, the udev rules file will be created. You can reload udev rules to apply changes immediately:

```
$ sudo udevadm control --reload-rules

```

If driver installed correctly and udev rule works, STATUS led should turn on (green or red depending on voltage presence on VREF PIN)

**Note:** This step is only required for versions of Xilinx ISE older than 11.1: In older versions, iMPACT doesn't correctly load the right drivers (it still tries to use windrvr6 drivers). To fix this, the environment variable LD_PRELOAD must be set so that the libusb drivers are loaded into iMPACT without recompiling it.

```
$ export LD_PRELOAD=/opt/Xilinx/usb-driver/libusb-driver.so

```

### Locale Issues

PlanAhead doesn't like locales using other literals than '.' as the decimal point (e.g. German, which uses ','). Run the following command before launching PlanAhead:

```
$ unset LANG

```

### Segmentation Fault on PlanAhead

When launching PlanAhead to generate a .ucf file, a segmentation fault may occur. The issue seems unrelated to the previous topic. The ISE console will show

```
"/opt/Xilinx/14.7/ISE_DS/PlanAhead/bin/rdiArgs.sh: line 64: 14275 Segmentation fault      $RDI_PROG $*"

```

The problem seems to come from the bundled JRE as described [here](http://forums.xilinx.com/t5/Installation-and-Licensing/RHEL5-64-bit-ISE-13-1-PlanAhead-launch-from-w-in-ISE-fails/td-p/148624/page/2). To fix the issue, symlink the OpenJDK libjvm.so into the Xilinx's installation directory.

```
# cd /opt/Xilinx/14.7/ISE_DS/PlanAhead/tps/lnx64/jre/lib/amd64/server
# mv libjvm.so{,-orig}
# ln -s /usr/lib/jvm/java-7-openjdk/jre/lib/amd64/server/libjvm.so

```

### GNU make

XSDK looks for the `gmake` executable, which is not present in Arch Linux by default. Create a symlink somewhere in your path, e.g.

```
$ ln -s /usr/bin/make /home/<user>/bin/gmake

```

Make sure this directory is in your PATH variable.

### Running Xilinx tools from within KDE

KDE by default defines the QT_PLUGIN_PATH shell variable. Some of the Xilinx ISE tools (ISE, Impact, XPS) are Qt applications, which means that they will search for Qt plugins in the locations defined by this shell variable.

Because the Xilinx tools are compiled against and ship with an older version of the Qt framework which cannot use these plugins, they will crash when launched with this environment variable present.

To fix this issue, run the following command before launching the tools:

```
$ unset QT_PLUGIN_PATH

```

### CORE Generator fails to generate core

In some cases, the CORE Generator will fails to generate a core and output something like this to its console:

```
ERROR:sim - Unable to evaluate Tcl file:
   /opt/Xilinx/14.7/ISE_DS/ISE/coregen/ip/xilinx/primary/com/xilinx/ip/clk_wiz_v3_6/generate/run_legacy_tcl_flow.tcl
ERROR:sim - Failed executing Tcl generator.

```

*   Solution #1

If that happens, make sure you don't have _JAVA_OPTIONS set in your environment. If you normally run coregen with

```
$ source /opt/Xilinx/14.7/ISE_DS/settings64.sh && coregen

```

you need to prepend that with an "unset _JAVA_OPTIONS":

```
$ unset _JAVA_OPTIONS && source /opt/Xilinx/14.7/ISE_DS/settings64.sh && coregen

```

*   Solution #2

Solution #1 no longer works due to: coregen's bundled java fails to start. Workaround force using ISE bundled java6 instead of java5.

Backup old version

```
$ mv /opt/Xilinx/14.7/ISE_DS/ISE/java/lin64/jre/bin/java /opt/Xilinx/14.7/ISE_DS/ISE/java/lin64/jre/bin/java.old

```

Add symbolic link to java6

```
$ ln -s /opt/Xilinx/14.7/ISE_DS/ISE/java6/lin64/jre/bin/java /opt/Xilinx/14.7/ISE_DS/ISE/java/lin64/jre/bin/java

```

*   Solution #3

If the previous methods fail, try to run the 32-bit version of coregen:

```
$ unset _JAVA_OPTIONS && source /opt/Xilinx/14.7/ISE_DS/settings32.sh && coregen

```