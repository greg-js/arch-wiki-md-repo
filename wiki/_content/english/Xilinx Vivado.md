ArchLinux is not officially supported by Vivado, but as happens with [Xilinx ISE WebPACK](/index.php/Xilinx_ISE_WebPACK "Xilinx ISE WebPACK"), most of its features can be used with a bit of hacking.

## Contents

*   [1 Prerequisites](#Prerequisites)
    *   [1.1 Dependencies](#Dependencies)
*   [2 Installation](#Installation)
    *   [2.1 Vivado and SDK](#Vivado_and_SDK)
    *   [2.2 Update patch](#Update_patch)
    *   [2.3 Licensing](#Licensing)
    *   [2.4 Digilent USB-JTAG Drivers](#Digilent_USB-JTAG_Drivers)
*   [3 Launching programs](#Launching_programs)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Synthesis segfaults](#Synthesis_segfaults)
    *   [4.2 xsct segfault](#xsct_segfault)
    *   [4.3 Vivado HLS testbench error with GCC](#Vivado_HLS_testbench_error_with_GCC)
    *   [4.4 Vivado Crashes with Wayland](#Vivado_Crashes_with_Wayland)

## Prerequisites

Xilinx Vivado can be downloaded from its official website [[1]](http://www.xilinx.com/products/design-tools/vivado.html). It's recommended to download "Vivado HLx 2018.1: Full Installer For Linux Single File Download Image Including SDK" tarball, but make sure not to be in a hurry, as it's a large download (near 17 GB). Update tarballs can also be downloaded and installed later.

### Dependencies

Installer needs ncurses5 libs, and will not work with ncurses 6 available at official repos. You can work-around this problem by installing [ncurses5-compat-libs](https://aur.archlinux.org/packages/ncurses5-compat-libs/) from the [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository"). You will also need to install [libpng12](https://www.archlinux.org/packages/?name=libpng12) and [lib32-libpng12](https://www.archlinux.org/packages/?name=lib32-libpng12) for Xilinx Document Navigator to launch.

## Installation

You must install the main package, and it is also recommended to install the latest update patch.

### Vivado and SDK

**Warning:** The patch below is not longer needed in the 2018.1 version. Just unpack and run the xsetup file.

Once downloaded and unpacked the tarball, the install script must be patched to be able to properly detect the machine architecture. You can do it by going to the directory where installer is extracted and running:

```
$ sed -i.original 's/uname -i/uname -m/' xsetup

```

Install script will be patched and original will be backed up as `xsetup.original`, just in case you need to restore it later. Once patched, just run the script; it should work perfect and install the suite without a problem:

```
# ./xsetup

```

It is recommended to install the suite at the default location `/opt/Xilinx`, as further instructions in this page will assume the suite is installed there.

### Update patch

**Warning:** The patch below is not longer needed in the 2018.1 version.

It is recommended to install the latest update patch, and repeat the process each time a new patch is released. Note that update patches cannot be applied to WebPACK installs. If you installed Vivado WebPACK, skip this section.

To install the update, repeat the same hack used to install the suite. Once downloaded and unpacked, go to the directory containing the extracted tarball, patch the install script and run it:

```
$ sed -i.original 's/uname -i/uname -m/' xsetup
# ./xsetup

```

### Licensing

**Warning:** In the 2018.1 Webpack version there is not longer required download an explicit license file, it just works.

If you already have a license file, you can load it using Vivado License Manager. Unfortunately, if you want to obtain a WebPack license, further steps are needed. Vivado installs old stdc++ libraries, causing problems when spawning programs not included with Vivado Suite (like your default browser). To fix this, do the following steps:

```
# cd /opt/Xilinx/Vivado/2015.4/lib/lnx64.o/
# mv libstdc++.so.6 libstdc++.so.6.orig
# ln -s /usr/lib/libstdc++.so.6

```

Close any running Vivado Suite program, and launch license manager:

```
$ /opt/Xilinx/Vivado/2015.4/bin/vlm

```

If you try obtaining a WebPack license, your default browser should open, and the license should be generated normally. If Vivado License Manager fails to automatically load the generated license, download the .lic file, and manually load it.

### Digilent USB-JTAG Drivers

To use Digilent Adept USB-JTAG adapters (e.g. the onboard JTAG adapter on the [ZedBoard](http://www.zedboard.org)) from Vivado, you need to install the Digilent [Adept Runtime](http://store.digilentinc.com/digilent-adept-2-download-only/).

Make sure you have installed [fxload](https://aur.archlinux.org/packages/fxload/) from the [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository") .

To install the Digilent Adept Runtime, it is recommended to install [digilent.adept.runtime](https://aur.archlinux.org/packages/digilent.adept.runtime/) from the [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository").

In addition, installing [digilent.adept.utilities](https://aur.archlinux.org/packages/digilent.adept.utilities/) may do good to configuring your board.

## Launching programs

To ease launching programs, you can create the following .desktop files for Vivado IDE, SDK and DocNav:

 `~/.local/share/applications/Xilinx-VivadoIDE.desktop` 
```
#!/usr/bin/env xdg-open
[Desktop Entry]
Version=1.0
Type=Application
Name=Xilinx Vivado IDE
Exec=sh -c "unset LANG && unset QT_PLUGIN_PATH && source /opt/Xilinx/Vivado/2018.1/settings64.sh && vivado"
Icon=/opt/Xilinx/Vivado/2018.1/doc/images/vivado_logo.png
Categories=Development;
Comment=Vivado Integrated Development Environment
```
 `~/.local/share/applications/Xilinx-SDK.desktop` 
```
#!/usr/bin/env xdg-open
[Desktop Entry]
Version=1.0
Type=Application
Name=Xilinx SDK
Exec=sh -c "unset LANG && unset QT_PLUGIN_PATH && source /opt/Xilinx/SDK/2018.1/settings64.sh && xsdk"
Icon=/opt/Xilinx/SDK/2018.1/data/sdk/images/sdk_logo.png
Categories=Development;
Comment=Xilinx Software Development Kit
```
 `~/.local/share/applications/Xilinx-DocNav.desktop` 
```
#!/usr/bin/env xdg-open
[Desktop Entry]
Version=1.0
Type=Application
Name=Xilinx Documentation Navigator 
Exec=sh -c "/opt/Xilinx/DocNav/docnav"
Icon=/opt/Xilinx/DocNav/resources/doc_nav_application_48.png
Categories=Development;
Comment=Xilinx Documentation Navigator
```

## Troubleshooting

### Synthesis segfaults

See [https://forums.xilinx.com/t5/Synthesis/Vivado-crashes-on-Arch-Linux-when-performing-synthesis/td-p/706847](https://forums.xilinx.com/t5/Synthesis/Vivado-crashes-on-Arch-Linux-when-performing-synthesis/td-p/706847)

You'll need to recompile glibc (just take the PKGBUILD from the abs) with `--disable-lock-elision`. Instead of patching the system libc in /usr/lib, copy the newly compiled `libpthread-2.25.so` and `libc-2.25.so` to `/opt/Xilinx/Vivado/2016.4/ids_lite/ISE/lib/lin64` Don't forget to repeat this when glibc gets upgraded.

### xsct segfault

xsct might crash with message:

```
 Xilinx/SDK/2018.1/bin/xsct: line 141:  5611 Segmentation fault      (core dumped) "$RDI_BINROOT"/unwrapped/"$RDI_PLATFORM$RDI_OPT_EXT"/rlwrap -rc -f "$RDI_APPROOT"/scripts/xsdb/xsdb/cmdlist -H "$HOME"/.xsctcmdhistory "$RDI_BINROOT"/loader -exec rdi_xsct "${RDI_ARGS[@]}"

```

This is a problem with the rlwrap version bundled with vivado, probably due the lack of legacy vsyscall emulation in Archlinux. To fix this issue either drop rlwrap altogether (losing history and autocompletion in xsct) or install [rlwrap](https://www.archlinux.org/packages/?name=rlwrap) from the official repo, and edit the corresponding line in the xsct startup script:

 `../Xilinx/SDK/2018.1/bin/xsct` 
```
# Use rlwrap to invoke XSCT
/usr/bin/rlwrap -rc -f "$RDI_APPROOT"/scripts/xsdb/xsdb/cmdlist -H "$HOME"/.xsctcmdhistory "$RDI_BINROOT"/loader -exec rdi_xsct "${RDI_ARGS[@]}"
# OR run xsct without rlwrap
#"$RDI_BINROOT"/loader -exec rdi_xsct "${RDI_ARGS[@]}"
```

### Vivado HLS testbench error with GCC

Vivado requires an older version of glibc (2.26 as of vivado 2018.1).

The solution proposed in [this thread](https://forums.xilinx.com/t5/High-Level-Synthesis-HLS/Testbench-error-with-gcc/td-p/756773) from Xilinx forums suggests to update the fixed headers shipped by Xilinx.

For vivado version 2016, run:

```
 # /opt/Xilinx/Vivado_HLS/<version>/lnx64/tools/gcc/libexec/gcc/x86_64-unknown-linux-gnu/4.6.3/install-tools/mkheaders /opt/Xilinx/Vivado_HLS/<version>/lnx64/tools/gcc/

```

For vivado 2017 and newer, run:

```
 # /opt/Xilinx/Vivado/2018.1/lnx64/tools/gcc/libexec/gcc/x86_64-unknown-linux-gnu/4.6.3/install-tools/mkheaders /opt/Xilinx/Vivado/2018.1/lnx64/tools/gcc

```

### Vivado Crashes with Wayland

If Vivado crashes and the error file contains something similar to this:

 `hs_err_pid*.log` 
```
#
# An unexpected error has occurred (11)
#
Stack:
/opt/Xilinx/Vivado/2018.2/tps/lnx64/jre/lib/amd64/server/libjvm.so(+0x923da9) [0x7fced0c19da9]
/opt/Xilinx/Vivado/2018.2/tps/lnx64/jre/lib/amd64/server/libjvm.so(JVM_handle_linux_signal+0xb6) [0x7fced0c203f6]
/opt/Xilinx/Vivado/2018.2/tps/lnx64/jre/lib/amd64/server/libjvm.so(+0x9209d3) [0x7fced0c169d3]
/usr/lib/libc.so.6(+0x368f0) [0x7fcf0ea408f0]
/opt/Xilinx/Vivado/2018.2/tps/lnx64/jre/lib/amd64/libawt_xawt.so(+0x42028) [0x7fceb1a20028]
/opt/Xilinx/Vivado/2018.2/tps/lnx64/jre/lib/amd64/libawt_xawt.so(+0x42288) [0x7fceb1a20288]
/opt/Xilinx/Vivado/2018.2/tps/lnx64/jre/lib/amd64/libawt_xawt.so(Java_sun_awt_X11_XRobotPeer_getRGBPixelsImpl+0x17c) [0x7fceb1a1867c]
[0x7fcec0cb94cf]
```

Switch to using Xorg instead of Wayland. The version of Java Vivado uses has compatibility problems with Wayland.