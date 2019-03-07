Related articles

*   [Xorg](/index.php/Xorg "Xorg")
*   [Touchpad Synaptics](/index.php/Touchpad_Synaptics "Touchpad Synaptics")
*   [Wayland](/index.php/Wayland "Wayland")

**翻译状态：** 本文是英文页面 [Libinput](/index.php/Libinput "Libinput") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2019-03-07，点击[这里](https://wiki.archlinux.org/index.php?title=Libinput&diff=0&oldid=553763)可以查看翻译后英文页面的改动。

来自[libinput](https://freedesktop.org/wiki/Software/libinput/) wiki 项目

	libinput 是一个函数库，在 Wayland 上用来接收设备的输入，在 X.Org 上提供输入设备的驱动。它提供对设备事件的检测和接收。对输入设备信号进行处理。它提供了一些列的函数供用户使用。

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 安装](#安装)
*   [2 配置](#配置)
    *   [2.1 使用 xinput](#使用_xinput)
    *   [2.2 使用 Xorg 配置文件](#使用_Xorg_配置文件)
    *   [2.3 图形工具](#图形工具)
*   [3 Tips and tricks](#Tips_and_tricks)
    *   [3.1 按键映射](#按键映射)
    *   [3.2 设置按键映射](#设置按键映射)
    *   [3.3 更改触摸板灵敏度](#更改触摸板灵敏度)
    *   [3.4 禁用触摸板](#禁用触摸板)
    *   [3.5 手势操作](#手势操作)
        *   [3.5.1 libinput-gestures](#libinput-gestures)
        *   [3.5.2 fusuma](#fusuma)
        *   [3.5.3 GnomeExtendedGestures](#GnomeExtendedGestures)
*   [4 疑难解答](#疑难解答)
    *   [4.1 触摸板在 GNOME 中无法工作](#触摸板在_GNOME_中无法工作)
    *   [4.2 KDE's Touchpad KCM 对触摸板设置不起作用](#KDE's_Touchpad_KCM_对触摸板设置不起作用)
    *   [4.3 触摸板没有被检测到](#触摸板没有被检测到)
*   [5 参阅](#参阅)

## 安装

在 Wayland 上使用 libinput 不需要安装。[libinput](https://www.archlinux.org/packages/?name=libinput) 包是所有 Wayland 图形环境的依赖包并且已经安装，也不需要额外的驱动。

如果想要在 [Xorg](/index.php/Xorg "Xorg") 上 [安装](/index.php/%E5%AE%89%E8%A3%85 "安装") libinput，使用 [xf86-input-libinput](https://www.archlinux.org/packages/?name=xf86-input-libinput) 包。此包允许 libinput 在 X 上作为驱动使用。此驱动会代替 evdev 和 synaptics 运行。 [[1]](https://freedesktop.org/wiki/Software/libinput/)

你可能也要安装 [xorg-xinput](https://www.archlinux.org/packages/?name=xorg-xinput) 来更改 runtime 设置

## 配置

在 [Wayland](/index.php/Wayland "Wayland") 上, 这里没有配置文件。 是否可配置这是由你的桌面环境开发者所决定的。详情请看 [#Graphical tools](#Graphical_tools).

对于 [Xorg](/index.php/Xorg "Xorg"), 默认的配置文件在 `/usr/share/X11/xorg.conf.d/40-libinput.conf`. 没必要用额外的配置文件来自动检测键盘，触摸板，小红点和触摸屏。

### 使用 xinput

首先，执行:

```
# libinput list-devices

```

这将会输出系统中的设备和它们被 libinput 支持的具体特性。

重启图形环境之后，如果没有其它驱动程序被配置为优先级，设备应由具有默认配置的 libinput 管理。

参见 [libinput(4)](https://jlk.fjfi.cvut.cz/arch/manpages/man/libinput.4) 了解可设定的常规选项和有关允许参数的信息。*xinput* 工具用于查看或更改运行中的的特定设备的可用选项。例如：

```
$ xinput list

```

查看所有设备并确定其名称和编号。 在下文中，`*device*` 是用于标识要操作的设备的名称或编号。

```
$ xinput list-props *device*

```

查看

```
$ xinput set-prop *device* *option-number* *setting*

```

以及修改一项设置。例如，设置开启 libinput 的两种单击选项（303），则使用以下命令：

```
$ xinput set-prop 14 303 {1 1}

```

### 使用 Xorg 配置文件

参见 [Xorg#Using .conf files](/index.php/Xorg#Using_.conf_files "Xorg") 了解永久的选项设置。[Logitech Marble Mouse#Using libinput](/index.php/Logitech_Marble_Mouse#Using_libinput "Logitech Marble Mouse") 和 [#Button re-mapping](#Button_re-mapping) 中做出了举例。

[Xorg#Input devices](/index.php/Xorg#Input_devices "Xorg") 的替代驱动程序通常可以安装共存。如果您打算为一个设备切换驱动程序以使用 libinput，请确保没有其它驱动程序的旧配置文件 `/etc/X11/xorg.conf.d/` 拥有优先级。

**Tip:** 如果你同时安装了 libinput 和 synaptics 并使用其默认配置（即 `/etc/X11/xorg.conf.d/` 中没有属于两者中任一的文件），synaptics 将因其在默认安装目录中拥有更高的数字顺序 `70-` 而获得优先级。为了避免这种情况，您可以将默认的 libinput 配置文件（`40-libinput.conf`）符号链接到目录搜索顺序优先于 `70-synaptics.conf` 的 `/etc/X11/xorg.conf.d/` 中去取代它：
```
# ln -s /usr/share/X11/xorg.conf.d/40-libinput.conf /etc/X11/xorg.conf.d/40-libinput.conf

```
如果你的 `/etc/X11/xorg.conf.d/` 中*确认*存在两者的配置文件，libinput 的文件一定拥有较次的优先级顺序; 见 [Xorg＃Using .conf files](/index.php?title=Xorg%EF%BC%83Using_.conf_files&action=edit&redlink=1 "Xorg＃Using .conf files (page does not exist)")。如果要禁用 libinput（并回退到较旧的驱动程序）- 只需从 `/etc/X11/xorg.conf.d/` 中删除之前创建的符号链接即可。

检查哪些设备是由 libinput 管理的一种方法是查看 [xorg logfile](/index.php?title=Xorg%EF%BC%83General&action=edit&redlink=1 "Xorg＃General (page does not exist)")。以下是一个例子：

 `$ grep -e "Using input driver 'libinput'" */path/to/Xorg.0.log*` 
```
[    28.799] (II) Using input driver 'libinput' for 'Power Button'
[    28.847] (II) Using input driver 'libinput' for 'Video Bus'
[    28.853] (II) Using input driver 'libinput' for 'Power Button'
[    28.860] (II) Using input driver 'libinput' for 'Sleep Button'
[    28.872] (II) Using input driver 'libinput' for 'AT Translated Set 2 keyboard'
[    28.878] (II) Using input driver 'libinput' for 'SynPS/2 Synaptics TouchPad'
[    28.886] (II) Using input driver 'libinput' for 'TPPS/2 IBM TrackPoint'
[    28.895] (II) Using input driver 'libinput' for 'ThinkPad Extra Buttons'
```

这是一台 `/etc/X11/xorg.conf.d/` 中没有任何配置文件的笔记本电脑，也就是说，设备是被自动检测出来的。

当然，你可以选择为一个设备使用替代的驱动程序，而为其它设备选择 libinput。许多因素可能会影响到底使用哪个驱动程序。举个例子，与 [Touchpad Synaptics](/index.php/Touchpad_Synaptics "Touchpad Synaptics") 相比，libinput 驱动程序根据自己的喜好去自定义触摸板行为的选项较少，但处理多点触控事件的程序逻辑要多得多（例如，手掌检测）。因此，如果你在使用某个驱动程序的时候，在硬件上遭遇了问题，那么尝试一下替代驱动程序是合理的。

自定义配置文件应放在 `/etc/X11/xorg.conf.d/` 中，并且通常选择被广泛使用的命名模式 `30-touchpad.conf` 作为文件名。

**Tip:** 阅读 `/usr/share/X11/xorg.conf.d/40-libinput.conf` 中的 CONFIGURATION DETAILS 以获取指导并参考 [libinput(4)](https://jlk.fjfi.cvut.cz/arch/manpages/man/libinput.4) 手册页有关可用配置选项的详细说明

一个基本的配置应该遵循以下的结构：

 `/etc/X11/xorg.conf.d/30-touchpad.conf` 
```
Section "InputClass"
    Identifier "devname"
    Driver "libinput"
    ...
EndSection

```

你可以在单个配置文件中定义任意多的部分（通常每个输入设备一个配置部分） 要配置你选择的设备，请指定 INPUTCLASS SECTION [xorg.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/xorg.conf.5) 中的一个过滤器，例如：

*   `MatchIsPointer "on"` (trackpoint)
*   `MatchIsKeyboard "on"`
*   `MatchIsTouchpad "on"`
*   `MatchIsTouchscreen "on"`

输入设备能够在 CONFIGURATION 中进行配置，详情请看 [libinput(4)](https://jlk.fjfi.cvut.cz/arch/manpages/man/libinput.4)。一些常用的配置选项有：

*   `Option "Tapping" "on"`: 触摸以点击
*   `Option "ClickMethod" "clickfinger"`: 触摸板不再拥有中右键区域的区分，与之代替的是双指代表右键，三指代表中键。 详情请看[docs](https://wayland.freedesktop.org/libinput/doc/latest/clickpad-softbuttons.html#clickfinger-behavior).
*   `Option "NaturalScrolling" "true"`: 自然滚动（反方向滚动）
*   `Option "ScrollMethod" "edge"`: 边缘滚动页面

注意：有的功能只在特定设备中起作用，并且你可能需要重启 “X服务” 来让功能生效。

### 图形工具

There are different GUI tools:

*   [GNOME](/index.php/GNOME "GNOME"):
    *   Control center has a basic UI. See [GNOME#Mouse and touchpad](/index.php/GNOME#Mouse_and_touchpad "GNOME").
    *   [gnome-tweaks](https://www.archlinux.org/packages/?name=gnome-tweaks) offers some additional settings.
*   [Cinnamon](/index.php/Cinnamon "Cinnamon"):
    *   Similar to the GNOME UI, with more options.
*   [KDE Plasma](/index.php/KDE_Plasma "KDE Plasma") 5:
    *   Set of keyboard, mouse, controller, and touch pad options. Some features are still placeholders.
    *   [kcm-pointing-devices-git](https://aur.archlinux.org/packages/kcm-pointing-devices-git/) is a rewritten KCM for all input devices supported by libinput.

## Tips and tricks

### 按键映射

Swapping two- and three-finger tap for a touchpad is a straight forward example. Instead of the default three-finger tap for pasting you can configure two-finger tap pasting by setting the `TappingButtonMap` option in your [Xorg](/index.php/Xorg "Xorg") configuration file. To set 1/2/3-finger taps to left/right/middle set `TappingButtonMap` to `lrm`, for left/middle/right set it to `lmr`.

 `/etc/X11/xorg.conf.d/30-touchpad.conf` 
```
Section "InputClass"
    Identifier "touchpad"
    Driver "libinput"
    MatchIsTouchpad "on"
    Option "Tapping" "on"
    Option "TappingButtonMap" "lmr"
EndSection
```

Remember to remove `MatchIsTouchpad "on"` if your device is not a touchpad and adjust the `Identifier` accordingly.

### 设置按键映射

For some devices it is desirable to change the button mapping. A common example is the use of a thumb button instead of the middle button (used in X11 for pasting) on mice where the middle button is part of the mouse wheel. You can query the current button mapping via:

```
$ xinput get-button-map *device*

```

where *device* is either the device name or the device ID, as returned by `xinput list`. You can freely permutate the button numbers and write them back. Example:

```
$ xinput set-button-map *device* 1 6 3 4 5 0 7

```

In this example, we mapped button 6 to be the middle button and disabled the original middle button by assigning it to button 0\. This may also be used for [Wayland](/index.php/Wayland "Wayland"), but be aware both the *device* number and its button-map will be different. Hence, settings are not directly interchangeable.

**Tip:** You can use *xev* (from the [xorg-xev](https://www.archlinux.org/packages/?name=xorg-xev) package) to find out which physical button is currently mapped to which ID.

Some devices occur several times under the same device name, with a different amount of buttons exposed. The following is an example for reliably changing the button mapping for a Logitech Revolution MX mouse via [xinitrc](/index.php/Xinitrc "Xinitrc"):

 `~/.xinitrc` 
```
...
for i in $(xinput list | grep "Logitech USB Receiver" | perl -n -e'/id=(\d+)/ && print "$1
"')
	do if xinput get-button-map "$i" 2>/dev/null| grep -q 20; then
		xinput set-button-map "$i" 1 17 3 4 5 8 7 6 9 10 11 12 13 14 15 16 2 18 19 20
	fi
done
...
```

### 更改触摸板灵敏度

The method of finding the correct thresholds for when libinput registers a touch as DOWN and back UP again can be found [[2]](https://wayland.freedesktop.org/libinput/doc/latest/touchpad-pressure-debugging.html#touchpad-pressure-hwdb) in the upstream documentation.

Custom touchpad pressure values can be set via temporary local device quirks. See [[3]](https://wayland.freedesktop.org/libinput/doc/latest/device-quirks.html).

**Note:**

Quirks are an internal API and are not guaranteed to work in future libinput versions. Between versions 1.11 and 1.12, udev rules [[4]](https://wayland.freedesktop.org/libinput/doc/1.11.3/udev_config.html#hwdb) were replaced by `.quirk` files [[5]](https://wayland.freedesktop.org/libinput/doc/latest/device-quirks.html).

### 禁用触摸板

To disable the touchpad, first get its name with `xinput list` and then disable it with `xinput disable *name*`.

**Note:**

*   It is more robust to disable it by name than by ID number. The devices may be renumbered.
*   It will be necessary to quote the name if it contains spaces.

To make it permanent, see [Autostarting](/index.php/Autostarting "Autostarting").

### 手势操作

虽然 libinput 已经提供了[手势操作](https://wayland.freedesktop.org/libinput/doc/latest/gestures.html)，比如：捏，滑。但 [Desktop environment](/index.php/Desktop_environment "Desktop environment") 和 [Window manager](/index.php/Window_manager "Window manager") 可能还没有使用这些功能。

#### libinput-gestures

对于 [EWMH](https://en.wikipedia.org/wiki/Extended_Window_Manager_Hints "w:Extended Window Manager Hints") (see also [wm-spec](https://www.freedesktop.org/wiki/Specifications/wm-spec/)) 兼容的窗口界面, 可以使用 [libinput-gestures](https://github.com/bulletmark/libinput-gestures) 。 这个程序读取 libinput 在触摸板的手势 (通过 `libinput debug-events`) ，然后根据设置映射成相对应的行为。这个程序提供了相当多了可自定义的功能。

要使用 [libinput-gestures](https://github.com/bulletmark/libinput-gestures), 请安装 [libinput-gestures](https://aur.archlinux.org/packages/libinput-gestures/) 。 你能使用很多系统级别的手势操作，也能自定义配置文件，详情请看 [README](https://github.com/bulletmark/libinput-gestures/blob/master/README.md) 。

#### fusuma

[Fusuma](https://github.com/iberianpig/fusuma) is a multitouch gesture recognizer, written in [Ruby](/index.php/Ruby "Ruby"), which can be used as an alternative to libinput-gestures.

Install the `fusuma` [Ruby gem](/index.php/Ruby#RubyGems "Ruby"):

```
$ gem install fusuma

```

Alternatively an outdated version is available in the AUR: [ruby-fusuma](https://aur.archlinux.org/packages/ruby-fusuma/).

then in `~/.config/fusuma/config.yml` you can set something like:

 `~/.config/fusuma/config.yml` 
```
swipe:
  3: 
    left: 
      shortcut: 'alt+Right'
    right: 
      shortcut: 'alt+Left'
    up: 
      shortcut: 'ctrl+shift+plus'
    down: 
      shortcut: 'ctrl+minus'
pinch:
  in:
    shortcut: 'ctrl+shift+plus'
  out:
    shortcut: 'ctrl+minus'

threshold:
  swipe: 0.5
  pinch: 0.2

interval:
  swipe: 0.2
  pinch: 0.2

```

The swipe threshold is important for not swiping back too many pages.

Notice that the config is for three fingers swipe.

#### GnomeExtendedGestures

For deeper integration with GNOME, there is [GnomeExtendedGestures](https://github.com/mpiannucci/GnomeExtendedGestures) ([gnome-shell-extension-extended-gestures-git](https://aur.archlinux.org/packages/gnome-shell-extension-extended-gestures-git/)). Three finger horizontal and vertical gestures can be configured to perform gnome-shell actions (such as toggling the application overview or cycling between them).

## 疑难解答

First, see whether executing `libinput debug-events` can support you in debugging the problem, see [libinput-debug-events(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/libinput-debug-events.1) for options.

Some inputs require kernel support. The tool *evemu-describe* from the [evemu](https://www.archlinux.org/packages/?name=evemu) package can be used to check:

Compare the output of [software supported input trackpad driver](http://ix.io/m6b) with [a supported trackpad](https://github.com/whot/evemu-devices/blob/master/touchpads/SynPS2%20Synaptics%20TouchPad-with-scrollbuttons.events). i.e. a couple of ABS_ axes, a couple of ABS_MT axes and no REL_X/Y axis. For a clickpad the `INPUT_PROP_BUTTONPAD` property should also be set, if it is supported.

### 触摸板在 GNOME 中无法工作

Ensure the touchpad events are being sent to the GNOME desktop by running the following command:

```
$ gsettings set org.gnome.desktop.peripherals.touchpad send-events enabled

```

Additionally, GNOME may override certain behaviors, like turning off Tapping and forcing Natural Scrolling. In this case the settings must be adapted using GNOMEs `gsettings` command line tool or a graphical frontend of your choice. For example if you wish to enable *Tapping* and disable *Natural Scrolling* for your user, adjust the touchpad key-values like the following:

```
$ gsettings set org.gnome.desktop.peripherals.touchpad tap-to-click true
$ gsettings set org.gnome.desktop.peripherals.touchpad natural-scroll false

```

### KDE's Touchpad KCM 对触摸板设置不起作用

KDE's Touchpad KCM has libinput support for [Xorg](/index.php/Xorg "Xorg"), but not all GUI settings are available yet. You may find that a setting such as *Disable touchpad when typing* has no effect and other options are greyed out. Until the support is extended, a workaround is to install [kcm-pointing-devices-git](https://aur.archlinux.org/packages/kcm-pointing-devices-git/) or set the options manually with `xinput set-prop`.

### 触摸板没有被检测到

If a touchpad device is not detected and shown as a device at all, a possible solution might be using one or more of these kernel parameters.

```
i8042.noloop i8042.nomux i8042.nopnp i8042.reset

```

## 参阅

*   [libinput Wayland documentation](https://wayland.freedesktop.org/libinput/doc/latest/index.html)
*   [FOSDEM 2015 - libinput](https://archive.fosdem.org/2015/schedule/event/libinput/attachments/slides/591/export/events/attachments/libinput/slides/591/libinput_xorg.pdf) - Hans de Goede on goals and plans of the project
*   [Peter Hutterer's Blog](http://who-t.blogspot.com.au/) - numerous posts on libinput from one of the project's hackers