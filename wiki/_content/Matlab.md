# Matlab

From the [official website](http://www.mathworks.com/products/matlab/):

	_MATLAB is a high-level language and interactive environment for numerical computation, visualization, and programming. Using MATLAB, you can analyze data, develop algorithms, and create models and applications. The language, tools, and built-in math functions enable you to explore multiple approaches and reach a solution faster than with spreadsheets or traditional programming languages, such as C/C++ or Java._

## Contents

*   [1 Overview](#Overview)
*   [2 Installation](#Installation)
    *   [2.1 Installing from the MATLAB installation software](#Installing_from_the_MATLAB_installation_software)
    *   [2.2 Installing from the AUR package](#Installing_from_the_AUR_package)
*   [3 Activation](#Activation)
    *   [3.1 R2013b and earlier](#R2013b_and_earlier)
*   [4 Configuration](#Configuration)
    *   [4.1 Java](#Java)
    *   [4.2 OpenGL acceleration](#OpenGL_acceleration)
    *   [4.3 Fonts for figures](#Fonts_for_figures)
    *   [4.4 Sound](#Sound)
    *   [4.5 GPU computing](#GPU_computing)
    *   [4.6 Install supported compilers](#Install_supported_compilers)
    *   [4.7 Help browser](#Help_browser)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 Static TLS errors](#Static_TLS_errors)
    *   [5.2 MATLAB crashes when displaying graphics](#MATLAB_crashes_when_displaying_graphics)
    *   [5.3 Blank/grey UI when using DWM/Awesome](#Blank.2Fgrey_UI_when_using_DWM.2FAwesome)
    *   [5.4 Garbled or invisible text](#Garbled_or_invisible_text)
    *   [5.5 Corrupted text and fonts in menus and fields](#Corrupted_text_and_fonts_in_menus_and_fields)
    *   [5.6 Installation](#Installation_2)
    *   [5.7 Install-Time Library Errors](#Install-Time_Library_Errors)
    *   [5.8 Resolving start warnings/errors](#Resolving_start_warnings.2Ferrors)
    *   [5.9 Segmentation Fault on startup](#Segmentation_Fault_on_startup)

## Overview

MATLAB is proprietary software produced by The MathWorks and requires a license to obtain, install, and activate. New versions of MATLAB are released twice a year (generally in March and September) with release names of R20XXa and R20XXb. The MathWorks also provide a discounted [Student Version](http://www.mathworks.com/academia/students.html) which is released once a year. Since R2012b MATLAB has only been available for 64-bit Linux. While MATLAB is officially supported on a number of [Linux distributions](http://www.mathworks.co.uk/support/sysreq/current_release/index.html?sec=linux), Arch is not officially supported. Despite the lack of official support, installing and using MATLAB on Arch is straight forward.

## Installation

A complete copy of the MATLAB software must be obtained before it can in installed. The MATLAB software is available to licenses holders on both a DVD and through the [The MathWorks website](http://www.mathworks.com). In addition to the software a file installation key is required for installation. It is possible to install MATLAB either with the [matlab](https://aur.archlinux.org/packages/matlab/)<sup><small>AUR</small></sup> package from the [AUR](/index.php/AUR "AUR") or from the MATLAB installation software directly. The advantage of the [matlab](https://aur.archlinux.org/packages/matlab/)<sup><small>AUR</small></sup> package is that it manages dependencies and some of the nuances of the installation process while installing directly from the MATLAB installation software can be done by regular users to their home directories and works for any release of MATLAB (the [matlab](https://aur.archlinux.org/packages/matlab/)<sup><small>AUR</small></sup> package only works for releases including and after R2010b).

### Installing from the MATLAB installation software

The MATLAB installation software is self contained and does not require any additional packages to install in silent mode. To install with the GUI a working [Xorg](/index.php/Xorg "Xorg") graphical display is necessary. The installation is handled by the `install` script. You can run the script as root to install MATLAB system-wide or your user to install it only for you.

MATLAB 2015b and earlier is not compatible with [ncurses](https://www.archlinux.org/packages/?name=ncurses) 6, so you must install the [ncurses5-compat-libs](https://aur.archlinux.org/packages/ncurses5-compat-libs/)<sup><small>AUR</small></sup> package. See [#Segmentation Fault on startup](#Segmentation_Fault_on_startup) for more info.

During the installation, you are asked if you want symlinks to be created. If you did not choose to do so, you can now manually create a symlink in `/usr/local/bin` to make it easier to launch in terminal:

```
# ln -s /{MATLAB}/bin/matlab /usr/local/bin

```

To create a menu item, we need to get a icon first:

```
# curl [https://upload.wikimedia.org/wikipedia/commons/2/21/Matlab_Logo.png](https://upload.wikimedia.org/wikipedia/commons/2/21/Matlab_Logo.png) -o /usr/share/icons/matlab.png

```

Then create a new `.desktop` file in `/usr/share/applications` with following lines:

 `/usr/share/applications/matlab.desktop` 

```
#!/usr/bin/env xdg-open
[Desktop Entry]
Type=Application
Icon=/usr/share/icons/matlab.png
Name=MATLAB
Comment=Start MATLAB - The Language of Technical Computing
Exec=matlab -desktop -nosplash
Categories=Development;
MimeType=text/x-matlab;

```

The `Exec` command line is composed as follows:

*   `-desktop` is a flag needed to run Matlab without a terminal.
*   `-nosplash` is a flag preventing the splash screen from showing and taking up a temporary space in your task bar.

You can also put this `.desktop` file in the `~/Desktop` directory to create a shortcut on your desktop. See also [[1]](https://help.ubuntu.com/community/MATLAB).

### Installing from the AUR package

The EULA for the proprietary MATLAB software is restrictive. The [matlab](https://aur.archlinux.org/packages/matlab/)<sup><small>AUR</small></sup> package from the [AUR](/index.php/AUR "AUR") is designed to allow MATLAB to be integrated into and managed by Arch. The package should be built on the system on which it is going to be installed and the package should be deleted from the installation location and the [Pacman](/index.php/Pacman "Pacman") cache following installation. Distributing the package is a clear violation of the EULA.

The [matlab](https://aur.archlinux.org/packages/matlab/)<sup><small>AUR</small></sup> package from the [AUR](/index.php/AUR "AUR") defaults to building a package for the most recent 64-bit release of MATLAB, although the PKGBUILD supports MATLAB releases from R2010b and even the installation of multiple releases simultaneous. The PKGBUILD defaults to installing all toolboxes that the file identification key allows, however, the PKGBUILD can be edited to include only a subset of the toolboxes. The selection of the toolboxes must be finalized at the time of package creation due to DRM policies put in place by The MathWorks. The [matlab](https://aur.archlinux.org/packages/matlab/)<sup><small>AUR</small></sup> package from the [AUR](/index.php/AUR "AUR") requires that both the MATLAB installation software and the file installation key are available in the source directory. The file installation key must be in a file called `matlab.fik` and the installation software must be in an iso file called `matlab.iso`. Once the iso file and file installation key are created, the MATLAB package can be created and install as usual.

For MATLAB releases between r2010b and r2011a the contents of the iso file must include: `./archives/`, `./bin/`, `./etc/`, `./help/`, `./java/`, `./activate.ini`, `./install`, and `./installer_input.txt`. If the MATLAB download agent is used to download the installation software, then the iso file can be trivially created by simply running `mkisofs -r -o` on the download directory.

For MATLAB releases including and after r2011b the contents of the iso file must include: `./archives/`, `./bin/`, `./etc/`, `./help/`, `./java/`, `./activate.ini`, `./install`, and `./installer_input.txt`. For version before r2014a, the MATLAB download agent could download all the required files and the iso file could be trivially created by simply running `mkisofs -r -o` on the download directory. For MATLAB releases including and after r2014a the MATLAB download agent only downloads the MATLAB installer. The MATLAB installer then needs to be run to downloaded the MATLAB software and toolboxes. Therefore, a two step process is required to generate this iso file with the MATLAB download agent. First, you download and run the MATLAB installer to install MATLAB in a temporary directory. This process downloads the MATLAB software and toolboxes by default to `~/Downloads/MathWorks` (this can be changed by passing the flag `-downloadFolder /path/to/directory`). It is actually possible quit the MATLAB installer once the software and toolboxes are downloaded. Once the software and toolboxes are downloaded the required iso file can be created by merging the installer directory (containing above mentioned files) and the download directory (containing `./archives/`), and then running `mkisofs -r -o` on the resulting directory.

## Activation

In order to run MATLAB it requires a license file to be installed. The license file can be generated with `$MATLABROOT/bin/activate_matlab.sh` or downloaded from [MATLAB](http://www.mathworks.com) directly.

### R2013b and earlier

Up to and including R2013b the license file was linked to the MAC address of eth0\. This causes problems with the [Predictable Network Interface Names](/index.php/Network_configuration#Device_names "Network configuration") used by Arch Linux. It is possible to disable predictable network interface names by adding `net.ifnames=0` in your kernel command line or by creating a udev rule file

 `# ln -s /dev/null /etc/udev/rules.d/80-net-setup-link.rules` 

It is also possible to [change the name of a device](/index.php/Network_configuration#Change_device_name "Network configuration"), but changing the name to eth0 can result in race conditions between the kernel and udev during boot. Another solution is to create a dummy network interface named eth0 with the MAC address linked to the license file. First, get that MAC address using `ip link`. Next, create the following file:

 `/etc/systemd/system/matlab.licensing.service` 

```
[Unit]
Description=Dummy network interface for MATLAB
Requires=systemd-modules-load.service

[Service]
Type=oneshot
ExecStart=/sbin/ip link set dev dummy0 name eth0
ExecStart=/sbin/ip link set dev eth0 address 00:00:00:00:00:00

[Install]
WantedBy=multi-user.target

```

Replace 00:00:00:00:00:00 with the MAC address linked to the license file.

Then make the script run on boot:

```
# systemctl enable matlab.licensing

```

Finally, set the dummy module to load on boot by creating the following file:

 `/etc/modules-load.d/dummy.conf`  `dummy` 

## Configuration

### Java

The MATLAB software is bundled with a JVM and therefore it is not necessary to install [Java](/index.php/Java "Java"). The JVM version bundled with MATLAB typically lags behind [jre7-openjdk](https://www.archlinux.org/packages/?name=jre7-openjdk) from the [official repositories](/index.php/Official_repositories "Official repositories") and it is possible, although not required, to use the `MATLAB_JAVA` environment variable to specify the path of an alternative JRE. For example, to specify the [jre7-openjdk](https://www.archlinux.org/packages/?name=jre7-openjdk) JRE and check the resulting version of Java, do:

 `$ MATLAB_JAVA=/usr/lib/jvm/java-7-openjdk/jre matlab -nodesktop -nosplash -r "version -java, exit" | grep Java` 

Using alternative JRE would often solve some long-standing problems, such as the extra "`MEvent. CASE!`" string when doing two-finger scrolling using touchpad. Another problem that can be solved in this way is the ugly, limited fonts provided by default, especially for some Chinese characters.

### OpenGL acceleration

MATLAB can take advantage of hardware based 2D and 3D OpenGL acceleration. Support for hardware acceleration needs to be configured outside of MATLAB. Appropriate [video drivers](/index.php/Video_drivers "Video drivers") need to be installed along with the OpenGL utility library [glu](https://www.archlinux.org/packages/?name=glu) package from the [official repositories](/index.php/Official_repositories "Official repositories"). If X11 forwarding is being used, the video drivers need to be installed on both the client and server. To check if MATLAB is making use of hardware based OpenGL acceleration run:

 `$ matlab -nodesktop -nosplash -r "opengl info; exit" | grep Software` 

If "software rendering" is not "false", then there is a problem with your hardware acceleration. If this is the case make sure OpenGL is configured correctly on the system. This can be done with the `glxinfo` program from the [mesa-demos](https://www.archlinux.org/packages/?name=mesa-demos) package from the [official repositories](/index.php/Official_repositories "Official repositories"):

 `$ glxinfo | grep "direct rendering"` 

If "direct rendering" is not "yes", then there is likely a problem with your system configuration.

### Fonts for figures

**Note:** This section only applies to R2014a and earlier as starting with R2014b MATLAB uses True Type Fonts. So as long as: `$ fc-match Helvetica` returns a font, figure fonts should work as expected.

While MATLAB can be run in a text only mode, it also provides advanced graphics capabilities. To confirm that MATLAB is making use of the system fonts run:

 `$ matlab -nodesktop -nosplash -r "xlabel('BIG FONT', 'FontSize', 42); ylabel('small font', 'FontSize', 12); pause; exit" > /dev/null` 

This should produce a MATLAB figure with "BIG FONT" in a large font on the abscissa and "small font" in a small font on the ordinate. If "BIG FONT" and "small font" are both the same size, refer to [Xorg fonts](/index.php/Xorg#Program_requests_.22font_.27.28null.29.27.22 "Xorg") to confirm that the correct the bitmap font package (either [xorg-fonts-100dpi](https://www.archlinux.org/packages/?name=xorg-fonts-100dpi) or [xorg-fonts-75dpi](https://www.archlinux.org/packages/?name=xorg-fonts-75dpi) from the [official repositories](/index.php/Official_repositories "Official repositories")) is installed on your system.

### Sound

To confirm that MATLAB is able to use the default soundcard to present sounds run:

 `$ matlab -nodesktop -nosplash -r "load handel; sound(y, Fs); pause(length(y)/Fs); exit" > /dev/null` 

This should play an except from Handel's "Hallelujah Chorus." If this fails make sure [ALSA](/index.php/ALSA "ALSA") is properly configured. This can be done with the `speaker-test` program from the [alsa-utils](https://www.archlinux.org/packages/?name=alsa-utils) package from the [official repositories](/index.php/Official_repositories "Official repositories"):

 `$ speaker-test` 

If you do not hear anything, then there is likely a problem with your system configuration.

### GPU computing

MATLAB can take advantage of [CUDA enabled GPUs](http://www.mathworks.co.uk/discovery/matlab-gpu.html) to speed up applications. In order to take advantage of a supported GPU install the [nvidia](https://www.archlinux.org/packages/?name=nvidia), [nvidia-utils](https://www.archlinux.org/packages/?name=nvidia-utils), [libcl](https://www.archlinux.org/packages/?name=libcl)<sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): replaced by [ocl-icd](https://www.archlinux.org/packages/?name=ocl-icd)]</sup>, [opencl-nvidia](https://www.archlinux.org/packages/?name=opencl-nvidia), and [cuda](https://www.archlinux.org/packages/?name=cuda) packages from the [official repositories](/index.php/Official_repositories "Official repositories"). To check if MATLAB is able to utilize the GPU run:

 `$ matlab -nodesktop -nosplash -r "x=rand(10, 'single'); g=gpuArray(x); Success=isequal(gather(g), x), exit"  | sed -ne '/Success =/,$p'` 

### Install supported compilers

In order to access the full functionality of MATLAB (e.g., to use Simulink, Builder JA, and MEX-file compilation), supported versions of the `gcc`, `g++`, `gfortran`, and `jdk` compilers must be installed. Details about the supported compilers for the [current release](http://www.mathworks.com/support/compilers/current_release/index.html?sec=glnxa64) and [previous releases](http://www.mathworks.com/support/sysreq/previous_releases.html) are available online. Many of the supported `gcc`, `g++`, `jdk` compiler versions for past MATLAB releases are available from the [AUR](/index.php/AUR "AUR") (e.g., [gcc43](https://aur.archlinux.org/packages/gcc43/)<sup><small>AUR</small></sup>, [gcc44](https://aur.archlinux.org/packages/gcc44/)<sup><small>AUR</small></sup>, [gcc47](https://aur.archlinux.org/packages/gcc47/)<sup><small>AUR</small></sup>, and [jdk6](https://aur.archlinux.org/packages/jdk6/)<sup><small>AUR</small></sup>), while past versions of the `gfortran` compilers are not packaged.

To use previous versions of the the `gcc`, `g++`, and `gfortran` compilers with MEX files, edit `${MATLAB}/bin/mexopts.sh` and replace all occurrences of `CC='gcc'` with `CC='gcc-4.X'`, `CXX='g++'` with `CXX='g++-4.X'`, and `FC='gfortran'` with `FC='gfortran-4.X'`, where `X` is the compiler version appropriate for the particular MATLAB release.

### Help browser

The help browser uses valuable slots in the dynamic thread vector and causes competition with core functionality provided by libraries like the BLAS that also depend on the dynamic thread vector. The help browser can be configured to use fewer slots in the dynamic thread vector with

```
 >> webutils.htmlrenderer('basic');

```

This is a persistent change and to reverse it use

```
 >> webutils.htmlrenderer('default');

```

## Troubleshooting

### Static TLS errors

MATLAB has a number of libraries that have been compiled with static thread local storage (TLS) including the help broswer `doc` and the BLAS libraries. For example,

```
>> doc('help');
>> ones(10)*randn(10);
 Error using  * 
BLAS loading error:
dlopen: cannot load any more object with static TLS 

```

is related to bugs [961964](http://www.mathworks.de/support/bugreports/961964) and [1003952](http://www.mathworks.com/support/bugreports/1003952). In some cases (e.g., bug [961964](http://www.mathworks.de/support/bugreports/961964)) patched libraries are available from [The MathWorks](http://www.mathworks.de/support/bugreports/license/accept_license/5730?fname=attachment_961964_12b_13a_13b_14a_glnxa64_2014-01-30.zip&geck_id=961964), while in others (e.g., bug [1003952](http://www.mathworks.com/support/bugreports/1003952)) work arounds exist. A more general solution of recompiling `glibc` has also been [suggested](http://stackoverflow.com/a/19468365/2787723).

### MATLAB crashes when displaying graphics

To identify this error, start MATLAB with

```
LIBGL_DEBUG=verbose matlab

```

from the terminal and try to collect OpenGL information with `opengl info` from the MATLAB command prompt. If it crashes again and there is an output line like

```
libGL error: dlopen /usr/lib/xorg/modules/dri/swrast_dri.so failed 
(/usr/local/MATLAB/R2011b/bin/glnxa64/../../sys/os/glnxa64/libstdc++.so.6: 
version `GLIBCXX_3.4.15' not found (required by /usr/lib/xorg/modules/dri/swrast_dri.so))

```

then the problem is that MATLAB uses its own GNU C++ library, which is an older version than the up-to-date version on your Archlinux system. Make MATLAB use the current C++ library for your system by

```
cd /usr/local/MATLAB/R(your release)/sys/os/glnxa64
sudo unlink libstdc++.so.6
sudo ln -s /usr/lib/libstdc++.so.6

```

### Blank/grey UI when using DWM/Awesome

[wmname](http://tools.suckless.org/wmname) is a utility to set the window manager name of the root window.

```
wmname LG3D

```

Then start Matlab.

### Garbled or invisible text

Set the environment variable `J2D_D3D` to `false`[[2]](https://stackoverflow.com/questions/22737535/swing-rendering-appears-broken-in-jdk-1-8-correct-in-jdk-1-7).

### Corrupted text and fonts in menus and fields

If you notice that the menus or the input fields are corrupted or not appearing correctly then you can try to activate the _"**Use antialiasing to smooth desktop fonts**"_ option in Matlab preferences, it seems to solve the problem. Go to _**Preferences -> Matlab -> Fonts**_ and activate it. You will need to restart Matlab in order to take affect.

### Installation

As one installs Matlab, it might complain that it cannot find a package, for the most part just look at the package name and then install it with [Pacman](/index.php/Pacman "Pacman"), or in the case of x86_64 there are some libraries only in [AUR](/index.php/AUR "AUR").

### Install-Time Library Errors

*   Make sure that the symlink `bin/glnx64/libstdc++.so.6` is pointing to the correct version of `libstdc++.so.xx` (which is also in the same directory and has numbers where 'xx' is). By default, it may be pointing to an older (and nonexistent) version (different value for 'xx').

*   Make sure the device you're installing from is not mounted as `noexec`

*   If you downloaded the files from Mathworks' website, make sure they are not on an NTFS or FAT partition, because that can mess up the symlinks. Ext4 or Ext3 should work.

### Resolving start warnings/errors

*   Even if all needed libraries are installed, Matlab when starting can still report some missing libraries. This is resolved by symbolic linking of needed libraries to directories that Matlab checks at start-up. For example, if Matlab triggers error/warning about missing `/lib64/libc.so.6` library, this can be resolved by:

```
# ln -s /lib/libc.so.6 /lib64

```

*   Matlab R2011b with an up-to-date Arch Linux (as of March 12, 2012) fails on startup with the familiar "Failure loading desktop class." A solution is to point Matlab to the system JVM (confirmed to work with the [jdk7-openjdk](https://www.archlinux.org/packages/?name=jdk7-openjdk) package):

```
export MATLAB_JAVA=/usr/lib/jvm/java-7-openjdk/jre

```

### Segmentation Fault on startup

If Matlab stops working after upgrading [ncurses](https://www.archlinux.org/packages/?name=ncurses) to v6.x, [install](/index.php/Install "Install") the [ncurses5-compat-libs](https://aur.archlinux.org/packages/ncurses5-compat-libs/)<sup><small>AUR</small></sup> package. See [BBS#202575](https://bbs.archlinux.org/viewtopic.php?id=202575).

Retrieved from "[https://wiki.archlinux.org/index.php?title=Matlab&oldid=415035](https://wiki.archlinux.org/index.php?title=Matlab&oldid=415035)"