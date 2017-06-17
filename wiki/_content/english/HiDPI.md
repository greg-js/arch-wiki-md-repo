HiDPI (High Dots Per Inch) displays, also known by Apple's "[Retina Display](https://en.wikipedia.org/wiki/Retina_Display "wikipedia:Retina Display")" marketing name, are screens with a high resolution in a relatively small format. They are mostly found in high-end laptops and monitors.

Not all software behaves well in high-resolution mode yet. Here are listed most common tweaks which make work on a HiDPI screen more pleasant.

## Contents

*   [1 Desktop environments](#Desktop_environments)
    *   [1.1 GNOME](#GNOME)
    *   [1.2 KDE](#KDE)
        *   [1.2.1 Using KDE system settings](#Using_KDE_system_settings)
        *   [1.2.2 Tray icons with fixed size](#Tray_icons_with_fixed_size)
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
    *   [6.11 VLC](#VLC)
    *   [6.12 Steam](#Steam)
    *   [6.13 Java applications](#Java_applications)
    *   [6.14 Unsupported applications](#Unsupported_applications)
*   [7 Multiple displays](#Multiple_displays)
    *   [7.1 Side display](#Side_display)
    *   [7.2 Mirroring](#Mirroring)
*   [8 Linux console](#Linux_console)
*   [9 See also](#See_also)

## Desktop environments

### GNOME

To enable HiDPI, use gsettings:

```
$ gsettings set org.gnome.desktop.interface scaling-factor 2

```

**Note:** `scaling-factor` only allows whole numbers to be set. 1 = 100%, 2 = 200%, etc...

A setting of `2, 3, etc`, which is all you can do with `scaling-factor`, may not be ideal for certain HiDPI displays and smaller screens (e.g. small tablets).

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

KDE plasma 5 provides excellent support for HiDPI screens out of the box. You can set the correct DPI by [#Using KDE system settings](#Using_KDE_system_settings). Alternatives are to use [SDDM#DPI settings](/index.php/SDDM#DPI_settings "SDDM") or the [#X Server](#X_Server) (currently not working). However, it seems that Gtk+ applications ignore both SDDM and X settings.

#### Using KDE system settings

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

#### Tray icons with fixed size

If the tray icons are not scaled with the rest of the desktop, the size can be set in the Plasma configuration. System-wide configuration is located in the file `/usr/share/plasma/plasmoids/org.kde.plasma.private.systemtray/contents/config/main.xml`, where the dimension of icons can be controlled by editing the default value for *iconSize* (a value of 2 should be fine):

 `/usr/share/plasma/plasmoids/org.kde.plasma.private.systemtray/contents/config/main.xml` 
```
<entry name="iconSize" type="Int">
    <label>Default icon size for the systray icons, it's an enum which values mean, 
           Small, SmallMedium, Medium, Large, Huge, Enormous respectively. On low 
           DPI systems they correspond to 16, 22, 32, 48, 64, 128 pixels. On high
           DPI systems those values would be scaled up, depending on the DPI.</label>                    
    <default>**2**</default>
</entry>

```

User configuration is located in the file `~/.config/plasma-org.kde.plasma.desktop-appletsrc`. The section containing the settings for the tray bar should look similar to this; if the `iconSize` field is not present, add it.

 `~/.config/plasma-org.kde.plasma.desktop-appletsrc` 
```
[Containments][47][General]
extraItems=org.kde.plasma.mediacontroller,org.kde.plasma.battery,org.kde.plasma.printmanager,org.kde.plasma.bluetooth,org.kde.plasma.clipboard,org.kde.plasma.notifications,org.kde.plasma.networkmanagement,org.kde.plasma.devicenotifier
hiddenItems=org.kde.ktp-contactlist,org.kde.plasma.battery
knownItems=org.kde.plasma.mediacontroller,org.kde.plasma.battery,org.kde.plasma.printmanager,org.kde.plasma.bluetooth,org.kde.plasma.clipboard,org.kde.plasma.notifications,org.kde.plasma.networkmanagement,org.kde.plasma.devicenotifier
shownItems=org.kde.plasma.notifications,org.kde.plasma.clipboard
**iconSize=2**

```

### Xfce

Go to Settings Manager → Appearance → Fonts, and change the DPI parameter. The value of 180 or 192 seems to work well on Retina screens. To get a more precise number, you can use `xdpyinfo | grep resolution`, and then double it.

To enlarge icons in system tray, right-click on it (aim for empty space / top pixels / bottom pixels, so that you will not activate icons themselves) → “Properties” → set “Maximum icon size” to 32, 48 or 64.

### Cinnamon

Supports HiDPI since 2.2\. The support is pretty good (e.g. window borders are correctly sized, which is not the case under Xfce).

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

If you are not using a desktop environment such as KDE, Xfce, or other that manipulates the X settings for you, you can set the desired DPI setting manually via the `Xft.dpi` variable in `~/.Xresources`:

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

If you failed to fix your DPI on your X server, there is a way to get your Qt applications to look good on HiDPI anyway.

Since Qt 5.6, Qt 5 applications can be instructed to disregard faulty screen DPI by setting the `QT_AUTO_SCREEN_SCALE_FACTOR` environment variable, for example by creating a file `/etc/profile.d/qt-hidpi.sh` (Note; this variable is unset in the startkde script, as KDE prefers the solution where the proper DPI was set on the actual X-server).

```
export QT_AUTO_SCREEN_SCALE_FACTOR=1

```

And set the executable bit on it.

If automatic detection of hi-DPI screens does not produce the desired effect, scaling can be set manually per-screen (`QT_SCREEN_SCALE_FACTORS`) or globally (`QT_SCALE_FACTOR`). For more details see the [Qt blog post](https://blog.qt.io/blog/2016/01/26/high-dpi-support-in-qt-5-6/).

Note if you manually set the screen factor, it's important to set QT_AUTO_SCREEN_SCALE_FACTOR=0 otherwise some applications which explicitly force high DPI enabling get scaled twice. This is why KDE disables this way of scaling.

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

## Boot managers

### GRUB

Set a lower resolution for the framebuffer as explained in [GRUB/Tips and tricks#Setting the framebuffer resolution](/index.php/GRUB/Tips_and_tricks#Setting_the_framebuffer_resolution "GRUB/Tips and tricks").

## Applications

### Browsers

#### Firefox

Open Firefox advanced preferences page (`about:config`) and set parameter `layout.css.devPixelsPerPx` to `2` (or find the one that suits you better; `2` is a good choice for Retina screens).

If you use a HiDPI monitor such as Retina display together with another monitor, you can use [AutoHiDPI](https://addons.mozilla.org/en-US/firefox/addon/autohidpi/) add-on in order to automatically adjust `layout.css.devPixelsPerPx` setting for the active screen.

From Firefox version 38 onwards, your system (GTK+ 3.10) settings should be taken into account.[[1]](https://bugzilla.mozilla.org/show_bug.cgi?id=975919)

If the menus and url-bar fonts are still tiny you can create a userChrome.css file for your profile that explicitly sets the font-size. The file needs to be placed in your $HOME/.mozilla/firefox/*.default/chrome/ folder. You likely need to create the chrome folder, do not try to put it in a chrome folder that already exists in another place, that will not work.

The content should be something like following. Please make sure that the namespace part is included as that is important.

```
@namespace url("http://www.mozilla.org/keymaster/gatekeeper/there.is.only.xul"); /* set default namespace to XUL */
* { font-size: 16px !important; }

```

If the preferences pages are still tiny, you should try setting a minimum font size in your preferences -> Content -> Font&Colors -> Advanced.

Also, since Firefox version 49, it auto-scales based on your screen resolution, making it easier to deal with 2 or more screens.

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

The new Skype for Linux Alpha with the [skypeforlinux](https://aur.archlinux.org/packages/skypeforlinux/)) package uses [#GDK 3 (GTK+ 3)](#GDK_3_.28GTK.2B_3.29), and the [skypeforlinux-bin](https://aur.archlinux.org/packages/skypeforlinux-bin/) package uses [#GTK+ 2](#GTK.2B_2).

The old legacy Skype ([skype](https://aur.archlinux.org/packages/skype/)) uses Qt 4, and needs to be configured separately. You cannot change the DPI setting for it, but at least you can change font size. Install [qt4](https://www.archlinux.org/packages/?name=qt4) and run `qtconfig-qt4` to do it.

### Spotify

Spotify can be launched with a custom scaling factor, for example

```
$ spotify --force-device-scale-factor=1.5

```

You can also override Spotify's `.desktop` file. Simply copy the file:

```
$ cp /usr/share/applications/spotify.desktop ~/.local/share/applications/

```

Then edit it and add the `--force-device-scale-factor` option:

```
[Desktop Entry]
Name=Spotify
GenericName=Music Player
Comment=Spotify streaming music client
Icon=spotify-client
Exec=spotify %U --force-device-scale-factor=1.5
TryExec=spotify
Terminal=false
Type=Application
Categories=Audio;Music;Player;AudioVideo;
MimeType=x-scheme-handler/spotify;

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

As of 2017-03-17, the git version [vlc-git](https://aur.archlinux.org/packages/vlc-git/) seems to solve most of the problems.

Qt5 may detect that you have a HiDPI display and if so the video will be played in one corner of the window with lots of black space around it, even in fullscreen. You can start vlc with `QT_AUTO_SCREEN_SCALE_FACTOR=0` to workaround the problem, although the interface elements will be smaller. ([source](https://trac.videolan.org/vlc/ticket/17484))

### Steam

The [HiDPI-Steam-Skin](https://github.com/MoriTanosuke/HiDPI-Steam-Skin) can be installed to increase the font size of the interface. While not perfect, it does improve usability.

**Note:** The README for the HiDPI skin lists several possible locations for where to place the skin. The correct folder out of these can be identified by the presence of a file named `skins_readme.txt`.

[MetroSkin Unofficial Patch](http://steamcommunity.com/groups/metroskin/discussions/0/517142253861033946/) also helps with HiDPI on Steam with Linux.

### Java applications

Java applications using the AWT/Swing framework can be scaled by defining the sun.java2d.uiScale variable when invoking java. For example,

```
java -Dsun.java2d.uiScale=2 -jar some_application.jar

```

### Unsupported applications

[run_scaled-git](https://aur.archlinux.org/packages/run_scaled-git/) can be used to scale applications (which uses [xpra-winswitch](https://aur.archlinux.org/packages/xpra-winswitch/) internally).

Another approach is to run the application full screen and without decoration in its own VNC desktop. Then scale the viewer. With Vncdesk ([vncdesk-git](https://aur.archlinux.org/packages/vncdesk-git/) from the [AUR](/index.php/AUR "AUR")) you can set up a desktop per application, then start server and client with a simple command such as `vncdesk 2`.

[x11vnc](/index.php/X11vnc "X11vnc") has an experimental option `-appshare`, which opens one viewer per application window. Perhaps something could be hacked up with that.

## Multiple displays

The HiDPI setting applies to the whole desktop, so non-HiDPI external displays show everything too large.

### Side display

One workaround is to using [xrandr](/index.php/Xrandr "Xrandr")'s scale option. To have a non-HiDPI monitor (on DP1) right of an internal HiDPI display (eDP1), one could run:

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

**Note:** Above solution with `--scale 2x2` does not work on some Nvidia cards. No solution is currently available.[[4]](https://bbs.archlinux.org/viewtopic.php?pid=1670840)

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