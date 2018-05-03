相关文章

*   [Kernel Mode Setting (简体中文)](/index.php/Kernel_Mode_Setting_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Kernel Mode Setting (简体中文)")
*   [Xorg](/index.php/Xorg_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Xorg (简体中文)")

**翻译状态：** 本文是英文页面 [Wayland](/index.php/Wayland "Wayland") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2015-11-06，点击[这里](https://wiki.archlinux.org/index.php?title=Wayland&diff=0&oldid=408148)可以查看翻译后英文页面的改动。

**Wayland** 是 Linux 的一个新的图形接口协议。使用 Wayland 需要更改或重新安装一部分系统中的软件。更多关于 Wayland 的信息参见 [主页](http://wayland.freedesktop.org/)。

## Contents

*   [1 系统需求](#.E7.B3.BB.E7.BB.9F.E9.9C.80.E6.B1.82)
*   [2 安装](#.E5.AE.89.E8.A3.85)
*   [3 使用](#.E4.BD.BF.E7.94.A8)
*   [4 Weston](#Weston)
    *   [4.1 安装](#.E5.AE.89.E8.A3.85_2)
    *   [4.2 使用](#.E4.BD.BF.E7.94.A8_2)
    *   [4.3 配置](#.E9.85.8D.E7.BD.AE)
        *   [4.3.1 XWayland](#XWayland)
        *   [4.3.2 视频录制](#.E8.A7.86.E9.A2.91.E5.BD.95.E5.88.B6)
        *   [4.3.3 高DPI显示器](#.E9.AB.98DPI.E6.98.BE.E7.A4.BA.E5.99.A8)
        *   [4.3.4 Shell font](#Shell_font)
*   [5 图形库](#.E5.9B.BE.E5.BD.A2.E5.BA.93)
    *   [5.1 GTK+ 3](#GTK.2B_3)
    *   [5.2 Qt5](#Qt5)
    *   [5.3 Clutter](#Clutter)
    *   [5.4 SDL](#SDL)
    *   [5.5 GLFW](#GLFW)
    *   [5.6 EFL](#EFL)
*   [6 窗口管理器和桌面 shell](#.E7.AA.97.E5.8F.A3.E7.AE.A1.E7.90.86.E5.99.A8.E5.92.8C.E6.A1.8C.E9.9D.A2_shell)
*   [7 疑难解答](#.E7.96.91.E9.9A.BE.E8.A7.A3.E7.AD.94)
    *   [7.1 LLVM assertion failure](#LLVM_assertion_failure)
    *   [7.2 Weston fails to launch after update to 1.7](#Weston_fails_to_launch_after_update_to_1.7)
*   [8 参阅](#.E5.8F.82.E9.98.85)

## 系统需求

目前 Wayland 只能在使用了 [KMS](/index.php/Kernel_mode_setting_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Kernel mode setting (简体中文)") 的系统上工作。

## 安装

**注意:** Wayland 应该已经作为[gtk2](https://www.archlinux.org/packages/?name=gtk2)和[gtk3](https://www.archlinux.org/packages/?name=gtk3)的依赖安装到系统里面

如果没有，可以从 [官方软件仓库](/index.php/Official_repositories "Official repositories") 安装软件包[wayland](https://www.archlinux.org/packages/?name=wayland)。

## 使用

Wayland 仅仅是一个库，无法单独工作。若要代替X server,需要有混合器(如weston)

## Weston

### 安装

[安装](/index.php/Help:Reading_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E5.AE.89.E8.A3.85.E8.BD.AF.E4.BB.B6.E5.8C.85 "Help:Reading (简体中文)") [weston](https://www.archlinux.org/packages/?name=weston) 包

### 使用

安装完了 Wayland 及它所依赖的包之后，就可以开始试用了。运行：

```
 $ weston

```

或者，要试着运行Weston本身，切换到终端并运行:

```
 $ weston-launch

```

接下来你就可以在 TTY 下打开 wayland 的终端：

```
$ weston-terminal

```

在屏幕上移动一朵花儿，用以测试帧控制功能：

```
$ weston-flower 

```

在 Wayland 上运行 glxgears 程序：

```
$ weston-gears 

```

显示图片：

```
$ weston-image image1.jpg image2.jpg...

```

### 配置

键盘布局，模块的选择，UI的修改的示例配置文件，请参阅[weston.ini(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/weston.ini.5)

 `~/.config/weston.ini` 
```
[core]
### uncomment this line for xwayland support ###
#modules=xwayland.so

[shell]
background-image=/usr/share/backgrounds/gnome/Aqua.jpg
background-color=0xff002244
panel-color=0x90ff0000
locking=true
animation=zoom
#binding-modifier=ctrl
#num-workspaces=6
### for cursor themes install xcursor-themes pkg from Extra. ###
#cursor-theme=whiteglass
#cursor-size=24

### tablet options ###
#lockscreen-icon=/usr/share/icons/gnome/256x256/actions/lock.png
#lockscreen=/usr/share/backgrounds/gnome/Garden.jpg
#homescreen=/usr/share/backgrounds/gnome/Blinds.jpg
#animation=fade

[keyboard]
keymap_rules=evdev
#keymap_layout=gb
#keymap_options=caps:ctrl_modifier,shift:both_capslock_cancel
### keymap_options from /usr/share/X11/xkb/rules/base.lst ###

[terminal]
#font=DroidSansMono
#font-size=14

[launcher]
icon=/usr/share/icons/gnome/24x24/apps/utilities-terminal.png
path=/usr/bin/gnome-terminal

[launcher]
icon=/usr/share/icons/gnome/24x24/apps/utilities-terminal.png
path=/usr/bin/weston-terminal

[launcher]
icon=/usr/share/icons/hicolor/24x24/apps/firefox.png
path=/usr/bin/firefox

[launcher]
icon=/usr/share/icons/gnome/24x24/apps/arts.png
path=./clients/flower

[screensaver]
# Uncomment path to disable screensaver
path=/usr/libexec/weston-screensaver
duration=600

[input-method]
path=/usr/libexec/weston-keyboard

###  for Laptop displays  ###
#[output]
#name=LVDS1
#mode=1680x1050
#transform=90

#[output]
#name=VGA1
# The following sets the mode with a modeline, you can get modelines for your preffered resolutions using the cvt utility
#mode=173.00 1920 2048 2248 2576 1080 1083 1088 1120 -hsync +vsync
#transform=flipped

#[output]
#name=X1
#mode=1024x768
#transform=flipped-270

```

简单的 `weston.ini` :

 `~/.config/weston.ini` 
```
[core]
modules=xwayland.so

[keyboard]
keymap_layout=gb

[launcher]
icon=/usr/share/icons/gnome/24x24/apps/utilities-terminal.png
path=/usr/bin/weston-terminal

[launcher]
icon=/usr/share/icons/hicolor/24x24/apps/firefox.png
path=/usr/bin/firefox

[output]
name=LVDS1
mode=1680x1050
transform=90

```

#### XWayland

[安装](/index.php/%E5%AE%89%E8%A3%85 "安装")软件包[xorg-server-xwayland](https://www.archlinux.org/packages/?name=xorg-server-xwayland).

要通过 Weston 运行 X 程序，需要启动 Xwayland 进行请求处理。需要如下配置文件：

 `~/.config/weston.ini` 
```
[core]
modules=xwayland.so

```

#### 视频录制

Weston has build-in screencast recording which can be started and stopped by pressing the `Super+r` key combination. Screencasts are saved to the file `capture.wcap` in the current working directory of Weston.

The WCAP format is a lossless video format specific to Weston, which only records the difference in frames. To be able to play the recorded screencast, the WCAP file will need to be converted to a format which a media player can understand.

To convert the file to webm, execute:

```
$ wcap-decode capture.wcap --yuv4mpeg2 | vpxenc --target-bitrate=1024 --best -t 4 -o foo.webm -

```

To convert the file to ogv, execute:

```
$ wcap-decode capture.wcap --yuv4mpeg2 | theora_encode - -o cap.ogv

```

#### 高DPI显示器

For [Retina](https://en.wikipedia.org/wiki/Retina_Display "wikipedia:Retina Display") or [HiDPI](/index.php/HiDPI "HiDPI") displays, use:

 `~/.config/weston.ini` 
```

[output]
name=...
scale=2

```

#### Shell font

Weston uses the default sans-serif font for window title bars, clocks, etc. See [Font configuration#Replace or set default fonts](/index.php/Font_configuration#Replace_or_set_default_fonts "Font configuration") for instructions on how to change this font.

## 图形库

在[官方资料](http://wayland.freedesktop.org/toolkits.html)上查看详细信息

### GTK+ 3

[extra]软件仓库中的[gtk3](https://www.archlinux.org/packages/?name=gtk3) 已经提供了 Wayland 支持.

GTK+ 3.0 开始，GTK+ 可以在运行时同时支持多个后端，和 Qt 一样进行切换。

Wayland 和 X 后端都启用时，GTK+ 默认会使用 X11。可以通过把`GDK_BACKEND`环境变量设为`wayland`来改变这一规则。

### Qt5

[qt5](https://www.archlinux.org/groups/x86_64/qt5/) 软件包已经提供了 Wayland 支持。 要使用 wayland 插件运行程序，需要设置 [环境变量](/index.php/Environment_variable "Environment variable"). `QT_QPA_PLATFORM=wayland-egl`

### Clutter

Clutter 工具包有 Wayland 后端支持，可以作为 Wayland 程式运行。这一后端支持已经存在软件仓库的版本中。要配置 `CLUTTER_BACKEND=wayland`.

### SDL

Experimental wayland support is now in SDL 2.0.2 and enabled by default on Arch Linux.To run a SDL application on Wayland, set `SDL_VIDEODRIVER=wayland`.

### GLFW

Experimental wayland support is now in GLFW 3.1 and can be enabled with the `-DGLFW_USE_WAYLAND=ON` CMake option at compile time. You can also install the package [glfw-wayland-git](https://aur.archlinux.org/packages/glfw-wayland-git/) from the AUR.

### EFL

EFL 已经完全支持 Wayland。请参考[这里](http://trac.enlightenment.org/e/wiki/Wayland)获取更多细节。

## 窗口管理器和桌面 shell

| Name | Type | Description |
| GNOME | Compositing | 参见 [GNOME#Starting GNOME](/index.php/GNOME#Starting_GNOME "GNOME"). |
| Hawaii | *(Unclear)* | 参见 [Hawaii](/index.php/Hawaii "Hawaii"). |
| sway | Tiling | [Sway](https://github.com/SirCmpwn/sway) is an i3-compatible window manager for Wayland. |
| KDE | Compositing | [KDE](/index.php/KDE "KDE") 4.11 added support for [KWin under Wayland system compositor](http://blog.martin-graesslin.com/blog/2013/06/starting-a-full-kde-plasma-session-in-wayland/). With [KDE Plasma 5.4](https://community.kde.org/KWin/Wayland#Start_a_Plasma_session_on_Wayland), the first technology preview of a Wayland session is released but it is currently targeted for the mobile platform and does not yet allow to use it as a full replacement for Xorg based desktop. |
| Orbment | Tiling | [orbment](https://github.com/Cloudef/orbment) (previously loliwm) is a tiling WM for Wayland. |
| Velox | Tiling | [velox](https://github.com/michaelforney/velox) is a simple window manager based on swc. It is inspired by [dwm](/index.php/Dwm "Dwm") and [xmonad](/index.php/Xmonad "Xmonad"). |
| Orbital | Compositing | [Orbital](https://github.com/giucam/orbital) is a Wayland compositor and shell, using Qt5 and Weston. The goal of the project is to build a simple yet flexible and good looking Wayland desktop. It is not a full fledged DE but rather the analogue of a WM in the X11 world, such as [Awesome](/index.php/Awesome "Awesome") or [Fluxbox](/index.php/Fluxbox "Fluxbox"). |
| Papyros Shell | *(Unclear)* | [Papyros Shell](https://github.com/papyros/papyros-shell) is the desktop shell for [Papyros](http://papyros.io), built using QtQuick and QtCompositor as a compositor for Wayland. |
| Maynard | *(Unclear)* | [Maynard](https://github.com/raspberrypi/maynard) is a desktop shell client for Weston based on GTK. It was based on weston-gtk-shell, a project by Tiago Vignatti. |
| Motorcar | *(Unclear)* | [Motorcar](https://github.com/evil0sheep/motorcar) is a wayland compositor to explore 3D windowing. |

Some of installed wayland desktop clients might store information in `/usr/share/wayland-sessions/*.desktop` files about how to start them in wayland.

## 疑难解答

### LLVM assertion failure

If you get an LLVM assertion failure, you need to rebuild [mesa](https://www.archlinux.org/packages/?name=mesa) without Gallium LLVM until this problem is fixed.

This may imply disabling some drivers which require LLVM. You may also try exporting the following, if having problems with hardware drivers:

```
$ export EGL_DRIVER=/usr/lib/egl/egl_gallium.so

```

### Weston fails to launch after update to 1.7

This is possibly caused by the `desktop-shell.so` module being loaded by your weston.ini. This used to be required, but is not anymore.

Remove it from the `[core]` section:

 `~/.config/weston.ini` 
```
[core]
modules=xwayland.so,desktop-shell.so

```

生成：

 `~/.config/weston.ini` 
```
[core]
modules=xwayland.so

```

## 参阅

*   [Cursor themes](/index.php/Cursor_themes "Cursor themes")
*   [forum discussion](https://bbs.archlinux.org/viewtopic.php?id=107499) 页面将持续关注 Wayland 信息 ，如有兴趣请留意。