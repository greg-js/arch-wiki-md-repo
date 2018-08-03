Related articles

*   [Font configuration](/index.php/Font_configuration "Font configuration")

HiDPI (High Dots Per Inch) displays, also known by Apple's "[Retina Display](https://en.wikipedia.org/wiki/Retina_Display "wikipedia:Retina Display")" marketing name, are screens with a high resolution in a relatively small format. They are mostly found in high-end laptops and monitors.

Not all software behaves well in high-resolution mode yet. Here are listed most common tweaks which make work on a HiDPI screen more pleasant.

## Contents

*   [1 Desktop environments](#Desktop_environments)
    *   [1.1 GNOME](#GNOME)
        *   [1.1.1 Fractional Scaling](#Fractional_Scaling)
    *   [1.2 KDE](#KDE)
        *   [1.2.1 Tray icons with fixed size](#Tray_icons_with_fixed_size)
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
*   [5 Boot managers](#Boot_managers)
    *   [5.1 GRUB](#GRUB)
        *   [5.1.1 Lower the framebuffer resolution](#Lower_the_framebuffer_resolution)
        *   [5.1.2 Change GRUB font size](#Change_GRUB_font_size)
*   [6 Applications](#Applications)
    *   [6.1 Browsers](#Browsers)
        *   [6.1.1 Firefox](#Firefox)
        *   [6.1.2 Chromium / Google Chrome](#Chromium_.2F_Google_Chrome)
        *   [6.1.3 Opera](#Opera)
    *   [6.2 Thunderbird](#Thunderbird)
    *   [6.3 Wine applications](#Wine_applications)
    *   [6.4 Skype](#Skype)
    *   [6.5 Spotify](#Spotify)
    *   [6.6 Zathura document viewer](#Zathura_document_viewer)
    *   [6.7 Sublime Text 3](#Sublime_Text_3)
    *   [6.8 IntelliJ IDEA](#IntelliJ_IDEA)
    *   [6.9 NetBeans](#NetBeans)
    *   [6.10 Gimp 2.8](#Gimp_2.8)
    *   [6.11 Steam](#Steam)
        *   [6.11.1 Official HiDPI support](#Official_HiDPI_support)
        *   [6.11.2 Unofficial](#Unofficial)
    *   [6.12 Java applications](#Java_applications)
    *   [6.13 Mono applications](#Mono_applications)
    *   [6.14 MATLAB](#MATLAB)
    *   [6.15 VirtualBox](#VirtualBox)
    *   [6.16 Zoom](#Zoom)
    *   [6.17 Unsupported applications](#Unsupported_applications)
*   [7 Multiple displays](#Multiple_displays)
    *   [7.1 Side display](#Side_display)
    *   [7.2 Multiple external monitors](#Multiple_external_monitors)
    *   [7.3 Mirroring](#Mirroring)
*   [8 Linux console](#Linux_console)
*   [9 See also](#See_also)

## Desktop environments

### GNOME

To enable HiDPI, Settings > Devices > Displays，or use gsettings:

```
$ gsettings set org.gnome.desktop.interface scaling-factor 2

```

**Note:** `scaling-factor` only allows whole numbers to be set. 1 = 100%, 2 = 200%, etc...

#### Fractional Scaling

A setting of `2, 3, etc`, which is all you can do with `scaling-factor`, may not be ideal for certain HiDPI displays and smaller screens (e.g. small tablets).

*   wayland

Enable fractional Scaling experimental-feature:

```
$ gsettings set org.gnome.mutter experimental-features "['scale-monitor-framebuffer']"

```

then open Settings > Devices > Displays

*   xorg

You can achieve any non-integer scale factor by using a combination of GNOME's `scaling-factor` and [xrandr](/index.php/Xrandr "Xrandr"). This combination keeps the TTF fonts properly scaled so that they do not become blurry if using `xrandr` alone. You specify zoom-in factor with `gsettings` and zoom-out factor with [xrandr](/index.php/Xrandr "Xrandr").

First scale GNOME up to the minimum size which is too big. Usually "2" is already too big, otherwise try "3" etc. Then start scaling down by setting zoom-out factor with [xrandr](/index.php/Xrandr "Xrandr"). First get the relevant output name, the examples below use `eDP1`. Start e.g. with zoom-out 1.25 times. If the UI is still too big, increase the scale factor; if it is too small decrease the scale factor.

```
$ xrandr --output eDP1 --scale 1.25x1.25

```

**Note:** To allow the mouse to reach the whole screen, you may need to use the `--panning` option as explained in [#Side display](#Side_display).

GNOME ignores X settings due to its xsettings Plugin in Gnome Settings Daemon, where DPI setting is hard coded. There is blog entry for [recompiling Gnome Settings Daemon](http://blog.drtebi.com/2012/12/changing-dpi-setting-on-gnome-34.html). In the source documentation there is another way mentioned to set X settings DPI:

You can use the dconf Editor and navigate to key

```
/org/gnome/settings-daemon/plugins/xsettings/overrides

```

and complement the entry with the value

```
'Xft/DPI': <153600>

```

From README.xsettings

Noting that variants must be specified in the usual way (wrapped in <>).

Note also that DPI in the above example is expressed in 1024ths of an inch.

### KDE

You can use KDE's settings to fine tune font, icon, and widget scaling. This solution affects both Qt and Gtk+ applications.

To adjust font, widget, and icon scaling together:

1.  System Settings → Display and Monitor → Display Configuration → Scale Display
2.  Drag the slider to the desired size
3.  Restart for the settings to take effect

To adjust only font scaling:

1.  System Settings → Fonts
2.  Check "Force fonts DPI" and adjust the DPI level to the desired value. This setting should take effect immediately for newly started applications. You will have to logout and login for it to take effect on Plasma desktop.

To adjust only icon scaling:

1.  System Settings → Icons → Advanced
2.  Choose the desired icon size for each category listed. This should take effect immediately.

**Display Scale not integer bug :**

When you use not integer values for Display Scale it causes font render issue in some QT application ( ex. okular ).

A workaround for this is to:

1.  Set the scale value to 1
2.  Adjust your font and icons and use the "Force fonts DPI" ( this affects all apps, also GTK but not create issue with the fonts )
3.  Restart KDE
4.  If required tune the GTK apps using the variables GDK_SCALE/GDK_DPI_SCALE (as described above)

#### Tray icons with fixed size

The tray icons are not scaled with the rest of the desktop, since Plasma ignores the Qt scaling settings by default. To make Plasma respect the Qt settings, set `PLASMA_USE_QT_SCALING` to `1`.

### Xfce

Go to Settings Manager → Appearance → Fonts, and change the DPI parameter. The value of 180 or 192 seems to work well on Retina screens. To get a more precise number, you can use `xdpyinfo | grep resolution`, and then double it.

To enlarge icons in system tray, right-click on it (aim for empty space / top pixels / bottom pixels, so that you will not activate icons themselves) → “Properties” → set “Maximum icon size” to 32, 48 or 64.

### Cinnamon

Has good support out of the box.

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

This example uses inaccurate dimensions (423mm x 328mm, even though the Dell XPS 9530 has 346mm x 194mm) to have a clean multiple of 96 dpi, in this case 192 dpi. This tends to work better than using the correct DPI — Pango renders fonts crisper in i3 for example.

If the DPI displayed by xdpyinfo is not correct, see [Xorg#Display size and DPI](/index.php/Xorg#Display_size_and_DPI "Xorg") for how to fix it.

## X Resources

If you are not using a desktop environment such as KDE, Xfce, or other that manipulates the X settings for you, you can set the desired DPI setting manually via the `Xft.dpi` variable in [Xresources](/index.php/Xresources "Xresources"):

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

Since Qt 5.6, Qt 5 applications can be instructed to honor screen DPI by setting the `QT_AUTO_SCREEN_SCALE_FACTOR` environment variable:

```
export QT_AUTO_SCREEN_SCALE_FACTOR=1

```

If automatic detection of DPI does not produce the desired effect, scaling can be set manually per-screen (`QT_SCREEN_SCALE_FACTORS`) or globally (`QT_SCALE_FACTOR`). For more details see the [Qt blog post](https://blog.qt.io/blog/2016/01/26/high-dpi-support-in-qt-5-6/).

**Note:**

*   If you manually set the screen factor, it is important to set `QT_AUTO_SCREEN_SCALE_FACTOR=0` otherwise some applications which explicitly force high DPI enabling get scaled twice.
*   `QT_SCALE_FACTOR` scales fonts, but `QT_SCREEN_SCALE_FACTORS` does not scale fonts.
*   If you also set the font DPI manually in *xrdb* to support other toolkits, `QT_SCALE_FACTORS` will give you huge fonts.
*   If you have multiple screens of differing DPI ie: [HiDPI#Side_display](/index.php/HiDPI#Side_display "HiDPI") you may need to do `QT_SCREEN_SCALE_FACTORS="2;2"`

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

## Boot managers

### GRUB

#### Lower the framebuffer resolution

Set a lower resolution for the framebuffer as explained in [GRUB/Tips and tricks#Setting the framebuffer resolution](/index.php/GRUB/Tips_and_tricks#Setting_the_framebuffer_resolution "GRUB/Tips and tricks").

#### Change GRUB font size

Find a ttf font that you like in `/usr/share/fonts/`.

Convert the font to a format that GRUB can utilize:

```
# grub-mkfont -s 30 -o /boot/grubfont.pf2 /usr/share/fonts/FontFamily/FontName.ttf

```

**Note:** Change the `-s 30` parameter to modify the font size

Edit `/etc/default/grub` to set the new font as shown in [GRUB/Tips and tricks#Background image and bitmap fonts](/index.php/GRUB/Tips_and_tricks#Background_image_and_bitmap_fonts "GRUB/Tips and tricks"):

```
GRUB_FONT="/boot/grubfont.pf2"

```

Update GRUB configuration by running `grub-mkconfig -o /boot/grub/grub.cfg`

## Applications

### Browsers

#### Firefox

Firefox should use the [#GDK 3 (GTK+ 3)](#GDK_3_.28GTK.2B_3.29) settings. However, the suggested `GDK_SCALE` suggestion doesn't consistently scale the entirety of Firefox, and doesn't work for fractional values (e.g., a factor of 158DPI/96DPI = 1.65 for a 1080p 14" laptop). You may want to use `GDK_DPI_SCALE` instead.

To override those, open Firefox advanced preferences page (`about:config`) and set parameter `layout.css.devPixelsPerPx` to `2` (or find the one that suits you better; `2` is a good choice for Retina screens), but it also doesn't consistently scale the entirety of Firefox. If Firefox is not scaling fonts, you may want to create `userChrome.css` and add appropriate styles to it. More information about `userChrome.css` at [mozillaZine](http://kb.mozillazine.org/index.php?title=UserChrome.css).

 `~/.mozilla/firefox/*<profile>*/chrome/userChrome.css` 
```
@namespace url("[http://www.mozilla.org/keymaster/gatekeeper/there.is.only.xul](http://www.mozilla.org/keymaster/gatekeeper/there.is.only.xul)");

/* #tabbrowser-tabs, #navigator-toolbox, menuitem, menu, ... */
* {
    font-size: 15px !important;
}

/* exception for badge on adblocker */
.toolbarbutton-badge {
    font-size: 8px !important;
}

```

If you use a HiDPI monitor such as Retina display together with another monitor, you can use [AutoHiDPI](https://addons.mozilla.org/en-US/firefox/addon/autohidpi/) add-on in order to automatically adjust `layout.css.devPixelsPerPx` setting for the active screen. Also, since Firefox version 49, it auto-scales based on your screen resolution, making it easier to deal with 2 or more screens.

#### Chromium / Google Chrome

Chromium should use the [#GDK 3 (GTK+ 3)](#GDK_3_.28GTK.2B_3.29) settings.

To override those, use the `--force-device-scale-factor` flag with a scaling value. This will scale all content and ui, including tab and font size. For example `chromium --force-device-scale-factor=2`.

Using this option, a scaling factor of 1 would be normal scaling. Floating point values can be used. To make the change permanent, for Chromium, you can add it to `~/.config/chromium-flags.conf`:

 `~/.config/chromium-flags.conf`  `--force-device-scale-factor=2` 

To make this work for Chrome, add the same option to `~/.config/chrome-flags.conf` instead.

If you use a HiDPI monitor such as Retina display together with another monitor, you can use the [reszoom](https://chrome.google.com/webstore/detail/resolution-zoom/enjjhajnmggdgofagbokhmifgnaophmh) extension in order to automatically adjust the zoom level for the active screen.

#### Opera

Opera should use the [#GDK 3 (GTK+ 3)](#GDK_3_.28GTK.2B_3.29) settings.

To override those, use the `--alt-high-dpi-setting=X` command line option, where X is the desired DPI. For example, with `--alt-high-dpi-setting=144` Opera will assume that DPI is 144\. Newer versions of opera will auto detect the DPI using the font DPI setting (in KDE: the force font DPI setting.)

### Thunderbird

See [#Firefox](#Firefox). To access `about:config`, go to Edit → Preferences → Advanced → Config editor.

### Wine applications

Run

```
$ winecfg

```

and change the "dpi" setting found in the "Graphics" tab. This only affects the font size.

### Skype

Skype for Linux ([skypeforlinux-stable-bin](https://aur.archlinux.org/packages/skypeforlinux-stable-bin/) package) uses [#GDK 3 (GTK+ 3)](#GDK_3_.28GTK.2B_3.29).

### Spotify

You can change scale factor by simple `Ctrl++` for zoom in, `Ctrl+-` for zoom out and `Ctrl+0` for default scale. Scaling setting will be saved in `~/.config/spotify/Users/YOUR-SPOTIFY-USER-NAME/prefs`:

 `~/.config/spotify/Users/YOUR-SPOTIFY-USER-NAME/prefs` 
```
app.browser.zoom-level=100

```

Also Spotify can be launched with a custom scaling factor which will be multiplied with setting specified in `~/.config/spotify/Users/YOUR-SPOTIFY-USER-NAME/prefs`, for example

```
$ spotify --force-device-scale-factor=1.5

```

### Zathura document viewer

No modifications required for document viewing.

UI text scaling is specified via [configuration file](https://pwmt.org/projects/zathura/documentation/) (note that "font" is a [girara option](https://pwmt.org/projects/girara/options/)):

```
set font "monospace normal 20"

```

### Sublime Text 3

Sublime Text 3 has full support for display scaling. Go to Preferences > Settings > User Settings and add `"dpi_scale": 2.0` to your settings [(source)](http://blog.wxm.be/2014/08/30/sublime-text-3-and-high-dpi-on-linux.html).

### IntelliJ IDEA

IntelliJ IDEA 15 and above should include HiDPI support.[[1]](http://blog.jetbrains.com/idea/2015/07/intellij-idea-15-eap-comes-with-true-hidpi-support-for-windows-and-linux/) If it does not work, the most convenient way to fix the problem in this case seems to be changing the Override Default Fonts setting:

	*File -> Settings -> Behaviour & Appearance -> Appearance*

The addition of `-Dhidpi=true` to the vmoptions file in either `$HOME/.IdeaC14/` or `/usr/share/intelligj-idea-ultimate-edition/bin/` of [release 14](https://youtrack.jetbrains.com/issue/IDEA-114944) should not be required anymore.

### NetBeans

NetBeans allows the font size of its interface to be controlled using the `--fontsize` parameter during startup. To make this change permanent edit the `/usr/share/netbeans/etc/netbeans.conf` file and append the `--fontsize` parameter to the `netbeans_default_options` property.[[2]](http://wiki.netbeans.org/FaqFontSize)

The editor fontsize can be controlled from Tools → Option → Fonts & Colors.

The output window fontsize can be controlled from Tools → Options → Miscelaneous → Output

### Gimp 2.8

Use a high DPI theme, or adjust `gtkrc` of an existing theme. (Change all occurrences of the size `button` to `dialog`, for example `GimpToolPalette::tool-icon-size`.)

There is also the [gimp-hidpi](https://github.com/jedireza/gimp-hidpi).

### Steam

#### Official HiDPI support

*   Starting on 25 of January 2018 in the beta program there is actual support for HiDPI and it should be automatically detected.
*   Steam -> Settings -> Interface -> check "Enlarge text and icons based on monitor size" (restart required)
*   If it not automatically detected use `GDK_SCALE=2` to set the desired scale factor.

#### Unofficial

The [HiDPI-Steam-Skin](https://github.com/MoriTanosuke/HiDPI-Steam-Skin) can be installed to increase the font size of the interface. While not perfect, it does improve usability.

**Note:** The README for the HiDPI skin lists several possible locations for where to place the skin. The correct folder out of these can be identified by the presence of a file named `skins_readme.txt`.

[MetroSkin Unofficial Patch](http://steamcommunity.com/groups/metroskin/discussions/0/517142253861033946/) also helps with HiDPI on Steam with Linux.

### Java applications

Java applications using the AWT/Swing framework can be scaled by defining the sun.java2d.uiScale variable when invoking java. For example,

```
java -Dsun.java2d.uiScale=2 -jar some_application.jar

```

Since Java 9 the GDK_SCALE environment variable is used to scale Swing applications accordingly.

### Mono applications

According to [[3]](https://bugzilla.xamarin.com/show_bug.cgi?id=35870), Mono applications should be scalable like [GTK3](#GDK_3_.28GTK.2B_3.29) applications.

### MATLAB

Recent versions (R2017b) of [Matlab](/index.php/Matlab "Matlab") allow to set the scale factor:

```
>> s = settings;s.matlab.desktop.DisplayScaleFactor
>> s.matlab.desktop.DisplayScaleFactor.PersonalValue = 2

```

The settings take effect after MATLAB is restarted.

### VirtualBox

**Note:** This ony applies to KDE with scaling enabled.

VirtualBox also applies the system-wide scaling to the virtual monitor, which reduces the maximum resolution inside VMs by your scaling factor (see [[4]](https://www.virtualbox.org/ticket/16604)).

This can be worked around by calculating the inverse of your scaling factor and manually setting this new scaling factor for the VirtualBox execution, e.g.

```
$ QT_SCALE_FACTOR=0.5 VirtualBox --startvm vm-name

```

### Zoom

Zoom can be started with a proper scaling by overriding the `QT_SCALE_FACTOR` environment variable.

```
$ QT_SCALE_FACTOR=2 zoom

```

### Unsupported applications

[run_scaled-git](https://aur.archlinux.org/packages/run_scaled-git/) can be used to scale applications (which uses [xpra](https://www.archlinux.org/packages/?name=xpra) internally).

Another approach is to run the application full screen and without decoration in its own VNC desktop. Then scale the viewer. With Vncdesk ([vncdesk-git](https://aur.archlinux.org/packages/vncdesk-git/) from the [AUR](/index.php/AUR "AUR")) you can set up a desktop per application, then start server and client with a simple command such as `vncdesk 2`.

[x11vnc](/index.php/X11vnc "X11vnc") has an experimental option `-appshare`, which opens one viewer per application window. Perhaps something could be hacked up with that.

## Multiple displays

The HiDPI setting applies to the whole desktop, so non-HiDPI external displays show everything too large. However, note that setting different scaling factors for different monitors is already supported in [Wayland](/index.php/Wayland "Wayland").

### Side display

One workaround is to use [xrandr](/index.php/Xrandr "Xrandr")'s scale option. To have a non-HiDPI monitor (on DP1) right of an internal HiDPI display (eDP1), one could run:

```
xrandr --output eDP-1 --auto --output DP-1 --auto --scale 2x2 --right-of eDP-1

```

When extending above the internal display, you may see part of the internal display on the external monitor. In that case, specify the position manually, e.g. using [this script](https://gist.github.com/wvengen/178642bbc8236c1bdb67).

You may run into problems with your mouse not being able to reach the whole screen. That is a [known bug](https://bugs.freedesktop.org/show_bug.cgi?id=39949) with an xserver-org patch (or try the panning option, but that might cause other problems).

An example of the panning syntax for a 4k laptop with an external 1920x1080 monitor to the right:

```
xrandr --output eDP-1 --auto --output HDMI-1 --auto --panning 3840x2160+3840+0 --scale 2x2 --right-of eDP-1

```

Generically if your HiDPI monitor is AxB pixels and your regular monitor is CxD and you are scaling by [ExF], the commandline for right-of is:

```
xrandr --output eDP-1 --auto --output HDMI-1 --auto --panning [C*E]x[D*F]+[A]+0 --scale [E]x[F] --right-of eDP-1

```

If panning is not a solution for you it may be better to set position of monitors and fix manually the total display screen.

An example of the syntax for a 2560x1440 WQHD 210 DPI laptop monitor (eDP1) using native resolution placed below a 1920x1080 FHD 96 DPI external monitor (HDMI) scaled to match global DPI settings:

```
xrandr --output eDP-1 --auto --pos 0x1458 --output HDMI-1 --scale 1.35x1.35 --auto --pos 0x0 --fb 2592x2898

```

The total screen size (--fb) and positioning (--pos) are to be calculated taking into account the scaling factor.

In this case laptop monitor (eDP1) has no scaling and uses native mode for resolution so it will total 2560x1440, but external monitor (HDMI) is scaled and it has to be considered a larger screen so (1920*1.35)x(1080*1.35) from where the eDP1 Y position came 1080*1.35=1458 and the total screen size: since one on top of the other X=(greater between eDP1 and HDMI, so 1920*1.35=2592) and Y=(sum of the calculated heights of eDP1 and HDMI, so 1440+(1080*1.35)=2898).

Generically if your hidpi monitor is AxB pixels and your regular monitor is CxD and you are scaling by [ExF] and hidpi is placed below regular one, the commandline for right-of is:

```
xrandr --output eDP-1 --auto --pos 0x(DxF) --output HDMI-1 --auto --scale [E]x[F] --pos 0x0 --fb [greater between A and (C*E)]x[B+(D*F)]

```

You may adjust the "sharpness" parameter on your monitor settings to adjust the blur level introduced with scaling.

**Note:** Above solution with `--scale 2x2` does not work on some Nvidia cards. No solution is currently available. [[5]](https://bbs.archlinux.org/viewtopic.php?pid=1670840) A potential workaround exists with configuring `ForceFullCompositionPipeline=On` on the `CurrentMetaMode` via `nvidia-settings`. For more info see [[6]](https://askubuntu.com/a/979551/763549).

### Multiple external monitors

There might be some problems in scaling more than one external monitors which have lower dpi than the built-in HiDPI display. In that case, you may want to try downscaling the HiDPI display instead, with e.g.

```
xrandr --output eDP1 --scale 0.5x0.5 --output DP2 --right-of eDP1 --output HDMI1 --right-of DP2

```

In addition, when you downscale the HiDPI display, the font on the HiDPI display will be slightly blurry, but it's a different kind of bluriness compared with the one introduced by upscaling the external displays. You may compare and see which kind of bluriness is less problematic for you.

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

For UHD to 1080p (3840/1920=2 2160/1080=2)

```
xrandr --output HDMI --scale 2x2

```

You may adjust the "sharpness" parameter on your monitor settings to adjust the blur level introduced with scaling.

## Linux console

The default [Linux console](https://en.wikipedia.org/wiki/Linux_console "w:Linux console") font will be very small on hidpi displays, the largest font present in the [kbd](https://www.archlinux.org/packages/?name=kbd) package is `latarcyrheb-sun32` and other packages like [terminus-font](https://www.archlinux.org/packages/?name=terminus-font) contain further alternatives, such as `ter-132n`(normal) and `ter-132b`(bold). See [Fonts#Console fonts](/index.php/Fonts#Console_fonts "Fonts") for configuration details.

After changing the font, it is often garbled and unreadable when changing to other virtual consoles (`tty2-6`). To fix this you can [force specific mode](/index.php/Kernel_mode_setting#Forcing_modes_and_EDID "Kernel mode setting") for KMS, such as `video=2560x1600@60` (substitute in the native resolution of your HiDPI display), and reboot.

## See also

*   [Ultra HD 4K Linux Graphics Card Testing](http://www.phoronix.com/scan.php?page=article&item=linux_uhd4k_gpus) (Nov 2013)
*   [Understanding pixel density](http://www.eizo.com/library/basics/pixel_density_4k/)