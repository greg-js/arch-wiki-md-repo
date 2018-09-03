Related articles

*   [Font configuration](/index.php/Font_configuration "Font configuration")

HiDPI (High Dots Per Inch) 显示器，指的是在较小尺寸下却拥有较高分辨率的显示器。Apple 将其称作“[视网膜屏幕](https://en.wikipedia.org/wiki/Retina_Display "wikipedia:Retina Display")”，这项技术主要存在于高端笔记本电脑和显示器中。

并非所有的软件都在高分辨率屏幕下工作良好。此页列出了一些常见的调整方法，让您更好的使用 HiDPI 显示器。

## Contents

*   [1 桌面环境](#.E6.A1.8C.E9.9D.A2.E7.8E.AF.E5.A2.83)
    *   [1.1 GNOME](#GNOME)
        *   [1.1.1 非整数倍缩放](#.E9.9D.9E.E6.95.B4.E6.95.B0.E5.80.8D.E7.BC.A9.E6.94.BE)
    *   [1.2 KDE](#KDE)
        *   [1.2.1 非整数倍缩放下的Bug](#.E9.9D.9E.E6.95.B4.E6.95.B0.E5.80.8D.E7.BC.A9.E6.94.BE.E4.B8.8B.E7.9A.84Bug)
        *   [1.2.2 托盘图标不缩放](#.E6.89.98.E7.9B.98.E5.9B.BE.E6.A0.87.E4.B8.8D.E7.BC.A9.E6.94.BE)
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
*   [5 引导程序](#.E5.BC.95.E5.AF.BC.E7.A8.8B.E5.BA.8F)
    *   [5.1 GRUB](#GRUB)
        *   [5.1.1 降低帧缓冲分辨率](#.E9.99.8D.E4.BD.8E.E5.B8.A7.E7.BC.93.E5.86.B2.E5.88.86.E8.BE.A8.E7.8E.87)
        *   [5.1.2 改变GRUB字体大小](#.E6.94.B9.E5.8F.98GRUB.E5.AD.97.E4.BD.93.E5.A4.A7.E5.B0.8F)
*   [6 应用程序](#.E5.BA.94.E7.94.A8.E7.A8.8B.E5.BA.8F)
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

## 桌面环境

### GNOME

可以在**设置** > **设备** > **显示** (Settings > Devices > Displays) 中开启 HiDPI 支持，也可以使用 gsettings 进行设置：

```
$ gsettings set org.gnome.desktop.interface scaling-factor 2

```

**注意:** `scaling-factor`仅能设置为整数。1 = 100%，2 = 200%……等等

#### 非整数倍缩放

在某些设备（例如小平板电脑）上使用 `scaling-factor`设置整数倍缩放的效果可能并不理想。

*   wayland

启用实验性的非整数倍缩放功能：

```
$ gsettings set org.gnome.mutter experimental-features "['scale-monitor-framebuffer']"

```

之后再次打开 **设置** > **设备** > **显示**。

*   xorg

您可以同时使用 `scaling-factor` 和 [xrandr](/index.php/Xrandr "Xrandr") 来实现任意的非整数倍缩放。这可以使 TTF 字体被正确缩放，防止出现单独使用 xrandr 时出现的模糊现象。您可以使用 `gsettings` 来指定放大系数，并用 [xrandr](/index.php/Xrandr "Xrandr") 指定缩小系数。

首先使将缩放设为“UI看起来太大”的最小值。通常“2”已经太大，如果不够大就继续尝试“3”以及更大的数。之后使用 [xrandr](/index.php/Xrandr "Xrandr") 设置缩小系数。首先获取相关的输出名称，下面的例子将使用 `eDP1` 。先试着将缩小系数设为1.25，如果 UI 看起来仍然太大，则增大缩放系数。反之则缩小缩放系数。

```
$ xrandr --output eDP1 --scale 1.25x1.25

```

**注意:** 如果你的鼠标光标移动范围和屏幕显示并不匹配，你可能需要同时使用 `--panning`。参阅[#Side display](#Side_display)。

在GNOME设置守护进程中的xsettings插件中，DPI设置是硬编码的。这将忽略Xorg的设置。这里有一篇[重编译 Gnome Settings Daemon](http://blog.drtebi.com/2012/12/changing-dpi-setting-on-gnome-34.html)的博客文章。在文档中还介绍了另一种方法来设置 xsettings 的DPI：

你可以使用dconf编辑器转到这个键值：

```
/org/gnome/settings-daemon/plugins/xsettings/overrides

```

加入这个条目：

```
'Xft/DPI': <153600>

```

来自 README.xsettings

注意必须使用这种方式指定（使用<>）。

另外，上面的例子中一英寸以1024ths定义。(Note also that DPI in the above example is expressed in 1024ths of an inch.)

### KDE

您可以使用KDE的设置来微调字体、图标和部件缩放，这些改动会同时影响 Qt 和 GTK+ 程序。

要调整整体缩放：

1.  **系统设置**→**显示和监控**→**显示配置**→**缩放显示**
2.  将滑块调整至适合的位置
3.  重新启动以使设置生效

要仅调整字体缩放：

1.  **系统设置**→**字体**
2.  勾选**“固定字体DPI”**并调整DPI的值。调整之后重新启动应用程序即可生效。要在整个桌面上生效，您需要注销之后重新登录。

要仅调整图标缩放：

1.  **系统设置**→**图标**→**配置图标大小**
2.  为每一项选择合适的图标大小，更改将会立即生效。

#### 非整数倍缩放下的Bug

当您使用非整数倍的缩放比例时，这可能导致一些 Qt 应用程序的字体渲染出现问题（例如 okular）。

有一个办法可以绕过这个问题：

1.  将缩放比例设为1
2.  用上面的方法调整字体和图标缩放（这会影响所有的应用程序，且不会导致字体问题）
3.  重新启动KDE
4.  如果需要缩放 GTK 程序，设置环境变量`GDK_SCALE/GDK_DPI_SCALE`（参见下文）。

#### 托盘图标不缩放

托盘图标不会随着整体而缩放。Plasma 默认会忽略 Qt 设置。要让 Plasma 使用 Qt 设置，将`PLASMA_USE_QT_SCALING` 设为1.

### Xfce

打开**设置管理器**→**外观**→**字体**，修改 DPI 的值。在 HiDPI 显示器上，通常可以设为180或者192。要获得更精确的数字，可以使用`xdpyinfo | grep resolution`，使用输出DPI两倍的值。

要增大托盘图标，右键点击托盘的空白处，选择属性，将最大图标大小设置为32,48或者64。

### Cinnamon

应当开箱即用。

### Enlightenment

对于E18，首先打开设置面板，在 **外观**→**缩放** 中，你可以调整缩放倍数。在MBPr 15 上，你可以选择1.2。

## X Server

某些程序使用 X Server 所提供的 DPI 值。比如 i3 （[来源](https://github.com/i3/i3/blob/next/libi3/dpi.c)） 和 Chromium（[来源](https://code.google.com/p/chromium/codesearch#chromium/src/ui/views/widget/desktop_aura/desktop_screen_x11.cc)）。

要验证 X Server 是否正确检测到了您的显示器的DPI，使用 [xorg-xdpyinfo](https://www.archlinux.org/packages/?name=xorg-xdpyinfo) 中的 `xdpyinfo` 工具。

```
$ xdpyinfo | grep -B 2 resolution
screen #0:
  dimensions:    3200x1800 pixels (423x238 millimeters)
  resolution:    192x192 dots per inch

```

这个例子中 X Server 检测到的屏幕尺寸并不准确（423mm x 328mm,实际上Dell XPS 9530的屏幕尺寸是346mm x 194mm），但报告的 DPI 是96的整数倍。通常这往往比正确的DPI更好，可以保证字体渲染正确。

如果 `xdpyinfo` 显示的DPI不正确，参阅[Xorg#Display size and DPI](/index.php/Xorg#Display_size_and_DPI "Xorg")了解如何修复。

## X Resources

如果你没有使用一个桌面环境，比如 KDE，Xfce，或是没有一个为您操作 Xorg 设置的程序，你可以通过在 [Xresources](/index.php/Xresources "Xresources") 中的 `Xft.dpi` 变量手动修改DPI设置。

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

确保设置在X启动时已经被载入。例如在`~/.xinitrc`中使用`xrdb -merge ~/.Xresources`。有关详细信息，请参阅 [Xresources](/index.php/Xresources "Xresources")。

通常这会让大多数地方的字体大小正确，但这并不会影响图标大小。

在设置`Xft.dpi`的同时设置 GUI toolkit 缩放（例如`GDK_SCALE`）可能导致某些程序界面元素过大（例如firefox）。

## GUI toolkits

### Qt 5

自从 Qt 5.6 开始，Qt 5 应用程序可以遵守屏幕DPI。设置环境变量`QT_AUTO_SCREEN_SCALE_FACTOR`以启用这项功能。

```
export QT_AUTO_SCREEN_SCALE_FACTOR=1

```

如果自动检测的 DPI 并不理想，你也可以按屏幕(`QT_SCREEN_SCALE_FACTORS`)或全局(`QT_SCALE_FACTOR`)手动设置缩放，有关详细信息，请参阅 [Qt 博客文章](https://blog.qt.io/blog/2016/01/26/high-dpi-support-in-qt-5-6/)。

**注意:**

*   如果您手动设置了缩放，则需要设置`QT_AUTO_SCREEN_SCALE_FACTOR=0`。否则某些明确启用 HiDPI 支持的程序会被缩放两次。
*   `QT_SCALE_FACTOR`缩放字体，但`QT_SCREEN_SCALE_FACTORS`并不会。
*   如果您还在**xrdb**中手动设置过DPI以支持其他toolkits，同时使用`QT_SCALE_FACTORS`会使字体过大。
*   如果您有多个不同DPI的屏幕，即 [#Side display](#Side_display)，您可能需要设置`QT_SCREEN_SCALE_FACTORS="2;2"`。

### GDK 3 (GTK+ 3)

要将UI缩放为两倍大小：

```
export GDK_SCALE=2

```

并同时不影响字体：

```
export GDK_DPI_SCALE=0.5

```

### GTK+ 2

GTK+ 2本身并不支持缩放UI。但您可以使用 [oomox-git](https://aur.archlinux.org/packages/oomox-git/) 创建预缩放过的主题。

### Elementary (EFL)

要将缩放倍数设为1.5：

```
 export ELM_SCALE=1.5

```

更多信息请查看 [https://phab.enlightenment.org/w/elementary/](https://phab.enlightenment.org/w/elementary/)

## 引导程序

### GRUB

#### 降低帧缓冲分辨率

参见[GRUB/Tips and tricks#Setting the framebuffer resolution](/index.php/GRUB/Tips_and_tricks#Setting_the_framebuffer_resolution "GRUB/Tips and tricks")。

#### 改变GRUB字体大小

在`/usr/share/fonts/`中找一个你喜欢的字体。

使用GRUB工具转换：

```
# grub-mkfont -s 30 -o /boot/grubfont.pf2 /usr/share/fonts/*FontFamily/FontName.ttf*

```

**注意:** `-s 30`是字体大小。

编辑`/etc/default/grub`来设置字体。参见[GRUB/Tips and tricks#Background image and bitmap fonts](/index.php/GRUB/Tips_and_tricks#Background_image_and_bitmap_fonts "GRUB/Tips and tricks"):

```
GRUB_FONT="/boot/grubfont.pf2"

```

使用`grub-mkconfig -o /boot/grub/grub.cfg`重新生成 GRUB 配置。

## 应用程序

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

**Warning:** The following extension is not compatible with Firefox Quantum (version 57 and above).

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