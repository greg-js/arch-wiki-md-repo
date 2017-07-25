As it pertains to general desktop use, an [ICC profile](https://en.wikipedia.org/wiki/ICC_profile "wikipedia:ICC profile") is a binary file which contains precise data regarding the color attributes of an input, or output device. Single, or multiple profiles can be applied across a system and its devices to produce consistent and repeatable results for graphic and document editing and publishing. ICC profiles are typically calibrated with a [(tristimulus) colorimeter](https://en.wikipedia.org/wiki/Tristimulus_colorimeter "wikipedia:Tristimulus colorimeter"), or a spectrophotometer when absolute color accuracy is required.

## Contents

*   [1 Profile generation](#Profile_generation)
    *   [1.1 Colorimeter or spectrometer](#Colorimeter_or_spectrometer)
    *   [1.2 Argyll CMS](#Argyll_CMS)
    *   [1.3 Monitor calibration and profiling with additional calibration hardware](#Monitor_calibration_and_profiling_with_additional_calibration_hardware)
    *   [1.4 Scanner calibration](#Scanner_calibration)
    *   [1.5 Printer calibration](#Printer_calibration)
    *   [1.6 File transfer](#File_transfer)
    *   [1.7 Gnome Color Manager](#Gnome_Color_Manager)
        *   [1.7.1 Manually](#Manually)
    *   [1.8 LPROF ICC Profiler](#LPROF_ICC_Profiler)
        *   [1.8.1 Monitor calibration](#Monitor_calibration)
            *   [1.8.1.1 Contrast/Brightness](#Contrast.2FBrightness)
            *   [1.8.1.2 Color temperature](#Color_temperature)
        *   [1.8.2 Monitor profiling without additional calibration hardware](#Monitor_profiling_without_additional_calibration_hardware)
    *   [1.9 ThinkPads](#ThinkPads)
*   [2 Loading ICC profiles](#Loading_ICC_profiles)
    *   [2.1 xcalib](#xcalib)
        *   [2.1.1 Xinitrc example](#Xinitrc_example)
        *   [2.1.2 JWM <StartupCommand> example](#JWM_.3CStartupCommand.3E_example)
    *   [2.2 dispwin](#dispwin)
        *   [2.2.1 Xinitrc example](#Xinitrc_example_2)
        *   [2.2.2 JWM <StartupCommand> example](#JWM_.3CStartupCommand.3E_example_2)
*   [3 Applications that support ICC profiles](#Applications_that_support_ICC_profiles)
*   [4 See also](#See_also)

## Profile generation

Color management is a workflow of hardware calibration, software profiling and embedding the profile into the picture or video. It's all based on using an [ICC profile](https://en.wikipedia.org/wiki/ICC_profile "wikipedia:ICC profile").

### Colorimeter or spectrometer

It is highly recommended to use a colorimeter or spectrometer device for hardware-assisted display, printer and scanner calibration. For home use there are several affordable colorimeters available. Some are well- or even better-supported under Linux than on other operating systems. Frequently recommended devices are [X-Rite ColorMunki Display](http://www.xrite.com/colormunki-display), [DataColor Spyder5 Express](http://spyder.datacolor.com/portfolio-view/spyder5express/) and the open source hardware [ColorHug](http://www.hughski.com/). You can find more Linux-supported devices listed in the [AgyllCMS documentation](http://www.argyllcms.com/doc/instruments.html).

### Argyll CMS

The [Argyll Color Management System](http://www.argyllcms.com/) is a complete suite of command-line profile creation and loading tools listed under [argyllcms](https://www.archlinux.org/packages/?name=argyllcms).

Review the official [Argyll CMS documentation](http://www.argyllcms.com/doc/ArgyllDoc.html) for details on how to profile selected devices.

### Monitor calibration and profiling with additional calibration hardware

There is a GUI frontend for ArgyllCMS called [DisplayCal](http://displaycal.net), available as [displaycal](https://www.archlinux.org/packages/?name=displaycal). In most common cases you will want to use its default settings. It is a common way to calibrate to a daylight color of 6500K and gamma 2,2\. Read the DispalGui documentation for more. Many tutorials are available on the net.

### Scanner calibration

Follow the scanner part of the [scanner calibration](https://blog.simon-dreher.de/color-management.html) tutorial.

### Printer calibration

See [cups-calibrate(8)](http://linux.die.net/man/8/cups-calibrate).

### File transfer

Profile generation on a Windows or macOS system is one of the easiest and most widely recommended methods to obtain a ICC monitor profile. Since ICC color profiles are written to an open specification, they are compatible across operating systems. Transferring profiles from one OS to another can be used as a workaround for the lack of support for certain spectrophotometers or colorimeters under Linux: one can simply produce a profile on a different OS and then use it in a Linux workflow. Note that the system on which the profile is generated must host the exact same video card and monitor for which the profile is to be used. Once generation of an ICC profile, or a series of profiles is complete on a Windows system, copy the file(s) from the default path:

```
C:\WINDOWS\System32\spool\drivers\color

```

macOS generally stores saved ICC profiles in one of two locations:

```
/Library/ColorSync/Profiles
/Users/USER_NAME/Library/ColorSync/Profile

```

Once the appropriate `.icc/.icm` files have been copied, install the device profiles to your desired system. Common installation device profiles directories on Linux include:

```
/usr/share/color/icc
/usr/local/share/color/icc
/home/USER_NAME/.color/icc

```

**Note:** Ensure that the calibrated contrast, brightness and RGB settings of the monitor do not change between the time of calibration and the loading of the ICC profile. Use this method only if you are absolutely certain that neither Linux nor the other OS does anything behind your back (in video drivers or vendor utilities) that alters the signal actually sent to the display, or the way the display interprets the signal. Watch out for "Broadcast RGB" or similar settings. One concrete example where profiling in Windows and Linux yields [significantly different results](https://bugzilla.kernel.org/show_bug.cgi?id=70721) is the Lenovo Ideapad Yoga 2 Pro laptop, because these OSes program the flat panel controller in very different ways.

### Gnome Color Manager

On Gnome, an ICC profile can easily be created by using [gnome-color-manager](https://www.archlinux.org/packages/?name=gnome-color-manager). Under Gnome, this is accessible via the Control Center and is pretty straightforward to use. You'll need a colorimeter device to use this feature.

#### Manually

Ensure *gnome-settings-daemon* is started, and run:

```
$ colormgr get-devices 

```

Look for the `Device ID` line of your monitor. If this is e.g. `xrandr-Lenovo Group Limited`, start calibration with the command:

```
gcm-calibrate --device "*xrandr-Lenovo Group Limited*"

```

### LPROF ICC Profiler

[LPROF](http://lprof.sourceforge.net/) is an ICC profiler with a graphical user interface listed under [lprof](https://aur.archlinux.org/packages/lprof/) in the [AUR](/index.php/AUR "AUR").

**Note:** The following walkthrough has been modified from the ArchWiki article [Using LPROF to profile monitors](/index.php/Using_LPROF_to_profile_monitors "Using LPROF to profile monitors").

#### Monitor calibration

##### Contrast/Brightness

Adjust the lighting in the room to what you will be using when working. Even if your screen is coated with an anti-reflective coating, you should avoid light falling directly on it. Let your monitor warm up for at least an hour for the image to get stabilized. If your calibration device has an ambient diffuser, adjust your room brightness to reach the recommended target lux point.

1.  Set the monitor contrast to maximum, or 100%.
2.  Next, display a pure black over entire screen by creating a small, black PNG image (all pixels have RGB = 0, 0, 0) and opening it up in a picture viewer that is capable of displaying an image in fullscreen mode without any controls.
3.  Reduce the vertical size of the monitor screen (not the PNG image displayed by a picture viewer but the whole of what's displayed on the screen) to 60% to 70% of the full height. What is revealed above and below the picture is called a *non-scanned area*, and since that area is not receiving any voltage, it is the blackest of black your monitor is capable of displaying.
4.  Locate the brightness control (usually a sun, circle with rays projecting from it's edges) and lower the value until the black *image* matches the non-scanned area.

##### Color temperature

As we said in the introduction, setting color temperature must occur at noon. If you only have fixed factory default color temperature, you do not really need to wait for the sunny day to come. Just set it to 6500K.

Place your monitor so that you can see outside the window *and* your screen at the same time. For this step, you also need to create a white square image (RGB = 255, 255, 255), roughly 10 by 10 centimeters (4 by 3 inches). Using the same Gwenview technique as with brightness/contrast, display the white square on a pure black background.

1.  First, prepare your eyes by staring at the outside world for a while. Let them adjust to the daylight viewing condition for a few minutes.
2.  Glance at the monitor, and the white square for a few second (it has to be short, because eyes will readjust quickly).
3.  If the square seems yellowish, you need higher color temperature, or if it has a blueish cast, the temperature needs to be lowered.
4.  Keep glancing, looking out the window, and adjusting the white temperature, until the square looks pure white

Take your time with the steps described above. It is essential to get it right.

#### Monitor profiling without additional calibration hardware

Start lprof. You will be presented by a fairly large window with multiple tabs on the right.

1.  Click on the *Monitor Profiler* tab. Then click on the large *Enter monitor values >>* button.
2.  White point should be set to *6500K (daylight)*.
3.  Primaries should be set to either *SMPTE RP145-1994*, or *EBU Tech.3213-E* or *P22*, or whatever appropriate values for your monitor. If you come across correct values for your monitor, enter those by selecting *User Defined* from the drop-down. If in doubt, you may use *P22* for all monitors with Trinitron CRTs (in this case, *Trinitron* is not related to Sony Trinitron mointors and TVs), and *SMPTE RP145-1994* for other CRTs.
4.  Click the *Set Gamma and Black Point* button.
5.  You will now see a full-screen view of two charts with some controls at the bottom.
6.  Uncheck the *Link channels* check-box and adjust individual Red, Green, and Blue gamma by either moving the slider left or right, or by entering and changing values in the three boxes to the left. The goal is to make the chart on the left (the smaller square one) flat. When you are satisfied with how it looks, check the *Link channels* check-box and adjust the gamma again.
7.  When you are done, click *OK*. Click *OK* again.

When you are finished entering monitor values, you might want to enter some information about the monitor. This is not mandatory, but it is always nice to know what profile is for what.

1.  Click *Profile identification* button.
2.  Fill in the data.
3.  Click *OK* to finish.

After you are all done, click on the '...' button next to *Output Profile File* box. Enter the name of your profile: *somemonitor.icc*. Click *Create Profile* button, and you are done.

### ThinkPads

See [color profiles](http://www.thinkwiki.org/wiki/Colour_profile) for IBM/Lenovo [ThinkPad](https://en.wikipedia.org/wiki/ThinkPad "wikipedia:ThinkPad") notebook [monitor profile](http://www-307.ibm.com/pc/support/site.wss/migr-62923.html) ([generic](http://www-307.ibm.com/pc/support/site.wss/migr-44320.html)) support.

## Loading ICC profiles

ICC profiles are loaded either by the session daemon or by a dedicated ICC loader. Both Gnome and KDE have daemons capable of loading ICC profiles from [colord](https://www.archlinux.org/packages/?name=colord). If you use colord in combination with either [gnome-settings-daemon](https://www.archlinux.org/packages/?name=gnome-settings-daemon) or [colord-kde](https://www.archlinux.org/packages/?name=colord-kde), the profile will be loaded automatically. If you're not using neither Gnome nor KDE, you may install an independent daemon, [xiccd](https://github.com/agalakhov/xiccd), which does the same but does not depend on your desktop environment. Do not start two ICC-capable daemons (e.g. gnome-settiongs-daemon and xiccd) at the same time.

If you're not using any ICC-capable session daemon, make sure you use only one ICC loader - either xcalib, dispwin, dispcalGUI-apply-profiles or others, otherwise you easily end up with uncontrolled environment. (The most recently run loader set the calibration, and the earlier loaded calibration is overwritten.)

Before using a particular ICC loader, you should understand that some tools set only the calibration curves (e.g. xcalib), other tools set only the display profile to X.org _ICC_PROFILE atom (e.g. xicc) and other tools do both tasks at once (e.g. dispwin, dispcalGUI-apply-profiles).

### xcalib

*   [xcalib](http://xcalib.sourceforge.net/) is a lightweight monitor calibration loader which can load an ICC monitor profile to be shared across desktop applications. [xcalib](https://aur.archlinux.org/packages/xcalib/) is part of the Arch User Repository (AUR).

#### Xinitrc example

Load profile `P221W-sRGB.icc` in `/usr/share/color/icc` on display host:0 when X server starts

```
#!/bin/bash

/usr/bin/xcalib -d :0 /usr/share/color/icc/P221W-sRGB.icc
```

#### JWM `<StartupCommand>` example

Load profile `P221W-Native.icc` in `/usr/local/share/color/icc` on display host:0 when JWM starts

```
 `<StartupCommand>`xcalib -d :0 /usr/local/share/color/icc/P221W-Native.icc`</StartupCommand>`

```

### dispwin

*   [dispwin](http://www.argyllcms.com/doc/dispwin.html) is a part of [argyllcms](https://www.archlinux.org/packages/?name=argyllcms).

#### Xinitrc example

Load profile `906w-6500K.icc` in `/home/arch/.color/icc` on display 0 when X server starts

```
#!/bin/bash

/usr/bin/dispwin -d0 /home/arch/.color/icc/906w-6500K.icc
```

#### JWM `<StartupCommand>` example

Load Argyll calibration file `906w-7000K.cal` in `/usr/local/share/color/icc` on display 1 when JWM starts

```
 `<StartupCommand>`dispwin -d1 /usr/local/share/color/icc/906w-7000K.cal`</StartupCommand>`

```

You can easily use one of these loaders to apply the color profile in early boot stage when starting a display manager, e.g. using [LightDM startup script](https://wiki.ubuntu.com/LightDM#Adding_System_Hooks). This allows to load a single icc profile file. This won't work with loading several profile files when using a multi monitopr setup.

## Applications that support ICC profiles

*   [Xsane](http://www.xsane.org/doc/sane-xsane-color-management-doc.html) can use ICC profiles for color-corrected scanning.
*   [CUPS](/index.php/CUPS "CUPS") can use ICC profiles for color-corrected printing using [Colord](https://www.freedesktop.org/software/colord/faq.html#cups)
*   [GIMP](/index.php/GIMP "GIMP") can use ICC profiles for display of the image being edited. The use of the installed ICC profile has to be explicitly enabled in the settings dialog, though.
*   [mpv](/index.php/Mpv "Mpv") can take an ICC profile into account when playing a video. The command line argument is: `--icc-profile=/path/to/profile.icc` or `--icc-profile-auto`. Only `--vo=opengl` does color management; other VO drivers will silently ignore the ICC profile options.
*   [Firefox](/index.php/Firefox "Firefox"), by default, uses the system-wide ICC profile only when displaying images that are already tagged with an ICC profile. To assume that untagged images use sRGB and apply color correction also to them, set the `gfx.color_management.mode` preference to 1.
*   Both [Eye of Gnome](https://www.archlinux.org/packages/?name=eog) and [Eye of MATE](https://www.archlinux.org/packages/?name=eom) automatically use the system-installed ICC profile.

## See also

*   [Using LPROF to profile monitors](/index.php/Using_LPROF_to_profile_monitors "Using LPROF to profile monitors") - Additional details on how to profile monitors
*   [Wikipedia:Linux color management](https://en.wikipedia.org/wiki/Linux_color_management "wikipedia:Linux color management")
*   [Argyll Color Management System](http://www.argyllcms.com/) - Official Site
*   [LPROF Main Help Window](http://lprof.sourceforge.net/help/lprof-help.html) - Details on profiling printers and scanners
*   [DisplayCal: Basic concept of display calibration and profiling](http://displaycal.net/#concept)
*   [Display color profiling on Linux (XFCE)](https://encrypted.pcode.nl/blog/2013/11/24/display-color-profiling-on-linux/)
*   [Monitor Hardware Calibration](https://linuxtidbits.wordpress.com/2013/04/20/handling-display-calibration/)