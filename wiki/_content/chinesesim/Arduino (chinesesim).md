**翻译状态：** 本文是英文页面 [Arduino](/index.php/Arduino "Arduino") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2019-12-17，点击[这里](https://wiki.archlinux.org/index.php?title=Arduino&diff=0&oldid=592053)可以查看翻译后英文页面的改动。

[Arduino](https://en.wikipedia.org/wiki/Arduino "wikipedia:Arduino") 是一款便捷灵活、方便上手的开源电子原型平台。它适用于艺术家，设计师，业余爱好者以及任何对创建交互式对象或环境感兴趣的人。

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 安装](#安装)
    *   [1.1 AVR Boards](#AVR_Boards)
    *   [1.2 Pinoccio Scout](#Pinoccio_Scout)
    *   [1.3 Intel Galileo](#Intel_Galileo)
    *   [1.4 On Arm7 devices](#On_Arm7_devices)
    *   [1.5 RedBear Duo](#RedBear_Duo)
*   [2 配置](#配置)
    *   [2.1 访问串口](#访问串口)
*   [3 stty](#stty)
*   [4 Arduino-Builder](#Arduino-Builder)
*   [5 Alternatives for IDE](#Alternatives_for_IDE)
    *   [5.1 ArduIDE](#ArduIDE)
    *   [5.2 gnoduino](#gnoduino)
    *   [5.3 Arduino-CMake](#Arduino-CMake)
    *   [5.4 Ino](#Ino)
    *   [5.5 Makefile](#Makefile)
    *   [5.6 Arduino-mk](#Arduino-mk)
    *   [5.7 Scons](#Scons)
    *   [5.8 PlatformIO](#PlatformIO)
        *   [5.8.1 Installation](#Installation)
        *   [5.8.2 Usage](#Usage)
    *   [5.9 Emacs](#Emacs)
*   [6 Troubleshooting](#Troubleshooting)
    *   [6.1 Version 1.6](#Version_1.6)
    *   [6.2 Arduino设备命名](#Arduino设备命名)
    *   [6.3 串口错误](#串口错误)
    *   [6.4 Working with Uno/Mega2560](#Working_with_Uno/Mega2560)
    *   [6.5 Not recognizing USB port with Mega2560 cheap Chinese clones](#Not_recognizing_USB_port_with_Mega2560_cheap_Chinese_clones)
    *   [6.6 Application not resizing with WM, menus immediately closing](#Application_not_resizing_with_WM,_menus_immediately_closing)
    *   [6.7 Fails to upload: programmer is not responding](#Fails_to_upload:_programmer_is_not_responding)
*   [7 See also](#See_also)

## 安装

*   安装 [arduino](https://www.archlinux.org/packages/?name=arduino) 和 [arduino-docs](https://www.archlinux.org/packages/?name=arduino-docs) 以便获得离线文档。
*   将用户添加到 `uucp` 和 `lock` [Users and groups (简体中文)](/index.php/Users_and_groups_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Users and groups (简体中文)") ( 详情[#访问串口](#访问串口) )。
*   你可能需要将`cdc_acm`加载到[Kernel module (简体中文)](/index.php/Kernel_modules "Kernel modules")。

### AVR Boards

要使用Arduino Uno等AVR板，您可以选择安装[arduino-avr-core](https://www.archlinux.org/packages/?name=arduino-avr-core)，以使用archlinux上游avr-gcc代替捆绑的旧版avr-core。如果您仍然想使用较旧的arduino-core，则需要将它安装在arduino的开发板管理器中[[1]](https://www.arduino.cc/en/Guide/Cores)。您始终可以在“工具>面板”菜单中的不同内核之间切换。

### Pinoccio Scout

[Pinoccio Scouts](https://pinocc.io/) can also be programmed using the Arduino IDE. Instructions can be found [here](https://pinocc.io/solo). Alternative you can install [arduino-pinoccio](https://aur.archlinux.org/packages/arduino-pinoccio/) from the [AUR](/index.php/AUR "AUR").

### Intel Galileo

要将Intel Galileo开发板与Archlinux一起使用，请安装Arduino IDE，然后通过“工具->板->板管理器”下载Galileo工具包。 修复安装问题，请访问[github](https://github.com/arduino/Arduino/issues/5523)。

### On Arm7 devices

See [here](http://blog.tklee.org/2014/10/arduino-ide-158-on-banana-pi.html) for a work around.

### RedBear Duo

You might need to install [perl-archive-zip](https://www.archlinux.org/packages/?name=perl-archive-zip) or you'll get an error about missing crc32.

## 配置

### 访问串口

arduino开发板通过串口或USB连接到计算机，因此用户需要对串口设备文件具有可读/写访问权限。[Udev](/index.php/Udev "Udev")创建 `uucp`组拥有的 `/ dev / ttyUSB0`之类的文件，因此将用户添加到 `uucp`组将提供所需的读/写访问权限。另外，如果您打算使用默认的Java IDE，请将您的用户添加到 `lock`组以进行 `/ var / lock / lockdev`访问。有关详细信息，请参见[Users and groups (简体中文)#用户组管理](/index.php/Users_and_groups_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#用户组管理 "Users and groups (简体中文)")。

在上传固件到Arduino之前，请确保在“工具”菜单中设置正确的串口，开发板类型和处理器。

## stty

Preparing:

```
# stty -F /dev/ttyACM0 cs8 9600 ignbrk -brkint -imaxbel -opost -onlcr -isig -icanon -iexten -echo -echoe -echok -echoctl -echoke noflsh -ixon -crtscts

```

Sending commands through Terminal without new line after command

```
# echo -n "Hello World" > /dev/ttyACM0

```

**Note:** As autoreset on serial connection is activated by default on most boards, you need to disable this feature if you want to communicate directly with your board with the last command instead of a terminal emulator (arduino IDE, screen, picocom...). If you have a Leonardo board, you are not concerned by this, because it does not autoreset. If you have an Uno board, connect a 10 µF capacitor between the RESET and GND pins. If you have another board, connect a 120 ohms resistor between the RESET and 5V pins. See [http://playground.arduino.cc/Main/DisablingAutoResetOnSerialConnection](http://playground.arduino.cc/Main/DisablingAutoResetOnSerialConnection) for more details.

Reading what your Arduino has to tell you

```
$ cat /dev/ttyACM0

```

## Arduino-Builder

You can also build Arduino sketches with the [arduino-builder](https://www.archlinux.org/packages/?name=arduino-builder) command line tool. In order to use the provided [arduino-avr-core](https://www.archlinux.org/packages/?name=arduino-avr-core) with upstream [avr-gcc](https://www.archlinux.org/packages/?name=avr-gcc) and [avrdude](https://www.archlinux.org/packages/?name=avrdude) you need to create a small settings file:

 `build.options.json` 
```
{
    "fqbn": "archlinux-arduino:avr:uno",
    "hardwareFolders": "/usr/share/arduino/hardware",
    "toolsFolders": "/usr/bin"
}
```

Compile a sketch with:

```
$ arduino-builder -build-options-file build.options.json blink.ino

```

Or pass all options via command line:

```
$ arduino-builder -fqbn archlinux-arduino:avr:uno -hardware /usr/share/arduino/hardware -tools /usr/bin blink.ino

```

## Alternatives for IDE

### ArduIDE

ArduIDE is a Qt-based IDE for Arduino. [arduide-git](https://aur.archlinux.org/packages/arduide-git/) is available in the [AUR](/index.php/AUR "AUR").

### gnoduino

[gnoduino](https://aur.archlinux.org/packages/gnoduino/) is an implementation of original Arduino IDE for GNOME available in the [AUR](/index.php/AUR "AUR"). The original Arduino IDE software is written in Java. This is a Python implementation and it is targeted at GNOME but will work on xfce4 and other WM. Its purpose is to be light, while maintaining compatibility with the original Arduino IDE. The source editor is based on gtksourceview.

If you prefer working from terminal, below there are some other options to choose from.

### Arduino-CMake

Using [Arduino-CMake-NG](https://github.com/arduino-cmake/Arduino-CMake-NG) and [CMake](http://www.cmake.org/cmake/resources/software.html) you can build Arduino firmware from the command line using multiple build systems. CMake lets you generate the build system that fits your needs, using the tools you like. It can generate any type of build system, from simple Makefiles, to complete projects for Eclipse, Visual Studio, XCode, etc.

Requirements: [cmake](https://www.archlinux.org/packages/?name=cmake), [arduino](https://www.archlinux.org/packages/?name=arduino), [avr-gcc](https://www.archlinux.org/packages/?name=avr-gcc), [avr-binutils](https://www.archlinux.org/packages/?name=avr-binutils), [avr-libc](https://www.archlinux.org/packages/?name=avr-libc), [avrdude](https://www.archlinux.org/packages/?name=avrdude).

### Ino

[Ino](https://github.com/amperka/ino) is a command line toolkit for working with arduino hardware. [ino](https://aur.archlinux.org/packages/ino/) is available in the [AUR](/index.php/AUR "AUR").

### Makefile

**Note:** Update 2015-03-23\. Due to recent changes in Arduino ≥v1.5, many old Makefiles do not work without some modification. A simple Makefile for Arduino version 1.5+ can be found [on GitHub](https://github.com/tomswartz07/arduino-makefile).

Instead of using the Arduino IDE it is possible to use another editor and a Makefile.

Set up a directory to program your Arduino and copy the Makefile into this directory. A copy of the Makefile can be obtained from `/usr/share/arduino/hardware/cores/arduino/Makefile`

You will have to modify this a little bit to reflect your settings. The makefile should be pretty self explanatory. Here are some lines you may have to edit.

```
PORT = usually /dev/ttyUSBx, where x is the usb serial port your arduino is plugged into
TARGET = your sketch's name
ARDUINO = /usr/share/arduino/lib/targets/arduino

```

Depending on which library functions you call in your sketch, you may need to compile parts of the library. To do that you need to edit your SRC and CXXSRC to include the required libraries.

Now you should be able to `make && make upload` to your board to execute your sketch.

### Arduino-mk

[arduino-mk](https://aur.archlinux.org/packages/arduino-mk/) is another alternative Makefile approach. It allows users to have a local Makefile that includes Arduino.mk. See [project page](https://github.com/sudar/Arduino-Makefile) for usage.

For Arduino 1.5, try the following local Makefile (because Arduino 1.5's library directory structure is slightly different):

```
ARDUINO_DIR = /usr/share/arduino
ARDMK_DIR = /usr/share/arduino
AVR_TOOLS_DIR = /usr
AVRDUDE_CONF = /etc/avrdude.conf
ARDUINO_CORE_PATH = /usr/share/arduino/hardware/archlinux-arduino/avr/cores/arduino
BOARDS_TXT = /usr/share/arduino/hardware/archlinux-arduino/avr/boards.txt
ARDUINO_VAR_PATH = /usr/share/arduino/hardware/archlinux-arduino/avr/variants
BOOTLOADER_PARENT = /usr/share/arduino/hardware/archlinux-arduino/avr/bootloaders

BOARD_TAG    = uno
ARDUINO_LIBS =

include /usr/share/arduino/Arduino.mk

```

In some cases you could need to install [avr-libc](https://www.archlinux.org/packages/?name=avr-libc) and [avrdude](https://www.archlinux.org/packages/?name=avrdude).

### Scons

Using [scons](http://www.scons.org/) together with [arscons](https://github.com/suapapa/arscons) it is very easy to use to compile and upload Arduino projects from the command line. Scons is based on python and you will need python-pyserial to use the serial interface. Install [python-pyserial](https://www.archlinux.org/packages/?name=python-pyserial) and [scons](https://www.archlinux.org/packages/?name=scons).

That will get the dependencies you need too. You will also need Arduino itself so install it as described above. Create project directory (eg. test), then create a arduino project file in your new directory. Use the same name as the directory and add .ino (eg. test.ino). Get the [SConstruct](https://github.com/suapapa/arscons/blob/master/SConstruct) script from arscons and put it in your directory. Have a peek in it and, if necessary, edit it. It is a python script. Edit your project as you please, then run

```
$ scons                # This will build the project
$ scons upload         # This will upload the project to your Arduino

```

### PlatformIO

[PlatformIO](http://docs.platformio.ikravets.com/en/latest/quickstart.html) is a python tool to build and upload sketches for multiple Hardware Platforms, at the moment of writing these are Arduino/AVR based boards, TI MSP430 and TI TM4C12x Boards. In the near future the author plans to add a library function that allows to search and include libraries directly from GitHub.

#### Installation

Install the [platformio](https://aur.archlinux.org/packages/platformio/) or [platformio-git](https://aur.archlinux.org/packages/platformio-git/) package.

#### Usage

```
$ platformio platforms install atmelavr
$ platformio init
$ vim platformio.ini

```

```
#
# Atmel AVR based board + Arduino Wiring Framework
#
[env:ArduinoMega2560]
platform = atmelavr
framework = arduino
board = megaatmega2560   
upload_port = /dev/ttyACM0 
targets = upload

```

```
$ platformio run

```

### Emacs

It is possible to configure [Emacs](/index.php/Emacs "Emacs") as IDE.

Install the package [emacs-arduino-mode-git](https://aur.archlinux.org/packages/emacs-arduino-mode-git/) from the [AUR](/index.php/AUR "AUR") in order to enable the `arduino-mode` in emacs.

Add to the init script:

 `~/.emacs` 
```
;; arduino-mode
(require 'cl)
(autoload 'arduino-mode "arduino-mode" "Arduino editing mode." t)
(add-to-list 'auto-mode-alist '("\.ino$" . arduino-mode))
```

You can compile and upload the sketches using `Arduino-mk` (see above) with `M-x compile` `make upload`.

Main resource: [here](http://www.emacswiki.org/emacs/ArduinoSupport).

## Troubleshooting

### Version 1.6

Some older 3rd party tools may only work with Arduino 1.0 ([arduino10](https://aur.archlinux.org/packages/arduino10/)). Some of the tools may partially work for Arduino version 1.6 ([arduino](https://www.archlinux.org/packages/?name=arduino)) and after. Check the version if the tools do not work. Note that some newer boards do not work with the old Arduino IDE.

### Arduino设备命名

如果您有多个arduino，您可能已经注意到，它们的名称/ dev / ttyUSB [0-9]是按连接顺序分配的。在IDE中，这并不是什么大问题，但是当您编写了自己的软件以在后台与arduino项目进行通信时，这可能会很烦人。使用以下udev规则为arduino分配静态符号链接：

 `/etc/udev/rules.d/52-arduino.rules` 
```
SUBSYSTEMS=="usb", KERNEL=="ttyUSB[0-9]*", ATTRS{idVendor}=="0403", ATTRS{idProduct}=="6001", SYMLINK+="sensors/ftdi_%s{serial}"

```

您的arduino将以"/dev/sensors/ftdi_A700dzaF"之类的名称提供。如果您愿意，还可以为多个设备分配更有意义的名称，如下所示：

 `/etc/udev/rules.d/52-arduino.rules` 
```
SUBSYSTEMS=="usb", KERNEL=="ttyUSB[0-9]*", ATTRS{idVendor}=="0403", ATTRS{idProduct}=="6001", ATTRS{serial}=="A700dzaF", SYMLINK+="arduino/nano"

```

这将在/dev/arduino/nano中创建到具有指定序列号的设备的符号链接。

您需要将arduino拔出并重新插入才能使它生效或运行。

```
udevadm trigger

```

常见的`idVendor`/`idProduct`对可在发行包中的`hardware/arduino/avr/boards.txt`中找到。 请注意，其中一些(尤其是[FTDI](https://en.wikipedia.org/wiki/FTDI "wikipedia:FTDI"))并不是Arduino平台所独有的。 使用`serial`属性是区分各种设备的好方法。

### 串口错误

在IDE启动时，您可能最初会看到串行端口，但是在上传固件时，TX/RX指示灯不起作用。您以前可能已经将串口中的波特率更改为了它不喜欢的内容。编辑～/.arduino/preferences.txt，使serial.debug_rate和Arduino设备相匹配。

### Working with Uno/Mega2560

The Arduino Uno and Mega2560 have an onboard USB interface (an Atmel 8U2) that accepts serial data, so they are accessed through /dev/ttyACM0 created by the cdc-acm kernel module when it is plugged in.

The 8U2 firmware may need an update to ease serial communications. See [[2]](http://www.arduino.cc/cgi-bin/yabb2/YaBB.pl?num=1286350399) for more details and reply #11 for a fix. The original arduino bbs, where you can find an image explaining how to get your Uno into DFU, is now in a read-only state. If you do not have an account to view the image, see [[3]](http://www.scribd.com/doc/45913857/Arduino-UNO).

You can perform a general function test of the Uno by putting it in loopback mode and typing characters into the arduino serial monitor at 115200 baud. It should echo the characters back to you. To put it in loopback, short pins 0 -> 1 on the digital side and either hold the reset button or short the GND -> RESET pins while you type.

### Not recognizing USB port with Mega2560 cheap Chinese clones

Try installing its driver: [i2c-ch341-dkms](https://aur.archlinux.org/packages/i2c-ch341-dkms/).

### Application not resizing with WM, menus immediately closing

see [Java#Gray window, applications not resizing with WM, menus immediately closing](/index.php/Java#Gray_window,_applications_not_resizing_with_WM,_menus_immediately_closing "Java")

### Fails to upload: programmer is not responding

Changing processor setting from `ATmega328P` to `ATmega328P (Old Bootloader)` (See Tools->Processor in Arduino IDE) may help with upload failures.

## See also

*   [Official website](https://www.arduino.cc/)
*   [https://bbs.archlinux.org/viewtopic.php?pid=295312](https://bbs.archlinux.org/viewtopic.php?pid=295312)
*   [https://bbs.archlinux.org/viewtopic.php?pid=981348](https://bbs.archlinux.org/viewtopic.php?pid=981348)
*   [http://answers.ros.org/question/9097/how-can-i-get-a-unique-device-path-for-my-arduinoftdi-device/](http://answers.ros.org/question/9097/how-can-i-get-a-unique-device-path-for-my-arduinoftdi-device/)
*   [https://www.reddit.com/r/archlinux/comments/8j53dq/how_do_i_install_ch340_chip_drivers_on_arch/](https://www.reddit.com/r/archlinux/comments/8j53dq/how_do_i_install_ch340_chip_drivers_on_arch/)