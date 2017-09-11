本指南最初是为基于 *USB* 的 Wacom 数位板撰写的，所以文中大部分内容都集中于它。通常推荐依赖于 [Xorg](/index.php/Xorg "Xorg") 的自动检测功能更或者使用*动态*的设置。 然而，对于一些*内嵌*的数位板，当自动检测功能不起作用时，可以考虑使用静态的 Xorg 设置。 一份静态的 Xorg 设置通常会导致，当你的 Wacom 数位板连接到不同的 *USB* 端口后，甚至当你在同一端口上重新拔插后，设备无法被识别。因此，此方法被认定是过时的。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
    *   [1.1 自动设置](#.E8.87.AA.E5.8A.A8.E8.AE.BE.E7.BD.AE)
    *   [1.2 手动设置](#.E6.89.8B.E5.8A.A8.E8.AE.BE.E7.BD.AE)
        *   [1.2.1 使用 udev](#.E4.BD.BF.E7.94.A8_udev)
            *   [1.2.1.1 USB设备](#USB.E8.AE.BE.E5.A4.87)
            *   [1.2.1.2 串行设备](#.E4.B8.B2.E8.A1.8C.E8.AE.BE.E5.A4.87)
        *   [1.2.2 静态设置](#.E9.9D.99.E6.80.81.E8.AE.BE.E7.BD.AE)
        *   [1.2.3 Xorg配置](#Xorg.E9.85.8D.E7.BD.AE)
*   [2 配置](#.E9.85.8D.E7.BD.AE)
    *   [2.1 常用概念](#.E5.B8.B8.E7.94.A8.E6.A6.82.E5.BF.B5)
        *   [2.1.1 临时配置](#.E4.B8.B4.E6.97.B6.E9.85.8D.E7.BD.AE)
        *   [2.1.2 持久化配置](#.E6.8C.81.E4.B9.85.E5.8C.96.E9.85.8D.E7.BD.AE)
        *   [2.1.3 更改方向](#.E6.9B.B4.E6.94.B9.E6.96.B9.E5.90.91)
        *   [2.1.4 重映射按钮](#.E9.87.8D.E6.98.A0.E5.B0.84.E6.8C.89.E9.92.AE)
            *   [2.1.4.1 获取按钮ID](#.E8.8E.B7.E5.8F.96.E6.8C.89.E9.92.AEID)
            *   [2.1.4.2 语法](#.E8.AF.AD.E6.B3.95)
            *   [2.1.4.3 示例](#.E7.A4.BA.E4.BE.8B)
            *   [2.1.4.4 执行自定义命令](#.E6.89.A7.E8.A1.8C.E8.87.AA.E5.AE.9A.E4.B9.89.E5.91.BD.E4.BB.A4)
        *   [2.1.5 LEDs](#LEDs)
        *   [2.1.6 TwinView设置](#TwinView.E8.AE.BE.E7.BD.AE)
            *   [2.1.6.1 临时TwinView设置](#.E4.B8.B4.E6.97.B6TwinView.E8.AE.BE.E7.BD.AE)
        *   [2.1.7 Xrandr设置](#Xrandr.E8.AE.BE.E7.BD.AE)
    *   [2.2 压力曲线](#.E5.8E.8B.E5.8A.9B.E6.9B.B2.E7.BA.BF)
    *   [2.3 力量比例](#.E5.8A.9B.E9.87.8F.E6.AF.94.E4.BE.8B)
    *   [2.4 使用kcm-wacomtablet](#.E4.BD.BF.E7.94.A8kcm-wacomtablet)
*   [3 针对特定应用程序的配置](#.E9.92.88.E5.AF.B9.E7.89.B9.E5.AE.9A.E5.BA.94.E7.94.A8.E7.A8.8B.E5.BA.8F.E7.9A.84.E9.85.8D.E7.BD.AE)
    *   [3.1 Blender](#Blender)
    *   [3.2 GIMP](#GIMP)
    *   [3.3 Inkscape](#Inkscape)
    *   [3.4 Krita](#Krita)
    *   [3.5 VirtualBox](#VirtualBox)
    *   [3.6 Web Browser Plugin](#Web_Browser_Plugin)
*   [4 故障排除](#.E6.95.85.E9.9A.9C.E6.8E.92.E9.99.A4)
    *   [4.1 未知的设备类型](#.E6.9C.AA.E7.9F.A5.E7.9A.84.E8.AE.BE.E5.A4.87.E7.B1.BB.E5.9E.8B)
    *   [4.2 系统冻结](#.E7.B3.BB.E7.BB.9F.E5.86.BB.E7.BB.93)
*   [5 参考文献](#.E5.8F.82.E8.80.83.E6.96.87.E7.8C.AE)

## 安装

1.  **检查内核是否已经识别你的数位板**
    对于 USB 数位板, 连接电脑并检查`lsusb`、`dmesg | grep -i wacom`或者`/proc/bus/input/devices`的输出。
    当你的数位板无法被识别，而能够识别它的驱动比内核中的驱动更新时，请尝试安装[input-wacom-dkms](https://aur.archlinux.org/packages/input-wacom-dkms/)。
2.  **安装 Wacom 驱动**
    请安装软件包 [xf86-input-wacom](https://www.archlinux.org/packages/?name=xf86-input-wacom) ，如果无法使用，请尝试不稳定的 [xf86-input-wacom-git](https://aur.archlinux.org/packages/xf86-input-wacom-git/) 包。

### 自动设置

新版本的 X 应当可以自动地检测并配置你的设备。在进一步之前，请重启 X 使新的 udev 规则生效。要测试你的设备是否已经被完整的识别（即笔和橡皮（如果有的话）都正常工作），请执行如下的命令

```
 $ xsetwacom --list devices

```

该命令应当检测出所有设备并给出类型，例如

```
 Wacom Bamboo 2FG 4x5 Pen stylus 	id: 8	type: STYLUS    
 Wacom Bamboo 2FG 4x5 Pen eraser 	id: 9	type: ERASER    
 Wacom Bamboo 2FG 4x5 Finger touch	id: 13	type: TOUCH     
 Wacom Bamboo 2FG 4x5 Finger pad 	id: 14	type: PAD       

```

你也可以通过打开 [gimp](https://www.archlinux.org/packages/?name=gimp) 或者 [xournal](https://www.archlinux.org/packages/?name=xournal) 测试设备，并且检查扩展输入设备部分（extended input devices section），或者任何数位板相关的配置是否被你选择的软件支持。

为了使其工作，你不需要 `xorg.conf` 文件，所有的配置更改都在 `/etc/X11/xorg.conf.d/` 文件夹中。 如果一切正常的话，你可以跳过手动设置章节继续阅读配置部分，了解如何更进一步地自定义你的数位板。

随着 Xorg 1.8 的到来，会弃用HAL支持转而使用udev。因为他们的 udev 规则还不存在，致使部分型号的平板电脑无法透过udev正常执行自动检测，因此你可能需要自己编写。

*xf86-input-wacom*驱动设计成与 Xorg 服务器配合工作，因此当你在 Wayland 上运行你的桌面环境的时候可能会出问题（Gnome 的默认窗口系统）。

### 手动设置

手动配置需要保存在 `/etc/X11/xorg.conf` 中，或者作为单独的文件保存在 `/etc/X11/xorg.conf.d/` 目录下。 访问 Wacom 数位板需要通过访问 `/dev/input/` 中的一个输入事件接口，该接口由内核驱动提供。 接口的编号 `event??` 可能会随着设备从 *USB* 端口的拔插而改变，特别是从不同的端口拔插。 因此，明智的做法是不要使用具体的 `event??` 接口（*静态*配置）来确定设备，而是让 *udev* 动态创建一个符号链接到正确的 `event` 文件（*动态*配置）。

#### 使用 udev

**注意:** AUR 中的 wacom-udev 包含了 udev 的规则文件。如果你正在使用这个包，可以跳过本小节，并从 `xorg.conf`配置 部分继续。

假设 *udev* 已经安装，你只需要简单地从 [AUR](/index.php/AUR "AUR") 安装 [wacom-udev](https://aur.archlinux.org/packages/wacom-udev/) 。

##### USB设备

在你（重新）插入你的 *USB* 数位板之后（或者至少是重启之后），`/dev/input` 下应当会出现一些关联到你的数位板设备的符号链接。

```
 $ ls /dev/input/wacom* 
 /dev/input/wacom  /dev/input/wacom-stylus  /dev/input/wacom-touch

```

如果没有，你的设备可能并没有包含在 *wacom-dev* 自带的 *udev* 配置中（位于 `/usr/lib/udev/rules.d/10-wacom.rules`）。在修改这个文件之前最好复制一份（例如，复制为 `10-my-wacom.rules`），不然它可能会在包升级的时候被覆盖（回滚）。

要将你的设备加入到文件中，请复制文件里的某一行并且更改其中的 *idVendor*，*idProduct* 和 *SYMLINK* 的值为你的设备的对应值。

其中两个 id 可以通过以下命令确认：

```
$ lsusb | grep -i wacom
Bus 002 Device 007: ID 056a:0062 Wacom Co., Ltd

```

在这个例子中 *idVendor* 的值为 056a，*idProduct* 的值为 0062。 如果你的设备有触摸功能（例如 Bamboo Pen&Touch），则可能需要为触摸输入接口添加一行配置。 更多详情请参考 linuxwacom 的 wiki [Fixed device files with udev](http://sourceforge.net/apps/mediawiki/linuxwacom/index.php?title=Fixed_device_files_with_udev)。

保存文件并使用命令 `udevadm control --reload-rules` 重新加载 udev 的配置文件。 再次检查 */dev/input*，确保符号链接 *wacom* 已出现。 注意，你可能需要重新拔插设备才能看到设备。

`/dev/input/wacom` 将会在 *Xorg* 配置中进一步使用，对于触摸设备来说，还有 `/dev/input/wacom_touch`。

##### 串行设备

软件包 [wacom-udev](https://aur.archlinux.org/packages/wacom-udev/) 也应当包括了对串行设备的支持。串行设备的用户也许会对 [linuxconsole](https://www.archlinux.org/packages/?name=linuxconsole) 软件包中的 inputattach 工具感兴趣。inputattach 命令允许你将串行设备绑定到 /dev/input 设备树上，例如：

```
 # inputattach --w8001 /dev/ttyS0

```

关于可用选项的帮助，请参见 *man inputattach*。 对于 USB 设备，最终你应得到一个 `/dev/input/wacom` 文件，然后继续进行 *Xorg* 配置。

#### 静态设置

If you insist in using a static setup just refer to your tablet in the *Xorg* configuration in the next section using the correct `/dev/input/event??` files as one can find out by looking into `/proc/bus/input/devices`.

#### Xorg配置

In either case, dynamic or static setup you got now one or two files in `/dev/input/` which refer to the correct input event devices of your tablet. All that is left to do is add the relevant information to `/etc/X11/xorg.conf`, or a dedicated file under `/etc/X11/xorg.conf.d/`. The exact configuration depends on your tablet's features of course. `xsetwacom --list devices` might give helpful information on what *InputDevice* sections are needed for your tablet.

An example configuration for a *Volito2* might look like this

```
Section "InputDevice"
    Driver        "wacom"
    Identifier    "stylus"
    Option        "Device"       "/dev/input/wacom"   # or the corresponding event?? for a static setup
    Option        "Type"         "stylus"
    Option        "USB"          "on"                 # USB ONLY
    Option        "Mode"         "Relative"           # other option: "Absolute"
    Option        "Vendor"       "WACOM"
    Option        "tilt"         "on"  # add this if your tablet supports tilt
    Option        "Threshold"    "5"   # the official linuxwacom howto advises this line
EndSection
Section "InputDevice"
    Driver        "wacom"
    Identifier    "eraser"
    Option        "Device"       "/dev/input/wacom"   # or the corresponding event?? for a static setup
    Option        "Type"         "eraser"
    Option        "USB"          "on"                  # USB ONLY
    Option        "Mode"         "Relative"            # other option: "Absolute"
    Option        "Vendor"       "WACOM"
    Option        "tilt"         "on"  # add this if your tablet supports tilt
    Option        "Threshold"    "5"   # the official linuxwacom howto advises this line
EndSection
Section "InputDevice"
    Driver        "wacom"
    Identifier    "cursor"
    Option        "Device"       "/dev/input/wacom"   # or the corresponding event?? for a static setup
    Option        "Type"         "cursor"
    Option        "USB"          "on"                  # USB ONLY
    Option        "Mode"         "Relative"            # other option: "Absolute"
    Option        "Vendor"       "WACOM"
EndSection

```

Make sure that you also change the path (`"Device"`) to your mouse, as it will be `/dev/input/mouse_udev` now.

```
Section "InputDevice"
    Identifier  "Mouse1"
    Driver      "mouse"
    Option      "CorePointer"
    Option      "Device"             "/dev/input/mouse_udev"
    Option      "SendCoreEvents"     "true"
    Option      "Protocol"           "IMPS/2"
    Option      "ZAxisMapping"       "4 5"
    Option      "Buttons"            "5"
EndSection

```

Add this to the *ServerLayout* section

```
InputDevice "cursor" "SendCoreEvents" 
InputDevice "stylus" "SendCoreEvents"
InputDevice "eraser" "SendCoreEvents"

```

And finally make sure to update the identifier of your mouse in the *ServerLayout* section – as mine went from

```
InputDevice    "Mouse0" "CorePointer"

```

to

```
InputDevice    "Mouse1" "CorePointer"

```

## 配置

### 常用概念

The configuration can be done in two ways temporary using the `xsetwacom` tool, which is included in *xf86-input-wacom* or permanent in `xorg.conf` or better in a extra file in `/etc/X11/xorg.conf.d`. The possible options are identical so it is recommended to first use `xsetwacom` for testing and later add the final config to the *Xorg* configuration files.

#### 临时配置

For the beginning it is a good idea to inspect the default configuration and all possible options using the following commands.

```
 $ xsetwacom --list devices                    # list the available devices for the get/set commands
 Wacom Bamboo 16FG 4x5 Finger touch	id: 12	type: TOUCH
 Wacom Bamboo 16FG 4x5 Finger pad	id: 13	type: PAD       
 Wacom Bamboo 16FG 4x5 Pen stylus	id: 17	type: STYLUS    
 Wacom Bamboo 16FG 4x5 Pen eraser	id: 18	type: ERASER
 $ xsetwacom --get "Wacom Bamboo 16FG 4x5" all # using the device name
 $ xsetwacom --get 17 all                      # or equivalently use the device id
 $ xsetwacom --list parameters                 # to get an explanation of the Options
 $ man wacom                                   # get even more details

```

**Caution**, do not use the device id when writing shell scripts to set some options as the ids might change after an hotplug.

Options can be changed with the `--set` flag. Some useful examples are

```
 $ xsetwacom --set "Wacom Bamboo 16FG 4x5 Finger touch" ScrollDistance 50  # change scrolling speed
 $ xsetwacom --set "Wacom Bamboo 16FG 4x5 Finger touch" Gesture off        # disable multitouch gestures
 $ xsetwacom --set "Wacom Bamboo 16FG 4x5 Finger touch" Touch off          # disable touch

```

**Note:** You can reset your temporary configuration at any time by unplugging and replugging in your tablet.

**Note:** There are some configurations that can only be set up dynamically with xsetwacom. In those cases it is possible to run a script that configures the device calling xsetwacom every time the device is plugged in. See [[1]](http://unix.stackexchange.com/a/290940/89955).

#### 持久化配置

To make a permanent configuration the preferred way for *Xorg*>1.8 is to create a new file in `/etc/X11/xorg.conf.d` e.g. `52-wacom-options.conf` with the following content.

 `/etc/X11/xorg.conf.d/52-wacom-options.conf` 
```
Section "InputClass"
    Identifier "Wacom Bamboo stylus options"
    MatchDriver "wacom"
    MatchProduct "Pen"

    # Apply custom Options to this device below.
    Option "Rotate" "none"
    Option "RawSample" "20"
    Option "PressCurve" "0,10,90,100"
EndSection

Section "InputClass"
    Identifier "Wacom Bamboo eraser options"
    MatchDriver "wacom"
    MatchProduct "eraser"

    # Apply custom Options to this device below.
    Option "Rotate" "none"
    Option "RawSample" "20"
    Option "PressCurve" "5,0,100,95"
EndSection

Section "InputClass"
    Identifier "Wacom Bamboo touch options"
    MatchDriver "wacom"
    MatchProduct "Finger"

    # Apply custom Options to this device below.
    Option "Rotate" "none"
    Option "ScrollDistance" "18"
    Option "TapTime" "220"
EndSection

Section "InputClass"
    Identifier "Wacom Bamboo pad options"
    MatchDriver "wacom"
    MatchProduct "pad"

    # Apply custom Options to this device below.
    Option "Rotate" "none"

    # Setting up buttons
    Option "Button1" "1"
    Option "Button2" "2"
    Option "Button3" "3"
    Option "Button4" "0"
EndSection

```

The identifiers can be set arbitrarily. The option names are (except for the buttons) identical to the ones listed by `xsetwacom --list parameters` and especially also in [wacom(4)](http://jlk.fjfi.cvut.cz/arch/manpages/man/wacom.4). As noted in [#Remapping Buttons](#Remapping_Buttons) the button ids seem to be different than the ones for `xsetwacom`.

#### 更改方向

If you want to use your tablet in a different orientation you have to tell this to the driver, else the movements do not cause the expected results. This is done by setting the **Rotate** option for all devices. Possible orientations are **none**,**cw**,**ccw** and **half**. A quick way is e.g.

```
 $ for i in 12 13 17 18; do xsetwacom --set $i Rotate half; done   # remember the ids might change when hotplugging

```

or use the following script like this `./wacomrot.sh half`

 `wacomrot.sh` 
```
#!/bin/bash
device="Wacom Bamboo 16FG 4x5"
stylus="$device Pen stylus"
eraser="$device Pen eraser"
touch="$device Finger touch"
pad="$device Finger pad"

xsetwacom --set "$stylus" Rotate $1
xsetwacom --set "$eraser" Rotate $1
xsetwacom --set "$touch"  Rotate $1
xsetwacom --set "$pad"    Rotate $1
```

#### 重映射按钮

It is possible to remap the buttons with hotkeys.

*   Check [Simple web-based GUI for xsetwacom](http://planetedessonges.org:8010/wakey/), supports *bamboo small* but more models may come.

##### 获取按钮ID

Sometimes it needs some trial&error to find the correct button IDs. For me they even differ for `xsetwacom` and the `xorg.conf` configuration. Very helpful tools are `xev` or `xbindkeys -mk`. An easy way to proceed is to temporarily assign keystrokes to your tablet's buttons like this:

```
 $ xsetwacom --set "Wacom Bamboo 16FG 4x5 Finger pad" Button 1 'key a'
 $ xsetwacom --set "Wacom Bamboo 16FG 4x5 Finger pad" Button 2 'key b'
 $ xsetwacom --set "Wacom Bamboo 16FG 4x5 Finger pad" Button 3 'key c'
 $ # and so on

```

Then fire up `xev` from a terminal window, place your mouse cursor above the window and hit the buttons and write down the IDs.

```
 $ xev | grep KeyPress -A 5

```

##### 语法

The syntax of `xsetwacom` is flexible but not very well documented. The general mapping syntax (extracted from the source code) for xsetwacom 0.17.0 is the following.

```
 KEYWORD [ARGS...] [KEYWORD [ARGS...] ...]

 KEYWORD + ARGS:
   key [+,-]KEY [[+,-]KEY ...]  where +:key down, -:key up, no prefix:down and up
   button BUTTON [BUTTON ...]   (1=left,2=middle,3=right mouse button, 4/5 scroll mouse wheel)
   modetoggle                   toggle absolute/relative tablet mode 
   displaytoggle                toggle cursor movement among all displays which include individual screens
                                plus the whole desktop for the selected tool if it is not a pad.
                                When the tool is a pad, the function applies to all tools that are asssociated
                                with the tablet

 BUTTON: button ID as integer number

 KEY: MODIFIER, SPECIALKEY or ASCIIKEY
 MODIFIER: (each can be prefix with an **l** or an **r** for the left/right modifier (no prefix = left)
    ctrl=ctl=control, meta, alt, shift, super, hyper
 SPECIALKEY: f1-f35, esc=Esc, up,down,left,right, backspace=Backspace, tab, PgUp,PgDn
 ASCIIKEY: (usual characters the key produces, e.g. a,b,c,1,2,3 etc.)

```

##### 示例

```
 $ xsetwacom --set "Wacom Bamboo 16FG 4x5 Finger pad" Button 1 3 # right mouse button
 $ xsetwacom --set "Wacom Bamboo 16FG 4x5 Finger pad" Button 1 "key +ctrl z -ctrl"
 $ xsetwacom --get "Wacom Bamboo 16FG 4x5 Finger pad" Button 1
 key +Control_L +z -z -Control_L
 $ xsetwacom --set "Wacom Bamboo 16FG 4x5 Finger pad" Button 1 "key +shift button 1 key -shift"

```

even little macros are possible

```
 $ xsetwacom --set "Wacom Bamboo 16FG 4x5 Finger pad" Button 1 "key +shift h -shift e l l o"

```

**Note:** There seems to be a bug in the *xf86-input-wacom* driver version 0.17.0, at least for my *Wacom Bamboo Pen & Touch*, but I guess this holds in general. It causes the keystrokes not to be overwritten correctly.
```
 $ xsetwacom --set "Wacom Bamboo 16FG 4x5 Finger pad" Button 1 "key a b c" # press button 1 -> abc
 $ xsetwacom --set "Wacom Bamboo 16FG 4x5 Finger pad" Button 1 "key d"     # press button 1 -> dbc  WRONG!

```

A simple workaround is to reset the mapping by mapping to "":

```
 $ xsetwacom --set "Wacom Bamboo 16FG 4x5 Finger pad" Button 1 ""          # to reset the mapping
 $ xsetwacom --set "Wacom Bamboo 16FG 4x5 Finger pad" Button 1 "key d"     # press button 1 -> d

```

**Note:** If you try to run a script with `xsetwacom` commands from a udev rule, you might find that it will not work, as the wacom input devices will not be ready at the time. A workaround is to add `sleep 1` at the beginning of your script.

##### 执行自定义命令

Mapping custom commands to the buttons is a little bit tricky but actually very simple. First, install [xbindkeys](https://www.archlinux.org/packages/?name=xbindkeys).

To get well defined button codes add the following to your permanent configuration file, e.g. `/etc/X11/xorg.conf.d/52-wacom-options.conf` in the InputClass section of your **pad** device. Map the tablet's buttons to some unused button ids.

```
 # Setting up buttons (preferably choose the correct button order, so the topmost key is mapped to 10 and so on)
 Option "Button1" "10"
 Option "Button2" "11"
 Option "Button3" "12"
 Option "Button4" "13"

```

Then restart your *Xorg* server and verify the buttons using `xev` or `xbindkeys -mk`.

Now set up your xbindkeys configuration, if you do not already have one you might want to create a default configuration

```
 $ xbindkeys --defaults > ~/.xbindkeysrc

```

Then add your custom key mapping to `~/.xbindkeysrc`, for example

```
 "firefox"
     m:0x10 + b:10   (mouse)
 "xterm"
     m:0x10 + b:11   (mouse)
 "xdotool key ctrl-z"
     m:0x10 + b:12   (mouse)
 "send-notify Test "No need for escaping the quotes""
     m:0x10 + b:13   (mouse)

```

#### LEDs

See the [sysfs-driver-wacom](https://www.kernel.org/doc/Documentation/ABI/testing/sysfs-driver-wacom) documentation. To make changes without requiring root permissions you will likely want to create a [udev](/index.php/Udev "Udev") rule like so:

 `/etc/udev/rules.d/99-wacom.rules` 
```
# Give the users group permissions to set Wacom device LEDs.
ACTION=="add", SUBSYSTEM=="hid", DRIVERS=="wacom", RUN+="/usr/bin/sh -c 'chown :users /sys/%p/wacom_led/*'"

```

Setting the Intuos OLEDs can be done using [i4oled](https://aur.archlinux.org/packages/i4oled/) from the AUR.

#### TwinView设置

If you are going to use two Monitors the aspect ratio while using the Tablet might feel unnatural. In order to fix this you need to add

```
Option "TwinView" "horizontal"

```

To all of your Wacom-InputDevice entries in the `xorg.conf` file. You may read more about that [HERE](http://ubuntuforums.org/showthread.php?t=640898)

##### 临时TwinView设置

For temporary mapping of a Wacom device to a single display **while preserving the aspect ratio**, [this script](https://gist.github.com/Quackmatic/6c19fe907945d735c045) may be used. This will letter-box the surface area of the device as required to ensure the input is not stretched on the display. This script may be executed in your `.xinitrc` file for it to automatically run.

#### Xrandr设置

xrandr sets two monitors as one big screen, mapping the tablet to the whole virtual screen and deforming aspect ratio. For a solution see this thread: [archlinux forum](https://bbs.archlinux.org/viewtopic.php?pid=797617).

If you just want to map the tablet to one of your screens, first find out what the screens are called

```
$ xrandr
Screen 0: minimum 320 x 200, current 3840 x 1080, maximum 16384 x 16384
**HDMI-0** disconnected (normal left inverted right x axis y axis)
**DVI-0** connected 1920x1080+0+0 (normal left inverted right x axis y axis) 477mm x 268mm
  1920x1080      60.0*+
  1680x1050      60.0  
  ...
**VGA-0** connected 1920x1080+1920+0 (normal left inverted right x axis y axis) 477mm x 268mm
  1920x1080      60.0*+
  1680x1050      60.0  
  ...

```

Then you need to know what is the ID of your tablet.

```
$ xsetwacom --list devices
WALTOP International Corp. Slim Tablet stylus   id: **12**  type: STYLUS

```

In my case I want to map the tablet (ID: **12**) to the screen on the right, which is **VGA-0**. I can do that with this command

```
$ xsetwacom --set **12** MapToOutput **"VGA-0"**

```

This should immediately work, no root necessary.

If xsetwacom replies with "Unable to find an output ..." an X11 geometry string of the form **WIDTHxHEIGHT+X+Y** can be specified instead of the screen identifier. In this example

```
$ xsetwacom --set **12** MapToOutput **"1920x1080+1920+0"**

```

should also map the tablet to the screen on the right.

Alternatively, you can use [this bash script](https://bitbucket.org/denilsonsa/small_scripts/src/3380435f92646190f860b87f566a39d0e215034c/xsetwacom_my_preferences.sh?at=default) to quickly map the tablet to one of your screens (or the entire desktop) and fix the aspect ratio.

In case **xsetwacom** doesn't work, you can try **xinput**.

First, you need to find your tablet's ID.

```
$ xinput list

```

In my case, the output is:

```
⎡ Virtual core pointer                          id=2    [master pointer  (3)]
⎜   ↳ Virtual core XTEST pointer                id=4    [slave  pointer  (2)]
⎜   ↳ Wacom Intuos PT S 2 Finger                id=11   [slave  pointer  (2)]
⎜   ↳ Wacom Intuos PT S 2 Pad                   id=12   [slave  pointer  (2)]
⎜   ↳ USB Keyboard                              id=14   [slave  pointer  (2)]
⎜   ↳ SynPS/2 Synaptics TouchPad                id=16   [slave  pointer  (2)]
⎜   ↳ TPPS/2 IBM TrackPoint                     id=17   [slave  pointer  (2)]
⎜   ↳ SteelSeries Kinzu V2 Gaming Mouse         id=9    [slave  pointer  (2)]
⎜   ↳ Wacom Intuos PT S 2 Pen Pen (0x6281780c)  id=20   [slave  pointer  (2)]
⎣ Virtual core keyboard                         id=3    [master keyboard (2)]
    ↳ Virtual core XTEST keyboard               id=5    [slave  keyboard (3)]
    ↳ Power Button                              id=6    [slave  keyboard (3)]
    ↳ Video Bus                                 id=7    [slave  keyboard (3)]
    ↳ Sleep Button                              id=8    [slave  keyboard (3)]
    ↳ Wacom Intuos PT S 2 Pen                   id=10   [slave  keyboard (3)]
    ↳ USB Keyboard                              id=13   [slave  keyboard (3)]
    ↳ AT Translated Set 2 keyboard              id=15   [slave  keyboard (3)]
    ↳ ThinkPad Extra Buttons                    id=18   [slave  keyboard (3)]
    ↳ USB Keyboard                              id=19   [slave  keyboard (3)]

```

This mean, my tablet's ID is **20**. Now we map it with **VGA-0** screen:

```
$ xinput map-to-output 20 VGA-0

```

### 压力曲线

Use [Wacom Pressure Demo](http://linuxwacom.sourceforge.net/misc/bezier.html) to find P1=red (eg. 50,0), P2=purple (eg. 100,80) and Threshold=green (eg. 27) of your desired curve. The x-axis is the input pressure you apply to the pen; the y-axis is the output pressure the application is given. ([example curve](http://250kb.de/u/150207/p/FoS1SiXuZQRP.png))

You can immediately test your desired values for your device (eg. "Wacom Intuos4 6x9 stylus") with

```
 xsetwacom --set "Wacom Intuos4 6x9 stylus" PressureCurve "50" "0" "100" "80"
 xsetwacom --set "Wacom Intuos4 6x9 stylus" Threshold "27"

```

Later you can apply them in `/etc/X11/xorg.conf` as shown below or you use the above shell commands in any startup script

 `/etc/X11/xorg.conf` 
```
  Option        "PressCurve"    "50,0,100,80"         # Custom preference
  Option        "Threshold"     "27"                  # sensitivity to do a "click"

```

### 力量比例

For standard (**16:9**) widescreen monitors with Wacom tablets it is a typical problem that your strokes are slightly more horizontally oriented than they physically were (so for example a perfectly drawn circle with the pen will turn into a horizontal ellipse in the computer) because the tablet drawing surface proportions are larger on the vertical axis by default (**16:10**) than your monitors aspect ratio and this inconsistency will subtly distort your strokes. It is possible to force the proportions of the drawing surface to match the aspect ratio of your monitor to solve this problem by cutting off the bottom of the drawing surface to accommodate for the differences in vertical resolution with the below options. This is an alternative to the "Force Proportions" option in the Windows driver settings. It is generally recommended to do this to ensure maximum accuracy of your tablet input.

To get the tablets default values run the following command (where "device name or ID" would be for your stylus):

```
   xsetwacom --get "device name or ID" Area

```

After this you can figure out your tablet's resolution by dividing the values with the ratio **11.25** (so **21600/11.25=1920** and **13500/11.25=1200**), so to convert this to **1920x1080** (**16:9**) resolution, do **1080*11.25=12150** then to set the proportions with xsetwacom:

```
   xsetwacom --set "device name or ID" Area 0 0 21600 12150

```

Here is how to do the same in the xorg configuration file:

```
   Option "BottomX" "21600"
   Option "BottomY" "12150"

```

(An alternative formula would would be aspect ratio multiplied by **1350**. So **16:9** is **16*1350=21600** and **9*1350=12150**)

**Note:** There is also a KeepShape option which reportedly should do this automatically but it does not seem to work, which is why we have to do it the hard way. I do not know whether these values should be kept the same or increased on a bigger resolution monitor, but I highly suspect that they should be kept the same (e.g. the values are relative to the tablet's resolution, not the monitor's resolution; the important part is that the aspect ratio is correct, not that the resolution is a match)

### 使用kcm-wacomtablet

The KDE configuration module [kcm-wacomtablet](https://aur.archlinux.org/packages/kcm-wacomtablet/) (or if you're on Plasma 5, [kcm-wacomtablet-frameworks-git](https://aur.archlinux.org/packages/kcm-wacomtablet-frameworks-git/)) supports easy configuration of the tablet through a graphical user interface, allowing for different profiles and proper hotplugging support. It will auto-detect the type of your tablet, and load your configuration profile automatically when the tablet is plugged in.

## 针对特定应用程序的配置

### Blender

To enable pad buttons and extra pen buttons in blender, you can create a xsetwacom wrapper to temporarily remap buttons for your blender session.

Provided example (for Bamboo fun) adapted to **Sculpt** mode: [blender_sculpt.sh](http://pastebin.archlinux.fr/1887946)

It remaps

*   Left tablet buttons to **Shift** and **Control** *(pan/tilt/zoom/smooth/invert)*
*   Right tablet buttons to **F** *(brush size/strenght)* and **Control-z** *(undo)*
*   Top pen button ton **m** *(mask control)*

### GIMP

To enabled proper usage, and pressure sensitive painting in [GIMP](http://www.gimp.org), just go to *Edit → Input Devices*. Now for each of your *eraser*, *stylus*, and *cursor* **devices**, set the **mode** to *Screen*, and remember to save.

*   Please take note that if present, the *pad* **device** should be kept disabled as I do not think GIMP supports such things. Alternatively, to use such features of your tablet you should map them to keyboard commands with a program such as [Wacom ExpressKeys](http://hem.bredband.net/devel/wacom/).

*   You should also take note that the tool selected for the *stylus* is independent to that of the *eraser*. This can actually be quite handy, as you can have the *eraser* set to be used as any tool you like.

For more information checkout the *Setting up GIMP* section of [GIMP Talk - Community - Install Guide: Getting Wacom Drawing Tablets To Work In Gimp](http://www.gimptalk.com/forum/topic.php?t=17992&start=1).

If the above was not enough, you may want to try setting up the tablet's stylus (and eraser) as a second mouse pointer (separating it from your mouse) by using the `xinput create-master` and `xinput reattach` commands. It can help when GIMP does not start painting even if the stylus touches the tablet.

### Inkscape

As in GIMP, to do the same simply got to *Edit → Input Devices...*. Now for each of your *eraser*, *stylus*, and *cursor* **devices**, set the **mode** to *Screen*, and remember to save.

### Krita

If your tablet does not draw in Krita (clicks/pressure are not registered) but works in the brush selection dialog which has a small test area, try putting Krita in full-screen or canvas-only mode.

Krita only requires that Qt is able to use your tablet to function properly. If your tablet is not working in Krita, then make sure to check it is working in Qt first. The effect of tablet pressure can then be tweaked in the painttop configuration, for example by selecting opacity, then selecting pressure from the drop down and adjusting the curve to your preference.

### VirtualBox

First, make sure that your tablet works well under Arch. Then, download and install the last driver from [Wacom website](http://www.wacom.com/downloads/drivers.php) on the guest OS. Shutdown the virtual machine, go to **Settings > USB**. Select **Add Filter From Device** and select your tablet (e.g. WACOM CTE-440-U V4.0-3 [0403]). Select **Edit Filter**, and change the last item **Remote** to **Any**.

### Web Browser Plugin

A plugin that imitates the official Wacom web plugin can be found on the AUR as [wacomwebplugin](https://aur.archlinux.org/packages/wacomwebplugin/). It has been tested successfully using Chromium and Firefox.

With this plugin it is possible to make use of online tools such as [deviantART's Muro](http://sta.sh/muro/). This plugin is in early stages so as always, your mileage may vary.

## 故障排除

对于新的数位板，其驱动可能还没有进入内核，需要额外的操作。一个著名的例子是新的 Intuos 数位板(Draw/Comic/Photo)。

### 未知的设备类型

如果你的数位板无法被 `xsetwacom` 识别，并且 `dmesg` 抱怨它是一个未知类型的设备，那么你需要安装一个打过补丁的 input-wacom。

请从 [SourceForge](http://sourceforge.net/p/linuxwacom/input-wacom/ci/jiri/for-4.4/~/tarball) 下载 for-4.4 分支并安装。 之后运行以下命令后你的设备应当可以被识别了：

```
 # rmmod wacom
 # insmod /lib/modules/YOUR_KERNEL/extra/wacom.ko.gz

```

### 系统冻结

如果在激活数位板的触控笔时，系统被冻结，那么你需要为你的内核打[补丁](/index.php/Patch "Patch")：[LKML](https://lkml.org/lkml/2015/11/20/690)。

## 参考文献

*   [Linux Wacom Project Wiki](http://sourceforge.net/apps/mediawiki/linuxwacom/index.php?title=Main_Page)
*   [GIMP Talk - Community - Install Guide: Getting Wacom Drawing Tablets To Work In Gimp](http://www.gimptalk.com/forum/topic.php?t=17992&start=1)
*   [Ubuntu Help: Wacom](https://help.ubuntu.com/community/Wacom)
*   [Ubuntu Forums - Install a LinuxWacom Kernel Driver for Tablet PC's](http://ubuntuforums.org/showthread.php?t=1038949)