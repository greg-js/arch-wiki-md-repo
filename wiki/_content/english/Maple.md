From the [official website](http://www.maplesoft.com/products/maple/):

	*Maple is a high-level language and interactive environment for numerical computation, visualization, and programming. Using Maple, you can analyze data, develop algorithms, and create models and applications. The language, tools, and built-in math functions enable you to explore multiple approaches and reach a solution faster than with spreadsheets or traditional programming languages, such as C/C++ or Java.*

## Contents

*   [1 Overview](#Overview)
*   [2 Installation](#Installation)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 Failed to determine Host ID of license server](#Failed_to_determine_Host_ID_of_license_server)
    *   [3.2 Blank main window with tiling window managers](#Blank_main_window_with_tiling_window_managers)
    *   [3.3 3D plots failing](#3D_plots_failing)

## Overview

Maple is proprietary software produced by Maplesoft and requires a license to obtain, install, and activate. Arch is not officially supported, but the installer provided by Maplesoft may work in some cases.

## Installation

Maplesoft provides an installer script that may work on some Arch Linux installations. Make sure that you have a working [Java](/index.php/Java "Java") installation before beginning.

After purchasing your license, [download](http://www.maplesoft.com/support/downloads/) the appropriate Maple release package and unpack it in a location of your choosing. Open a terminal, change to the directory in which you unpacked the files, and run the installer script as a normal user. Installing the program's files inside of a user's home directory is the default option, and allows for easy removal of all components at a later time.

Once the package is installed, you will need to provide a license activation code. This should have been included in your installation archive.

## Troubleshooting

### Failed to determine Host ID of license server

In order to get Maple to accept your activation code, you may need to [install](/index.php/Install "Install") the [ld-lsb](https://aur.archlinux.org/packages/ld-lsb/) package. This will fake a standard Linux standard base runtime and convince the authentication server to accept your valid activation code. The [lsb-release](https://www.archlinux.org/packages/?name=lsb-release) package does not solve this issue, as the [MapleSoft installation support site](http://www.maplesoft.com/support/Faqs/detail.aspx?sid=32610) might lead one to believe.

### Blank main window with tiling window managers

See [Java#Non-reparenting_window_managers](/index.php/Java#Non-reparenting_window_managers "Java").

### 3D plots failing

Maple ships with its own C++ runtime, which seems to cause issues with 3D rendering (plot3d, implicitplot3d, ...).

Linking the system's libstdc++ instead seems to fix the problem, for example for Maple 2016 on x64 systems, go to

```
   maple2016/bin.X86_64_LINUX/system

```

and link libstdc++.so.6.0.20 and libstdc++.so.6 to your system's version:

```
   libstdc++.so.6 -> /usr/lib64/libstdc++.so.6
   libstdc++.so.6.0.20 -> /usr/lib64/libstdc++.so.6.0.22

```