ArchLinux is not officially supported by Vivado, but as happens with [Xilinx ISE WebPACK](/index.php/Xilinx_ISE_WebPACK "Xilinx ISE WebPACK"), most of its features can be used with a bit of hacking.

## Contents

*   [1 Prerequisites](#Prerequisites)
    *   [1.1 Dependencies](#Dependencies)
*   [2 Installation](#Installation)
    *   [2.1 Vivado and SDK](#Vivado_and_SDK)
    *   [2.2 Update patch](#Update_patch)
    *   [2.3 Licensing](#Licensing)
*   [3 Launching programs](#Launching_programs)

## Prerequisites

Xilinx Vivado can be downloaded from its official website [[1]](http://www.xilinx.com/products/design-tools/vivado.html). Vivado only supports 64-bit systems, so you will need a working 64-bit ArchLinux install. It's recommended to download "Vivado HLx 2015.4: Full Installer For Linux Single File Download Image Including SDK" tarball, but make sure not to be in a hurry, as it's a large download (near 9 GB). Update tarballs can also be downloaded and installed later.

### Dependencies

Installer needs ncurses5 libs, and will not work with ncurses 6 available at official repos. You can work-around this problem by installing [ncurses5-compat-libs](https://aur.archlinux.org/packages/ncurses5-compat-libs/) from the [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository"). You will also need to install [lib32-libpng12](https://aur.archlinux.org/packages/lib32-libpng12/) for Xilinx Document Navigator to launch.

## Installation

You must install the main package, and it is also recommended to install the latest update patch.

### Vivado and SDK

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

It is recommended to install the latest update patch, and repeat the process each time a new patch is released. Note that update patches cannot be applied to WebPACK installs. If you installed Vivado WebPACK, skip this section.

To install the update, repeat the same hack used to install the suite. Once downloaded and unpacked, go to the directory containing the extracted tarball, patch the install script and run it:

```
$ sed -i.original 's/uname -i/uname -m/' xsetup
# ./xsetup

```

### Licensing

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

## Launching programs

To ease launching programs, you can create the following .desktop files for Vivado IDE, SDK and DocNav:

 `~/.local/share/applications/Xilinx-VivadoIDE.desktop` 
```
#!/usr/bin/env xdg-open
[Desktop Entry]
Version=1.0
Type=Application
Name=Xilinx Vivado IDE
Exec=sh -c "unset LANG && unset QT_PLUGIN_PATH && source /opt/Xilinx/Vivado/2015.4/settings64.sh && vivado"
Icon=/opt/Xilinx/Vivado/2015.4/doc/images/vivado_logo.png
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
Exec=sh -c "unset LANG && unset QT_PLUGIN_PATH && source /opt/Xilinx/SDK/2015.4/settings64.sh && xsdk"
Icon=/opt/Xilinx/SDK/2015.4/data/sdk/images/sdk_logo.png
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