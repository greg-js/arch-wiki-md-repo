Related articles

*   [Octave](/index.php/Octave "Octave")
*   [Sage-mathematics](/index.php/Sage-mathematics "Sage-mathematics")
*   [Mathematica](/index.php/Mathematica "Mathematica")

**翻译状态：** 本文是英文页面 [Matlab](/index.php/Matlab "Matlab") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2017-12-1，点击[这里](https://wiki.archlinux.org/index.php?title=Matlab&diff=0&oldid=498851)可以查看翻译后英文页面的改动。

据[官方网站](http://www.mathworks.com/products/matlab/):

	*MATLAB是可用于数值计算，可视化和编程的高级语言和交互式环境。MATLAB可以分析数据，开发算法和创建模型和应用程序。与电子表格或传统编程语言（如C / C ++或Java）相比，Matlab的语言，工具和内置数学函数可以使用户更快地探索多种解决问题的方法并形成解决方案。*

## Contents

*   [1 概览](#.E6.A6.82.E8.A7.88)
*   [2 安装](#.E5.AE.89.E8.A3.85)
    *   [2.1 使用Matlab安装程序安装](#.E4.BD.BF.E7.94.A8Matlab.E5.AE.89.E8.A3.85.E7.A8.8B.E5.BA.8F.E5.AE.89.E8.A3.85)
        *   [2.1.1 桌面图标](#.E6.A1.8C.E9.9D.A2.E5.9B.BE.E6.A0.87)
    *   [2.2 从AUR安装](#.E4.BB.8EAUR.E5.AE.89.E8.A3.85)
*   [3 激活](#.E6.BF.80.E6.B4.BB)
    *   [3.1 R2013b及更早版本](#R2013b.E5.8F.8A.E6.9B.B4.E6.97.A9.E7.89.88.E6.9C.AC)
*   [4 配置](#.E9.85.8D.E7.BD.AE)
    *   [4.1 Java](#Java)
    *   [4.2 OpenGL加速](#OpenGL.E5.8A.A0.E9.80.9F)
    *   [4.3 字体配置（仅适用于R2014a及更早版本）](#.E5.AD.97.E4.BD.93.E9.85.8D.E7.BD.AE.EF.BC.88.E4.BB.85.E9.80.82.E7.94.A8.E4.BA.8ER2014a.E5.8F.8A.E6.9B.B4.E6.97.A9.E7.89.88.E6.9C.AC.EF.BC.89)
    *   [4.4 音频](#.E9.9F.B3.E9.A2.91)
    *   [4.5 GPU计算](#GPU.E8.AE.A1.E7.AE.97)
    *   [4.6 安装额外的编译器](#.E5.AE.89.E8.A3.85.E9.A2.9D.E5.A4.96.E7.9A.84.E7.BC.96.E8.AF.91.E5.99.A8)
    *   [4.7 Matlab的帮助查看器的配置](#Matlab.E7.9A.84.E5.B8.AE.E5.8A.A9.E6.9F.A5.E7.9C.8B.E5.99.A8.E7.9A.84.E9.85.8D.E7.BD.AE)
*   [5 问题对策](#.E9.97.AE.E9.A2.98.E5.AF.B9.E7.AD.96)
    *   [5.1 静态线程本地存储错误](#.E9.9D.99.E6.80.81.E7.BA.BF.E7.A8.8B.E6.9C.AC.E5.9C.B0.E5.AD.98.E5.82.A8.E9.94.99.E8.AF.AF)
    *   [5.2 Matlab在显示图像时崩溃](#Matlab.E5.9C.A8.E6.98.BE.E7.A4.BA.E5.9B.BE.E5.83.8F.E6.97.B6.E5.B4.A9.E6.BA.83)
    *   [5.3 Blank/grey UI when using WM (non-reparenting window manager)](#Blank.2Fgrey_UI_when_using_WM_.28non-reparenting_window_manager.29)
    *   [5.4 文本乱码或不可见](#.E6.96.87.E6.9C.AC.E4.B9.B1.E7.A0.81.E6.88.96.E4.B8.8D.E5.8F.AF.E8.A7.81)
    *   [5.5 菜单和输入窗口的文字显示异常](#.E8.8F.9C.E5.8D.95.E5.92.8C.E8.BE.93.E5.85.A5.E7.AA.97.E5.8F.A3.E7.9A.84.E6.96.87.E5.AD.97.E6.98.BE.E7.A4.BA.E5.BC.82.E5.B8.B8)
    *   [5.6 安装时的问题](#.E5.AE.89.E8.A3.85.E6.97.B6.E7.9A.84.E9.97.AE.E9.A2.98)
    *   [5.7 安装时library错误](#.E5.AE.89.E8.A3.85.E6.97.B6library.E9.94.99.E8.AF.AF)
    *   [5.8 解决启动时警告/错误问题](#.E8.A7.A3.E5.86.B3.E5.90.AF.E5.8A.A8.E6.97.B6.E8.AD.A6.E5.91.8A.2F.E9.94.99.E8.AF.AF.E9.97.AE.E9.A2.98)
    *   [5.9 启动Matlab时与ncurses有关的错误（启动时出现分段错误）](#.E5.90.AF.E5.8A.A8Matlab.E6.97.B6.E4.B8.8Encurses.E6.9C.89.E5.85.B3.E7.9A.84.E9.94.99.E8.AF.AF.EF.BC.88.E5.90.AF.E5.8A.A8.E6.97.B6.E5.87.BA.E7.8E.B0.E5.88.86.E6.AE.B5.E9.94.99.E8.AF.AF.EF.BC.89)
    *   [5.10 与Intel显卡有关的错误](#.E4.B8.8EIntel.E6.98.BE.E5.8D.A1.E6.9C.89.E5.85.B3.E7.9A.84.E9.94.99.E8.AF.AF)
    *   [5.11 附加组件管理器无法使用](#.E9.99.84.E5.8A.A0.E7.BB.84.E4.BB.B6.E7.AE.A1.E7.90.86.E5.99.A8.E6.97.A0.E6.B3.95.E4.BD.BF.E7.94.A8)
    *   [5.12 LiveScript错误](#LiveScript.E9.94.99.E8.AF.AF)
    *   [5.13 Using webcam/video device](#Using_webcam.2Fvideo_device)
    *   [5.14 关闭帮助窗口时Matlab数秒无响应](#.E5.85.B3.E9.97.AD.E5.B8.AE.E5.8A.A9.E7.AA.97.E5.8F.A3.E6.97.B6Matlab.E6.95.B0.E7.A7.92.E6.97.A0.E5.93.8D.E5.BA.94)
    *   [5.15 一些下拉菜单无法被选中](#.E4.B8.80.E4.BA.9B.E4.B8.8B.E6.8B.89.E8.8F.9C.E5.8D.95.E6.97.A0.E6.B3.95.E8.A2.AB.E9.80.89.E4.B8.AD)
    *   [5.16 因许可证问题造成的无法启动Matlab](#.E5.9B.A0.E8.AE.B8.E5.8F.AF.E8.AF.81.E9.97.AE.E9.A2.98.E9.80.A0.E6.88.90.E7.9A.84.E6.97.A0.E6.B3.95.E5.90.AF.E5.8A.A8Matlab)
    *   [5.17 启动Matlab时显示"Failure loading desktop class"并崩溃](#.E5.90.AF.E5.8A.A8Matlab.E6.97.B6.E6.98.BE.E7.A4.BA.22Failure_loading_desktop_class.22.E5.B9.B6.E5.B4.A9.E6.BA.83)
*   [6 在systemd-nspawn容器中运行](#.E5.9C.A8systemd-nspawn.E5.AE.B9.E5.99.A8.E4.B8.AD.E8.BF.90.E8.A1.8C)

## 概览

MATLAB是MathWorks公司开发的专有软件。获取，安装和激活Matlab需要许可证。MATLAB的新版本一年发布两次，发布名称由`R`,发布年份和`a`或`b`构成。从R2012b开始，只有64位Linux才可使用Matlab。Matlab在Arch Linux上一般可以正常运行。参见[系统要求](https://cn.mathworks.com/support/sysreq.html)

## 安装

可通过[MathWorks公司网站](https://www.mathworks.com)下载安装程序。可以直接从MATLAB安装软件中安装，也可以通过[matlab](https://aur.archlinux.org/packages/matlab/)（前者的优点是可以由无root权限的用户安装到到他们的主目录)。

### 使用Matlab安装程序安装

Matlab在安装时可能会自己额外下载程序,有的甚至如果没有网络连接就无法安装（如）。Matlab安装软件安装时需要一个可用的GUI（Xorg或Wayland）。可以以root用户身份运行脚本来为所有用户安装MATLAB，或者不使用root只为你安装。 在安装过程中，系统会询问您是否想要自己创建软链接，如果选否的话，以后可以手动创建符号链接，以便于在终端启动matlab：

```
 ＃ ln -s /{MATLAB}/bin/matlab /usr/local/bin

```

#### 桌面图标

Optionally create a [desktop entry](/index.php/Desktop_entry "Desktop entry"). The MIME type of MATLAB files is `text/x-matlab`.

Start `matlab` with:

*   `-desktop` to run Matlab without a terminal.
*   `-nosplash` to prevent the splash screen from showing up.

In order for icons to appear correctly `StartupWMClass` needs to be set in the desktop entry. To find it out start MATLAB, run `xprop | grep WM_CLASS` and select the MATLAB window.

### 从AUR安装

The EULA for the proprietary MATLAB software is restrictive. The [matlab](https://aur.archlinux.org/packages/matlab/) package from the [AUR](/index.php/AUR "AUR") is designed to allow MATLAB to be integrated into and managed by Arch. The package should be built on the system on which it is going to be installed and the package should be deleted from the installation location and the [Pacman](/index.php/Pacman "Pacman") cache following installation. Distributing the package is a clear violation of the EULA.

The [matlab](https://aur.archlinux.org/packages/matlab/) package from the [AUR](/index.php/AUR "AUR") defaults to building a package for the most recent 64-bit release of MATLAB, although the PKGBUILD supports MATLAB releases from R2010b and even the installation of multiple releases simultaneous. The PKGBUILD defaults to installing all toolboxes that the file identification key allows, however, the PKGBUILD can be edited to include only a subset of the toolboxes. The selection of the toolboxes must be finalized at the time of package creation due to DRM policies put in place by The MathWorks. The [matlab](https://aur.archlinux.org/packages/matlab/) package from the [AUR](/index.php/AUR "AUR") requires that both the MATLAB installation software and the file installation key are available in the source directory. The file installation key must be in a file called `matlab.fik` and the installation software must be in an iso file called `matlab.iso`. Once the iso file and file installation key are created, the MATLAB package can be created and install as usual.

For MATLAB releases between r2010b and r2011a the contents of the iso file must include: `./archives/`, `./bin/`, `./etc/`, `./help/`, `./java/`, `./activate.ini`, `./install`, and `./installer_input.txt`. If the MATLAB download agent is used to download the installation software, then the iso file can be trivially created by simply running `mkisofs -r -o` on the download directory.

For MATLAB releases including and after r2011b the contents of the iso file must include: `./archives/`, `./bin/`, `./etc/`, `./help/`, `./java/`, `./activate.ini`, `./install`, and `./installer_input.txt`. For version before r2014a, the MATLAB download agent could download all the required files and the iso file could be trivially created by simply running `mkisofs -r -o` on the download directory. For MATLAB releases including and after r2014a the MATLAB download agent only downloads the MATLAB installer. The MATLAB installer then needs to be run to downloaded the MATLAB software and toolboxes. Therefore, a two step process is required to generate this iso file with the MATLAB download agent. First, you download and run the MATLAB installer to install MATLAB in a temporary directory. This process downloads the MATLAB software and toolboxes by default to `~/Downloads/MathWorks` (this can be changed by passing the flag `-downloadFolder /path/to/directory`). It is actually possible quit the MATLAB installer once the software and toolboxes are downloaded. Once the software and toolboxes are downloaded the required iso file can be created by merging the installer directory (containing above mentioned files) and the download directory (containing `./archives/`), and then running `mkisofs -r -o` on the resulting directory.

## 激活

In order to run MATLAB it requires a license file to be installed. The license file can be generated with `$MATLABROOT/bin/activate_matlab.sh` or downloaded from [MATLAB](http://www.mathworks.com) directly.

### R2013b及更早版本

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

## 配置

### Java

The MATLAB software is bundled with a JVM and therefore it is not necessary to install [Java](/index.php/Java "Java"). The JVM version bundled with MATLAB typically lags behind [jre7-openjdk](https://www.archlinux.org/packages/?name=jre7-openjdk) from the [official repositories](/index.php/Official_repositories "Official repositories") and it is possible, although not required, to use the `MATLAB_JAVA` environment variable to specify the path of an alternative JRE. For example, to specify the [jre7-openjdk](https://www.archlinux.org/packages/?name=jre7-openjdk) JRE and check the resulting version of Java, do:

```
$ MATLAB_JAVA=/usr/lib/jvm/java-7-openjdk/jre matlab -nodesktop -nosplash -r "version -java, exit" | grep Java

```

Using alternative JRE would often solve some long-standing problems, such as the extra "`MEvent. CASE!`" string when doing two-finger scrolling using touchpad. Another problem that can be solved in this way is the ugly, limited fonts provided by default, especially for some Chinese characters.

### OpenGL加速

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

### 字体配置（仅适用于R2014a及更早版本）

**Note:** This section only applies to R2014a and earlier as starting with R2014b MATLAB uses True Type Fonts. So as long as `fc-match Helvetica` returns a font, figure fonts should work as expected.

While MATLAB can be run in a text only mode, it also provides advanced graphics capabilities. To confirm that MATLAB is making use of the system fonts run:

```
$ matlab -nodesktop -nosplash -r "xlabel('BIG FONT', 'FontSize', 42); ylabel('small font', 'FontSize', 12); pause; exit" > /dev/null

```

This should produce a MATLAB figure with "BIG FONT" in a large font on the abscissa and "small font" in a small font on the ordinate. If "BIG FONT" and "small font" are both the same size, refer to [Xorg fonts](/index.php/Xorg#Program_requests_.22font_.27.28null.29.27.22 "Xorg") to confirm that the correct the bitmap font package (either [xorg-fonts-100dpi](https://www.archlinux.org/packages/?name=xorg-fonts-100dpi) or [xorg-fonts-75dpi](https://www.archlinux.org/packages/?name=xorg-fonts-75dpi) from the [official repositories](/index.php/Official_repositories "Official repositories")) is installed on your system.

### 音频

To confirm that MATLAB is able to use the default soundcard to present sounds run:

```
$ matlab -nodesktop -nosplash -r "load handel; sound(y, Fs); pause(length(y)/Fs); exit" > /dev/null

```

This should play an except from Handel's "Hallelujah Chorus." If this fails make sure [ALSA](/index.php/ALSA "ALSA") is properly configured. This can be done with the `speaker-test` program from the [alsa-utils](https://www.archlinux.org/packages/?name=alsa-utils) package from the [official repositories](/index.php/Official_repositories "Official repositories"):

```
$ speaker-test

```

If you do not hear anything, then there is likely a problem with your system configuration.

### GPU计算

MATLAB can take advantage of [CUDA enabled GPUs](http://www.mathworks.co.uk/discovery/matlab-gpu.html) to speed up applications. In order to take advantage of a supported GPU install the [nvidia](https://www.archlinux.org/packages/?name=nvidia), [nvidia-utils](https://www.archlinux.org/packages/?name=nvidia-utils), [ocl-icd](https://www.archlinux.org/packages/?name=ocl-icd), [opencl-nvidia](https://www.archlinux.org/packages/?name=opencl-nvidia), and [cuda](https://www.archlinux.org/packages/?name=cuda) packages from the [official repositories](/index.php/Official_repositories "Official repositories"). To check if MATLAB is able to utilize the GPU run:

```
$ matlab -nodesktop -nosplash -r "x=rand(10, 'single'); g=gpuArray(x); Success=isequal(gather(g), x), exit"  | sed -ne '/Success =/,$p'

```

### 安装额外的编译器

In order to access the full functionality of MATLAB (e.g., to use Simulink, Builder JA, and MEX-file compilation), supported versions of the `gcc`, `g++`, `gfortran`, and `jdk` compilers must be installed. Details about the supported compilers for the [current release](http://www.mathworks.com/support/compilers/current_release/index.html?sec=glnxa64) and [previous releases](http://www.mathworks.com/support/sysreq/previous_releases.html) are available online. Many of the supported `gcc`, `g++`, `jdk` compiler versions for past MATLAB releases are available from the [AUR](/index.php/AUR "AUR") (e.g., [gcc43](https://aur.archlinux.org/packages/gcc43/), [gcc44](https://aur.archlinux.org/packages/gcc44/), [gcc47](https://aur.archlinux.org/packages/gcc47/), [gcc49](https://aur.archlinux.org/packages/gcc49/)and [jdk6](https://aur.archlinux.org/packages/jdk6/)), while past versions of the `gfortran` compilers are not packaged.

To use previous versions of the the `gcc`, `g++`, and `gfortran` compilers with MEX files, edit `${MATLAB}/bin/mexopts.sh` and replace all occurrences of `CC='gcc'` with `CC='gcc-4.X'`, `CXX='g++'` with `CXX='g++-4.X'`, and `FC='gfortran'` with `FC='gfortran-4.X'`, where `X` is the compiler version appropriate for the particular MATLAB release.

**Note:** Though, it's no officially supported, one could still use higher version of compiler, and ignore the warnings.

### Matlab的帮助查看器的配置

The help browser uses valuable slots in the dynamic thread vector and causes competition with core functionality provided by libraries like the BLAS that also depend on the dynamic thread vector. The help browser can be configured to use fewer slots in the dynamic thread vector with

```
>> webutils.htmlrenderer('basic');

```

This is a persistent change and to reverse it use

```
>> webutils.htmlrenderer('default');

```

## 问题对策

### 静态线程本地存储错误

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

A more general solution of recompiling `glibc` has also been suggested. [[1]](http://stackoverflow.com/a/19468365/2787723)

### Matlab在显示图像时崩溃

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

### 文本乱码或不可见

Set the environment variable `J2D_D3D` to `false`[[2]](https://stackoverflow.com/questions/22737535/swing-rendering-appears-broken-in-jdk-1-8-correct-in-jdk-1-7).

In newer versions of MATLAB (R2015b) [[3]](https://www.reddit.com/r/archlinux/comments/3yaga8/matlab_installer_bonked/) this also requires setting `MATLAB_JAVA` to something openjdk based. Example:

```
export J2D_D3D=false
./bin/glnxa64/install_unix -javadir /usr/lib/jvm/java-7-openjdk/jre

```

### 菜单和输入窗口的文字显示异常

If you notice that the menus or the input fields are corrupted or not appearing correctly then you can try to activate the *"**Use antialiasing to smooth desktop fonts**"* option in Matlab preferences, it seems to solve the problem. Go to ***Preferences -> Matlab -> Fonts*** and activate it. You will need to restart Matlab in order to take affect.

### 安装时的问题

As one installs Matlab, it might complain that it cannot find a package, for the most part just look at the package name and then install it with [Pacman](/index.php/Pacman "Pacman"), or in the case of x86_64 there are some libraries only in [AUR](/index.php/AUR "AUR").

### 安装时library错误

*   Make sure that the symlink `bin/glnx64/libstdc++.so.6` is pointing to the correct version of `libstdc++.so.xx` (which is also in the same directory and has numbers where 'xx' is). By default, it may be pointing to an older (and nonexistent) version (different value for 'xx').

*   Make sure the device you're installing from is not mounted as `noexec`

*   If you downloaded the files from Mathworks' website, make sure they are not on an NTFS or FAT partition, because that can mess up the symlinks. Ext4 or Ext3 should work.

### 解决启动时警告/错误问题

*   Even if all needed libraries are installed, Matlab when starting can still report some missing libraries. This is resolved by symbolic linking of needed libraries to directories that Matlab checks at start-up. For example, if Matlab triggers error/warning about missing `/lib64/libc.so.6` library, this can be resolved by:

```
# ln -s /lib/libc.so.6 /lib64

```

*   Matlab R2011b with an up-to-date Arch Linux (as of March 12, 2012) fails on startup with the familiar "Failure loading desktop class." A solution is to point Matlab to the system JVM (confirmed to work with the [jdk7-openjdk](https://www.archlinux.org/packages/?name=jdk7-openjdk) package):

```
export MATLAB_JAVA=/usr/lib/jvm/java-7-openjdk/jre

```

*   Matlab R2017b with an up-to-date Arch Linux (as of September 30, 2017) fails on startup with the familiar "Failure loading desktop class." A solution is to install outdated versions of the libraries in the packages [cairo](https://www.archlinux.org/packages/?name=cairo) (1.14.10 works) and [harfbuzz](https://www.archlinux.org/packages/?name=harfbuzz) (1.4.6 works) to a local directory and add them to the LD_LIBRARY_PATH for matlab (See also: [[4]](https://bbs.archlinux.org/viewtopic.php?id=228944)):

```
LD_LIBRARY_PATH="/opt/matlab/outdatedLibraries/:$LD_LIBRARY_PATH" /opt/matlab/R2017b/bin/matlab

```

### 启动Matlab时与ncurses有关的错误（启动时出现分段错误）

If Matlab (R2016a or earlier) stops working after upgrading [ncurses](https://www.archlinux.org/packages/?name=ncurses) to v6.x, [install](/index.php/Install "Install") the [ncurses5-compat-libs](https://aur.archlinux.org/packages/ncurses5-compat-libs/) package. See [BBS#202575](https://bbs.archlinux.org/viewtopic.php?id=202575).

In newer versions (e.g. R2017b), the issue could also be due to a font display failing to load. Try moving the libfreetype.so.6 font display file in $MATLAB/bin/glnxa64/ to an 'exclude' directory; see [BBS#231299](https://bbs.archlinux.org/viewtopic.php?id=231299).

### 与Intel显卡有关的错误

Some users have reported issues with DRI3 enabled on Intel Graphics chips. A possible workaround is to disable DRI3 and run MATLAB with hardware rendering on DRI2; to do so, launch MATLAB with the environment variable LIBGL_DRI3_DISABLE set to 1:

```
LIBGL_DRI3_DISABLE=1 /{MATLAB}/bin/matlab

```

If the previous workaround does not work, the issue can be circumvented by selecting software rendering with the MATLAB command (beware, performance may be very poor when doing e.g. big or complex 3D plots):

```
opengl('save','software')

```

See [[5]](https://bugzilla.redhat.com/show_bug.cgi?id=1357571) and [[6]](https://bugs.freedesktop.org/show_bug.cgi?id=96671) for more.

### 附加组件管理器无法使用

Addon manager requires the [libselinux](https://aur.archlinux.org/packages/libselinux/) package to work. (in Matlab 2017b)

Since upgrade from pango-1.40.5 to pango-1.40.6, the MATLABWindow application (responsible for Add-On Manager, Simulation Data Inspector and perhaps something else) cannot be started. [[7]](https://bugs.archlinux.org/task/54257) A workaround is to point MATLAB shipping glib libraries to those glib libraries from your system. There are 5 of those libraries in `matlabroot/R2017b/cefclient/sys/os/glnxa64`, namely, as of R2017b:

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

### LiveScript错误

If you get the error when attempting to load or create a LiveScript:

```
 `Viewing matlab live script files is not currently supported by this operating system configuration`

```

The steps in [#Addon manager not working](#Addon_manager_not_working) may resolve the issue.

### Using webcam/video device

Make sure the correct support package addons are installed (webcam or OS Generic Video Interface for example). If running matlab as a user, make sure your user has write permissions to wherever the support packages are being downloaded and installed.

At least Matlab 2016b doesn't recognize webcams or imaq adapters correctly without gstreamer0.10\. The gstreamer0.10 can be found in the aur and installed as a work around.

Since MATLAB R2017a, Image Acqusition Toolbox is using GStreamer library version 1.0\. It previously used version 0.10.

### 关闭帮助窗口时Matlab数秒无响应

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

### 一些下拉菜单无法被选中

In some interfaces - such as Simulation Data Inspector or Simulink Test Manager - nothing happens when choosing an item in dropdown menu (for example, when trying to change a number of subplots in Simulation Data Inspector). To work around this issue, hold down the Shift key while clicking the item in dropdown menu.

### 因许可证问题造成的无法启动Matlab

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

### 启动Matlab时显示"Failure loading desktop class"并崩溃

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

## 在systemd-nspawn容器中运行

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