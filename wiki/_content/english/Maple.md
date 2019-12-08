Related articles

*   [Octave](/index.php/Octave "Octave")
*   [Sage-mathematics](/index.php/Sage-mathematics "Sage-mathematics")
*   [Mathematica](/index.php/Mathematica "Mathematica")
*   [Matlab](/index.php/Matlab "Matlab")

From the [official website](http://www.maplesoft.com/products/maple/):

	Maple is a high-level language and interactive environment for numerical computation, visualization, and programming. Using Maple, you can analyze data, develop algorithms, and create models and applications. The language, tools, and built-in math functions enable you to explore multiple approaches and reach a solution faster than with spreadsheets or traditional programming languages, such as C/C++ or Java.

Maple is proprietary software produced by Maplesoft and requires a license to obtain, install, and activate. Arch is not officially supported, but the installer provided by Maplesoft may work in some cases.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Troubleshooting](#Troubleshooting)
    *   [2.1 Failed to determine Host ID of license server](#Failed_to_determine_Host_ID_of_license_server)
    *   [2.2 Blank main window with tiling window managers](#Blank_main_window_with_tiling_window_managers)
    *   [2.3 3D plots failing](#3D_plots_failing)
    *   [2.4 Offline activation](#Offline_activation)

## Installation

Maplesoft provides an installer script that may work on some Arch Linux installations. Version 18 is supported by [maple18](https://aur.archlinux.org/packages/maple18/). Make sure that you have a working [Java](/index.php/Java "Java") installation before beginning.

After purchasing your license, [download](http://www.maplesoft.com/support/downloads/) the appropriate Maple release package and unpack it in a location of your choosing. Open a terminal, change to the directory in which you unpacked the files, and run the installer script as a normal user. Installing the program's files inside of a user's home directory is the default option, and allows for easy removal of all components at a later time.

Once the package is installed, you will need to provide a license activation code. This should have been included in your installation archive.

## Troubleshooting

### Failed to determine Host ID of license server

In order to get Maple to accept your activation code, you may need to [install](/index.php/Install "Install") the [ld-lsb](https://www.archlinux.org/packages/?name=ld-lsb) package. This will fake a standard Linux standard base runtime and convince the authentication server to accept your valid activation code. The [lsb-release](https://www.archlinux.org/packages/?name=lsb-release) package does not solve this issue, as the [MapleSoft installation support site](http://www.maplesoft.com/support/Faqs/detail.aspx?sid=32610) might lead one to believe.

### Blank main window with tiling window managers

See [Java#Gray window, applications not resizing with WM, menus immediately closing](/index.php/Java#Gray_window,_applications_not_resizing_with_WM,_menus_immediately_closing "Java").

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

### Offline activation

If activation by license key doesn't work, you may try [Offline Activation](https://www.maplesoft.com/contact/webforms/offlineactivation/index.aspx).

Enter your license key in the Purchase Code field, and select either Host ID or Disk Serial Number as the hardware activation method.

To obtain your Host ID, run the following command:

```
   ip address show | grep link/ether | awk '{ print $2; }' | sed 's/://g'

```

and use one of the resulting IDs.

Enter your e-mail address (or use a disposable one), then copy the contents into `*maplehome*/license/license.dat`.

This should activate Maple on next startup.