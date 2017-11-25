Related articles

*   [Octave](/index.php/Octave "Octave")
*   [Sage-mathematics](/index.php/Sage-mathematics "Sage-mathematics")
*   [Mathematica](/index.php/Mathematica "Mathematica")

From the [official website](http://www.mathworks.com/products/matlab/):

	*MATLAB is a high-level language and interactive environment for numerical computation, visualization, and programming. Using MATLAB, you can analyze data, develop algorithms, and create models and applications. The language, tools, and built-in math functions enable you to explore multiple approaches and reach a solution faster than with spreadsheets or traditional programming languages, such as C/C++ or Java.*

## Contents

*   [1 Overview](#Overview)
*   [2 Installation](#Installation)
    *   [2.1 Installing from the MATLAB installation software](#Installing_from_the_MATLAB_installation_software)
        *   [2.1.1 Desktop entry](#Desktop_entry)
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
    *   [4.8 Garbled Interface](#Garbled_Interface)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 Static TLS errors](#Static_TLS_errors)
    *   [5.2 MATLAB crashes when displaying graphics](#MATLAB_crashes_when_displaying_graphics)
    *   [5.3 Blank/grey UI when using WM (non-reparenting window manager)](#Blank.2Fgrey_UI_when_using_WM_.28non-reparenting_window_manager.29)
    *   [5.4 Garbled or invisible text](#Garbled_or_invisible_text)
    *   [5.5 Corrupted text and fonts in menus and fields](#Corrupted_text_and_fonts_in_menus_and_fields)
    *   [5.6 Installation](#Installation_2)
    *   [5.7 Install-time library errors](#Install-time_library_errors)
    *   [5.8 Resolving start warnings/errors](#Resolving_start_warnings.2Ferrors)
    *   [5.9 Segmentation fault on startup](#Segmentation_fault_on_startup)
    *   [5.10 Hangs on rendering or exiting with Intel graphics](#Hangs_on_rendering_or_exiting_with_Intel_graphics)
    *   [5.11 Addon manager not working](#Addon_manager_not_working)
    *   [5.12 Live Script Errors](#Live_Script_Errors)
    *   [5.13 Using webcam/video device](#Using_webcam.2Fvideo_device)
    *   [5.14 MATLAB hangs for several minutes when closing Help Browser](#MATLAB_hangs_for_several_minutes_when_closing_Help_Browser)
    *   [5.15 Some dropdown menus cannot be selected](#Some_dropdown_menus_cannot_be_selected)
    *   [5.16 Not starting - licensing error](#Not_starting_-_licensing_error)
    *   [5.17 MATLAB crashes with "Failure loading desktop class" on startup](#MATLAB_crashes_with_.22Failure_loading_desktop_class.22_on_startup)
*   [6 Matlab in a systemd-nspawn](#Matlab_in_a_systemd-nspawn)

## Overview

MATLAB is proprietary software produced by The MathWorks and requires a license to obtain, install, and activate. New versions of MATLAB are released twice a year, release names are composed of `R`, the year of the release and `a` or `b`. Since R2012b MATLAB has only been available for 64-bit Linux. Arch Linux is not officially supported. [[1]](http://www.mathworks.co.uk/support/sysreq/current_release/index.html)

## Installation

A complete copy of the MATLAB software must be obtained before it can be installed. The MATLAB software is available to licenses holders on both a DVD and through the [The MathWorks website](http://www.mathworks.com). In addition to the software a file installation key is required for installation. It is possible to install MATLAB either with the [matlab](https://aur.archlinux.org/packages/matlab/) package from the [AUR](/index.php/AUR "AUR") or from the MATLAB installation software directly. The advantage of the [matlab](https://aur.archlinux.org/packages/matlab/) package is that it manages dependencies and some of the nuances of the installation process while installing directly from the MATLAB installation software can be done by regular users to their home directories and works for any release of MATLAB (the [matlab](https://aur.archlinux.org/packages/matlab/) package only works for releases including and after R2010b).

### Installing from the MATLAB installation software

The MATLAB installation software is self contained and does not require any additional packages to install in silent mode. To install with the GUI a working [Xorg](/index.php/Xorg "Xorg") graphical display is necessary. The installation is handled by the `install` script. You can run the script as root to install MATLAB system-wide or your user to install it only for you.

MATLAB 2016a and earlier is not compatible with [ncurses](https://www.archlinux.org/packages/?name=ncurses) 6, so you must install the [ncurses5-compat-libs](https://aur.archlinux.org/packages/ncurses5-compat-libs/) package. See [#Segmentation fault on startup](#Segmentation_fault_on_startup) for more info.

During the installation, you are asked if you want symlinks to be created. If you did not choose to do so, you can now manually create a symlink in `/usr/local/bin` to make it easier to launch in terminal:

```
# ln -s /{MATLAB}/bin/matlab /usr/local/bin

```

#### Desktop entry

Optionally create a [desktop entry](/index.php/Desktop_entry "Desktop entry"). The MIME type of MATLAB files is `text/x-matlab`.

Start `matlab` with:

*   `-desktop` to run Matlab without a terminal.
*   `-nosplash` to prevent the splash screen from showing up.

In order for icons to appear correctly `StartupWMClass` needs to be set in the desktop entry. To find it out start MATLAB, run `xprop | grep WM_CLASS` and select the MATLAB window.

### Installing from the AUR package

The EULA for the proprietary MATLAB software is restrictive. The [matlab](https://aur.archlinux.org/packages/matlab/) package from the [AUR](/index.php/AUR "AUR") is designed to allow MATLAB to be integrated into and managed by Arch. The package should be built on the system on which it is going to be installed and the package should be deleted from the installation location and the [Pacman](/index.php/Pacman "Pacman") cache following installation. Distributing the package is a clear violation of the EULA.

The [matlab](https://aur.archlinux.org/packages/matlab/) package from the [AUR](/index.php/AUR "AUR") defaults to building a package for the most recent 64-bit release of MATLAB, although the PKGBUILD supports MATLAB releases from R2010b and even the installation of multiple releases simultaneous. The PKGBUILD defaults to installing all toolboxes that the file identification key allows, however, the PKGBUILD can be edited to include only a subset of the toolboxes. The selection of the toolboxes must be finalized at the time of package creation due to DRM policies put in place by The MathWorks. The [matlab](https://aur.archlinux.org/packages/matlab/) package from the [AUR](/index.php/AUR "AUR") requires that both the MATLAB installation software and the file installation key are available in the source directory. The file installation key must be in a file called `matlab.fik` and the installation software must be in an iso file called `matlab.iso`. Once the iso file and file installation key are created, the MATLAB package can be created and install as usual.

For MATLAB releases between r2010b and r2011a the contents of the iso file must include: `./archives/`, `./bin/`, `./etc/`, `./help/`, `./java/`, `./activate.ini`, `./install`, and `./installer_input.txt`. If the MATLAB download agent is used to download the installation software, then the iso file can be trivially created by simply running `mkisofs -r -o` on the download directory.

For MATLAB releases including and after r2011b the contents of the iso file must include: `./archives/`, `./bin/`, `./etc/`, `./help/`, `./java/`, `./activate.ini`, `./install`, and `./installer_input.txt`. For version before r2014a, the MATLAB download agent could download all the required files and the iso file could be trivially created by simply running `mkisofs -r -o` on the download directory. For MATLAB releases including and after r2014a the MATLAB download agent only downloads the MATLAB installer. The MATLAB installer then needs to be run to downloaded the MATLAB software and toolboxes. Therefore, a two step process is required to generate this iso file with the MATLAB download agent. First, you download and run the MATLAB installer to install MATLAB in a temporary directory. This process downloads the MATLAB software and toolboxes by default to `~/Downloads/MathWorks` (this can be changed by passing the flag `-downloadFolder /path/to/directory`). It is actually possible quit the MATLAB installer once the software and toolboxes are downloaded. Once the software and toolboxes are downloaded the required iso file can be created by merging the installer directory (containing above mentioned files) and the download directory (containing `./archives/`), and then running `mkisofs -r -o` on the resulting directory.

## Activation

In order to run MATLAB it requires a license file to be installed. The license file can be generated with `$MATLABROOT/bin/activate_matlab.sh` or downloaded from [MATLAB](http://www.mathworks.com) directly.

### R2013b and earlier

Up to and including R2013b the license file was linked to the MAC address of eth0\. This causes problems with the [Predictable Network Interface Names](/index.php/Network_configuration#Device_names "Network configuration") used by Arch Linux. It is possible to disable predictable network interface names by adding `net.ifnames=0` in your kernel command line or by creating a udev rule file

```
# ln -s /dev/null /etc/udev/rules.d/80-net-setup-link.rules

```

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

```
$ MATLAB_JAVA=/usr/lib/jvm/java-7-openjdk/jre matlab -nodesktop -nosplash -r "version -java, exit" | grep Java

```

Using alternative JRE would often solve some long-standing problems, such as the extra "`MEvent. CASE!`" string when doing two-finger scrolling using touchpad. Another problem that can be solved in this way is the ugly, limited fonts provided by default, especially for some Chinese characters.

### OpenGL acceleration

MATLAB can take advantage of hardware based 2D and 3D OpenGL acceleration. Support for hardware acceleration needs to be configured outside of MATLAB. Appropriate [video drivers](/index.php/Video_drivers "Video drivers") need to be installed along with the OpenGL utility library [glu](https://www.archlinux.org/packages/?name=glu) package. If X11 forwarding is being used, the video drivers need to be installed on both the client and server. To check if MATLAB is making use of hardware based OpenGL acceleration run:

```
$ matlab -nodesktop -nosplash -r "opengl info; exit" | grep Software

```

If "software rendering" is not "false", then there is a problem with your hardware acceleration. If this is the case make sure OpenGL is configured correctly on the system. This can be done with the `glxinfo` program from the [mesa-demos](https://www.archlinux.org/packages/?name=mesa-demos) package:

```
$ glxinfo | grep "direct rendering"

```

If "direct rendering" is not "yes", then there is likely a problem with your system configuration.

If glxinfo works but not matlab, you can try to run:

```
$ export LD_PRELOAD=/usr/lib/libstdc++.so; export LD_LIBRARY_PATH=/usr/lib/xorg/modules/dri/; matlab -nodesktop -nosplash -r "opengl info; exit" | grep Software

```

If its works, you can edit Matlab launcher script to add:

```
export LD_PRELOAD=/usr/lib/libstdc++.so
export LD_LIBRARY_PATH=/usr/lib/xorg/modules/dri/

```

### Fonts for figures

**Note:** This section only applies to R2014a and earlier as starting with R2014b MATLAB uses True Type Fonts. So as long as `fc-match Helvetica` returns a font, figure fonts should work as expected.

While MATLAB can be run in a text only mode, it also provides advanced graphics capabilities. To confirm that MATLAB is making use of the system fonts run:

```
$ matlab -nodesktop -nosplash -r "xlabel('BIG FONT', 'FontSize', 42); ylabel('small font', 'FontSize', 12); pause; exit" > /dev/null

```

This should produce a MATLAB figure with "BIG FONT" in a large font on the abscissa and "small font" in a small font on the ordinate. If "BIG FONT" and "small font" are both the same size, refer to [Xorg fonts](/index.php/Xorg#Program_requests_.22font_.27.28null.29.27.22 "Xorg") to confirm that the correct the bitmap font package (either [xorg-fonts-100dpi](https://www.archlinux.org/packages/?name=xorg-fonts-100dpi) or [xorg-fonts-75dpi](https://www.archlinux.org/packages/?name=xorg-fonts-75dpi) from the [official repositories](/index.php/Official_repositories "Official repositories")) is installed on your system.

### Sound

To confirm that MATLAB is able to use the default soundcard to present sounds run:

```
$ matlab -nodesktop -nosplash -r "load handel; sound(y, Fs); pause(length(y)/Fs); exit" > /dev/null

```

This should play an except from Handel's "Hallelujah Chorus." If this fails make sure [ALSA](/index.php/ALSA "ALSA") is properly configured. This can be done with the `speaker-test` program from the [alsa-utils](https://www.archlinux.org/packages/?name=alsa-utils) package from the [official repositories](/index.php/Official_repositories "Official repositories"):

```
$ speaker-test

```

If you do not hear anything, then there is likely a problem with your system configuration.

### GPU computing

MATLAB can take advantage of [CUDA enabled GPUs](http://www.mathworks.co.uk/discovery/matlab-gpu.html) to speed up applications. In order to take advantage of a supported GPU install the [nvidia](https://www.archlinux.org/packages/?name=nvidia), [nvidia-utils](https://www.archlinux.org/packages/?name=nvidia-utils), [ocl-icd](https://www.archlinux.org/packages/?name=ocl-icd), [opencl-nvidia](https://www.archlinux.org/packages/?name=opencl-nvidia), and [cuda](https://www.archlinux.org/packages/?name=cuda) packages from the [official repositories](/index.php/Official_repositories "Official repositories"). To check if MATLAB is able to utilize the GPU run:

```
$ matlab -nodesktop -nosplash -r "x=rand(10, 'single'); g=gpuArray(x); Success=isequal(gather(g), x), exit"  | sed -ne '/Success =/,$p'

```

### Install supported compilers

In order to access the full functionality of MATLAB (e.g., to use Simulink, Builder JA, and MEX-file compilation), supported versions of the `gcc`, `g++`, `gfortran`, and `jdk` compilers must be installed. Details about the supported compilers for the [current release](http://www.mathworks.com/support/compilers/current_release/index.html?sec=glnxa64) and [previous releases](http://www.mathworks.com/support/sysreq/previous_releases.html) are available online. Many of the supported `gcc`, `g++`, `jdk` compiler versions for past MATLAB releases are available from the [AUR](/index.php/AUR "AUR") (e.g., [gcc43](https://aur.archlinux.org/packages/gcc43/), [gcc44](https://aur.archlinux.org/packages/gcc44/), [gcc47](https://aur.archlinux.org/packages/gcc47/), [gcc49](https://aur.archlinux.org/packages/gcc49/)and [jdk6](https://aur.archlinux.org/packages/jdk6/)), while past versions of the `gfortran` compilers are not packaged.

To use previous versions of the the `gcc`, `g++`, and `gfortran` compilers with MEX files, edit `${MATLAB}/bin/mexopts.sh` and replace all occurrences of `CC='gcc'` with `CC='gcc-4.X'`, `CXX='g++'` with `CXX='g++-4.X'`, and `FC='gfortran'` with `FC='gfortran-4.X'`, where `X` is the compiler version appropriate for the particular MATLAB release.

**Note:** Though, it's no officially supported, one could still use higher version of compiler, and ignore the warnings.

### Help browser

The help browser uses valuable slots in the dynamic thread vector and causes competition with core functionality provided by libraries like the BLAS that also depend on the dynamic thread vector. The help browser can be configured to use fewer slots in the dynamic thread vector with

```
>> webutils.htmlrenderer('basic');

```

This is a persistent change and to reverse it use

```
>> webutils.htmlrenderer('default');

```

### Garbled Interface

```
export J2D_D3D=false
export MATLAB_JAVA=/usr/lib/jvm/java-7-openjdk/jre

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

is related to the bugs:

*   [961964](http://www.mathworks.de/support/bugreports/961964) for which patched libraries are available from [MathWorks](http://www.mathworks.de/support/bugreports/license/accept_license/5730?fname=attachment_961964_12b_13a_13b_14a_glnxa64_2014-01-30.zip&geck_id=961964)
*   [1003952](http://www.mathworks.com/support/bugreports/1003952) for which workarounds exist

A more general solution of recompiling `glibc` has also been suggested. [[2]](http://stackoverflow.com/a/19468365/2787723)

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

If MATLAB still crashes or corrupts graphics (during startup or when plotting), make sure Java's 2D OpenGL rendering is disabled. The environment variable `_JAVA_OPTIONS` should not contain `-Dsun.java2d.opengl=true`.

### Blank/grey UI when using WM (non-reparenting window manager)

This is a common issue in a number of window managers. (DWM, Awesome, bspwm) Java does not play well with these window managers. There are two methods.

First try setting the environment variable by running

```
$ export _JAVA_AWT_WM_NONREPARENTING=1

```

If Matlab works afterwards, export the variable in your `.xinitrc`.

If it doesn't resolve, you have to fool Java into thinking the WM is named LG3D. (It's an old, depreciated WM that Java applications ironically support) Clean the previous environment variable, install the [wmname](http://tools.suckless.org/wmname) utility, and run.

```
wmname LG3D

```

Try running Matlab. If it works, put the fix in your starting script. (`.xinitrc`, `bspwmrc` and similar should be OK) Do note that other applications (such as `neofetch`, or `tdrop`) will think your WM is named LG3D, so you will have to configure them accordingly. Another solution is to run the command only before launching Matlab, and fixing the name after you are done with Matlab.

If it doesn't work, try the combination of both. (The second line works in bspwm) If it still doesn't work, try googling similar issues with java in general.

### Garbled or invisible text

Set the environment variable `J2D_D3D` to `false`[[3]](https://stackoverflow.com/questions/22737535/swing-rendering-appears-broken-in-jdk-1-8-correct-in-jdk-1-7).

In newer versions of MATLAB (R2015b) [[4]](https://www.reddit.com/r/archlinux/comments/3yaga8/matlab_installer_bonked/) this also requires setting `MATLAB_JAVA` to something openjdk based. Example:

```
export J2D_D3D=false
./bin/glnxa64/install_unix -javadir /usr/lib/jvm/java-7-openjdk/jre

```

### Corrupted text and fonts in menus and fields

If you notice that the menus or the input fields are corrupted or not appearing correctly then you can try to activate the *"**Use antialiasing to smooth desktop fonts**"* option in Matlab preferences, it seems to solve the problem. Go to ***Preferences -> Matlab -> Fonts*** and activate it. You will need to restart Matlab in order to take affect.

### Installation

As one installs Matlab, it might complain that it cannot find a package, for the most part just look at the package name and then install it with [Pacman](/index.php/Pacman "Pacman"), or in the case of x86_64 there are some libraries only in [AUR](/index.php/AUR "AUR").

### Install-time library errors

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

*   Matlab R2017b with an up-to-date Arch Linux (as of September 30, 2017) fails on startup with the familiar "Failure loading desktop class." A solution is to install outdated versions of the libraries in the packages [cairo](https://www.archlinux.org/packages/?name=cairo) (1.14.10 works) and [harfbuzz](https://www.archlinux.org/packages/?name=harfbuzz) (1.4.6 works) to a local directory and add them to the LD_LIBRARY_PATH for matlab (See also: [[5]](https://bbs.archlinux.org/viewtopic.php?id=228944)):

```
LD_LIBRARY_PATH="/opt/matlab/outdatedLibraries/:$LD_LIBRARY_PATH" /opt/matlab/R2017b/bin/matlab

```

### Segmentation fault on startup

If Matlab (R2016a or earlier) stops working after upgrading [ncurses](https://www.archlinux.org/packages/?name=ncurses) to v6.x, [install](/index.php/Install "Install") the [ncurses5-compat-libs](https://aur.archlinux.org/packages/ncurses5-compat-libs/) package. See [BBS#202575](https://bbs.archlinux.org/viewtopic.php?id=202575).

In newer versions (e.g. R2017b), the issue could also be due to a font display failing to load. Try moving the libfreetype.so.6 font display file in $MATLAB/bin/glnxa64/ to an 'exclude' directory; see [BBS#231299](https://bbs.archlinux.org/viewtopic.php?id=231299).

### Hangs on rendering or exiting with Intel graphics

Some users have reported issues with DRI3 enabled on Intel Graphics chips. A possible workaround is to disable DRI3 and run MATLAB with hardware rendering on DRI2; to do so, launch MATLAB with the environment variable LIBGL_DRI3_DISABLE set to 1:

```
LIBGL_DRI3_DISABLE=1 /{MATLAB}/bin/matlab

```

If the previous workaround does not work, the issue can be circumvented by selecting software rendering with the MATLAB command (beware, performance may be very poor when doing e.g. big or complex 3D plots):

```
opengl('save','software')

```

See [[6]](https://bugzilla.redhat.com/show_bug.cgi?id=1357571) and [[7]](https://bugs.freedesktop.org/show_bug.cgi?id=96671) for more.

### Addon manager not working

Addon manager requires the [libselinux](https://aur.archlinux.org/packages/libselinux/) package to work. (in Matlab 2017b)

Since upgrade from pango-1.40.5 to pango-1.40.6, the MATLABWindow application (responsible for Add-On Manager, Simulation Data Inspector and perhaps something else) cannot be started. [[8]](https://bugs.archlinux.org/task/54257) A workaround is to point MATLAB shipping glib libraries to those glib libraries from your system. There are 5 of those libraries in `matlabroot/R2017b/cefclient/sys/os/glnxa64`, namely, as of R2017b:

```
libgio-2.0.so
libglib-2.0.so
libgmodule-2.0.so
libgobject-2.0.so
libgthread-2.0.so

```

Make it so that these symlinks are pointing to your system glib libraries instead of versions located in `matlabroot/R2017b/cefclient/sys/os/glnxa64`. On a standard arch install the local files reside in `/usr/lib/`.

Relinking of "libfreetype.so.6" is also necessary to open these interfaces. This is found in `matlabroot/R2017b/bin/glnxa64/`.

If the window opens but is blank, consider switching the html renderer to: " webutils.htmlrenderer('basic');" as described in [#Help browser](#Help_browser).

### Live Script Errors

If you get the error when attempting to load or create a LiveScript:

```
 `Viewing matlab live script files is not currently supported by this operating system configuration`

```

The steps in [#Addon manager not working](#Addon_manager_not_working) may resolve the issue.

### Using webcam/video device

Make sure the correct support package addons are installed (webcam or OS Generic Video Interface for example). If running matlab as a user, make sure your user has write permissions to wherever the support packages are being downloaded and installed.

At least Matlab 2016b doesn't recognize webcams or imaq adapters correctly without gstreamer0.10\. The gstreamer0.10 can be found in the aur and installed as a work around.

Since MATLAB R2017a, Image Acqusition Toolbox is using GStreamer library version 1.0\. It previously used version 0.10.

### MATLAB hangs for several minutes when closing Help Browser

Since upgrade of glibc from 2.24 to 2.25, MATLAB (at least R2017a) hangs when closing Help Browser. The issue is related to the particular version of jxbrowser-chromium shipped with MATLAB. This issue is still present with glibc 2.26 and MATLAB R2017b.

To fix this issue, download the [latest jxbrowser](https://www.teamdev.com/jxbrowser) and replace the following jars from MATLAB:

```
matlabroot/java/jarext/jxbrowser-chromium/jxbrowser-chromium.jar
matlabroot/java/jarext/jxbrowser-chromium/jxbrowser-linux64.jar

```

MATLAB should automatically unpack those jars into `matlabroot/sys/jxbrowser-chromium/glnxa64/chromium` when first opening Help Browser. Remove `matlabroot/sys/jxbrowser-chromium/glnxa64/chromium` directory to make sure MATLAB uses the latest jxbrowser.

Unfortunately, this workaround doesn't work in R2017b anymore. Going deeper into investigation of this issue, it is related to a crash of one of jxbrowser-chromium processes. The parent process of jxbrowser-chromium then sits there and waits for response from a process that is already dead. This causes MATLAB main window to freeze. You can easily unfreeze MATLAB by manually killing all leftover jxbrowser-chromium processes.

I've come up with this simple script that uses inotify and waits for user to close Help browser in MATLAB. It triggers when user closes Help browser and sends kill signal to all leftover jxbrowser-chromium processes:

```
#!/usr/bin/bash

if [ -z "$1" ]; then
	REL=R2017b
else
	REL=$1
fi

JXPATH="/path/to/MATLAB/$REL/sys/jxbrowser-chromium/glnxa64/chromium"
CMD="inotifywait -m -e CLOSE $JXPATH/resources.pak"

#Exit if the daemon is already active
if ! pgrep -f "$CMD" > /dev/null; then
	#Wait for user to close Help Browser, then killall leftover jxbrowser processes
	$CMD |
	while read line
	do
		killall "$JXPATH/jxbrowser-chromium"
	done
else
	exit
fi

```

I run this script as part of my MATLAB start script like that:

```
~/bin/unfreeze_matlab.sh R2017b &

```

To make sure that this background job is killed when I exit MATLAB, I use this in the beginning of MATLAB start script:

```
trap "trap - SIGTERM && kill -- -$$" SIGINT SIGTERM EXIT

```

### Some dropdown menus cannot be selected

In some interfaces - such as Simulation Data Inspector or Simulink Test Manager - nothing happens when choosing an item in dropdown menu (for example, when trying to change a number of subplots in Simulation Data Inspector). To work around this issue, hold down the Shift key while clicking the item in dropdown menu.

### Not starting - licensing error

In case MATLAB will not start from a [desktop environment](/index.php/Desktop_environment "Desktop environment") by the call of its [desktop file](/index.php/Desktop_file "Desktop file") one should see the output as you start it from the terminal. For a *Licensing error* such as:

 `# matlab` 
```
MATLAB is selecting SOFTWARE OPENGL rendering.
License checkout failed.
License Manager Error -9
This error may occur when: 
-The hostid of this computer does not match the hostid in the license file. 
-A Designated Computer installation is in use by another user. 
If no other user is currently running MATLAB, you may need to activate.

Troubleshoot this issue by visiting: 
[http://www.mathworks.com/support/lme/R2017a/9](http://www.mathworks.com/support/lme/R2017a/9)

Diagnostic Information:
Feature: MATLAB 
License path: /home/<USER>/.matlab/R2017a_licenses/license_<NUM>_R2017a.lic:/home/<USER>/.matlab/R2017a_licenses/lice
nse_Darkness_<NUM>_R2017a.lic:/opt/MATLAB/R2017a/licenses/license.dat:/opt/MATLAB/R2017a/licenses/*
.lic 
Licensing error: -9,57.

```

a re-[activation](#Activation) might solve the problem.

### MATLAB crashes with "Failure loading desktop class" on startup

In case MATLAB won't start and starting it from command line gives you the following error:

 `$ matlab` 
```
Fatal Internal Error: Internal Error: Failure occurs during desktop startup. Details: Failure loading desktop class.

```

and you have the option [`-Dswing.defaultlaf=com.sun.java.swing.plaf.gtk.GTKLookAndFeel`](/index.php/Java#GTK_LookAndFeel "Java") set in your `_JAVA_OPTIONS` environment variable, start MATLAB with

```
$ _JAVA_OPTIONS= matlab

```

If this works, add the line

```
export _JAVA_OPTIONS=

```

to your MATLAB launcher script. Optionally re-add other Java options.

## Matlab in a systemd-nspawn

Matlab can be run within a systemd-nspawn container to maintain a static system and avoid the library issues that often plague matlab installs after significant updates to libraries in Arch. Refer to [Systemd-nspawn](/index.php/Systemd-nspawn "Systemd-nspawn") for detailed information on setting up such containers.

The following lists instruction to get a MATLAB 2017b install running in a minimal debian 9 environment. It assumes matlab is already installed as normal in "/usr/local/MATLAB/R2017b".

Use [Xhost](/index.php/Xhost "Xhost") to allow the nspawn environment to use the existing X server instance.

Create a minimal debian environment in a folder ("deb9" here) with:

```
$ debootstrap --arch=amd64 stretch deb9

```

Set a password for the root user and then boot the environment with:

```
$ systemd-nspawn --bind-ro=/dev/dri --bind=/tmp/.X11-unix --bind=/usr/local/MATLAB/ -b -D deb9

```

Install the following packages to have the requisite libraries in the nspawn environment for MATLAB. "mesa-utils" and "usbutils" can be installed to debug graphics acceleration and usb interfaces for I/O with MATLAB.

```
$ apt-get install xorg build-essential libgtk2.0-0 libnss3 libasound2 

```

Install the MATLAB-support (from contrib source) package in the environment for some convenient integration.

```
$ apt-get install matlab-support

```

Set the $DISPLAY variable to use your existing X server instance.

```
$ export DISPLAY=:0

```

MATLAB can be launched from within the environment normally by using the binary at $MATLABROOT/bin.