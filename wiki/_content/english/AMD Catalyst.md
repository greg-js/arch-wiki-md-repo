Related articles

*   [ATI](/index.php/ATI "ATI")
*   [Xorg](/index.php/Xorg "Xorg")

Owners of ATI/AMD video cards have a choice between AMD's proprietary driver ([catalyst](https://aur.archlinux.org/packages/catalyst/)) and the open source driver ([ATI](/index.php/ATI "ATI") for older or [AMDGPU](/index.php/AMDGPU "AMDGPU") for newer cards). This article covers the proprietary driver.

AMD's Linux driver package *catalyst* was previously named *fglrx* (**F**ire**GL** and **R**adeon **X**). Only the package name has changed, while the kernel module retains its original *fglrx.ko* filename. Therefore, any mention of fglrx below is specifically in reference to the *kernel module*, **not the package**.

**Catalyst packages are no longer offered in the official repositories. It is no longer updated by AMD and does not support the latest Xorg, so installing an old Xorg is required.**

Compared with the open source driver, Catalyst performs generally worse in 2D rendering and generally equal in 3D rendering, also having better power management, but it lacks efficient multi-head support. Catalyst does support OpenCL 2.0 though and that's the main difference between Catalyst and open source drivers. Supported devices are [ATI/AMD Radeon](https://en.wikipedia.org/wiki/Radeon "wikipedia:Radeon") video cards with R600 to Volcanic Islands chipsets (Radeon HD 2xxx to Rx 300 cards). See the [Release notes](https://support.amd.com/en-us/kb-articles/Pages/AMDRadeonSoftwareCrimsonEdition15-12LINReleaseNotes.aspx), [Xorg decoder ring](https://www.x.org/wiki/RadeonFeature/#index5h2) or [this table](https://en.wikipedia.org/wiki/List_of_AMD_graphics_processing_units "wikipedia:List of AMD graphics processing units"), to translate *model* names (HD2400, HD6990) to/from *chip* names (R600, *Northern Islands* respectively).

## Contents

*   [1 Selecting the right driver](#Selecting_the_right_driver)
*   [2 Installation](#Installation)
    *   [2.1 Installing the driver](#Installing_the_driver)
        *   [2.1.1 Installing from the unofficial repository](#Installing_from_the_unofficial_repository)
        *   [2.1.2 Installing from the AUR](#Installing_from_the_AUR)
    *   [2.2 Configuring the driver](#Configuring_the_driver)
        *   [2.2.1 Configuring X](#Configuring_X)
        *   [2.2.2 Loading the module at boot](#Loading_the_module_at_boot)
        *   [2.2.3 Disable kernel mode setting](#Disable_kernel_mode_setting)
        *   [2.2.4 Checking operation](#Checking_operation)
    *   [2.3 Custom kernels](#Custom_kernels)
    *   [2.4 PowerXpress support](#PowerXpress_support)
        *   [2.4.1 Running two X servers (one using the Intel driver, another one using fglrx) simultaneously](#Running_two_X_servers_.28one_using_the_Intel_driver.2C_another_one_using_fglrx.29_simultaneously)
        *   [2.4.2 Issues with PowerXpress laptops running in AMD mode (pxp_switch_catalyst amd) with external / secondary monitor](#Issues_with_PowerXpress_laptops_running_in_AMD_mode_.28pxp_switch_catalyst_amd.29_with_external_.2F_secondary_monitor)
*   [3 Xorg repositories](#Xorg_repositories)
    *   [3.1 xorg117](#xorg117)
    *   [3.2 xorg116](#xorg116)
    *   [3.3 xorg115](#xorg115)
    *   [3.4 xorg114](#xorg114)
    *   [3.5 xorg113](#xorg113)
    *   [3.6 xorg112](#xorg112)
*   [4 Tools](#Tools)
    *   [4.1 Catalyst-hook](#Catalyst-hook)
    *   [4.2 Catalyst-generator](#Catalyst-generator)
    *   [4.3 OpenCL and OpenGL development](#OpenCL_and_OpenGL_development)
        *   [4.3.1 amdapp-aparapi](#amdapp-aparapi)
        *   [4.3.2 amdapp-sdk (formerly known as amdstream)](#amdapp-sdk_.28formerly_known_as_amdstream.29)
        *   [4.3.3 amdapp-codexl](#amdapp-codexl)
*   [5 Features](#Features)
    *   [5.1 Tear Free Rendering](#Tear_Free_Rendering)
    *   [5.2 Video acceleration](#Video_acceleration)
    *   [5.3 GPU/Mem frequency, Temperature, Fan speed, Overclocking utilities](#GPU.2FMem_frequency.2C_Temperature.2C_Fan_speed.2C_Overclocking_utilities)
    *   [5.4 Double Screen (Dual Head / Dual Screen / Xinerama)](#Double_Screen_.28Dual_Head_.2F_Dual_Screen_.2F_Xinerama.29)
        *   [5.4.1 Introduction](#Introduction)
        *   [5.4.2 ATI Catalyst Control Center](#ATI_Catalyst_Control_Center)
        *   [5.4.3 Installation](#Installation_2)
        *   [5.4.4 Configuration](#Configuration)
*   [6 Uninstallation](#Uninstallation)
*   [7 Troubleshooting](#Troubleshooting)
    *   [7.1 Failed to start atieventsd.service](#Failed_to_start_atieventsd.service)
    *   [7.2 Failed to open fglrx_dri.so](#Failed_to_open_fglrx_dri.so)
    *   [7.3 GDM fails to start](#GDM_fails_to_start)
    *   [7.4 3D Wine applications freeze](#3D_Wine_applications_freeze)
        *   [7.4.1 TLS](#TLS)
        *   [7.4.2 Compiz](#Compiz)
    *   [7.5 Problems with video colours](#Problems_with_video_colours)
    *   [7.6 KWin and composite](#KWin_and_composite)
    *   [7.7 Black screen with complete lockups and/or hangs after reboot or startx](#Black_screen_with_complete_lockups_and.2For_hangs_after_reboot_or_startx)
        *   [7.7.1 Faulty ACPI hardware calls](#Faulty_ACPI_hardware_calls)
    *   [7.8 KDM disappears after logout](#KDM_disappears_after_logout)
    *   [7.9 Hibernate/Sleep issues](#Hibernate.2FSleep_issues)
        *   [7.9.1 Video fails to resume from suspend2ram](#Video_fails_to_resume_from_suspend2ram)
    *   [7.10 System freezes/Hard locks](#System_freezes.2FHard_locks)
    *   [7.11 Hardware conflicts](#Hardware_conflicts)
    *   [7.12 Temporary hangs when playing video](#Temporary_hangs_when_playing_video)
    *   [7.13 "aticonfig: No supported adapters detected"](#.22aticonfig:_No_supported_adapters_detected.22)
    *   [7.14 WebGL support in Chromium](#WebGL_support_in_Chromium)
    *   [7.15 Lag/freezes when watching flash videos via Adobe's flashplugin](#Lag.2Ffreezes_when_watching_flash_videos_via_Adobe.27s_flashplugin)
    *   [7.16 Lag/slow windows movement in GNOME3](#Lag.2Fslow_windows_movement_in_GNOME3)
    *   [7.17 Not using full screen resolution at 1920x1080 (underscanning, black borders around the screen)](#Not_using_full_screen_resolution_at_1920x1080_.28underscanning.2C_black_borders_around_the_screen.29)
    *   [7.18 Dual Screen Setup: general problems with acceleration, OpenGL, compositing, performance](#Dual_Screen_Setup:_general_problems_with_acceleration.2C_OpenGL.2C_compositing.2C_performance)
    *   [7.19 Disabling VariBright feature](#Disabling_VariBright_feature)
    *   [7.20 Hybrid/PowerXpress: turning off discrete GPU](#Hybrid.2FPowerXpress:_turning_off_discrete_GPU)
    *   [7.21 Switching from X session to TTYs gives a blank screen/low resolution TTY](#Switching_from_X_session_to_TTYs_gives_a_blank_screen.2Flow_resolution_TTY)
    *   [7.22 Switching from X session to TTYs gives a black screen with the monitor backlight on](#Switching_from_X_session_to_TTYs_gives_a_black_screen_with_the_monitor_backlight_on)
    *   [7.23 Switching to TTYs then back to X session gives a black screen with a mouse cursor](#Switching_to_TTYs_then_back_to_X_session_gives_a_black_screen_with_a_mouse_cursor)
    *   [7.24 30 FPS / Tear-Free / V-Sync bug](#30_FPS_.2F_Tear-Free_.2F_V-Sync_bug)
    *   [7.25 Backlight adjustment does not work](#Backlight_adjustment_does_not_work)
    *   [7.26 Chromium glitching when using plasma](#Chromium_glitching_when_using_plasma)
    *   [7.27 Xorg crashes](#Xorg_crashes)
        *   [7.27.1 Unsupported Xorg Version](#Unsupported_Xorg_Version)
*   [8 See also](#See_also)

## Selecting the right driver

Depending on the card you have, find the right driver in [Xorg#AMD](/index.php/Xorg#AMD "Xorg"). This page has instructions for **Catalyst** and **Catalyst legacy**.

## Installation

There are three ways of installing Catalyst on your system. One way is to use [Vi0L0's](https://aur.archlinux.org/account/Vi0l0/) (Arch's unofficial Catalyst maintainer) repository. This repository contains all the necessary packages. The second method you can use is the AUR; PKGBUILDs offered here are also made by Vi0L0 and are the same he uses to built packages for his repository. Lastly, you can install the driver directly from AMD.

Before choosing the method you prefer, you will have to see which driver you need. For Radeon HD 5xxx to Rx 300, there is the regular Catalyst driver. The Radeon HD 2xxx, 3xxx and 4xxx cards need the **legacy** Catalyst driver. Regardless of the driver you need, you will also need the Catalyst utilities.

**Note:** After the instructions for every method of installing, you will find general instructions **everyone** has to perform, regardless of the method you used.

### Installing the driver

#### Installing from the unofficial repository

If you do not fancy building the packages from the [AUR](/index.php/AUR "AUR"), this is the way to go. The repository is maintained by our unofficial Catalyst maintainer, [Vi0l0](/index.php/User:Vi0L0 "User:Vi0L0"). All packages are signed and are considered safe to use. As you will see later on in this article, Vi0L0 is also responsible for many other packages that will help you get your system working with your ATI graphic cards.

Vi0L0 has three different Catalyst repositories, each having different drivers:

*   [catalyst](/index.php/Unofficial_user_repositories#catalyst "Unofficial user repositories") for the regular Catalyst driver needed by Radeon HD 5xxx to Rx 300, it contains the latest beta release (Catalyst 15.12).
*   *catalyst-stable* for the regular Catalyst driver needed by Radeon HD 5xxx to Rx 300, with the latest stable release (Catalyst 15.9).
*   [catalyst-hd234k](/index.php/Unofficial_user_repositories#catalyst-hd234k "Unofficial user repositories") for the legacy Catalyst driver needed by Radeon HD 2xxx, 3xxx and 4xxx cards (Catalyst 12.4).

To enable one of these, follow the instructions in [Unofficial user repositories](/index.php/Unofficial_user_repositories "Unofficial user repositories"). Remember to add the chosen repository **above all other repositories** in `pacman.conf`.

**Note:** The *catalyst* and *catalyst-stable* repositories share the same URL. To enable *catalyst-stable*, follow the instructions for enabling *catalyst* and replace `[catalyst]` with `[catalyst-stable]` in `pacman.conf`. If you need to stick with an old version, there are also some versioned repositories using the same URL (for example *catalyst-stable-13.4*).

Once you have added some Catalyst repository, update pacman's database and [install](/index.php/Install "Install") these packages (see [#Tools](#Tools) for more information):

*   *catalyst-hook*
*   *catalyst-utils*
*   *catalyst-libgl*
*   *opencl-catalyst* - optional, needed for OpenCL support
*   *lib32-catalyst-utils* - optional, needed for 32-bit OpenGL support on 64-bit systems
*   *lib32-catalyst-libgl* - optional, needed for 32-bit OpenGL support on 64-bit systems
*   *lib32-opencl-catalyst* - optional, needed for 32-bit OpenCL support on 64-bit systems

**Note:** If pacman asks you about removing **libgl** you can safely do so.

**Warning:** catalyst package was removed from Vi0L0's repository, its place was taken by catalyst-hook.

#### Installing from the AUR

The second way to install Catalyst is from the [AUR](/index.php/AUR "AUR"). If you want to build the packages specifically for your computer, this is the way to go. Note that this is also the most tedious way to install Catalyst; it requires the most work and also requires manual updates upon every kernel update.

**Warning:** If you install the Catalyst package from the AUR, you will have to rebuild Catalyst every time the kernel is updated. Otherwise X **will** fail to start.

All packages mentioned above in Vi0L0's unofficial repository are also available on the [AUR](/index.php/AUR "AUR"):

*   [catalyst](https://aur.archlinux.org/packages/catalyst/)
*   [catalyst-generator](https://aur.archlinux.org/packages/catalyst-generator/)
*   [catalyst-hook](https://aur.archlinux.org/packages/catalyst-hook/)
*   [catalyst-utils](https://aur.archlinux.org/packages/catalyst-utils/)
*   [lib32-catalyst-utils](https://aur.archlinux.org/packages/lib32-catalyst-utils/)

The AUR also holds some packages that are **not** found in any of the repositories. These packages contain the so-called *Catalyst-total* packages and the beta versions:

*   [catalyst-total](https://aur.archlinux.org/packages/catalyst-total/)
*   [catalyst-total-hd234k](https://aur.archlinux.org/packages/catalyst-total-hd234k/)
*   [catalyst-test](https://aur.archlinux.org/packages/catalyst-test/)

The [catalyst-total](https://aur.archlinux.org/packages/catalyst-total/) packages are made to make the lives of AUR users easier. It builds the driver, the kernel utilities and the 32 bit kernel utilities. It also builds the [catalyst-hook](https://aur.archlinux.org/packages/catalyst-hook/) package, which is described in [#Tools](#Tools).

### Configuring the driver

After you have installed the driver via your chosen method, you will have to configure X to work with Catalyst. Also, you will have to make sure the module gets loaded at boot. Also, one should disable [kernel mode setting](/index.php/Kernel_mode_setting "Kernel mode setting").

#### Configuring X

To configure X, you will have to create an `xorg.conf` file. Catalyst provides its own `aticonfig` tool to create and/or modify this file. It also can configure virtually every aspect of the card for it also accesses the `/etc/ati/amdpcsdb` file. For a complete list of `aticonfig` options, run:

```
# aticonfig --help | less

```

**Warning:** Use the `--output` option before committing to `/etc/X11/` as an `xorg.conf` file will override anything in `/etc/X11/xorg.conf.d/`

**Note:** To adhere to the new config location use `# aticonfig [...] --output` to adapt the `Device` section to `/etc/X11/xorg.conf.d/20-radeon.conf`. The drawback is that many `aticonfig` options rely on an `xorg.conf`, and will be unavailable.

Now, to configure Catalyst. If you have only one monitor, run this:

```
# aticonfig --initial

```

However, if you have two monitors and want to use both of them, you can run the command stated below. Note that this will generate a dual head configuration with the second screen located above the first screen.

```
# aticonfig --initial=dual-head --screen-layout=above

```

**Note:** See [#Double Screen (Dual Head / Dual Screen / Xinerama)](#Double_Screen_.28Dual_Head_.2F_Dual_Screen_.2F_Xinerama.29) for more information on setting up dual monitors.

You can compare the generated file to one of the [Sample Xorg.conf](/index.php/Xorg#Sample_configurations "Xorg") examples listed on the Xorg page.

Although the current Xorg versions auto-detect most options when started, you may want to specify some in case the defaults change between versions.

Here is an example (with notes) **for reference**. Entries with `#` should be required, add entries with `##` as needed:

 `/etc/X11/xorg.conf` 
```
Section "ServerLayout"
        Identifier     "Arch"
        Screen      0  "Screen0" 0 0          # 0's are necessary.
EndSection
Section "Module"
        Load [...]
        [...]
EndSection
Section "Monitor"
        Identifier   "Monitor0"
        [...]
EndSection
Section "Device"
        Identifier  "Card0"
        Driver      "fglrx"                         # Essential.
        BusID       "PCI:1:0:0"                     # Recommended if autodetect fails.
        Option      "OpenGLOverlay" "0"             ##
        Option      "XAANoOffscreenPixmaps" "false" ##
EndSection
Section "Screen"
        Identifier "Screen0"
        Device     "Card0"
        Monitor    "Monitor0"
        DefaultDepth    24
        SubSection "Display"
                Viewport   0 0
                Depth     24                        # Should not change from '24'
                Modes "1280x1024" "2048x1536"       ## 1st value=default resolution, 2nd=maximum.
                Virtual 1664 1200                   ## (x+64, y) to workaround potential OGL rect. artifacts/
        EndSubSection                               ## fixed in Catalyst 9.8
EndSection
Section "DRI"
        Mode 0666                                   # May help enable direct rendering.
EndSection
```

**Note:** With **every** Catalyst update you should remove `amdpcsdb` file in this way: kill X, remove `/etc/ati/amdpcsdb`, start X and then run `amdcccle` - otherwise the version of Catalyst may display wrongly in `amdcccle`.

*If you need more information on Catalyst, visit [this thread](https://bbs.archlinux.org/viewtopic.php?id=57084).*

#### Loading the module at boot

We have to blacklist the `radeon` module to prevent it from auto-loading. To do so, blacklist *radeon* in `/etc/modprobe.d/modprobe.conf`. Also, make sure that it is not loaded by any file under `/etc/modules-load.d/`. For more information, see [kernel modules#Blacklisting](/index.php/Kernel_modules#Blacklisting "Kernel modules").

Then we will have to make sure that the `fglrx` module gets auto-loaded. Either add `fglrx` on a new line of an existing module file located under `/etc/modules-load.d/`, or create a new file and add `fglrx`.

#### Disable kernel mode setting

**Note:** Do not do this if you are using powerXpress technology (or hybrid AMD-Intel graphics) because Intel driver needs it.

Disabling kernel mode setting is important, as the Catalyst driver does not take advantage of [KMS](/index.php/KMS "KMS"). If you do not deactivate KMS, your system might freeze when trying to switch to a TTY or even when shutting down via your DE.

To disable kernel mode setting, add `nomodeset` to your [kernel parameters](/index.php/Kernel_parameters "Kernel parameters").

#### Checking operation

Assuming that a reboot to your login was successful, you can check if `fglrx` is running properly with the following commands:

```
$ lsmod | grep fglrx

```

If you get output, it works. Finally, run X manually with `$ startx` or by using a display manager (see [Xorg#Running](/index.php/Xorg#Running "Xorg")).

The following command should output your graphic card model name:

```
$ fglrxinfo

```

You can then verify that direct rendering is enabled by running the following command in a terminal:

```
$ glxinfo | grep "direct rendering"

```

If it says `"direct rendering: yes"` then you are good to go! If the `$ glxinfo` command is not found install the [mesa-demos](https://www.archlinux.org/packages/?name=mesa-demos) package.

**Note:** You can also use:
```
$ fgl_glxgears

```

as the fglrx alternative test to `glxgears`.

**Warning:** In recent versions of Xorg, the paths of libs are changed. So, sometimes `libGL.so` cannot be correctly loaded even if it is installed. Check this if your GL is not working. Please read [#Troubleshooting](#Troubleshooting) section for details.

### Custom kernels

**Note:** If you are at all uncomfortable or inexperienced with making packages, read up the [ABS](/index.php/ABS "ABS") wiki page first so things go smoothly.

To install catalyst for a custom kernel, you will need to build your own `catalyst-$kernel` package:

1.  Obtain the `PKGBUILD` and `catalyst.install` files from [Catalyst](/index.php/AUR "AUR").
2.  Editing the PKGBUILD. Two changes need to be made here:
    1.  Change `pkgname=catalyst` to `pkgname=catalyst-$kernel_name`, where `$kernel_name` is whatever you want (e.g. custom, mm, themostawesomekernelever).
    2.  Change the dependency of `linux` to `$kernel_name`.
3.  Build your package and install; run `makepkg -i` or `makepkg` followed by `# pacman -U pkgname.pkg.tar.gz`

**Note:**

*   If you run multiple kernels, you have to install the [catalyst-utils](https://aur.archlinux.org/packages/catalyst-utils/) packages for all kernels. They will not conflict with one another.
*   [catalyst-generator](https://aur.archlinux.org/packages/catalyst-generator/) is able to build `catalyst-{kernver}` packages for you so you do not actually need to perform all those steps manually. For more information, see [Tools section](#Tools).

### PowerXpress support

PowerXpress technology allows switching notebooks with dual-graphic capability from integrated graphics (IGP) to discrete graphics either to increase battery life or to achieve better 3D rendering capabilities.

To use such functionality on Arch you will have to:

*   Get and build [catalyst-total](https://aur.archlinux.org/packages/catalyst-total/) / [catalyst-test](https://aur.archlinux.org/packages/catalyst-test/) package from the [AUR](/index.php/AUR "AUR"), or
*   Install **catalyst-libgl** alongside with **catalyst-utils** packages from the [catalyst] repository.

To perform a switch into Intel's IGP you will also have to install the [mesa](https://www.archlinux.org/packages/?name=mesa) package and Intel's drivers: [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel).

**Note:** Catalyst sometimes has problems with newest intel drivers. If this is happening please downgrade [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) to the previous version found on [Arch Linux Archive](/index.php/Arch_Linux_Archive "Arch Linux Archive") or maybe even from archive [#Xorg repositories](#Xorg_repositories) alongside with xorg-server package(s).

Now you can switch between the integrated and the discrete GPU, using these commands:

```
# aticonfig --px-igpu    #for integrated GPU
# aticonfig --px-dgpu    #for discrete GPU
```

Just remember that fglrx needs `/etc/X11/xorg.conf` configured for AMD's card with `fglrx` inside.

You can also use the `pxp_switch_catalyst` switching script that will perform some additional usefull operations:

*   Switching `xorg.conf` - it will rename `xorg.conf` into `xorg.conf.cat` (if there is fglrx inside) or `xorg.conf.oth` (if there is intel inside) and then it will create a symlink to `xorg.conf`, depending on what you chose.
*   Running `aticonfig --px-Xgpu`.
*   Running `switchlibGL`.
*   Adding/removing `fglrx` into/from `/etc/modules-load.d/catalyst.conf`.

Usage:

```
# pxp_switch_catalyst amd
# pxp_switch_catalyst intel
```

If you have got problems when you try to run X on Intel's driver you may try to force "UXA" acceleration. Just make sure you got `Option "AccelMethod" "uxa"` in `xorg.conf`:

 `/etc/X11/xorg.conf` 
```
Section "Device"
        Identifier  "Intel Graphics"
        Driver      "intel"
        #Option      "AccelMethod"  "sna"
        **Option      "AccelMethod"  "uxa"**
        #Option      "AccelMethod"  "xaa"
EndSection
```

#### Running two X servers (one using the Intel driver, another one using fglrx) simultaneously

Because fglrx is crash-prone (regarding PowerXpress), it could be a good idea to use the Intel driver in the main X server and have a secondary X server using fglrx when 3D acceleration is needed. However, simply switching to the discrete GPU from the integrated GPU using `aticonfig` or `amdcccle` will cause all sorts of weird bugs when starting the second X.

To run two X servers at the same time (each using different drivers), you should firstly set up a fully working X with Catalyst and then move its `xorg.conf` to a temporary place (for example, `/etc/X11/xorg.conf.fglrx`. The next time X is started, it will use the Intel driver by default instead of fglrx.

To start a second X server using fglrx, simply move `xorg.conf` back to the proper place (`/etc/X11/xorg.conf`) before starting X. This method even allows you to switch between running X sessions. When you are done using fglrx, move `xorg.conf` somewhere else again.

The only disadvantage of this method is not having 3D acceleration using the Intel driver. 2D acceleration, however, is fully functional. Other than that, this will provide us with a completely stable desktop.

#### Issues with PowerXpress laptops running in AMD mode (pxp_switch_catalyst amd) with external / secondary monitor

When using a PowerXpress laptop in AMD-only mode (ie, setting the discrete card to render everything) you sometimes run into issues with artifacting/duplicating between displays. This is a known issue, and seems to effect 7xxxM series cards.

The artifacting disappears when you transform one of the monitors by either rotating or scaling. So you can use xrandr to fix this:

 `xrandr --output HDMI1 --left-of LVDS1 --primary --scale 1x1 --output LVDS1 --scale 1.0001x1.0001` 

## Xorg repositories

Catalyst is notorious for its slow update process. As such, it is common that a new Xorg version is pushed down from upstream that will break compatibility for Catalyst. This means that Catalyst users either have to build Xorg packages on their own, or use a backported repository that only contains the Xorg packages that should be held back. Vi0L0 has stepped in to fulfil this task and provides several backported repositories.

To enable one of these, follow the instructions in [Unofficial user repositories](/index.php/Unofficial_user_repositories "Unofficial user repositories") (use the same PGP key as for the [catalyst](/index.php/Unofficial_user_repositories#catalyst "Unofficial user repositories") repository). Remember to add the chosen repository **above all other repositories** in `pacman.conf`, even above your *catalyst* repository, should you use one.

### xorg117

Catalyst does not support xorg-server 1.18

```
[xorg117]
Server = http://mirror.hactar.xyz/Vi0L0/xorg117/$arch

```

### xorg116

Catalyst < 15.7 does not support xorg-server 1.17

```
[xorg116]
Server = http://mirror.hactar.xyz/Vi0L0/xorg116/$arch

```

### xorg115

Catalyst < 14.9 does not support xorg-server 1.16

```
[xorg115]
Server = http://mirror.hactar.xyz/Vi0L0/xorg115/$arch

```

### xorg114

Catalyst < 14.1 does not support xorg-server 1.15.

```
[xorg114]
Server = http://mirror.hactar.xyz/Vi0L0/xorg114/$arch

```

### xorg113

Catalyst < 13.6 does not support xorg-server 1.14.

```
[xorg113]
Server = http://mirror.hactar.xyz/Vi0L0/xorg113/$arch

```

### xorg112

Catalyst < 12.10 and Catalyst Legacy do not support xorg-server 1.13.

```
[xorg112]
Server = http://mirror.hactar.xyz/Vi0L0/xorg112/$arch

```

## Tools

### Catalyst-hook

[Catalyst-hook](https://aur.archlinux.org/packages/Catalyst-hook/) is a [systemd](/index.php/Systemd "Systemd") service that will automatically rebuild the `fglrx` modules while the system shuts down or reboots, but only if it is necessary (e.g. after an update).

Before using this package make sure that both the [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/) group and the [linux-headers](https://www.archlinux.org/packages/?name=linux-headers) package (the one specific to the kernel you use) are installed.

To enable the automatic update, enable the `catalyst-hook.service`:

```
# systemctl enable catalyst-hook
# systemctl start catalyst-hook

```

You can also use this package to build the `fglrx` module manually. Simply run the `catalyst_build_module` script after the kernel has been updated:

```
# catalyst_build_module all

```

**A few more technical details:**

The `catalyst-hook.service` is stopping the systemd "river" and is forcing systemd to wait until catalyst-hook finishes its job.

The `catalyst-hook.service` is calling the `catalyst_build_module check` function which checks if fglrx rebuilds are really necessary.

The `check` function is checking if the `fglrx` module exists, if it:

*   does not exist, it will build it;

*   does exist, it will compare the two values to be sure that a rebuild is necessary.

These values are md5sums of the `/usr/lib/modules/<kernel_version>/build/Module.symvers` file (because I, Vi0L0, noticed that this file is unique and different for every kernel's release). The first value is the md5sum of the existing `Module.symvers` file. The second value is the md5sum of the `Module.symvers` file which existed in a moment of the `fglrx` module creation. This value was compiled into the `fglrx` module by a `catalyst_build_module` script.

If the values are different, it will compile the new `fglrx` module.

The check is checking the whole `/usr/lib/modules/` directory and building modules for all of the installed kernels if it is necessary. If the build or rebuild is not necessary, the whole process takes only some milliseconds to complete before it gets killed by systemd.

### Catalyst-generator

[catalyst-generator](https://aur.archlinux.org/packages/catalyst-generator/) is a package that is able to build and install the `fglrx` module packed into pacman compliant `catalyst-${kernver}` packages. The basic difference from [#Catalyst-hook](#Catalyst-hook) is that you will have to trigger this command manually, whereas Catalyst-hook will do this automatically at boot when a new kernel got installed.

It creates `catalyst-${kernver}` packages using [makepkg](/index.php/Makepkg "Makepkg") and installs them with [pacman](/index.php/Pacman "Pacman"). `${kernver}` is the kernel version for which each package was built (e.g. catalyst-2.6.35-ARCH package was built for 2.6.35-ARCH kernel).

To build and install `catalyst-${kernver}` package for a currently booted kernel as an unprivileged user (non-root; safer way), use `catalyst_build_module`. You will be asked for your root password to proceed to package installation.

A short summary on how to use this package:

1.  As root: `catalyst_build_module remove`. This will remove all unused `catalyst-{kernver}` packages.
2.  As unprivileged user: `catalyst_build_module ${kernver}`, where `${kernver}` is the version of the kernel to which you just updated. For example: `catalyst_build_module 2.6.36-ARCH`. You can also build `catalyst-{kernver}` for all installed kernels by using `catalyst_build_module all`.
3.  If you want to remove `catalyst-generator`, it is best to run this as root before removing catalyst-generator: `catalyst_build_module remove_all`. **This will remove all `catalyst-{kernver}` packages from the system.**

`Catalyst-generator` is not able to remove all those `catalyst-{kernver}` packages automatically while being removed because there can not be more than one instance of pacman running. If you forget to run `# catalyst_build_module remove_all` before using `# pacman -R catalyst-generator` catalyst-generator will tell you which `catalyst-{kernver}` packages you will have to remove manually after removing catalyst-generator itself.

Catalyst-generator is most safe and KISS-friendly solution because:

1.  you can use unprivileged user to build the package;
2.  it is building modules in a fakeroot environment;
3.  it is not throwing files here and there, [pacman](/index.php/Pacman "Pacman") always knows where they are;
4.  all you have to do is to remember to use it

**Note:** If you see those warnings:
```
**WARNING:** Package contains reference to $srcdir

```

```
**WARNING:** '.pkg' is not a valid archive extension.

```
while building `catalyst-{kernver}` package, do not be concerned, it is normal.

### OpenCL and OpenGL development

Since years AMD is working on tools for OpenCL and OpenGL developement.

Now under the banner of **"Heterogeneous Computing"** AMD is providing even more of them, fortunately most of their computing tools are available also for Linux.

In the AUR and the [catalyst] repositories you will find packages that represent the most important work from AMD, namely:

*   [amdapp-aparapi](https://aur.archlinux.org/packages/amdapp-aparapi/)
*   [amdapp-sdk](https://aur.archlinux.org/packages/amdapp-sdk/)
*   [amdapp-codexl](https://aur.archlinux.org/packages/amdapp-codexl/)

APP shortcut stands for Accelerated Parallel Processing.

#### amdapp-aparapi

AMD's Aparapi is an API for expressing data parallel workloads in Java and a runtime component capable of converting the Java bytecode of compatible workloads into OpenCL so that it can be executed on a variety of GPU devices. If Aparapi can’t execute on the GPU, it will execute in a Java thread pool.

You can find more information about Aparapi [here](http://developer.amd.com/tools/heterogeneous-computing/aparapi/).

#### amdapp-sdk (formerly known as amdstream)

The AMD APP Software Development Kit (SDK) is a complete development platform created by AMD to allow you to quickly and easily develop applications accelerated by AMD APP technology. The SDK provides samples, documentation and other materials to quickly get you started leveraging accelerated compute using OpenCL, Bolt, or C++ AMP in your C/C++ application.

Since version 2.8 amdapp-sdk is providing aparapiUtil as well as aparapi's samples. A package is available on the [catalyst] repository; it depends on the [amdapp-aparapi](https://aur.archlinux.org/packages/amdapp-aparapi/) package. The AUR's package will let you decide whether you want aparapi's additions or not.

Version 2.8 does not provide Profiler functionality, it has been moved to CodeXL.

You can find more information about AMD APP SDK [here](https://developer.amd.com/amd-accelerated-parallel-processing-app-sdk/).

#### amdapp-codexl

CodeXL is an OpenCL and OpenGL Debugger and Profiler, with a static OpenCL kernel analyzer. It is a GUI application written atop of the well known gdebugger.

## Features

### Tear Free Rendering

Presented in **Catalyst 11.1**, the *Tear Free Desktop* feature reduces tearing in 2D, 3D and video applications. This likely adds triple-buffering and v-sync. Do note that it requires additional GPU processing.

To enable 'Tear Free Desktop' run `amdcccle` and go to: `Display Options` → `Tear Free`.

Or run:

```
# aticonfig --set-pcs-u32=DDX,EnableTearFreeDesktop,1

```

To disable, again use `amdcccle` or run:

```
# aticonfig --del-pcs-key=DDX,EnableTearFreeDesktop

```

### Video acceleration

Catalyst supports [hardware video acceleration](/index.php/Hardware_video_acceleration "Hardware video acceleration") via VA-API. Applications can take advantage of AMD Radeons UVD2 chipsets via AMD's [X-Video Bitstream Acceleration (XvBA)](https://en.wikipedia.org/wiki/X-Video_Bitstream_Acceleration "wikipedia:X-Video Bitstream Acceleration") library. There is no need to manually install it as it is included in the [catalyst-test](https://aur.archlinux.org/packages/catalyst-test/), [catalyst-total](https://aur.archlinux.org/packages/catalyst-total/) and [catalyst-utils](https://aur.archlinux.org/packages/catalyst-utils/) packages.

For **mplayer**: Install [mplayer-vaapi](https://aur.archlinux.org/packages/mplayer-vaapi/) and [libva](https://www.archlinux.org/packages/?name=libva). Then just set your video player to use `vaapi:gl` as video output:

```
$ mplayer -vo vaapi:gl movie.avi

```

These options can be added to your mplayer configuration file, see [MPlayer](/index.php/MPlayer "MPlayer").

For **smplayer**:

```
Options → Preferences → General → Video (tab) → Output driver: User Defined : vaapi:gl
Options → Preferences → General → Video (tab) → Double buffering **on**
Options → Preferences → General → General → Screenshots → Turn screenshots **off**
Options → Preferences → Performance → Threads for decoding: **1** (to turn off -lavdopts parameter)

```

**Note:** If Tear Free Desktop is enabled it is better to use:
```
Options → Preferences → General → Video (tab) → Output driver: vaapi

```

If Video Output **vaapi:gl** is not working - please check:

```
**vaapi**, **vaapi:gl2** or simply **xv(0 - AMD Radeon [AVIVO Video](https://en.wikipedia.org/wiki/Avivo "wikipedia:Avivo"))**.

```

For **VLC**:

```
Tools → Preferences → Input & Codecs → Use GPU accelerated decoding

```

It might help to enable v-sync in **amdcccle**:

```
3D → More Settings → Wait for vertical refresh = Always On

```

**Note:** If you are using **Compiz/KWin**, the only way to **avoid video flickering** is to watch videos in **full-screen** and only when **Unredirect Fullscreen is off**. In **compiz** you need to set **Redirected Direct Rendering** in General Options of ccsm. If it is still flickering, try to disable this option in CCSM. It is off by default in **KWin**, but if you see flickering try to turn "Suspend desktop effects for fullscreen windows" on or off in `System Settings` → `Desktop Effects` → `Advanced`.

### GPU/Mem frequency, Temperature, Fan speed, Overclocking utilities

You can get the GPU/Mem clocks with: `$ aticonfig --od-getclocks`.

You can get the fan speed with: `$ aticonfig --pplib-cmd "get fanspeed 0"`

You can get the temperature with: `$ aticonfig --odgt`

To set the fanspeed with: `$ aticonfig --pplib-cmd "set fanspeed 0 50"` Query Index: 50, Speed in percent

To overclock and/or underclock it is easier to use a GUI, like **ATi Overclocking Utility**, which is very simple and requires qt to work. It might be out of date/old, but you can get it [here](http://kde-apps.org/content/show.php/ATI+Overclock?content=47796).

Another, more complex utility to perform such operations is **AMDOverdriveCtrl**. Its homepage is [here](http://sourceforge.net/projects/amdovdrvctrl) and you can build [amdoverdrivectrl](https://aur.archlinux.org/packages/amdoverdrivectrl/) from the AUR or from Vi0L0's unofficial repositories.

### Double Screen (Dual Head / Dual Screen / Xinerama)

#### Introduction

**Warning:** you should know that there is not one specific solution because each setup differs and needs its own configuration. That is why you will have to adapt the steps below to your own needs. It is possible that you have to try more than once. Therefore, you should save your working `/etc/X11/xorg.conf` **before** you start modifying and be able to recover from a command-line environment.

*   In this chapter, we will describe the installation of two different-sized screens on only one graphics card with two different output ports (DVI + HDMI) using a "BIG Desktop" configuration.

*   The Xinerama solution has some inconveniences, especially because it is not compatible with XrandR. For that very reason, you should not use this solution, because XrandR is a must for our later configuration.

*   The Dual Head solution would allow you to have 2 different sessions (one for each screen). It could be what you want, but you will not be able to move windows from one screen to another. If you have only one screen, you will have to define the mouse inside your Xorg session for each of the two sessions inside the Server Layout section.

[ATI Documentation](http://support.amd.com/us/kbarticles/Pages/1105-HowCanIConfigureMultip.aspx)

#### ATI Catalyst Control Center

The GUI tool shipped by ATI is very useful and we will try to use it as much as we can. To launch it, open a terminal and use the following command:

```
$ {kdesu/gksu} amdcccle

```

**Warning:** Do **not** use sudo directly with a GUI. Sudo gives you admin rights with user account information. Instead, use *gksu* (GNOME) or *kdesu* (KDE).

#### Installation

Before we start, make sure that your hardware is plugged in correctly, that power is on and that you know your hardware characteristics (screen dimensions, sizes, refreshment rates, etc.) Normally, both screens are recognized during boot time but not necessarily identified properly, especially if you are not using any Xorg base configuration file (`/etc/X11/xorg.conf`) but relying on the hot-plugging feature.

The first step is to make sure that you screens will be recognized by your DE and by X. For this, you need to generate a basic Xorg configuration file for your two screens:

```
# aticonfig --initial --desktop-setup=horizontal --overlay-on=1

```

or

```
# aticonfig --initial=dual-head --screen-layout=left

```

**Note:** `overlay` is important because it allows you to have 1 pixel (or more) shared between the 2 screens.

**Tip:** For the other possible and available options, do not hesitate to type `aticonfig --help` inside a terminal to display all available command lines.

Now you should have a basic Xorg configuration file that you can edit to add your screen resolutions. It is important to use the precise resolution, especially if you have screens of different sizes. These resolutions have to be added in the "Screen" section:

```
SubSection "Display"
    Depth     24
    Modes     "X-resolution screen 1xY-resolution screen 1" "Xresolution screen 2xY-resolution screen 2"
EndSubSection

```

From now on, instead of editing the `xorg.conf` file manually, let us use the ATI GUI tool. Restart X to be sure that your two screens are properly supported and that the resolutions are properly recognized (Screens must be independent, not mirrored).

#### Configuration

Now you will only have to launch the ATI control center with root privileges, go to the display menu and choose how you would like to set your configuration (small arrow of the drop down menu). A last restart of X and you should be done!

Before you restart X, do not hesitate to verify your new `xorg.conf` file. At this stage, inside the "Display" sub-section of the "Screen" section, you should see a "Virtual" command line, of which the resolution should be the sum of both screens. The "Server Layout" section says all the rest.

## Uninstallation

If for any reason this driver is not working for you or if you simply want to try out the open source driver, remove the `catalyst` and `catalyst-utils` packages. Also you should remove [catalyst-generator](https://aur.archlinux.org/packages/catalyst-generator/), [catalyst-hook](https://aur.archlinux.org/packages/catalyst-hook/) and [lib32-catalyst-utils](https://aur.archlinux.org/packages/lib32-catalyst-utils/) packages if they have been installed on your system.

**Warning:**

*   You may need to use `# pacman -Rdd` to remove [catalyst-utils](https://aur.archlinux.org/packages/catalyst-utils/) (and/or [lib32-catalyst-utils](https://aur.archlinux.org/packages/lib32-catalyst-utils/)) because that package contains *gl* related files and many of your installed packages depend on them. These dependencies will be satisfied again when you install [xf86-video-ati](https://www.archlinux.org/packages/?name=xf86-video-ati).
*   You may need to remove `/etc/profile.d/ati-flgrx.sh` and `/etc/profile.d/lib32-catalyst` (if it exists on your system), otherwise `r600_dri.so` will fail to load and you would not have 3D support.

**Note:** You should remove unofficial repositories from your `/etc/pacman.conf` and run `# pacman -Syu`, because those repositories include out-dated Xorg packages to allow use of `catalyst` and the [xf86-video-ati](https://www.archlinux.org/packages/?name=xf86-video-ati) package needs up-to-date Xorg packages from the [Official repositories](/index.php/Official_repositories "Official repositories").

Also follow these steps:

*   If you have the `/etc/modprobe.d/blacklist-radeon.conf` file remove it or comment the line `blacklist radeon` in that file.
*   If you have a file in `/etc/modules-load.d` to load the `fglrx` module on boot, remove it or comment the line containing `fglrx`.
*   Make sure to remove or backup `/etc/X11/xorg.conf`.
*   If you have installed the [catalyst-hook](https://aur.archlinux.org/packages/catalyst-hook/) package, make sure to disable the systemd service.
*   If you used the `nomodeset` option in your [kernel parameters](/index.php/Kernel_parameters "Kernel parameters") and plan to use KMS, remove it.
*   **Reboot** before installing another driver.

## Troubleshooting

If you can still boot to command-line, then the problem probably lies in `/etc/X11/xorg.conf`

You can parse the whole `/var/log/Xorg.0.log` or, for clues:

```
$ grep '(EE)' /var/log/Xorg.0.log
$ grep '(WW)' /var/log/Xorg.0.log

```

If you are still confused about what is going on, search the forums first. Then post a message in the [thread specific to ATI/AMD](https://bbs.archlinux.org/viewtopic.php?pid=1166052#p1166052/). Provide the information from `xorg.conf` and both commands mentioned above.

### Failed to start atieventsd.service

Install [acpid](https://www.archlinux.org/packages/?name=acpid) from the [official repositories](/index.php/Official_repositories "Official repositories"). Start and enable the acpid [service](/index.php/Daemon "Daemon").

If the service still fails to start, edit `/usr/lib/systemd/system/atieventsd.service` and change `acpid.socket` to `acpid.service`.

### Failed to open fglrx_dri.so

Create a symlink from `/usr/lib/xorg/modules/dri/fglrx_dri.so` to `/usr/X11R6/lib64/modules/dri/fglrx_dri.so` (or other requested path)

```
# mkdir -p /usr/X11R6/lib64/modules/dri
# ln -s /usr/lib/xorg/modules/dri/fglrx_dri.so /usr/X11R6/lib64/modules/dri/fglrx_dri.so

```

### GDM fails to start

Downgrade the [xorg-server](https://www.archlinux.org/packages/?name=xorg-server) package or try to use another [display manager](/index.php/Display_manager "Display manager") like [LightDM](/index.php/LightDM "LightDM").

### 3D Wine applications freeze

If you use a 3D Wine application and it hangs, watch out for the following workarounds.

#### TLS

One source of problems is TLS. To disable it, either use `aticonfig` or edit `/etc/X11/xorg.conf`. To use `aticonfig`:

```
# aticonfig --tls=off

```

Or, to edit `/etc/X11/xorg.conf`; first open the file in an editor as root and then add `Option "UseFastTLS" "off"` to the *Device* section of this file.

After applying either of the solutions, restart X for it to take effect.

#### Compiz

In case you are using compiz as the windows compositer, disable it. For instance, if you are using XFCE as your desktop environment, open a terminal and execute:

```
$ xfwm4 --replace &

```

### Problems with video colours

You may still use `vaapi:gl` to avoid video flickering, but without video acceleration:

*   Run **mplayer** without `-vo vaapi` switch.

*   Run **smplayer** remove `-vo vaapi` from Options → Preferences → Advanced → Options for MPlayer → Options: -vo vaapi

Plus for **smplayer** you may now safely turn screenshots on.

### KWin and composite

You may use XRender if the rendering with OpenGL is slow. However, XRender might also be slower than OpenGL depending on your card. XRender also solves artefact issues in some cases, for instance when resizing Konsole.

### Black screen with complete lockups and/or hangs after reboot or startx

Ensure you have added the `nomodeset` option to the kernel options line in your bootloader (see [#Disable kernel mode setting](#Disable_kernel_mode_setting)). Make sure that Catalyst is compatible with your installed Xorg version and used Linux kernel version.

If you are using the legacy driver (`catalyst-hd234k`) and get a black screen, try downgrading xorg-server to 1.12 by using the [#xorg112](#xorg112) repository.

#### Faulty ACPI hardware calls

It is possible that fglrx does not cooperate well with the system's ACPI hardware calls, so it auto-disables itself and there is no screen output.

If so, try to run this:

```
$ aticonfig --acpi-services=off

```

### KDM disappears after logout

If you are running Catalyst proprietary driver and you get a console (tty1) instead of the expected KDM greeting when you log out, you must instruct KDM to restart the X server after each logout. Uncomment the following line under the section titled `[X-:*-Core]`

 `/usr/share/config/kdm/kdmrc`  `TerminateServer=True` 

KDM should now appear when you log out of KDE.

### Hibernate/Sleep issues

#### Video fails to resume from suspend2ram

ATI's proprietary Catalyst driver cannot resume from suspend if the framebuffer is enabled. To disable the framebuffer, add `vga=0` to your kernel [kernel parameters](/index.php/Kernel_parameters "Kernel parameters").

To see where you need to add this with other bootloaders, see [#Disable kernel mode setting](#Disable_kernel_mode_setting).

### System freezes/Hard locks

*   The `radeonfb` framebuffer drivers have been known in the past to cause problems of this nature. If your kernel has radeonfb support compiled in, you may want to try a different kernel and see if this helps.

*   If you experience system freezes when exiting your DE (shut down, suspend, switching to tty etc.) you probably forgot to deactivate KMS. (See [#Disable kernel mode setting](#Disable_kernel_mode_setting))

### Hardware conflicts

Radeon cards used in conjunction with some versions of the nForce3 chipset (e.g. nForce 3 250Gb) will not have 3D acceleration. Currently the cause of this issue is unknown, but some sources indicate that it may be possible to get acceleration with this combination of hardware by booting Windows with the drivers from nVIDIA and then rebooting the system. This can be verified by getting output something similar to this (using an nForce3-based system):

 `$ dmesg | grep agp` 
```
agpgart: Detected AGP bridge 0
agpgart: Setting up Nforce3 AGP.
agpgart: aperture base > 4G

```

and also if issuing the following command gets you the following output:

 `$ tail -n 100 /var/log/Xorg.0.log | grep agp`  `(EE) fglrx(0): [agp] unable to acquire AGP, error "xf86_ENODEV"` 

you have this bug.

Some sources indicate that in some situations, downgrading the motherboard BIOS may help, but this cannot be verified in all cases. Also, **a bad BIOS downgrade can render your hardware useless, so beware.**

See [this bugreport](http://bugzilla.kernel.org/show_bug.cgi?id=6350) for more information and a potential fix.

### Temporary hangs when playing video

This problem may occur when using the proprietary Catalyst.

If you experience temporary hangs lasting from a few seconds to several minutes occuring randomly during playback with mplayer, check the system logs for output like:

 `/var/log/messages.log` 
```
Nov 28 18:31:56 pandemonium [<c01c64a6>] ? proc_get_sb+0xc6/0x160
Nov 28 18:31:56 pandemonium [<c01c64a6>] ? proc_get_sb+0xc6/0x160
Nov 28 18:31:56 pandemonium [<f8bc628c>] ? ip_firegl_ioctl+0x1c/0x30 [fglrx]
Nov 28 18:31:56 pandemonium [<c01c64a6>] ? proc_get_sb+0xc6/0x160
Nov 28 18:31:56 pandemonium [<c0197038>] ? vfs_ioctl+0x78/0x90
Nov 28 18:31:56 pandemonium [<c01970b7>] ? do_vfs_ioctl+0x67/0x2f0
Nov 28 18:31:56 pandemonium [<c01973a6>] ? sys_ioctl+0x66/0x70
Nov 28 18:31:56 pandemonium [<c0103ef3>] ? sysenter_do_call+0x12/0x33
Nov 28 18:31:56 pandemonium [<c01c64a6>] ? proc_get_sb+0xc6/0x160
Nov 28 18:31:56 pandemonium =======================
```

Adding the `nopat` and/or `nomodeset` [kernel parameters](/index.php/Kernel_parameters "Kernel parameters") should work.

### "aticonfig: No supported adapters detected"

If you get the following:

 `# aticonfig --initial` 
```
aticonfig: No supported adapters detected

```

It may still be possible to get Catalyst working by manually setting the device in your your `etc/X11/xorg.conf` file or by copying an older working `/etc/ati/control` file (preferred - this also fixes the watermark issue).

To get an older control file, download a previous version of fglrx from AMD and run it with `--extract driver` parameter. You will find the control file in `driver/common/etc/ati/control`. Copy the extracted file over the system file and restart Xorg. You can try different versions of the file.

To set your model in `xorg.conf`, edit the device section of `/etc/X11/xorg.conf` to:

 `/etc/X11/xorg.conf` 
```
Section "Device"
        Identifier "ATI radeon ********"
        Driver     "fglrx"
EndSection

```

Where `****` should be replaced with your device's marketing number (e.g. 6870 for the HD 6870 and 6310 for the E-350 APU).

Xorg will start and it is possible to use `amdcccle` instead of `aticonfig`. There will be an "AMD Unsupported hardware" watermark.

You can remove this watermark using the following script:

```
#!/bin/sh
DRIVER=/usr/lib/xorg/modules/drivers/fglrx_drv.so
for x in $(objdump -d $DRIVER|awk '/call/&&/EnableLogo/{print "\\x"$2"\\x"$3"\\x"$4"\\x"$5"\\x"$6}'); do
   sed -i "s/$x/\x90\x90\x90\x90\x90/g" $DRIVER
done

```

and then reboot your machine.

### WebGL support in Chromium

Google has blacklisted Linux's Catalyst driver from supporting webGL in their Chromium/Chrome browsers. See [Chromium#WebGL](/index.php/Chromium#WebGL "Chromium") for details.

### Lag/freezes when watching flash videos via Adobe's flashplugin

Edit:

 `/etc/adobe/mms.cfg` 
```
#EnableLinuxHWVideoDecode=1
OverrideGPUValidation=true
```

If you are using KDE make sure that "Suspend desktop effects for fullscreen windows" is unchecked under `System Settings` → `Desktop Effects` → `Advanced`.

### Lag/slow windows movement in GNOME3

You can try this solution, it has been reported to work for many people.

Add this line into `~/.profile` or into `/etc/profile`:

```
export CLUTTER_VBLANK=none

```

Restart X server or reboot your system.

### Not using full screen resolution at 1920x1080 (underscanning, black borders around the screen)

This usually happens when you use a HDMI connection to connect your monitor/TV to your computer.

Seemed to be a feature by AMD/ATI to work with all HDTVs that could be adjusted via the amdccle.

Using the amdcccle GUI you can select the affected display, go to adjustments, and set underscan to 0% (aticonfig defaults to 15% underscan). It is possible as well that the underscan slider will not show under the display's adjustments, as sometimes in (at least) version 14.10.

The problem is that the settings will not persist after restarting X server or rebooting or wake up or might even revert after changing TTYs.

For the changes to become permanent, you will need to adjust the underscan settings manually using "aticonfig" via console (as root) or manually edit the file `/etc/ati/amdpcsdb` (as root)

**using aticonfig method:**

```
# aticonfig --set-pcs-u32=MCIL,DigitalHDTVDefaultUnderscan,0

```

After changing the settings, reboot.

For newer version (for example, 12.11), if Catalyst control center repeatedly fails to save the overscan setting you can also try:

```
# aticonfig --set-pcs-u32=MCIL,TVEnableOverscan,0

```

**Manually editing /etc/ati/amdpcsdb method:**

Add the following line anywhere under the following header `[AMDPCSROOT/SYSTEM/MCIL]`

```
# DigitalHDTVDefaultUnderscan=V0

```

For newer version (for example, 12.11), if Catalyst control center repeatedly fails to save the overscan setting you can also try: locate under `[AMDPCSROOT/SYSTEM/MCIL]` the following line

```
# TVEnableOverscan=V1

```

and change it to

```
# TVEnableOverscan=V0

```

After changing the settings, reboot.

**Note:** You might find that the file `/etc/ati/amdpcsdb` will be overwritten and revert no matter what you do as user or as root even with log in/log out/reboot, ergo the modification will not stick.

For the amd database file not to be overwritten you have to modify it without the fglrx driver running.

This can be made by rebooting in any "safe mode" that will not use the driver or directly booting into console mode

**Workaround:** For whatever reason you can find yourself not wanting to touch ATI's config files you can circumvent the problem by forcing the panel's position and resolution: as user:

```
# aticonfig --set-dispattrib=DISPLAYTYPE,positionX:0
# aticonfig --set-dispattrib=DISPLAYTYPE,positionY:0
# aticonfig --set-dispattrib=DISPLAYTYPE,sizeX:1920
# aticonfig --set-dispattrib=DISPLAYTYPE,sizeY:1080

```

`DISPLAYTYPE` will be the name of the monitor you want to change its attributes, for example "dfp9". To get the name of your `DISPLAYTYPE` run the following command:

```
# xrandr --current

```

Should RandR be not enabled use:

```
# aticonfig --query-monitor

```

Using the display switch or DISPLAY variable set to the appropriate display/screen (:0.1 for example) might be necessary.

That will show you which displays are connected and disconnected and its properties

This workaround will not persist but it is a quick fix that will show that the panel works just fine and that the above solutions are to be put into place.

**Note:** `aticonfig --set-pcs-val=MCIL,DigitalHDTVDefaultUnderscan,0` should not be used on newer versions of the driver as it is deprecated and will be soon removed as stated by ATI.

Try `aticonfig --help | grep set-pcs-val` to read ATI's notice

### Dual Screen Setup: general problems with acceleration, OpenGL, compositing, performance

Try to disable xinerama and xrandr12\. Check out ie. this way:

Type those commands:

```
# aticonfig --initial
# aticonfig --set-pcs-str="DDX,EnableRandR12,FALSE"

```

Then reboot your system. In `/etc/X11/xorg.conf` check that xinerama is disabled, if it is not, disable it and reboot your system.

Next run `amdcccle` and pick up amdcccle → display manager → multi-display → multidisplay desktop with display(s) 2.

Reboot again and set up your display layout whatever you desire.

### Disabling VariBright feature

[Vari-Bright](http://support.hp.com/vn-en/document/c02848104) is a feature designed to save power by dynamically adjusting how much power the display panel uses. Enter the following command to disable VariBright:

```
# aticonfig --set-pcs-u32=MCIL,PP_UserVariBrightEnable,0

```

### Hybrid/PowerXpress: turning off discrete GPU

When you are using packages with powerXpress support and you are switching to integrated GPU you may notice that discrete GPU is still working, consuming power and making your system's temperature higher.

Sometimes ie. when your integrated GPU is intel's one you can use `vgaswitcheroo` to turn the discrete GPU off. Sometimes unfortunately, it is not working.

Then you may check out [acpi_call](https://aur.archlinux.org/packages/?O=0&K=acpi_call). MrDeepPurple has prepared the script which he is using to perform 'turn off' task. He is calling script via systemd service while booting and resuming his system. Here is his script:

```
#!/bin/sh
libglx=$(/usr/lib/fglrx/switchlibglx query)
modprobe acpi_call
if [ "$libglx" = "intel" ]; then
    echo '\_SB.PCI0.PEG0.PEGP._OFF' > /proc/acpi/call
fi

```

### Switching from X session to TTYs gives a blank screen/low resolution TTY

Workaround for this "feature", which appeared in catalyst 13.2 betas, is to use `vga=` kernel option, like `vga=792`. You can get the list of supported resolutions with the

```
$ hwinfo --framebuffer

```

command. Get the one that corresponds to your wanted resolution, and copy-paste it into kernel line of your bootloader, so it could look like ie. `vga=0x03d4`

### Switching from X session to TTYs gives a black screen with the monitor backlight on

Use [uvesafb](/index.php/Uvesafb "Uvesafb") as your framebuffer driver. Moreover with `uvesafb` it is also possible to set whatever resolution for the TTY.

### Switching to TTYs then back to X session gives a black screen with a mouse cursor

If you experience this bug, try adding

```
Option      "XAANoOffscreenPixmaps" "true"

```

to the 'Device' section of your xorg.conf file.

Also, make sure you have a [polkit authentication agent](/index.php/Polkit#Authentication_agents "Polkit") installed and running, as this behavior can happen when a program is asking for a password, but does not have an authentication agent installed to display the password dialog box.

### 30 FPS / Tear-Free / V-Sync bug

Bug introduced in Catalyst 13.6 beta, not fixed till now (13.9).

After enabling "Tear-Free" functionality every freshly started OpenGL application is lagging, often generates only 30 FPS, it also touches composited desktop.

Workaround is pretty simple and was found by M132:

1.  Open "AMD Catalyst Control Center" (amdcccle) application
2.  Enable Tear-Free, it will set 3D V-Sync option to "Always on".
3.  Set 3D V-Sync to "Always Off".
4.  Make sure Tear-Free is still on.
5.  Restart X / Re-login.

It is working well on KDE 4.11.x, but in case of problems M132 suggests: "Try disabling "Detect refresh rate" and specify monitor's refresh rate in the Composite plugin."

### Backlight adjustment does not work

If you have a problem with backlight adjustment, you can try the following command:

```
# aticonfig --set-pcs-u32=MCIL,PP_PhmUseDummyBackEnd,1

```

Some users reported that this can decrease FPS. To restore defaults, run:

```
# aticonfig --set-pcs-u32=MCIL,PP_PhmUseDummyBackEnd,0

```

[Read more about this bug](http://ati.cchtml.com/show_bug.cgi?id=711)

### Chromium glitching when using plasma

Add --disable-gpu execute option to the chromium, ie. to /usr/share/applications/chromium.desktop file, like here:

```
# cat /usr/share/applications/chromium.desktop | grep -i exec
Exec=chromium %U --disable-gpu

```

### Xorg crashes

#### Unsupported Xorg Version

When having a supported Linux kernel version but an unsupported Xorg version, you might get this error message and Xorg will crash

```
(WW) fglrx: No matching Device section for instance (BusID PCI:0@0:17:0) found
(...)
/usr/bin/Xorg.bin: symbol lookup error: /usr/lib/xorg/modules/drivers/fglrx_drv.so: undefined symbol: GlxInitVisuals2D
xinit: giving up
xinit: unable to connect to X server: Connection refused
xinit: server error

```

For example: fglrx 15.20.3 does not support Xorg 1.17.

To solve this, you should downgrade Xorg. A helpful list of steps can be found on [[1]](https://gist.github.com/anonymous/9ea8d3774f7afce3a605)

## See also

*   [Unofficial Wiki for the ATI Linux Driver](http://wiki.cchtml.com/index.php/Main_Page)
*   [Unofficial ATI Linux Driver Bugzilla](http://ati.cchtml.com/query.cgi)