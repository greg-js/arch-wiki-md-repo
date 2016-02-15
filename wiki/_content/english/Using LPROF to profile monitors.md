This article will explain the concept of monitor calibration and profiling. It explains the building of lprof color profiler from the provided PKGBUILD, and its use in profiling your monitor.

## Contents

*   [1 Before you read](#Before_you_read)
    *   [1.1 About LCD monitors](#About_LCD_monitors)
    *   [1.2 When to calibrate monitors](#When_to_calibrate_monitors)
*   [2 About monitor calibration](#About_monitor_calibration)
    *   [2.1 Black point](#Black_point)
    *   [2.2 Color (white) temperature](#Color_.28white.29_temperature)
    *   [2.3 Brightness](#Brightness)
    *   [2.4 Contrast](#Contrast)
    *   [2.5 Phosphors](#Phosphors)
*   [3 Building lprof](#Building_lprof)
*   [4 Calibrating the monitor](#Calibrating_the_monitor)
    *   [4.1 Setting brightness/contrast](#Setting_brightness.2Fcontrast)
    *   [4.2 Setting the color temperature](#Setting_the_color_temperature)
    *   [4.3 Profiling the monitor](#Profiling_the_monitor)
*   [5 Where to save profiles](#Where_to_save_profiles)
*   [6 Monitor phosphor characteristics](#Monitor_phosphor_characteristics)
*   [7 See also](#See_also)

## Before you read

Monitor calibration is an essential step in accurate color rendering. DTP software such as [Scribus](http://www.scribus.net/) makes use of monitor ICC profile to display color accurately and enable preview of publication's colors as they would appear on a printed copy.

For general use (such as watching videos, viewing family photos, etc) monitor calibration is not necessary. This article is intended for DTP and pre-press professionals who need accurate color reproduction.

### About LCD monitors

LCD monitors require a different approach to monitor profiling. They are not covered in this article, because the original author had no access to such devices.

### When to calibrate monitors

Some people may say any time is a good time. But to do it correctly, weather is the primary concern. Yes, the weather. 6500K daylight color temperature (standard in DTP and pre-press) is not some arbitrary temperature (you do not really have to know what that means, really). It is the temperature of white on a sunny day at noon. What that means is that we need a _sunny day_, and around _noon_ to profile our monitor properly. This advice comes from seasoned image editing technicians, so take it and you will be happy. :)

## About monitor calibration

Monitor calibration is carried out in three simple steps.

1.  set monitor's black point by adjusting brightness control
2.  set monitor's color temperature
3.  profile monitor using a profiling tool

But before you do that, we will discuss some terms that will be used in this article.

### Black point

Black point of the monitor is the _black_ that is displayed when the device gets no input from the graphic card. If you display an image that has RGB values of 0, 0, 0, then you will be able to 'see' the monitor's black point.

### Color (white) temperature

Also referred to as the _white point_, this is the color temperature of the white. The higher the temperature, the cooler the white (which runs contrary to our notion of hot and cold), and vice versa. For DTP and pre-press, the standard white point is 6500K.

The factory default of most monitors sets the white point at 9300K. This is too cool for DTP. On some monitor makes and models, there are advanced controls for fine-tuning the white point.

### Brightness

What people usually refer to as brightness is actually a control that shifts the black point. By shifting the black point, one gets the impression that the picture is becoming brighter or darker. What actually happens is that the black point gets moved, so the pure black also gets brighter or darker.

### Contrast

Contrast control adjusts the distance of white (RGB = 255, 255, 255) to black (RGB = 0, 0, 0) point. The black point is not changed while the white point becomes brighter or darker effectively expanding or compressing the range of brightness values that can be reproduced. For monitor calibration purposes, this value should always be the maximum available on a device.

### Phosphors

The phosphors, or _primaries_ as they are often called, are three sets of values (two numbers each). Some manufacturers publish data on phosphor values in user manuals, but this is not true in most cases. Using specialized software, or web search engines is the most common method of getting this information.

## Building lprof

Install [lprof](https://aur.archlinux.org/packages/lprof/), which is available in the [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository").

## Calibrating the monitor

Before you start lprof (or any other calibration/profiling tool) there are some steps must can carry out that do not require any software.

### Setting brightness/contrast

Adjust the lighting in the room to what you will be using when working. Even if your screen is coated with an anti-reflective coating, you should avoid light falling directly on it. Let your monitor warm up for at least an hour for the image to get stabilized. It is not uncommon for Linux to be kept up 24/7 without shutting down, so you may consider that unless you hate the noise and/or light. That way, monitor will be always on (and your unpaid electric bills will quickly block your doorway),

1.  Set contrast (usually a control with half-black-half-white circle) to maximum. If you find you cannot tolerate the bright highlights, you may lower contrast a little. The higher the better.
2.  Next, display a pure black over entire screen. You can do this by creating a small black PNG image (all pixels have RGB = 0, 0, 0). Open it up in [Gwenview](http://gwenview.sourceforge.net/) (you can install it along with KDE) or any other picture viewer that is capable of displaying an image in full-screen mode without any controls.
3.  Reduce the vertical size of the picture (not the PNG image displayed by a picture viewer but the whole of what's displayed on the screen) to something around 60% or 70% of the full height. What is revealed above and below the picture is called a _non-scanned area_, and since that are is not receiving any voltage, it is the blackest of black your monitor is capable of displaying.
4.  Locate the brightness control (usually a sun, circle with rays projecting from it's edges) and lower the value until the black _image_ matches the non-scanned area.

### Setting the color temperature

As we said in the introduction, setting color temperature must occur at noon. If you only have fixed factory default color temperature, you do not really need to wait for the sunny day to come. Just set it to 6500K.

Place your monitor so that you can see outside the window _and_ your screen at the same time. For this step, you also need to create a white square image (RGB = 255, 255, 255), roughly 10 by 10 centimeters (4 by 3 inches). Using the same Gwenview technique as with brightness/contrast, display the white square on a pure black background.

1.  First, prepare your eyes by staring at the outside world for a while. Let them adjust to the daylight viewing condition for a few minutes.
2.  Glance at the monitor, and the white square for a few second (it has to be short, because eyes will readjust quickly).
3.  If the square seems yellowish, you need higher color temperature, or if it has a blueish cast, the temperature needs to be lowered.
4.  Keep glancing, looking out the window, and adjusting the white temperature, until the square looks pure white

Take your time with the steps described above. It is essential to get it right.

### Profiling the monitor

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

## Where to save profiles

You can save your created profiles anywhere you want, but the common locations for color profiles are:

*   /usr/share/color/icc (used by Scribus and Separate plugin for The GIMP)
*   /usr/lib/scribus/profiles (used by Scribus)
*   /home/(your_user_name)/.color/icc (used by Scribus)

None of the locations seem to be standard. It is recommended that you put your profiles in /usr/share/color/icc, and keep copies in a non-hidden directory in your home directory.

## Monitor phosphor characteristics

| make/model | monitor type | phosphor type | RED | GREEN | BLUE |
| DELL P1110 | CRT | P22 | 0.625 / 0.34 | 0.28 / 0.595 | 0.155 / 0.07 |

## See also

*   [Information on CRT (Wikipedia)](https://en.wikipedia.org/wiki/Cathode_ray_tube "wikipedia:Cathode ray tube")
*   [International Color Consortium (ICC home page)](http://www.color.org/)
*   [A completely different view on image processing (Accurate Image Manipulation)](http://www.aim-dtp.net/)
*   [About color management (Wikipedia)](https://en.wikipedia.org/wiki/Color_management "wikipedia:Color management")
*   [Introduction to ICC color profile format (ICC home page)](http://www.color.org/iccprofile.html)

**Related software:**

*   [VIGRA](http://kogs-www.informatik.uni-hamburg.de/~koethe/vigra/)
*   [lcms](http://www.littlecms.com/)