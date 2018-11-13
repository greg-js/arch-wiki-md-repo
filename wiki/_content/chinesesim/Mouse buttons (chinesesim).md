Related articles

*   [Mouse acceleration](/index.php/Mouse_acceleration "Mouse acceleration")
*   [Mouse polling rate](/index.php/Mouse_polling_rate "Mouse polling rate")

**翻译状态：** 本文是英文页面 [Mouse buttons](/index.php/Mouse_buttons "Mouse buttons") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2017-10-13，点击[这里](https://wiki.archlinux.org/index.php?title=Mouse+buttons&diff=0&oldid=493023)可以查看翻译后英文页面的改动。

这篇文章将介绍如何配置按键超过 3 个的鼠标。

## Contents

*   [1 写在前面](#写在前面)
*   [2 查找鼠标名称](#查找鼠标名称)
*   [3 配置Xorg](#配置Xorg)
*   [4 Post Configuration](#Post_Configuration)
    *   [4.1 Google Chrome](#Google_Chrome)
    *   [4.2 Opera](#Opera)
    *   [4.3 Firefox](#Firefox)
        *   [4.3.1 Horizontal scroll](#Horizontal_scroll)
    *   [4.4 Thumb Buttons - forward and back](#Thumb_Buttons_-_forward_and_back)
    *   [4.5 xmodmap tweaking](#xmodmap_tweaking)
    *   [4.6 xinput tweaking](#xinput_tweaking)
*   [5 Alternate methods](#Alternate_methods)
    *   [5.1 IMPS/2](#IMPS/2)
    *   [5.2 ExplorerPS/2](#ExplorerPS/2)
    *   [5.3 Auto](#Auto)
    *   [5.4 easystroke](#easystroke)
*   [6 Binding keyboard to mouse buttons](#Binding_keyboard_to_mouse_buttons)
    *   [6.1 xvkbd and xbindkeys](#xvkbd_and_xbindkeys)
    *   [6.2 evrouter](#evrouter)
    *   [6.3 Binding + and - in Logitech G5 mouse](#Binding_+_and_-_in_Logitech_G5_mouse)
*   [7 User tools](#User_tools)
*   [8 Device Specific Configuration Files](#Device_Specific_Configuration_Files)
    *   [8.1 Logitech G600](#Logitech_G600)
    *   [8.2 Mad Catz Mouse](#Mad_Catz_Mouse)
    *   [8.3 Logitech M560/M545/M546](#Logitech_M560/M545/M546)

## 写在前面

**Note:** These are helper comments, and can be ignored if you are looking for nothing but raw information. Due to community feedback, I decided to add a bit more commenting that describes what's going on "behind the scenes" with this configuration.

我们将为Xorg使用`evdev`驱动。EVentDEvice是一款高级USB设备驱动，可以提供比常规Xorg `mouse` 驱动更强大，更“直接”的功能，减少输入延迟以及交流问题。

*   注意：`evdev` 是内核与Xorg包共有的输入驱动。所有的Arch内核都与`evdev`模块有关。

较新的Xorg版本（比如11R7.0）只需要进行下列步骤中对 `/etc/X11/xorg.conf` 的更改而不需要其它的步骤。

## 查找鼠标名称

**Note:** 为了得到更准确的信息，有时你需要在未加载Xorg或者鼠标驱动时执行命令。

第一步：查找你鼠标的名字。你可以通过输入以下命令来查询：

```
$ egrep "Name|Handlers" /proc/bus/input/devices | egrep -B1 'Handlers.*mouse'

```

输出会像下面这样:

```
N: Name="Logitech USB Gaming Mouse"
H: Handlers=mouse0 event0 ts0 

```

如果你拥有多于一个的鼠标：

```
N: Name="Kensington Kensington Expert Mouse Wireless"
H: Handlers=event0 mouse0 
--
N: Name="Logitech USB Receiver"
H: Handlers=kbd event2 mouse1

```

**Note:** 译者注：在VMware等虚拟环境下鼠标类型可能与实际不符。

你的鼠标名就是其中一个含有`Handlers=mouse0`的设备名，所以本例中的鼠标名为 `Logitech USB Gaming Mouse`。

**Note:** 本例中使用的鼠标是Logitech G5,你所用的鼠标或许与之不同，所以`名字`可能不同

拷贝你鼠标的名字，打开`/etc/X11/xorg.conf`。

## 配置Xorg

我们需要一个入口点告诉X服务器如何使用这个鼠标，它可能会像是这样：

Section "InputDevice"

```
  Identifier      "Evdev Mouse"
  Driver          "evdev"
  Option          "Name" "Logitech USB Gaming Mouse"
  Option          "evBits"  "+1-2"
  Option          "keyBits" "~272-287"
  Option          "relBits" "~0-2 ~6 ~8"
  Option          "Pass"    "3"
  Option          "CorePointer"
EndSection

```

将`Name`选项用你刚刚复制的名字覆盖。如果你在使用多个鼠标或者在加载Xorg时出现错误，可以忽略掉`CorePointer`选项。其他选项均为`evdev`对鼠标的默认配置，因此应该可以对大多数鼠标生效。

接下来，我们需要告诉X使用这个刚配置好的鼠标，因此，要在`xorg.conf`中寻找`ServerLayout`。

修改`ServerLayout`块来启用“Evdev Mouse”（刚刚设置好的设备的Identifier）。完成后，它应该像下面这样：

```
Section "ServerLayout"
  Identifier     "Default Layout"
  Screen 0       "Monitor0" 0 0
  InputDevice    "Keyboard0" "CoreKeyboard"
  InputDevice    "Evdev Mouse" "CorePointer"
EndSection

```

你只需要更改其中的`InputDevice`一行指向你刚刚配置好的鼠标。

完成后，准备工作就告一段落了。

*   由xxsashixx编辑：

这是为Logitech G5鼠标用户写的。我没有为其他鼠标做测试。不过如果不做这一步，你的鼠标“可能”不能正常工作。 如果你不需要添加这些，就不要添加。

将

```
Option "Device" "/dev/input/event[#]"

```

加入`InputDevice` 块中，不然鼠标可能不会被检测到。 请把[#]替换成下面命令的执行结果：

```
egrep "Name|Handlers" /proc/bus/input/devices

```

*   由bapman编辑：

这个方法完成后，你的鼠标在重启后可能会失灵（因为改变了event number）。如果出现这种情况，你可以在`/dev/input/by-id`中使用symlink，比如：

```
Option      "Device" "/dev/input/by-id/usb-Logitech_USB_Receiver-event-mouse"

```

“usb-Logitech_USB_Receiver-event-mouse”可以使用

```
ls /dev/input/by-id

```

命令查询到。

*   由Diamir编辑：

With a Desktop type keyboard-mouse, this does not work because there is only one USB attachment and `/dev/input/by-id` contains only the keyboard. In this case, we can create a udev rule to get a consistent link. The following rules create the link `/dev/input/usbmouse` which points on the correct event entry:

```
KERNEL=="event[0-9]*", BUS=="usb", SYSFS{modalias}=="usb:v045Ep008Ad7373dc00dsc00dp00ic03isc00ip00", SYMLINK+="input/usbmouse"

```

You can call it `z10_usb_mouse.rules` and put it in `/etc/udev/rules.d`

The cryptic value to use for `SYSFS(modalias)` can be gotten in the following way:

enter the command `cat /proc/bus/input/devices`

You will find the keyboard and the mouse and see event4 is the mouse in this case:

```
I: Bus=0003 Vendor=045e Product=008a Version=0111
N: Name="Microsoft Microsoft Wireless Optical Desktop� 1.00"
P: Phys=usb-0000:00:10.0-2/input0
S: Sysfs=/devices/pci0000:00/0000:00:10.0/usb1/1-2/1-2:1.0/input/input3
U: Uniq=
H: Handlers=kbd event0 
B: EV=120013
B: KEY=1000000000007 ff800000000007ff febeffdff3cfffff fffffffffffffffe
B: MSC=10
B: LED=107

```

```
I: Bus=0003 Vendor=045e Product=008a Version=0111
N: Name="Microsoft Microsoft Wireless Optical Desktop� 1.00"
P: Phys=usb-0000:00:10.0-2/input1
S: Sysfs=/devices/pci0000:00/0000:00:10.0/usb1/1-2/1-2:1.1/input/input4
U: Uniq=
H: Handlers=kbd mouse0 event1 
B: EV=17
B: KEY=3000000000000 0 1f0000 f8400244000 601878d800d448 1e000000000000 0
B: REL=7c3
B: MSC=10

```

So I enter the following command (adapt event # to your particular case):

```
udevinfo -a -p $(udevinfo -q path -n /dev/input/event4) | grep modalias
ATTRS{modalias}=="input:b0003v045Ep008Ae0111-0,1,2,4,k71,72,73,74,83,86,8A,8C,8E,8F,9B,9C,9E,9F,A3,A4,A5,A6,AB,AC,B5,B6,CE,D2,D5,E2,E7,E8,E9,EA,EB,110,111,112,113,114,1B0,1B1,r0,1,6,7,8,9,A,am4,lsfw"
ATTRS{modalias}=="usb:v045Ep008Ad7373dc00dsc00dp00ic03isc00ip00"
ATTRS{modalias}=="pci:v00001106d00003038sv00001043sd000080EDbc0Csc03i00"
```

grab the ATTRS which becomes with usb: to complete "SYSFS{modalias}== " entry

And finally, use `usbmouse` as the Device Option in `xorg.conf`:

```
Option "Device" "/dev/input/usbmouse"

```

## Post Configuration

### Google Chrome

It works. Horizontal scroll works out of the box - push the scroll wheel left or right. Thumb buttons also work as next/previous page.

### Opera

It works. Note: buttons can be mapped to functions easily in `Preferences > Advanced > Shortcuts > Mouse set-up`. For example, to bind *button 8* to *back*:

1.  Navigate to mouse set-up and expand the *Application* drop-down
2.  In the input column, type: *Button 8*
3.  In the actions column, type: *Back*

### Firefox

#### Horizontal scroll

To get back and forward enabled, instead of scroll left/right, change the following settings in `about:config`:

```
mousewheel.default.action.override_x         2
mousewheel.default.delta_multiplier_x       -100

```

### Thumb Buttons - forward and back

**Note:** The following maybe redundant depending on whether xev detects all your mouse buttons correctly (functions can be mapped on a per-app basis) or you want to change the default behaviour.

To do this we need to map keystrokes to the desired mouse buttons and install [xvkbd](https://aur.archlinux.org/packages/xvkbd/) and [xbindkeys](https://www.archlinux.org/packages/?name=xbindkeys).

In most modern applications which use back/forward features, XF86Back is mapped to back and XF86Forward is mapped to forward by default. On most MX mice the thumb buttons resolve to 8 & 9\. If your mouse is different, check button numbers using xev and replace the numbers used in the example (b:8 & b:9).

So if you have an MX mouse you would create the file ~/.xbindkeysrc, containing:

```
# Mouse Buttons
"xvkbd -xsendevent -text "\[XF86Back]""
m:0x0 + b:8 
"xvkbd -xsendevent -text "\[XF86Forward]""
m:0x0 + b:9

```

Now to test... Run the following command and if it works as expected remember to add xbindkeys to `.xinitrc` or somewhere where it will be executed each time X starts. Also, this should work with Epiphany and Konqueror without any additional configuration or use of [Imwheel](/index.php/Imwheel "Imwheel").

```
xbindkeys

```

The above info and more help may be found in the [MX1000 Buttons](/index.php/MX1000_Buttons "MX1000 Buttons") wiki.

### xmodmap tweaking

**Note:** None of the below is necessary with evdev, but it's here for non-evdev users. Unless something does not work on your mouse, ignore this whole section!

If you use .xinitrc to load X, then add this to `.xinitrc` (change for the number of buttons you have):

```
 xmodmap -e "pointer = 1 2 3 6 7 8 9 10 11 12 4 5" &

```

Note that buttons 4 and 5 **must go on the end** or else your scroll wheel will not work.

If you use GDM/XDM/KDM instead of .xinitrc, then create the file `~/.Xmodmap` and add this to it (change for the number of buttons you have):

```
 pointer = 1 2 3 6 7 8 9 10 11 12 4 5

```

*   GDM/XDM/KDM read the `~/.Xmodmap` file if it's present, whereas `startx` does not. Another solution would be to add this to your ~/.xinitrc: `xmodmap ~/.Xmodmap`. This would allow you to use *DM and `startx` while only having to edit `~/.Xmodmap` when you need to make changes.

You may have to play with these numbers a bit to get your desired behavior. Some mice use buttons 6 and 7 for the scroll wheel, in which case those buttons would have to be the last numbers. Keep playing with it until it works!

You can also check to see which buttons are being read with a program called 'xev', which is part of XOrg. When xev is run, it will show a box on your desktop that you can put the cursor into and click buttons to find out what buttons have been mapped.

### xinput tweaking

For debugging purposes `xinput` can be used as it is able to change the button map on the fly in userspace. The following line corrects the button mapping (there have been reported cases with Logitech M505/B605 mice and possibly others) so the received events are mapped correctly:

```
 $ xinput set-button-map "$(xinput | awk -F'[=]' '/Logitech M505\/B605/ {print $2}' | awk '{print $1}')" 1 2 3 4 5 8 9

```

## Alternate methods

The following methods use standard X.org mouse input driver (xf86-input-mouse) instead of using the evdev driver. It works on mice up to 7 buttons. Edit `/etc/X11/xorg.conf` InputDevice section for your mouse to reflect the changes shown below. Then restart X and you are done.

### IMPS/2

This has been tested on an IntelliMouse Explorer 3.0\. Your mileage may vary, as this does not seem to work for all said mice.

```
   Driver      "mouse"
   Option      "Protocol" "IMPS/2"
   Option      "Device" "/dev/input/mice"
   Option      "ZAxisMapping" "4 5 6 7"

```

### ExplorerPS/2

This has been tested on a Logitech MX400 and MX518 and should work on any mx series mouse with up to 7 buttons.

```
   Driver         "mouse"
   Option         "Protocol" "ExplorerPS/2"
   Option         "Device" "/dev/input/mice"
   Option         "Buttons" "7"
   Option         "ZAxisMapping" "4 5"
   Option         "ButtonMapping" "1 2 3 6 7"

```

Settings from above also works for Microsoft InteliMouse Explorer 3.0 that connects through USB.

### Auto

This has been tested on a Logitech MX400 and should work on most mice with up to 7 buttons.

```
   Driver         "mouse"
   Option         "Protocol" "auto"
   Option         "Device" "/dev/input/mice"
   Option         "Buttons" "7"
   Option         "ZAxisMapping" "4 5"
   Option         "ButtonMapping" "1 2 3 6 7"

```

This has been tested to work with Logitech MX1000.

```
   Driver         "mouse"
   Option         "Protocol" "auto"
   Option         "Device" "/dev/input/mice"
   Option         "Emulate3Buttons" "no"
   Option         "Buttons" "12"
   Option         "ZAxisMapping" "4 5 7 6 8 9"

```

### easystroke

[easystroke is a gesture-recognition application for X11](http://sourceforge.net/projects/easystroke/)

easystroke is a mouse gesture application, but it can be used to manage mouse buttons as well. It's main advantage o-ver btnx is that it's more versatile. On the other hand, it's user-based, so any user has to configure it to reflect his own needs.

In order to set up easystroke to manage your extra mouse buttons, you will need to do this (example features Back/Forward mouse buttons) : run:

```
easystroke -g

```

Go to Preferences tab > Additional buttons > Add, and add any special button.

**Note:** In case of easystroke does not automatically detect mouse buttons, you can specify it manually. Button identifiers (numbers) can be viewed by xev.

Go to *Action tab > Add action*, give the new action a name, as Type choose "Key", as Details set "Alt+Left" for Back button, "Alt+Right" for Forward button, as Stroke click the proper mouse button (confirm if a warning is displayed), and voilà! Your mouse button is configured.

## Binding keyboard to mouse buttons

### xvkbd and xbindkeys

Let us say we want to bind some mouse buttons to keyboard ones. The problem we will encounter is that we do not know how to emulate a key press. Here comes in handy [xvkbd](https://aur.archlinux.org/packages/xvkbd/). We can use it along with [xbindkeys](https://www.archlinux.org/packages/?name=xbindkeys).

```
$ xbindkeys --defaults >> ~/.xbindkeysrc
$ xbindkeys

```

To restart xbindkeys type:

```
$ pkill -f xbindkeys
$ xbindkeys 

```

Here is example `~/.xbindkeysrc` config:

```
"xvkbd  -text "\[F8]""
       m:0x0 + b:8
"xvkbd  -text "\[Shift]\[Left]""
       m:0x0 + b:9
"xvkbd  -text "\[Shift]\[Right]""
       m:0x0 + b:10
"xvkbd  -text 2"
       m:0x0 + b:11
"xvkbd  -text 3"
       m:0x0 + b:12

```

If you want to check your mouse buttons number use xev. Do not forget to type capital letters in xvkbd -text usage and to escape opening bracket with \ or you get simply [Shift] written.

Here is an example for xbindkeys to enable x selection paste(third click pasting), you need both xsel and xvkbd installed, What it does it executes that command whenever button 13 of the mouse is pressed (in ~/.xbindkeysrc) :

```
 "xvkbd -no-jump-pointer -text "\D1$(xsel)" 2>/dev/null"
 b:13

```

This is an example for a keybinding for Meta+M:

```
 "xvkbd  -text "\{+Super_L}m\{-Super_L}""
 b:10

```

### evrouter

Some programs, especially games, use different methods of reading input, so another program is needed: [evrouter](https://aur.archlinux.org/packages/evrouter/).

For the `evrouter` command to be able to read the input devices, it will have to be run in the `input` group (or as root). This can be achieved by adding yourself to that group:

```
# gpasswd -a *user* input

```

Now we can use the `--dump` option to display what the button to be changed is called:

**Tip:** For USB devices udev will usually create symbolic links in `/dev/input/by-id/` which can be used to refer to specific devices.
 `$ evrouter --dump /dev/input/event*` 
```
device  0: /dev/input/event0: AT Translated Set 2 keyboard
device  1: /dev/input/event1: Microsoft Microsoft Trackball Explorer®
device  2: /dev/input/event2: Sleep Button
device  3: /dev/input/event3: Power Button
device  4: /dev/input/event4: Power Button
device  5: /dev/input/event5: PC Speaker
Display name: :0.0

```

Now press the buttons that you wish to change:

```
Window "(null)": # Window title
# Window "(null)": # Resource name
# Window "(null)": # Class name
"Microsoft Trackball Explorer®" "/dev/input/event1" none key/275 "fill this in!"

Window "(null)": # Window title
# Window "(null)": # Resource name
# Window "(null)": # Class name
"Microsoft Trackball Explorer®" "/dev/input/event1" none key/276 "fill this in!"

```

The line that ends with "fill this in!" can be copied into the config file which by default is `~/.evrouterrc`. For example, using the X11 key event emulator built into evrouter:

 `~/.evrouterrc` 
```
"Microsoft Trackball Explorer®" "/dev/input/event*" any key/275 "XKey/1"
"Microsoft Trackball Explorer®" "/dev/input/event*" any key/276 "XKey/2"
```

The 'event1' was changed to 'event*' in case udev gives it a different device number at boot. The 'none' was changed to 'any' so that the rule works even if any modifier keys are pressed when the button is pressed. To determine the key codes (in brackets) you can use

```
# xmodmap -pk

```

See evrouter(1) for a full explanation of the fields.

**Tip:** Rules can apply only to specific windows, see evrouter(1) for details.

After setting up the config file, run it as a daemon:

```
$ evrouter /dev/input/event*

```

To stop the daemon:

```
$ evrouter -q
$ rm -f /tmp/.evrouter*

```

**Note:** `evrouter` will fail to start if the `/tmp/.evrouter:0.0` file exists but does not delete it when exiting, so you will have to delete it yourself.

### Binding + and - in Logitech G5 mouse

If you want to bind the buttons `+` and `-` in G5/7 mouse, which normally changes DPI, you have to use `g5hack` [[2]](http://piie.net/temp/g5_hiddev.c) released by a lomoco author.

```
wget http://piie.net/temp/g5_hiddev.c
gcc -o g5hack g5_hiddev.c
./g5hack /dev/usb/hiddev0 3

```

This will change your DPI to 2000, light the 1st LED and disables DPI on-the-fly changing, so you can use it with evrouter. If you would use it frequently I suggest you to copy it to the `/usr/bin` directory:

```
# cp g5hack /usr/bin/

```

If you want to bind your `+` and `-` buttons you must copy the line at the bottom (one with the comment '"-" button does not function anymore' above) to the mode you will be using, like, for example, under the "case 3:" you can put it on the line with the comment 'turn on third led' above (deleting the old one before of course).

For the newest G5 mouse which is reported as "product 0xc049" original hack does not work. You have to simply change the `#define MOUSE_G5 0xc041` to `#define MOUSE_G5 0xc049` and recompile.

You can execute the g5hack tool at system start up using systemd unit. See [Systemd#Writing unit files](/index.php/Systemd#Writing_unit_files "Systemd") for detail.

## User tools

[imwheel](https://www.archlinux.org/packages/?name=imwheel) provides configurable mouse wheel and button mapping. It can be configured globally or for individual processes.

Sample `~/.imwheelrc` to enable back/forward thumb buttons for all applications and increased scroll speed in Chromium:

```
"^chromium$"
None, Up, Button4, 3
None, Down, Button5, 3

".*"
None, Thumb1, Alt_L|Left
None, Thumb2, Alt_L|Right

```

[lomoco](https://aur.archlinux.org/packages/lomoco/) for Logitech MX mice will help you set the proper resolution, enable or disable smart scroll (with boot time support too!), etc. lomoco is available from the `[community]` repository and can be installed with the following command:

Be sure to look at `/etc/udev/lomoco_mouse.conf` and set up the the options you want to be automatically applied when the mouse gets loaded by [udev](/index.php/Udev "Udev").

**Note:** The lomoco package may be out of date. There is a hack for newer Logitech mice: [[3]](http://piie.net/temp/g5_hiddev.c)

## Device Specific Configuration Files

### Logitech G600

It is known that in xorg-server 1.18.0-3 side buttons of G600 are not recognized as a separate keyboard device, but another mouse which causes strange (moving mouse cursor to an edge of screen when one of main mouse buttons are clicked) behavior. To force xorg to recognize them as a keyboard buttons, add following section to your `/etc/X11/xorg.conf`:

```
Section "InputClass"
    Identifier "G600 misconfiguration fix"
    MatchProduct "G600"
    # Match just the keyboard section of the G600
    MatchIsKeyboard "true"
    # evdev assumes it's a mouse when it sees the absolute axis. Stop that from happening. 
    Option "IgnoreAbsoluteAxes" "on"  
EndSection

```

### Mad Catz Mouse

[Mad Catz Mouse](/index.php/Mad_Catz_Mouse "Mad Catz Mouse")

### Logitech M560/M545/M546

These mouse is designed for Windows 8, and has a non conventional behavior: the mouse appears as a pair of mouse and keyboard and some buttons don't emit the standard mouse button event, but instead a combination of keyboard and mouse button. This prevent a "confortable" use of this mouse under Linux.

This driver allow to use this mouse like an ordinary mouse. It's recommend use it with xbindkeys to mapping buttons.

[kernel module for M560](https://github.com/kreijack/logitech-m560)(already merged into kernel v4.2)

[kernel module for M545/M546](https://github.com/CzBiX/logitech-m560/tree/m545)