Related articles

*   [Font configuration](/index.php/Font_configuration "Font configuration")

HiDPI (High Dots Per Inch) displays, also known by Apple's "[Retina Display](https://en.wikipedia.org/wiki/Retina_Display "wikipedia:Retina Display")" marketing name, are screens with a high resolution in a relatively small format. They are mostly found in high-end laptops and monitors.

Not all software behaves well in high-resolution mode yet. Here are listed most common tweaks which make work on a HiDPI screen more pleasant.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Desktop environments](#Desktop_environments)
    *   [1.1 GNOME](#GNOME)
        *   [1.1.1 Fractional Scaling](#Fractional_Scaling)
            *   [1.1.1.1 Wayland](#Wayland)
            *   [1.1.1.2 Xorg](#Xorg)
        *   [1.1.2 Text Scaling](#Text_Scaling)
            *   [1.1.2.1 GTK+ vs Gnome Shell elements on Xorg](#GTK+_vs_Gnome_Shell_elements_on_Xorg)
    *   [1.2 KDE Plasma](#KDE_Plasma)
        *   [1.2.1 Tray icons with fixed size](#Tray_icons_with_fixed_size)
    *   [1.3 Xfce](#Xfce)
    *   [1.4 Cinnamon](#Cinnamon)
    *   [1.5 Enlightenment](#Enlightenment)
*   [2 X Resources](#X_Resources)
*   [3 X Server](#X_Server)
*   [4 GUI toolkits](#GUI_toolkits)
    *   [4.1 Qt 5](#Qt_5)
    *   [4.2 GDK 3 (GTK 3)](#GDK_3_(GTK_3))
    *   [4.3 GTK 2](#GTK_2)
    *   [4.4 Elementary (EFL)](#Elementary_(EFL))
*   [5 Boot managers](#Boot_managers)
    *   [5.1 GRUB](#GRUB)
        *   [5.1.1 Lower the framebuffer resolution](#Lower_the_framebuffer_resolution)
        *   [5.1.2 Change GRUB font size](#Change_GRUB_font_size)
    *   [5.2 systemd-boot](#systemd-boot)
*   [6 Applications](#Applications)
    *   [6.1 Atom](#Atom)
    *   [6.2 Browsers](#Browsers)
        *   [6.2.1 Firefox](#Firefox)
        *   [6.2.2 Chromium / Google Chrome](#Chromium_/_Google_Chrome)
        *   [6.2.3 Opera](#Opera)
    *   [6.3 Gimp 2.8](#Gimp_2.8)
    *   [6.4 Inkscape](#Inkscape)
    *   [6.5 IntelliJ IDEA](#IntelliJ_IDEA)
    *   [6.6 Java applications](#Java_applications)
        *   [6.6.1 AWT/Swing](#AWT/Swing)
        *   [6.6.2 JavaFX](#JavaFX)
        *   [6.6.3 Mixed AWT/Swing and JavaFX](#Mixed_AWT/Swing_and_JavaFX)
    *   [6.7 MATLAB](#MATLAB)
    *   [6.8 Mono applications](#Mono_applications)
    *   [6.9 NetBeans](#NetBeans)
    *   [6.10 Skype](#Skype)
    *   [6.11 Slack](#Slack)
    *   [6.12 Spotify](#Spotify)
    *   [6.13 Steam](#Steam)
        *   [6.13.1 Official HiDPI support](#Official_HiDPI_support)
        *   [6.13.2 Unofficial](#Unofficial)
    *   [6.14 Sublime Text 3](#Sublime_Text_3)
    *   [6.15 Thunderbird](#Thunderbird)
    *   [6.16 VirtualBox](#VirtualBox)
    *   [6.17 Wine applications](#Wine_applications)
    *   [6.18 Zathura document viewer](#Zathura_document_viewer)
    *   [6.19 Zoom](#Zoom)
    *   [6.20 Unsupported applications](#Unsupported_applications)
*   [7 Multiple displays](#Multiple_displays)
    *   [7.1 Side display](#Side_display)
    *   [7.2 Multiple external monitors](#Multiple_external_monitors)
    *   [7.3 Mirroring](#Mirroring)
    *   [7.4 Tools](#Tools)
*   [8 Linux console](#Linux_console)
*   [9 See also](#See_also)

## Desktop environments

### GNOME

To enable HiDPI, navigate to *Settings > Devices > Displays > Scale* and choose an appropriate value. Or, use gsettings:

```
$ gsettings set org.gnome.settings-daemon.plugins.xsettings overrides "[{'Gdk/WindowScalingFactor', <2>}]"
$ gsettings set org.gnome.desktop.interface scaling-factor 2

```

**Note:** GNOME only allows integer scaling numbers to be set. 1 = 100%, 2 = 200%, etc. See Fractional Scaling below.

#### Fractional Scaling

A setting of `2, 3, etc`, which is all you can do with `scaling-factor`, may not be ideal for certain HiDPI displays and smaller screens (e.g. small tablets). Fractional scaling is possible on both Wayland and Xorg, though the process differs.

##### Wayland

Enable the experimental fractional scaling feature:

```
$ gsettings set org.gnome.mutter experimental-features "['scale-monitor-framebuffer']"

```

then open *Settings > Devices > Displays* (the new options may only appear after a restart).

##### Xorg

You can achieve any non-integer scale factor by using a combination of GNOME's `scaling-factor` and [xrandr](/index.php/Xrandr "Xrandr"). This combination keeps the TTF fonts properly scaled so that they do not become blurry if using `xrandr` alone. You specify zoom-in factor with `gsettings` and zoom-out factor with [xrandr](/index.php/Xrandr "Xrandr").

First scale GNOME up to the minimum size which is too big. Usually "2" is already too big, otherwise try "3" etc. Then start scaling down by setting zoom-out factor with [xrandr](/index.php/Xrandr "Xrandr"). First get the relevant output name, the examples below use `eDP1`. Start e.g. with zoom-out 1.25 times. If the UI is still too big, increase the scale factor; if it is too small decrease the scale factor.

```
$ xrandr --output eDP1 --scale 1.25x1.25

```

**Note:** To allow the mouse to reach the whole screen, you may need to use the `--panning` option as explained in [#Side display](#Side_display).

GNOME ignores X settings due to its xsettings Plugin in Gnome Settings Daemon, where DPI setting is hard coded. There is blog entry for [recompiling Gnome Settings Daemon](http://blog.drtebi.com/2012/12/changing-dpi-setting-on-gnome-34.html). In the source documentation there is another way mentioned to set X settings DPI:

You can use the gsettings, just make sure to read previous setting first and merge it. In just simply set it with this command:

```
gsettings set org.gnome.settings-daemon.plugins.xsettings overrides "{'Xft/DPI': <153600>}"

```

From README.xsettings

Noting that variants must be specified in the usual way (wrapped in <>).

Note also that DPI in the above example is expressed in 1024ths of an inch.

#### Text Scaling

Alternatively, or in addition to changing the display scaling, you can separately scale text. This can be done by navigating to *Fonts > Scaling Factor* in Gnome Tweaks, or using gsettings. Note that the text scaling factor need not be limited to whole integers, for example:

```
$ gsettings set org.gnome.desktop.interface text-scaling-factor 1.5

```

##### GTK+ vs Gnome Shell elements on Xorg

Adjusting the text scaling as per the above only affects GTK+ elements of the GNOME desktop. This should cover everything on Wayland. However, those on an Xorg session may find that they need to make further adjustments on HiDPI environments, since the GNOME Shell UI (including the top bar, dock, application menus, etc.) relies separately on the [St](/index.php/St "St") toolkit. Note that this is a long-standing issue to which a recent patch has been submitted.[[1]](https://gitlab.gnome.org/GNOME/gnome-shell/merge_requests/486) However, as of October 2019, the proposed patch has yet to be merged with the main GNOME codebase. In the interim, Xorg users can resolve most of the Gnome shell scaling problems by manually editing the shell theme that they are currently using. The relevant CSS files are normally located at `/usr/share/themes/YOUR-THEME/gnome-shell/gnome-shell.css`. Users should increase all "font-size" elements in this file in proportion to their display scaling (doubling font sizes for 200% scaling, etc.) For example, the top of an edited CSS file for the [Adapta](https://github.com/adapta-project/adapta-gtk-theme) shell theme might look like:

 `usr/share/themes/Adapta/gnome-shell/gnome-shell.css`  `stage { font-size: 20pt; font-family: Roboto, Noto Sans, Sans-Serif; color: #263238; }` 

Once these changes have been saved, activate them by switching to another theme (for example, using [gnome-tweaks](https://www.archlinux.org/packages/?name=gnome-tweaks)) and then reverting back again. The top bar, application menus, calendar, and other shell elements should now be correctly scaled.

In addition to editing the relevant shell theme's CSS file, users on Xorg may also wish to increase the title bar font at the top of open applications. This can be done through the dconf editor (`org > gnome > desktop > wm > preferences :: titlebar-font`). Note that the `title-bar-uses-system-fonts` option should also be turned off. Alternatively, use gsettings:

```
$ gsettings set org.gnome.desktop.wm.preferences titlebar-font 'Cantarell Bold 22' ## Change as needed
$ gsettings set org.gnome.desktop.wm.preferences titlebar-uses-system-font false

```

### KDE Plasma

You can use Plasma's settings to fine tune font, icon, and widget scaling. This solution affects both Qt and GTK applications.

To adjust font, widget, and icon scaling together:

1.  *System Settings > Display and Monitor > Display Configuration > Scale Display*
2.  Drag the slider to the desired size
3.  Restart for the settings to take effect

To adjust only font scaling:

1.  *System Settings > Fonts*
2.  Check "Force fonts DPI" and adjust the DPI level to the desired value. This setting should take effect immediately for newly started applications. You will have to logout and login for it to take effect on Plasma desktop.

To adjust only icon scaling:

1.  *System Settings > Icons > Advanced*
2.  Choose the desired icon size for each category listed. This should take effect immediately.

**Display Scale not integer bug**

When using not integer values for Display Scale it may causes font render issue in some Qt application. A workaround for this is to:

1.  Set the scale value to `1`
2.  Adjust your font and icons and use the "Force fonts DPI" ( this affects all apps, also GTK but not create issue with the fonts )
3.  Restart Plasma
4.  If required tune the GTK apps using the variables `GDK_SCALE`/`GDK_DPI_SCALE` (as described above)

#### Tray icons with fixed size

The tray icons are not scaled with the rest of the desktop, since Plasma ignores the Qt scaling settings by default. To make Plasma respect the Qt settings, set `PLASMA_USE_QT_SCALING` to `1`.

### Xfce

Xfce supports HiDPI scaling which can be enabled using the settings manager:

1.  Go to *Settings Manager > Appearance > Settings > Window Scaling* and select 2 as the scaling factor.
2.  Go to *Settings Manager > Window Manager > Style* and select `Default-xhdpi` theme.

Alternatively, it is possible to do the same from command line using `xfconf-query`:

```
xfconf-query -c xsettings -p /Gdk/WindowScalingFactor -s 2
xfconf-query -c xfwm4 -p /general/theme -s Default-xhdpi

```

The steps above would set 2x scaled resolution for Xfce and other GTK 3 apps.

Scaling for Qt 5 apps should be set manually, see [#Qt 5](#Qt_5).

### Cinnamon

Has good support out of the box.

### Enlightenment

For E18, go to the E Setting panel. In *Look > Scaling*, you can control the UI scaling ratios. A ratio of 1.2 seems to work well for the native resolution of the MBPr 15" screen.

## X Resources

If you are not using a desktop environment such as KDE, Xfce, or other that manipulates the X settings for you, you can set the desired DPI setting manually via the `Xft.dpi` variable in [Xresources](/index.php/Xresources "Xresources"):

 `~/.Xresources` 
```
Xft.dpi: 192

! These might also be useful depending on your monitor and personal preference:
Xft.autohint: 0
Xft.lcdfilter:  lcddefault
Xft.hintstyle:  hintfull
Xft.hinting: 1
Xft.antialias: 1
Xft.rgba: rgb
```

For `Xft.dpi`, using integer multiples of 96 usually works best, e.g. 192 for 200% scaling.

Make sure the settings are loaded properly when X starts, for instance in your `~/.xinitrc` with `xrdb -merge ~/.Xresources` (see [Xresources](/index.php/Xresources "Xresources") for more information).

This will make the font render properly in most toolkits and applications, it will however not affect things such as icon size! Setting `Xft.dpi` at the same time as toolkit scale (e.g. `GDK_SCALE`) may cause interface elements to be much larger than intended in some programs like firefox.

## X Server

Some programs may still interpret the DPI given by the X server (most interpret X Resources, though, directly or indirectly). Older versions of i3 (before 2017) and Chromium (before 2017) used to do this.

To verify that the X Server has properly detected the physical dimensions of your monitor, use the *xdpyinfo* utility from the [xorg-xdpyinfo](https://www.archlinux.org/packages/?name=xorg-xdpyinfo) package:

 `$ xdpyinfo | grep -B 2 resolution` 
```
screen #0:
  dimensions:    3200x1800 pixels (423x238 millimeters)
  resolution:    192x192 dots per inch

```

This example uses inaccurate dimensions (423mm x 328mm, even though the Dell XPS 9530 has 346mm x 194mm) to have a clean multiple of 96 dpi, in this case 192 dpi. This tends to work better than using the correct DPI — Pango renders fonts crisper in i3 for example.

If the DPI displayed by xdpyinfo is not correct, see [Xorg#Display size and DPI](/index.php/Xorg#Display_size_and_DPI "Xorg") for how to fix it.

## GUI toolkits

### Qt 5

Since Qt 5.6, Qt 5 applications can be instructed to honor screen DPI by setting the `QT_AUTO_SCREEN_SCALE_FACTOR` environment variable:

```
export QT_AUTO_SCREEN_SCALE_FACTOR=1

```

If automatic detection of DPI does not produce the desired effect, scaling can be set manually per-screen (`QT_SCREEN_SCALE_FACTORS`) or globally (`QT_SCALE_FACTOR`). For more details see the [Qt blog post](https://blog.qt.io/blog/2016/01/26/high-dpi-support-in-qt-5-6/) or [Qt developer documentation](https://doc.qt.io/qt-5/highdpi.html).

**Note:**

*   If you manually set the screen factor, it is important to set `QT_AUTO_SCREEN_SCALE_FACTOR=0` otherwise some applications which explicitly force high DPI enabling get scaled twice.
*   `QT_SCALE_FACTOR` scales fonts, but `QT_SCREEN_SCALE_FACTORS` does not scale fonts.
*   If you also set the font DPI manually in *xrdb* to support other toolkits, `QT_SCALE_FACTORS` will give you huge fonts.
*   If you have multiple screens of differing DPI ie: [#Side display](#Side_display) you may need to do `QT_SCREEN_SCALE_FACTORS="2;2"`

An [alternative](https://bugreports.qt.io/browse/QTBUG-53022) is e.g.:

```
QT_FONT_DPI=96 vym

```

### GDK 3 (GTK 3)

**Note:** As stated in the [#X Resources](#X_Resources) section, if you have xft.dpi set to a larger dpi, it will make other scales larger than usual, including GDK.

Setting the GDK scale will scale the UI, however it will not scale icons. If you are using a minimal window manager where you are setting the dpi via Xft.dpi, GDK should scale perfectly fine with it. In other cases, do the following:

To scale UI elements by a factor of two:

```
export GDK_SCALE=2

```

To undo scaling of text:

```
export GDK_DPI_SCALE=0.5

```

### GTK 2

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

### systemd-boot

Adding the following line and running `bootctl update` increases font-size in the [systemd-boot](/index.php/Systemd-boot#Loader_configuration "Systemd-boot") menu:

 `/boot/loader/loader.conf`  `console-mode 1` 

## Applications

As a general rule, applications can be launched with a custom scaling value, e.g. `$ atom --force-device-scale-factor=2`. A more permanent solution is to add this scaling factor as a flag to the relevant .conf or .desktop file (normally located at `/usr/share/applications/`). In the latter instance, the flag should be added to the line beginning with "Exec=", e.g. `Exec=/usr/bin/atom --force-device-scale-factor=2 %F`. The next section provides more details on implementing this for specific applications.

### Atom

Add `--force-device-scale-factor=2` as a flag to the atom.desktop file:

 `/usr/share/applications/atom.desktop`  `Exec=/usr/bin/atom --force-device-scale-factor=2 %F` 

### Browsers

#### Firefox

Firefox should use the [#GDK 3 (GTK 3)](#GDK_3_(GTK_3)) settings. However, the suggested `GDK_SCALE` suggestion does not consistently scale the entirety of Firefox, and does not work for fractional values (e.g., a factor of 158DPI/96DPI = 1.65 for a 1080p 14" laptop). You may want to use `GDK_DPI_SCALE` instead. Another option, which will avoid Firefox-specific settings in many setups is to use the settings in [#X Resources](#X_Resources) as Firefox should respect the `Xft.dpi` value defined there.

To override those, open Firefox advanced preferences page (`about:config`) and set parameter `layout.css.devPixelsPerPx` to `2` (or find the one that suits you better; `2` is a good choice for Retina screens), but it also does not consistently scale the entirety of Firefox. If Firefox is not scaling fonts, you may want to create `userChrome.css` and add appropriate styles to it. More information about `userChrome.css` at [mozillaZine](http://kb.mozillazine.org/index.php?title=UserChrome.css).

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

**Warning:** The AutoHiDPI extension is not compatible with Firefox Quantum (version 57 and above).

If you use a HiDPI monitor such as Retina display together with another monitor, you can use [AutoHiDPI](https://addons.mozilla.org/en-US/firefox/addon/autohidpi/) add-on in order to automatically adjust `layout.css.devPixelsPerPx` setting for the active screen. Also, since Firefox version 49, it auto-scales based on your screen resolution, making it easier to deal with 2 or more screens. For users of Firefox version 57 and above, the [ffreszoom](https://addons.mozilla.org/firefox/addon/ffreszoom/) add-on will adjust the page zoom if it detects you are using a large monitor (zoom level and threshold are configurable). Modifying the internal CSS DPI setting from an extension is currently unsupported [[2]](https://bugzilla.mozilla.org/show_bug.cgi?id=1373607).

If you use Wayland, see [Firefox#Wayland](/index.php/Firefox#Wayland "Firefox") for instructions to enable the optional Wayland backend on [firefox](https://www.archlinux.org/packages/?name=firefox). This is also appicable to [thunderbird](https://www.archlinux.org/packages/?name=thunderbird).

You can also use the Wayland-enabled packages of Firefox from the AUR: [firefox-wayland](https://aur.archlinux.org/packages/firefox-wayland/) (compiles from source) or [fedora-firefox-wayland-bin](https://aur.archlinux.org/packages/fedora-firefox-wayland-bin/) (binary from Fedora). You might experience some minor visual glitches with these packages.

#### Chromium / Google Chrome

Chromium should use the [#GDK 3 (GTK 3)](#GDK_3_(GTK_3)) settings.

To override those, use the `--force-device-scale-factor` flag with a scaling value. This will scale all content and ui, including tab and font size. For example `chromium --force-device-scale-factor=2`.

Using this option, a scaling factor of 1 would be normal scaling. Floating point values can be used. To make the change permanent, for Chromium, you can add it to `~/.config/chromium-flags.conf`:

 `~/.config/chromium-flags.conf`  `--force-device-scale-factor=2` 

To make this work for Chrome, add the same option to `~/.config/chrome-flags.conf` instead.

If you use a HiDPI monitor such as Retina display together with another monitor, you can use the [reszoom](https://chrome.google.com/webstore/detail/resolution-zoom/enjjhajnmggdgofagbokhmifgnaophmh) extension in order to automatically adjust the zoom level for the active screen.

#### Opera

Opera should use the [#GDK 3 (GTK 3)](#GDK_3_(GTK_3)) settings.

To override those, use the `--alt-high-dpi-setting=X` command line option, where X is the desired DPI. For example, with `--alt-high-dpi-setting=144` Opera will assume that DPI is 144\. Newer versions of opera will auto detect the DPI using the font DPI setting (in KDE: the force font DPI setting.)

### Gimp 2.8

Use a high DPI theme, or adjust `gtkrc` of an existing theme. (Change all occurrences of the size `button` to `dialog`, for example `GimpToolPalette::tool-icon-size`.)

There is also the [gimp-hidpi](https://github.com/jedireza/gimp-hidpi).

### Inkscape

To scale the icons to a "usable" size go to *Preferences > Interface* and set the icon size to Large or Larger[[3]](http://www.inkscapeforum.com/viewtopic.php?t=18684)[[4]](http://wiki.inkscape.org/wiki/index.php/HiDPI).

### IntelliJ IDEA

IntelliJ IDEA 15 and above should include HiDPI support.[[5]](http://blog.jetbrains.com/idea/2015/07/intellij-idea-15-eap-comes-with-true-hidpi-support-for-windows-and-linux/) If it does not work, the most convenient way to fix the problem in this case seems to be changing the Override Default Fonts setting:

	*File > Settings > Behaviour & Appearance > Appearance*

The addition of `-Dhidpi=true` to the vmoptions file in either `$HOME/.IdeaC14/` or `/usr/share/intelligj-idea-ultimate-edition/bin/` of [release 14](https://youtrack.jetbrains.com/issue/IDEA-114944) should not be required anymore.

### Java applications

#### AWT/Swing

Java applications using the *AWT/Swing* framework can be scaled by defining the `sun.java2d.uiScale` VM property when invoking `java`. The value can be an integer percentage value, or a float value. For example,

```
java -Dsun.java2d.uiScale=2 -jar some_swing_application.jar
java -Dsun.java2d.uiScale=300% -jar some_swing_application.jar

```

Since Java 9 the `GDK_SCALE` environment variable is used to scale Swing applications accordingly.

Note that at this point, Java *AWT/Swing* (up to including OpenJDK 13) only effectively supports integer values. A setting of `-Dsun.java2d.uiScale=250%` or `GDK_SCALE=2.5` will be treated as if it were set to `-Dsun.java2d.uiScale=2` resp. `GDK_SCALE=2`.

#### JavaFX

Java applications using *JavaFX* can be scaled by defining the `glass.gtk.uiScale` VM property when invoking `java`. The value can be an integer percentage value, an integer DPI value (where `96dpi` represents a scale factor of `100%`, and for example `192dpi` represents a scale factor of `200%`), or a float value. For example,

```
java -Dglass.gtk.uiScale=200% -jar some_jfx_application.jar
java -Dglass.gtk.uiScale=192dpi -jar some_jfx_application.jar
java -Dglass.gtk.uiScale=2.0 -jar some_jfx_application.jar

```

*JavaFX* perfectly well supports fractions. Using values like `-Dglass.gtk.uiScale=250%` or `-Dglass.gtk.uiScale=2.5` will deliver the expected result.

#### Mixed AWT/Swing and JavaFX

Some Java applications mix *JavaFX* and *AWT/Swing* (via `javafx.embed.swing.JFXPanel`). In that case, the settings for *AWT/Swing* will also affect *JavaFX*, and setting `-Dglass.gtk.uiScale` will have no effect.

### MATLAB

Recent versions (R2017b) of [MATLAB](/index.php/MATLAB "MATLAB") allow to set the scale factor[[6]](https://www.mathworks.com/matlabcentral/answers/406956-does-matlab-support-high-dpi-screens-on-linux):

```
>> s = settings;s.matlab.desktop.DisplayScaleFactor
>> s.matlab.desktop.DisplayScaleFactor.PersonalValue = 2

```

The settings take effect after MATLAB is restarted.

### Mono applications

According to [[7]](https://bugzilla.xamarin.com/show_bug.cgi?id=35870), Mono applications should be scalable like [GTK 3](#GDK_3_(GTK_3)) applications.

### NetBeans

NetBeans allows the font size of its interface to be controlled using the `--fontsize` parameter during startup. To make this change permanent edit the `/usr/share/netbeans/etc/netbeans.conf` file and append the `--fontsize` parameter to the `netbeans_default_options` property.[[8]](http://wiki.netbeans.org/FaqFontSize)

The editor fontsize can be controlled from *Tools > Option > Fonts & Colors*.

The output window fontsize can be controlled from *Tools > Options > Miscelaneous > Output*

### Skype

Skype for Linux ([skypeforlinux-stable-bin](https://aur.archlinux.org/packages/skypeforlinux-stable-bin/) package) uses [#GDK 3 (GTK 3)](#GDK_3_(GTK_3)).

### Slack

Slack ([slack-desktop](https://aur.archlinux.org/packages/slack-desktop/)), like all [Electron](https://electronjs.org/) apps, can be configured to use a custom scaling value by adding a `--force-device-scale-factor` flag to the .desktop file. This is normally located at `/usr/share/applications/`. The flag should be added to the line beginning with "Exec=". For example:

 `/usr/share/applications/slack.desktop`  `Exec=env LD_PRELOAD=/usr/lib/libcurl.so.3 /usr/bin/slack --force-device-scale-factor=1.5 %U` 

### Spotify

You can change scale factor by simple `Ctrl++` for zoom in, `Ctrl+-` for zoom out and `Ctrl+0` for default scale. Scaling setting will be saved in `~/.config/spotify/Users/YOUR-SPOTIFY-USER-NAME/prefs`, you may have to create this file by yourself:

 `~/.config/spotify/Users/YOUR-SPOTIFY-USER-NAME/prefs`  `app.browser.zoom-level=100` 

Also Spotify can be launched with a custom scaling factor which will be multiplied with setting specified in `~/.config/spotify/Users/YOUR-SPOTIFY-USER-NAME/prefs`, for example

```
$ spotify --force-device-scale-factor=1.5

```

### Steam

#### Official HiDPI support

*   Starting on 25 of January 2018 in the beta program there is actual support for HiDPI and it should be automatically detected.
*   *Steam > Settings > Interface*, check "Enlarge text and icons based on monitor size" (restart required)
*   If it not automatically detected use `GDK_SCALE=2` to set the desired scale factor.

#### Unofficial

The [HiDPI-Steam-Skin](https://github.com/MoriTanosuke/HiDPI-Steam-Skin) can be installed to increase the font size of the interface. While not perfect, it does improve usability.

**Note:** The README for the HiDPI skin lists several possible locations for where to place the skin. The correct folder out of these can be identified by the presence of a file named `skins_readme.txt`.

[MetroSkin Unofficial Patch](http://steamcommunity.com/groups/metroskin/discussions/0/517142253861033946/) also helps with HiDPI on Steam with Linux.

### Sublime Text 3

Sublime Text 3 has full support for display scaling. Go to *Preferences > Settings > User Settings* and add `"ui_scale": 2.0` to your settings.

### Thunderbird

See [#Firefox](#Firefox). To access `about:config`, go to *Edit > Preferences > Advanced >Config editor*.

### VirtualBox

**Note:** This only applies to KDE with scaling enabled.

VirtualBox also applies the system-wide scaling to the virtual monitor, which reduces the maximum resolution inside VMs by your scaling factor (see [[9]](https://www.virtualbox.org/ticket/16604)).

This can be worked around by calculating the inverse of your scaling factor and manually setting this new scaling factor for the VirtualBox execution, e.g.

```
$ QT_SCALE_FACTOR=0.5 VirtualBox --startvm vm-name

```

### Wine applications

Run

```
$ winecfg

```

and change the "dpi" setting found in the "Graphics" tab. This only affects the font size.

### Zathura document viewer

No modifications required for document viewing.

UI text scaling is specified via [configuration file](https://pwmt.org/projects/zathura/documentation/) (note that "font" is a [girara option](https://pwmt.org/projects/girara/options/)):

```
set font "monospace normal 20"

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
$ xrandr --output eDP-1 --auto --output DP-1 --auto --scale 2x2 --right-of eDP-1

```

When extending above the internal display, you may see part of the internal display on the external monitor. In that case, specify the position manually.

You may adjust the "sharpness" parameter on your monitor settings to adjust the blur level introduced with scaling.

**Note:** Above solution with `--scale 2x2` does not work on some Nvidia cards. No solution is currently available. [[10]](https://bbs.archlinux.org/viewtopic.php?pid=1670840) A potential workaround exists with configuring `ForceFullCompositionPipeline=On` on the `CurrentMetaMode` via `nvidia-settings`. For more info see [[11]](https://askubuntu.com/a/979551/763549).

**Note:** If you are using the `modesetting` driver you will get mouse flickering. This can be solved by scaling your non-scaled screen by 0.9999x0.9999.

### Multiple external monitors

There might be some problems in scaling more than one external monitors which have lower dpi than the built-in HiDPI display. In that case, you may want to try downscaling the HiDPI display instead, with e.g.

```
$ xrandr --output eDP1 --scale 0.5x0.5 --output DP2 --right-of eDP1 --output HDMI1 --right-of DP2

```

In addition, when you downscale the HiDPI display, the font on the HiDPI display will be slightly blurry, but it's a different kind of bluriness compared with the one introduced by upscaling the external displays. You may compare and see which kind of bluriness is less problematic for you.

### Mirroring

If all you want is to mirror ("unify") displays, this is easy as well:

With AxB your native HiDPI resolution (for ex 3200x1800) and CxD your external screen resolution (e.g. 1920x1200)

```
$ xrandr --output HDMI --scale [A/C]x[B/D]

```

In this example which is QHD (3200/1920 = 1.66 and 1800/1200 = 1.5)

```
$ xrandr --output HDMI --scale 1.66x1.5

```

For UHD to 1080p (3840/1920=2 2160/1080=2)

```
$ xrandr --output HDMI --scale 2x2

```

You may adjust the "sharpness" parameter on your monitor settings to adjust the blur level introduced with scaling.

### Tools

There are several tools which automate the commands described above.

*   [This script](https://gist.github.com/wvengen/178642bbc8236c1bdb67) extend a non-HiDPI external display above a HiDPI internal display.
*   [xrandr-extend](https://github.com/ashwinvis/xrandr-extend).
*   [xlayoutdisplay](https://aur.archlinux.org/packages/xlayoutdisplay/) is a CLI front end for xrandr which detects and sets correct DPI: [README](https://github.com/alex-courtis/xlayoutdisplay)

## Linux console

The default [Linux console](https://en.wikipedia.org/wiki/Linux_console "w:Linux console") font will be very small on HiDPI displays, the largest font present in the [kbd](https://www.archlinux.org/packages/?name=kbd) package is `latarcyrheb-sun32` and other packages like [terminus-font](https://www.archlinux.org/packages/?name=terminus-font) contain further alternatives, such as `ter-132n` (normal) and `ter-132b` (bold). See [Linux console#Fonts](/index.php/Linux_console#Fonts "Linux console") for configuration details. Also see [Linux console#Persistent configuration](/index.php/Linux_console#Persistent_configuration "Linux console") in particular for applying the font setting during the early userspace boot sequence.

After changing the font, it is often garbled and unreadable when changing to other virtual consoles (`tty2-6`). To fix this you can [force specific mode](/index.php/Kernel_mode_setting#Forcing_modes_and_EDID "Kernel mode setting") for KMS, such as `video=2560x1600@60` (substitute in the native resolution of your HiDPI display), and reboot.

Users booting though [UEFI](/index.php/UEFI "UEFI") may experience the console and [boot loader](/index.php/Boot_loader "Boot loader") being constrained to a low resolution despite correct [KMS](/index.php/KMS "KMS") settings being set. This can be caused by legacy/BIOS boot being enabled in UEFI settings. Disabling legacy boot to bypass the compatibility layer should allow the system to boot at the correct resolution.

To make early Linux boot stages use a large font, one can set `CONFIG_FONT_TER16x32=y` in the kernel build configuration, and make Linux use it by default by passing `fbcon=font:TER16x32` on the kernel command line.

## See also

*   [Ultra HD 4K Linux Graphics Card Testing](http://www.phoronix.com/scan.php?page=article&item=linux_uhd4k_gpus) (Nov 2013)
*   [Understanding pixel density](http://www.eizo.com/library/basics/pixel_density_4k/)
*   [Mixed DPI and the X Window System](http://wok.oblomov.eu/tecnologia/mixed-dpi-x11/)