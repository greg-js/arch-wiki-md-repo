# ICC profiles

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

As it pertains to general desktop use, an ICC profile is a binary file which contains precise data regarding the color attributes of an input, or output device ([Source](http://en.wikipedia.org/wiki/ICC_profile)). Single, or multiple profiles can be applied across a system and its devices to produce consistent and repeatable results for graphic and document editing and publishing. ICC profiles are typically calibrated with a [(tristimulus) colorimeter](http://en.wikipedia.org/wiki/Tristimulus_colorimeter), or a spectrophotometer when absolute color accuracy is required.

## Contents

*   [1 Profile Generation](#Profile_Generation)
    *   [1.1 File Transfer](#File_Transfer)
    *   [1.2 Gnome Color Manager](#Gnome_Color_Manager)
        *   [1.2.1 Manually](#Manually)
    *   [1.3 LPROF ICC Profiler](#LPROF_ICC_Profiler)
        *   [1.3.1 Monitor Calibration](#Monitor_Calibration)
            *   [1.3.1.1 Contrast/Brightness](#Contrast.2FBrightness)
            *   [1.3.1.2 Color Temperature](#Color_Temperature)
        *   [1.3.2 Monitor Profiling](#Monitor_Profiling)
    *   [1.4 Argyll CMS](#Argyll_CMS)
    *   [1.5 ThinkPads](#ThinkPads)
*   [2 Loading ICC Profiles](#Loading_ICC_Profiles)
    *   [2.1 xcalib](#xcalib)
        *   [2.1.1 Xinitrc Example](#Xinitrc_Example)
        *   [2.1.2 JWM <StartupCommand> Example](#JWM_.3CStartupCommand.3E_Example)
    *   [2.2 dispwin](#dispwin)
        *   [2.2.1 Xinitrc Example](#Xinitrc_Example_2)
        *   [2.2.2 JWM <StartupCommand> Example](#JWM_.3CStartupCommand.3E_Example_2)
*   [3 Applications that can use ICC profiles](#Applications_that_can_use_ICC_profiles)
*   [4 See also](#See_also)

## Profile Generation

### File Transfer

Profile generation on a Windows 7/Vista/XP, or [Mac OS X](http://www.apple.com/macosx/) system is one of the easiest and most widely recommended methods to obtain a ICC monitor profile. Since ICC color profiles are written to an open specification, they are compatible across operating systems. Transferring profiles from one OS to another can be used as a workaround for the lack of support for certain spectrophotometers, or colorimeters under [Linux](http://www.linux.org/): one can simply produce a profile on a different OS and then use it in a Linux workflow ([Source](http://en.wikipedia.org/wiki/Linux_color_management)). Recommended colorimeters include the [X-Rite i1Display 2](http://www.xrite.com/product_overview.aspx?ID=788), the [Spyder3 Pro](http://spyder.datacolor.com/product-mc-s3pro.php) and the open Source Hardware [ColorHug](http://www.hughski.com/). Note that the system on which the profile is generated must host the exact same video card and monitor for which the profile is to be used. Once generation of an ICC profile, or a series of profiles is complete on a Windows 7/Vista/XP system, copy the file(s) from the default path:

```
C:\WINDOWS\System32\spool\drivers\color

```

Mac OS X generally stores saved ICC profiles in one of two locations:

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

Ensure _gnome-settings-daemon_ is started, and run:

```
$ colormgr get-devices 

```

Look for the `Device ID` line of your monitor. If this is e.g. `xrandr-Lenovo Group Limited`, start calibration with the command:

```
gcm-calibrate --device "_xrandr-Lenovo Group Limited_"

```

### LPROF ICC Profiler

[LPROF](http://lprof.sourceforge.net/) is an ICC profiler with a graphical user interface listed under [lprof](https://aur.archlinux.org/packages/lprof/)<sup><small>AUR</small></sup> in the [AUR](/index.php/AUR "AUR").

**Note:** The following walkthrough has been modified from the ArchWiki article [Using LPROF to profile monitors](/index.php/Using_LPROF_to_profile_monitors "Using LPROF to profile monitors").

#### Monitor Calibration

##### Contrast/Brightness

Adjust the lighting in the room to what you will be using when working. Even if your screen is coated with an anti-reflective coating, you should avoid light falling directly on it. Let your monitor warm up for at least an hour for the image to get stabilized. If your calibration device has an ambient diffuser, adjust your room brightness to reach the recommended target lux point.

1.  Set the monitor contrast to maximum, or 100%.
2.  Next, display a pure black over entire screen by creating a small, black PNG image (all pixels have RGB = 0, 0, 0) and opening it up in a picture viewer that is capable of displaying an image in fullscreen mode without any controls.
3.  Reduce the vertical size of the monitor screen (not the PNG image displayed by a picture viewer but the whole of what's displayed on the screen) to 60% to 70% of the full height. What is revealed above and below the picture is called a _non-scanned area_, and since that area is not receiving any voltage, it is the blackest of black your monitor is capable of displaying.
4.  Locate the brightness control (usually a sun, circle with rays projecting from it's edges) and lower the value until the black _image_ matches the non-scanned area.

##### Color Temperature

As we said in the introduction, setting color temperature must occur at noon. If you only have fixed factory default color temperature, you do not really need to wait for the sunny day to come. Just set it to 6500K.

Place your monitor so that you can see outside the window _and_ your screen at the same time. For this step, you also need to create a white square image (RGB = 255, 255, 255), roughly 10 by 10 centimeters (4 by 3 inches). Using the same Gwenview technique as with brightness/contrast, display the white square on a pure black background.

1.  First, prepare your eyes by staring at the outside world for a while. Let them adjust to the daylight viewing condition for a few minutes.
2.  Glance at the monitor, and the white square for a few second (it has to be short, because eyes will readjust quickly).
3.  If the square seems yellowish, you need higher color temperature, or if it has a blueish cast, the temperature needs to be lowered.
4.  Keep glancing, looking out the window, and adjusting the white temperature, until the square looks pure white

Take your time with the steps described above. It is essential to get it right.

#### Monitor Profiling

Start lprof. You will be presented by a fairly large window with multiple tabs on the right.

1.  Click on the _Monitor Profiler_ tab. Then click on the large _Enter monitor values >>_ button.
2.  White point should be set to _6500K (daylight)_.
3.  Primaries should be set to either _SMPTE RP145-1994_, or _EBU Tech.3213-E_ or _P22_, or whatever appropriate values for your monitor. If you come across correct values for your monitor, enter those by selecting _User Defined_ from the drop-down. If in doubt, you may use _P22_ for all monitors with Trinitron CRTs (in this case, _Trinitron_ is not related to Sony Trinitron mointors and TVs), and _SMPTE RP145-1994_ for other CRTs.
4.  Click the _Set Gamma and Black Point_ button.
5.  You will now see a full-screen view of two charts with some controls at the bottom.
6.  Uncheck the _Link channels_ check-box and adjust individual Red, Green, and Blue gamma by either moving the slider left or right, or by entering and changing values in the three boxes to the left. The goal is to make the chart on the left (the smaller square one) flat. When you are satisfied with how it looks, check the _Link channels_ check-box and adjust the gamma again.
7.  When you are done, click _OK_. Click _OK_ again.

When you are finished entering monitor values, you might want to enter some information about the monitor. This is not mandatory, but it is always nice to know what profile is for what.

1.  Click _Profile identification_ button.
2.  Fill in the data.
3.  Click _OK_ to finish.

After you are all done, click on the '...' button next to _Output Profile File_ box. Enter the name of your profile: _somemonitor.icc_. Click _Create Profile_ button, and you are done.

### Argyll CMS

The [Argyll Color Management System](http://www.argyllcms.com/) is a complete suite of command-line profile creation and loading tools listed under [argyllcms](https://www.archlinux.org/packages/?name=argyllcms).

*   Review the official [Argyll CMS documentation](http://www.argyllcms.com/doc/ArgyllDoc.html) for details on how to profile selected devices.

### ThinkPads

See [color profiles](http://www.thinkwiki.org/wiki/Colour_profile) for IBM/Lenovo [ThinkPad](https://en.wikipedia.org/wiki/ThinkPad "wikipedia:ThinkPad") notebook [monitor profile](http://www-307.ibm.com/pc/support/site.wss/migr-62923.html) ([generic](http://www-307.ibm.com/pc/support/site.wss/migr-44320.html)) support.

## Loading ICC Profiles

ICC profiles are loaded either by the session daemon or by a dedicated ICC loader. Both Gnome and KDE have daemons capable of loading ICC profiles from [colord](https://www.archlinux.org/packages/?name=colord). If you use colord in combination with either [gnome-settings-daemon](https://www.archlinux.org/packages/?name=gnome-settings-daemon) or [colord-kde](https://aur.archlinux.org/packages/colord-kde/)<sup><small>AUR</small></sup>, the profile will be loaded automatically. If you're not using neither Gnome nor KDE, you may install an independent daemon, [xiccd](https://github.com/agalakhov/xiccd), which does the same but does not depend on your desktop environment. Do not start two ICC-capable daemons (e.g. gnome-settiongs-daemon and xiccd) at the same time.

If you're not using any ICC-capable session daemon, make sure you use only one ICC loader - either xcalib, dispwin, dispcalGUI-apply-profiles or others, otherwise you easily end up with uncontrolled environment. (The most recently run loader set the calibration, and the earlier loaded calibration is overwritten.)

Before using a particular ICC loader, you should understand that some tools set only the calibration curves (e.g. xcalib), other tools set only the display profile to X.org _ICC_PROFILE atom (e.g. xicc) and other tools do both tasks at once (e.g. dispwin, dispcalGUI-apply-profiles).

### xcalib

*   [xcalib](http://xcalib.sourceforge.net/) is a lightweight monitor calibration loader which can load an ICC monitor profile to be shared across desktop applications. [xcalib](https://aur.archlinux.org/packages/xcalib/)<sup><small>AUR</small></sup> is part of the Arch User Repository (AUR).

#### Xinitrc Example

Load profile `P221W-sRGB.icc` in `/usr/share/color/icc` on display host:0 when X server starts

```
#!/bin/bash

/usr/bin/xcalib -d :0 /usr/share/color/icc/P221W-sRGB.icc
```

#### JWM `<StartupCommand>` Example

Load profile `P221W-Native.icc` in `/usr/local/share/color/icc` on display host:0 when JWM starts

```
 `<StartupCommand>`xcalib -d :0 /usr/local/share/color/icc/P221W-Native.icc`</StartupCommand>`

```

### dispwin

*   [dispwin](http://www.argyllcms.com/doc/dispwin.html) is a part of [argyllcms](https://www.archlinux.org/packages/?name=argyllcms).

#### Xinitrc Example

Load profile `906w-6500K.icc` in `/home/arch/.color/icc` on display 0 when X server starts

```
#!/bin/bash

/usr/bin/dispwin -d0 /home/arch/.color/icc/906w-6500K.icc
```

#### JWM `<StartupCommand>` Example

Load Argyll calibration file `906w-7000K.cal` in `/usr/local/share/color/icc` on display 1 when JWM starts

```
 `<StartupCommand>`dispwin -d1 /usr/local/share/color/icc/906w-7000K.cal`</StartupCommand>`

```

## Applications that can use ICC profiles

*   [GIMP](/index.php/GIMP "GIMP") can use ICC profiles for color-corrected display of the image being edited. The use of the installed ICC profile has to be explicitly enabled in the settings dialog, though.
*   [mpv](/index.php/Mpv "Mpv") can take an ICC profile into account when playing a video. The command line argument is: `--vo=opengl:icc-profile=/path/to/profile.icc`.
*   [Firefox](/index.php/Firefox "Firefox"), by default, uses the system-wide ICC profile only when displaying images that are already tagged with an ICC profile. To assume that untagged images use sRGB and apply color correction also to them, set the `gfx.color_management.mode` preference to 1.
*   Both [Eye of Gnome](https://www.archlinux.org/packages/?name=eog) and [Eye of MATE](https://www.archlinux.org/packages/?name=eom) automatically use the system-installed ICC profile.

## See also

*   [Using LPROF to profile monitors](/index.php/Using_LPROF_to_profile_monitors "Using LPROF to profile monitors") - Additional details on how to profile monitors
*   [Linux Color Management](http://en.wikipedia.org/wiki/Linux_color_management) - Wikipedia
*   [Argyll Color Management System](http://www.argyllcms.com/) - Official Site
*   [LPROF Main Help Window](http://lprof.sourceforge.net/help/lprof-help.html) - Details on profiling printers and scanners
*   [dispcalGUI: Basic concept of display calibration and profiling](http://dispcalgui.hoech.net/#concept)
*   [Display color profiling on Linux (XFCE)](https://encrypted.pcode.nl/blog/2013/11/24/display-color-profiling-on-linux/)

Retrieved from "[https://wiki.archlinux.org/index.php?title=ICC_profiles&oldid=414055](https://wiki.archlinux.org/index.php?title=ICC_profiles&oldid=414055)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Image manipulation](/index.php/Category:Image_manipulation "Category:Image manipulation")