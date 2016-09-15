HiDPI (High Dots Per Inch) displays, also known by Apple's "[Retina Display](https://en.wikipedia.org/wiki/Retina_Display "wikipedia:Retina Display")" marketing name, are screens with a high resolution in a relatively small format. They are mostly found in high-end laptops and monitors.

Not all software behaves well in high-resolution mode yet. Here are listed most common tweaks which make work on a HiDPI screen more pleasant.

## Contents

*   [1 Desktop environments](#Desktop_environments)
    *   [1.1 GNOME](#GNOME)
        *   [1.1.1 How to use non-whole numbers](#How_to_use_non-whole_numbers)
    *   [1.2 KDE](#KDE)
    *   [1.3 Xfce](#Xfce)
    *   [1.4 Cinnamon](#Cinnamon)
    *   [1.5 Enlightenment](#Enlightenment)
*   [2 X Server](#X_Server)
*   [3 X Resources](#X_Resources)
*   [4 GUI toolkits](#GUI_toolkits)
    *   [4.1 Qt 5](#Qt_5)
    *   [4.2 GDK 3 (GTK+ 3)](#GDK_3_.28GTK.2B_3.29)
    *   [4.3 GTK+ 2](#GTK.2B_2)
    *   [4.4 Elementary (EFL)](#Elementary_.28EFL.29)
*   [5 Display managers](#Display_managers)
    *   [5.1 SDDM](#SDDM)
*   [6 Boot managers](#Boot_managers)
    *   [6.1 GRUB](#GRUB)
*   [7 Applications](#Applications)
    *   [7.1 Browsers](#Browsers)
        *   [7.1.1 Firefox](#Firefox)
        *   [7.1.2 Chromium / Google Chrome](#Chromium_.2F_Google_Chrome)
        *   [7.1.3 Opera](#Opera)
    *   [7.2 Thunderbird](#Thunderbird)
    *   [7.3 Wine applications](#Wine_applications)
    *   [7.4 Skype](#Skype)
    *   [7.5 Spotify](#Spotify)
    *   [7.6 Zathura document viewer](#Zathura_document_viewer)
    *   [7.7 IntelliJ IDEA](#IntelliJ_IDEA)
    *   [7.8 NetBeans](#NetBeans)
    *   [7.9 Gimp 2.8](#Gimp_2.8)
    *   [7.10 VLC](#VLC)
    *   [7.11 Steam](#Steam)
    *   [7.12 Unsupported applications](#Unsupported_applications)
*   [8 Multiple displays](#Multiple_displays)
    *   [8.1 Side display](#Side_display)
    *   [8.2 Mirroring](#Mirroring)
*   [9 Linux console](#Linux_console)
*   [10 See also](#See_also)

## Desktop environments

### GNOME

To enable HiDPI, use gsettings:

```
gsettings set org.gnome.desktop.interface scaling-factor 2

```

**Note:** `scaling-factor` only allows whole numbers to be set. 1 = 100%, 2 = 200%, etc...

#### How to use non-whole numbers

A setting of `2, 3, etc`, which is all you can do with `scaling-factor`, may not be ideal for certain HiDPI displays and smaller screens (e.g. small tablets).

Alternatively, you can achieve any non-integer scale factor by using a combination of `scaling-factor` and `xrandr`. This combination keeps the TTF fonts properly scaled so that they do not become blurry if using `xrandr` alone. You specify zoom-in factor with `gsettings` and zoom-out factor with `xrandr`.

Here is a method to find a comfortable scale factor for your screen:

```
# First scale Gnome up to the minimum size which is too big.
# Usually "2" is already too big, but if "2" is still small for you, try "3", etc.
gsettings set org.gnome.desktop.interface scaling-factor 2
# Now start scaling down by setting zoom-out factor with xrandr.
# First get the output name:
xrandr | grep -v disconnected | grep connected | cut -d' ' -f1
# eDP1
#
# Use this value to specify --output further on.
# If you have two or more screens you can set their scale independently.
# Now, to zoom-out 1.2 times, run the following:
xrandr --output eDP1 --scale 1.2x1.2
# If the UI is still too big, increase the scale:
xrandr --output eDP1 --scale 1.25x1.25
# If UI becomes too small, decrease the scale factor a bit.
# Repeat until you find a value which works best for your screen and your eyes.
# Finally, you need to allow the mouse to navigate the whole screen.
# To do this you need to get the current scaled resolution:
xrandr | grep eDP1
# eDP1 connected primary 2304x1296+0+0 (normal left inverted right x axis y axis) 239mm x 134mm
#
# Now use the acquired resolution value to set correct panning:
xrandr --output eDP1 --panning 2304x1296

```

### KDE

KDE plasma 5 provides decent support for HiDPI screens.

Please follow these guidelines for HiDPI support in KDE plasma 5

1.  System Settings → Display and Monitor → Display Configuration → Scale Display
2.  Then drag the slider to 2
3.  Log out and back in for all applications to take the new setting into account

### Xfce

Go to Settings Manager → Appearance → Fonts, and change the DPI parameter. The value of 180 or 192 seems to work well on Retina screens. To get a more precise number, you can use `xdpyinfo | grep resolution`, and then double it.

To enlarge icons in system tray, right-click on it (aim for empty space / top pixels / bottom pixels, so that you will not activate icons themselves) → “Properties” → set “Maximum icon size” to 32, 48 or 64.

### Cinnamon

Supports HiDPI since 2.2\. Even without rebuilding GTK3, the support is pretty good (e.g. window borders are correctly sized, which is not the case under Xfce).

### Enlightenment

For E18, go to the E Setting panel. In Look → Scaling, you can control the UI scaling ratios. A ratio of 1.2 seems to work well for the native resolution of the MBPr 15" screen.

## X Server

Some programs use the DPI given by the X server. Examples are i3 ([source](https://github.com/i3/i3/blob/next/libi3/dpi.c)) and Chromium ([source](https://code.google.com/p/chromium/codesearch#chromium/src/ui/views/widget/desktop_aura/desktop_screen_x11.cc)).

To verify that the X Server has properly detected the physical dimensions of your monitor, use the *xdpyinfo* utility from the [xorg-xdpyinfo](https://www.archlinux.org/packages/?name=xorg-xdpyinfo) package:

```
$ xdpyinfo | grep -B 2 resolution
screen #0:
  dimensions:    3200x1800 pixels (423x238 millimeters)
  resolution:    192x192 dots per inch

```

This examples uses inaccurate dimensions (423mm x 328mm, even though the Dell XPS 9530 has 346mm x 194mm) to have a clean multiple of 96 dpi, in this case 192 dpi. This tends to work better than using the correct DPI — Pango renders fonts crisper in i3 for example.

If the DPI displayed by xdpyinfo is not correct, see [Xorg#Display size and DPI](/index.php/Xorg#Display_size_and_DPI "Xorg") for how to fix it.

## X Resources

If you are not using a desktop environment such as GNOME, KDE, Xfce, or other that manipulates the X settings for you, you can set the desired DPI setting manually via the `Xft.dpi` variable in `~/.Xresources`:

 `~/.Xresources` 
```
Xft.dpi: 180
Xft.autohint: 0
Xft.lcdfilter:  lcddefault
Xft.hintstyle:  hintfull
Xft.hinting: 1
Xft.antialias: 1
Xft.rgba: rgb

```

Make sure the settings are loaded properly when X starts, for instance in your `~/.xinitrc` with `xrdb -merge ~/.Xresources` (see [Xresources](/index.php/Xresources "Xresources") for more information).

This will make the font render properly in most toolkits and applications, it will however not affect things such as icon size! Setting `Xft.dpi` at the same time as toolkit scale (e.g. `GDK_SCALE`) may cause interface elements to be much larger than intended in some programs like firefox.

## GUI toolkits

### Qt 5

Since Qt 5.6, Qt 5 applications can be instructed to honor screen DPI by setting the `QT_AUTO_SCREEN_SCALE_FACTOR` environment variable, for example by creating a file `/etc/profile.d/qt-hidpi.sh`

```
export QT_AUTO_SCREEN_SCALE_FACTOR=1

```

And set the executable bit on it.

If automatic detection of DPI does not produce the desired effect, scaling can be set manually per-screen (`QT_SCREEN_SCALE_FACTORS`) or globally (`QT_SCALE_FACTOR`). For more details see the [Qt blog post](https://blog.qt.io/blog/2016/01/26/high-dpi-support-in-qt-5-6/).

Note if you manually set the screen factor, it's important to set QT_AUTO_SCREEN_SCALE_FACTOR=0 otherwise some applications which explicitly force high DPI enabling get scaled twice.

QT_SCALE_FACTOR will scale fonts QT_SCREEN_SCALE_FACTORS will *not* scale fonts

If you also set the font DPI manually in xrdb to support other toolkits - QT_SCALE_FACTORS will give you a huge fonts.

### GDK 3 (GTK+ 3)

To scale UI elements by a factor of two:

```
export GDK_SCALE=2

```

To undo scaling of text:

```
export GDK_DPI_SCALE=0.5

```

### GTK+ 2

Scaling of UI elements is not supported by the toolkit itself, however it's possible to generate a theme with elements pre-scaled for HiDPI display using [oomox-git](https://aur.archlinux.org/packages/oomox-git/).

### Elementary (EFL)

To scale UI elements by a factor of 1.5:

```
 export ELM_SCALE=1.5

```

For more details see [https://phab.enlightenment.org/w/elementary/](https://phab.enlightenment.org/w/elementary/)

## Display managers

### SDDM

To scale SDDM you have to change the following properties in `/etc/sddm.conf`. It is recommended to make a backup of your config before editing it.

```
[X11]
# X server arguments
ServerArguments=-dpi 144

```

## Boot managers

### GRUB

A possible solution is to use a big size font. Generate a GRUB font of custom size, e.g. using the font DejaVu Sans Mono and size 36:

```
# grub-mkfont --output=/boot/grub/fonts/DejaVuSansMono36.pf2 --size=36 /usr/share/fonts/TTF/DejaVuSansMono.ttf

```

then set GRUB to use it, adding the `GRUB_FONT` line to `/etc/default/grub`

 `/etc/default/grub`  `GRUB_FONT=/boot/grub/fonts/DejaVuSansMono36.pf2` 

and finally update GRUB configuration with

```
# grub-mkconfig -o /boot/grub/grub.cfg

```

## Applications

### Browsers

#### Firefox

Open Firefox advanced preferences page (`about:config`) and set parameter `layout.css.devPixelsPerPx` to `2` (or find the one that suits you better; `2` is a good choice for Retina screens).

If you use a HiDPI monitor such as Retina display together with another monitor, you can use [AutoHiDPI](https://addons.mozilla.org/en-US/firefox/addon/autohidpi/) add-on in order to automatically adjust `layout.css.devPixelsPerPx` setting for the active screen.

From Firefox version 38 onwards, your system (GTK+ 3.10) settings should be taken into account.[[1]](https://bugzilla.mozilla.org/show_bug.cgi?id=975919)

#### Chromium / Google Chrome

Full out of the box HiDPI support is available in [chromium](https://www.archlinux.org/packages/?name=chromium) and [google-chrome](https://aur.archlinux.org/packages/google-chrome/) as tested (with google-chrome) on Gnome and Cinnamon. Additionally, for environments where out of the box support does not work, the browser can be launched with the command line flag `--force-device-scale-factor` and a scaling value. This will scale all content and ui, including tab and font size. For example:

 `chromium --force-device-scale-factor=2` 

Using this option, a scaling factor of 1 would be normal scaling. Floating point values can be used.

If you use a HiDPI monitor such as Retina display together with another monitor, you can use the [reszoom](https://chrome.google.com/webstore/detail/resolution-zoom/enjjhajnmggdgofagbokhmifgnaophmh) extension in order to automatically adjust the zoom level for the active screen.

#### Opera

Since version 24 one can alter Opera's DPI by starting it with the `--alt-high-dpi-setting=X` command line option, where X is the desired DPI. For example, with `--alt-high-dpi-setting=144` Opera will assume that DPI is 144\. Newer versions of opera will auto detect the DPI using the font DPI setting (in KDE: the force font DPI setting.)

Generally speaking, Opera's HiDPI support is excellent. Since it is also built using Chromium's blink renderer, and has an extension which runs most Chrome extensions, it is a very viable alternative to Chromium/Chrome.

### Thunderbird

See [#Firefox](#Firefox). To access `about:config`, go to Edit → Preferences → Advanced → Config editor.

### Wine applications

Run

```
$ winecfg

```

and change the "dpi" setting found in the "Graphics" tab. This only affects the font size.

### Skype

Skype is a Qt program, and needs to be configured separately. You cannot change the DPI setting for it, but at least you can change font size. Install [qt4](https://www.archlinux.org/packages/?name=qt4) and run `qtconfig-qt4` to do it.

### Spotify

Spotify can be launched with a custom scaling factor, for example

```
$ spotify --force-device-scale-factor=1.5

```

### Zathura document viewer

No modifications required for document viewing.

UI text scaling is specified via [configuration file](https://pwmt.org/projects/zathura/documentation/) (note that "font" is a [girara option](https://pwmt.org/projects/girara/options/)):

```
set font "monospace normal 20"

```

### IntelliJ IDEA

IntelliJ IDEA 15 and above should include HiDPI support.[[2]](http://blog.jetbrains.com/idea/2015/07/intellij-idea-15-eap-comes-with-true-hidpi-support-for-windows-and-linux/) If it does not work, the most convenient way to fix the problem in this case seems to be changing the Override Default Fonts setting:

	*File -> Settings -> Behaviour & Appearance -> Appearance*

The addition of `-Dhidpi=true` to the vmoptions file in either `$HOME/.IdeaC14/` or `/usr/share/intelligj-idea-ultimate-edition/bin/` of [release 14](https://youtrack.jetbrains.com/issue/IDEA-114944) should not be required anymore.

### NetBeans

NetBeans allows the font size of its interface to be controlled using the `--fontsize` parameter during startup. To make this change permanent edit the `/usr/share/netbeans/etc/netbeans.conf` file and append the `--fontsize` parameter to the `netbeans_default_options` property.[[3]](http://wiki.netbeans.org/FaqFontSize)

The editor fontsize can be controlled from Tools → Option → Fonts & Colors.

The output window fontsize can be controlled from Tools → Options → Miscelaneous → Output

### Gimp 2.8

Use a high DPI theme, or [adjust](http://gimpforums.com/thread-increase-all-icons-on-hidpi-screen?pid=39113#pid39113) `gtkrc` of an existing theme. (Change all occurrences of the size `button` to `dialog`, for example `GimpToolPalette::tool-icon-size`.)

There's also the [gimp-hidpi](https://github.com/jedireza/gimp-hidpi).

### VLC

As of May 2015, the git version [vlc-git](https://aur.archlinux.org/packages/vlc-git/) seems to solve some of the problems.

### Steam

The [HiDPI-Steam-Skin](https://github.com/MoriTanosuke/HiDPI-Steam-Skin) can be installed to increase the font size of the interface. While not perfect, it does improve usability.

**Note:** The skin must be downloaded to `~/.local/share/Steam/skins`, not `~/.steam/skins/` as the README says.

### Unsupported applications

One approach is to run the application full screen and without decoration in its own VNC desktop. Then scale the viewer. With Vncdesk ([vncdesk-git](https://aur.archlinux.org/packages/vncdesk-git/) from the [AUR](/index.php/AUR "AUR")) you can set up a desktop per application, then start server and client with a simple command such as `vncdesk 2`.

[x11vnc](/index.php/X11vnc "X11vnc") has an experimental option `-appshare`, which opens one viewer per application window. Perhaps something could be hacked up with that.

## Multiple displays

The HiDPI setting applies to the whole desktop, so non-HiDPI external displays show everything too large.

### Side display

One workaround is to using [xrandr](/index.php/Xrandr "Xrandr")'s scale option. To have a non-HiDPI monitor (on DP1) right of an internal HiDPI display (eDP1), one could run:

```
xrandr --output eDP1 --auto --output DP1 --auto --scale 2x2 --right-of eDP1

```

When extending above the internal display, you may see part of the internal display on the external monitor. In that case, specify the position manually, e.g. using [this script](https://gist.github.com/wvengen/178642bbc8236c1bdb67).

You may run into problems with your mouse not being able to reach the whole screen. That is a [known bug](https://bugs.freedesktop.org/show_bug.cgi?id=39949) with an xserver-org patch (or try the panning option, but that might cause other problems).

An example of the panning syntax for a 4k laptop with an external 1920x1080 monitor to the right:

```
xrandr --output eDP1 --auto --output HDMI1 --auto --panning 3840x2160+3840+0 --scale 2x2 --right-of eDP1

```

Generically if your hidpi monitor is AxB pixels and your regular monitor is CxD and you are scaling by [ExF], the commandline for right-of is:

```
xrandr --output eDP1 --auto --output HDMI1 --auto --panning [C*E]x[D*F]+[A]+0 --scale [E]x[F] --right-of eDP1

```

If panning is not a solution for you it may be better to set position of monitors and fix manually the total display screen.

An example of the syntax for a 2560x1440 WQHD 210 DPI laptop monitor (eDP1) using native resolution placed below a 1920x1080 FHD 96 DPI external monitor (HDMI) scaled to match global DPI settings:

```
xrandr --output eDP1 --auto --pos 0x1458 --output HDMI --scale 1.35x1.35 --auto --pos 0x0 --fb 2592x2898

```

The total screen size (--fb) and positioning (--pos) are to be calculated taking into account the scaling factor.

In this case laptop monitor (eDP1) has no scaling and uses native mode for resolution so it will total 2560x1440, but external monitor (HDMI) is scaled and it has to be considered a larger screen so (1920*1.35)x(1080*1.35) from where the eDP1 Y position came 1080*1.35=1458 and the total screen size: since one on top of the other X=(greater between eDP1 and HDMI, so 1920*1.35=2592) and Y=(sum of the calculated heights of eDP1 and HDMI, so 1440+(1080*1.35)=2898).

Generically if your hidpi monitor is AxB pixels and your regular monitor is CxD and you are scaling by [ExF] and hidpi is placed below regular one, the commandline for right-of is:

```
xrandr --output eDP1 --auto --pos 0x(DxF) --output HDMI --auto --scale [E]x[F] --pos 0x0 --fb [greater between A and (C*E)]x[B+(D*F)]

```

You may adjust the "sharpness" parameter on your monitor settings to adjust the blur level introduced with scaling.

### Mirroring

If all you want is to mirror ("unify") displays, this is easy as well:

With AxB your native HiDPI resolution (for ex 3200x1800) and CxD your external screen resolution (for ex 1920x1200)

```
xrandr --output HDMI --scale [A/C]x[B/D]

```

In this example which is QHD (3200/1920 = 1.66 and 1800/1200 = 1.5)

```
xrandr --output HDMI --scale 1.66x1.5

```

For UHD to 1080p (3840/1920=2 2160/1080=1.98)

```
xrandr --output HDMI --scale 2x1.98

```

You may adjust the "sharpness" parameter on your monitor settings to adjust the blur level introduced with scaling.

## Linux console

The default [Linux console](https://en.wikipedia.org/wiki/Linux_console "w:Linux console") font will be very small on hidpi displays, the largest font present in the [kbd](https://www.archlinux.org/packages/?name=kbd) package is `latarcyrheb-sun32` and other packages like [terminus-font](https://www.archlinux.org/packages/?name=terminus-font) contain further alternatives, such as `ter-132n`(normal) and `ter-132b`(bold). See [Fonts#Console fonts](/index.php/Fonts#Console_fonts "Fonts") for configuration details.

## See also

*   [Ultra HD 4K Linux Graphics Card Testing](http://www.phoronix.com/scan.php?page=article&item=linux_uhd4k_gpus) (Nov 2013)
*   [Understanding pixel density](http://www.eizo.com/library/basics/pixel_density_4k/)