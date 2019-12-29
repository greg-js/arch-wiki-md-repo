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
*   [5 IDE 替代](#IDE_替代)
    *   [5.1 ArduIDE](#ArduIDE)
    *   [5.2 gnoduino](#gnoduino)
    *   [5.3 Arduino-CMake](#Arduino-CMake)
    *   [5.4 Ino](#Ino)
    *   [5.5 Makefile](#Makefile)
    *   [5.6 Arduino-mk](#Arduino-mk)
    *   [5.7 Scons](#Scons)
    *   [5.8 PlatformIO](#PlatformIO)
        *   [5.8.1 安装](#安装_2)
        *   [5.8.2 使用](#使用)
    *   [5.9 Emacs](#Emacs)
*   [6 Troubleshooting](#Troubleshooting)
    *   [6.1 Version 1.6](#Version_1.6)
    *   [6.2 Arduino设备命名](#Arduino设备命名)
    *   [6.3 串口错误](#串口错误)
    *   [6.4 使用Uno/Mega2560](#使用Uno/Mega2560)
    *   [6.5 Mega2560无法识别USB端口](#Mega2560无法识别USB端口)
    *   [6.6 Application not resizing with WM, menus immediately closing](#Application_not_resizing_with_WM,_menus_immediately_closing)
    *   [6.7 上传失败](#上传失败)
*   [7 See also](#See_also)

## 安装

*   安装 [arduino](https://www.archlinux.org/packages/?name=arduino) 和 [arduino-docs](https://www.archlinux.org/packages/?name=arduino-docs) 以便获得离线文档。
*   将用户添加到 `uucp` 和 `lock` [Users and groups (简体中文)](/index.php/Users_and_groups_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Users and groups (简体中文)") ( 详情[#访问串口](#访问串口) )。
*   你可能需要将`cdc_acm`加载到[Kernel module (简体中文)](/index.php/Kernel_modules "Kernel modules")。

### AVR Boards

要使用Arduino Uno等AVR板，您可以选择安装 [arduino-avr-core](https://www.archlinux.org/packages/?name=arduino-avr-core)，以使用archlinux上游avr-gcc代替捆绑的旧版avr-core。如果您仍然想使用较旧的arduino-core，则需要将它安装在arduino的开发板管理器中[[1]](https://www.arduino.cc/en/Guide/Cores)。您始终可以在“工具>面板”菜单中的不同内核之间切换。

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

设置:

```
# stty -F /dev/ttyACM0 cs8 9600 ignbrk -brkint -imaxbel -opost -onlcr -isig -icanon -iexten -echo -echoe -echok -echoctl -echoke noflsh -ixon -crtscts

```

通过终端发送命令，无换行

```
# echo -n "Hello World" > /dev/ttyACM0

```

**Note:** 由于大多数板上默认情况下会激活串行连接上的自动重置功能，因此，如果要使用最后一条命令而不是终端仿真器（arduino IDE，屏幕，picocom ...）直接与您的板通信，则需要禁用此功能。如果您有Leonardo面板，则不必担心，因为它不会自动重置。如果您有Uno板，请在RESET和GND引脚之间连接一个10 µF电容器。如果有另一块板，则在RESET和5V引脚之间连接一个120欧姆的电阻。 有关更多详细信息，请参见 [http://playground.arduino.cc/Main/DisablingAutoResetOnSerialConnection](http://playground.arduino.cc/Main/DisablingAutoResetOnSerialConnection)

读取Arduino发送的信息

```
$ cat /dev/ttyACM0

```

## Arduino-Builder

您也可以使用[arduino-builder](https://www.archlinux.org/packages/?name=arduino-builder)命令行工具来构建Arduino的内置例程。 为了使用所提供的[arduino-avr-core](https://www.archlinux.org/packages/?name=arduino-avr-core)与上游[avr-gcc](https://www.archlinux.org/packages/?name=avr-gcc)和[avrdude](https://www.archlinux.org/packages/?name=avrdude)你需要创建一个小的设置文件：

 `build.options.json` 
```
{
    "fqbn": "archlinux-arduino:avr:uno",
    "hardwareFolders": "/usr/share/arduino/hardware",
    "toolsFolders": "/usr/bin"
}
```

通过下面的命令来编译一个内置例程:

```
$ arduino-builder -build-options-file build.options.json blink.ino

```

或通过命令行传递所有选项:

```
$ arduino-builder -fqbn archlinux-arduino:avr:uno -hardware /usr/share/arduino/hardware -tools /usr/bin blink.ino

```

## IDE 替代

### ArduIDE

ArduIDE是基于QT的Arduino IDE。已在[AUR](/index.php/AUR "AUR")中可用[arduide-git](https://aur.archlinux.org/packages/arduide-git/)。

### gnoduino

[gnoduino](https://aur.archlinux.org/packages/gnoduino/)是[AUR](/index.php/AUR "AUR")中可用的GNOME原始Arduino IDE实现。原始的Arduino IDE软件是用Java编写的。这是一个Python的实现，针对GNOME，但可以在xfce4和其他WM上使用。其目的是减轻重量，同时保持与原始Arduino IDE的兼容性。源代码编辑器基于gtksourceview。

如果您更喜欢在终端上工作，则下面还有一些其他选项可供选择。

### Arduino-CMake

阅读[Arduino-CMake-NG](https://github.com/arduino-cmake/Arduino-CMake-NG)和[CMake](http://www.cmake.org/cmake/resources/software.html)，您可以在命令行下使用多个构建系统来构建Arduino固件。CMake可以让您使用自己喜欢的工具生成适合您需求的构建系统。它可以生成任何类型的构建系统，从简单的Makefile到Eclipse，Visual Studio，XCode等的完整项目。

要求: [cmake](https://www.archlinux.org/packages/?name=cmake), [arduino](https://www.archlinux.org/packages/?name=arduino), [avr-gcc](https://www.archlinux.org/packages/?name=avr-gcc), [avr-binutils](https://www.archlinux.org/packages/?name=avr-binutils), [avr-libc](https://www.archlinux.org/packages/?name=avr-libc), [avrdude](https://www.archlinux.org/packages/?name=avrdude).

### Ino

[Ino](https://github.com/amperka/ino)是用于arduino硬件的命令行工具包。 [ino](https://aur.archlinux.org/packages/ino/)在[AUR](/index.php/AUR "AUR")中可用。

### Makefile

**注意:** 更新2015-03-23。由于Arduino≥v1.5中的最新更改，许多旧的Makefile在不进行某些修改的情况下无法正常工作。可以在GitHub上找到一个简单的Arduino 1.5+版本的Makefile [[2]](https://github.com/tomswartz07/arduino-makefile)。

除了使用Arduino IDE，还可以使用其他编辑器和Makefile。设置目录以对Arduino进行编程，然后将Makefile复制到该目录中。 可以从`/usr/share/arduino/hardware/cores/arduino/Makefile`获取Makefile的副本。

您必须在此稍作修改以反映您的设置。Makefile应该很容易说明。这是您可能需要编辑的几行:

```
PORT = usually /dev/ttyUSBx, where x is the usb serial port your arduino is plugged into
TARGET = your sketch's name
ARDUINO = /usr/share/arduino/lib/targets/arduino

```

根据您在例程代码中调用的库函数，您可能需要编译库的某些部分。为此，您需要编辑SRC和CXXSRC以包括所需的库。

现在，您应该可以`make && make upload`编译并上传您的程序到板子了。

### Arduino-mk

[arduino-mk](https://aur.archlinux.org/packages/arduino-mk/)是另一种Makefile方法。它允许用户使用包含Arduino.mk的本地Makefile。参见[project page](https://github.com/sudar/Arduino-Makefile)。

对于Arduino 1.5，请尝试以下本地Makefile（因为Arduino 1.5的库目录结构略有不同）:

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

在某些情况下，您可能需要安装[avr-libc](https://www.archlinux.org/packages/?name=avr-libc)和[avrdude](https://www.archlinux.org/packages/?name=avrdude)。

### Scons

结合使用[scons](http://www.scons.org/)和[arscons](https://github.com/suapapa/arscons)，可以很容易地从命令行编译和上传Arduino项目。 Scons基于python，您将需要python-pyserial才能使用串行接口。安装[python-pyserial](https://www.archlinux.org/packages/?name=python-pyserial)和[scons](https://www.archlinux.org/packages/?name=scons)。

那也将获得您需要的依赖项。您还将需要Arduino本身，因此如上所述安装它。创建项目目录(例如test)，然后在新目录中创建arduino项目文件。使用与目录相同的名称并添加.ino(例如test.ino)。从arscons获取[SConstruct](https://github.com/suapapa/arscons/blob/master/SConstruct)脚本并将其放在目录中。稍微窥视一下，如有必要，对其进行编辑。这是一个python脚本。根据需要编辑项目，然后运行

```
$ scons                # This will build the project
$ scons upload         # This will upload the project to your Arduino

```

### PlatformIO

[PlatformIO](http://docs.platformio.ikravets.com/en/latest/quickstart.html)是一个python工具，用于为多个硬件平台构建和上传示例程序，在编写本文时，它们是基于Arduino/AVR的板卡TI MSP430和TI TM4C12x板。作者计划在不久的将来添加一个库功能，该功能允许直接从GitHub搜索和包含库。

#### 安装

安装[platformio](https://aur.archlinux.org/packages/platformio/) 或 [platformio-git](https://aur.archlinux.org/packages/platformio-git/).

#### 使用

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

当然可以将[Emacs](/index.php/Emacs "Emacs")配置为IDE。

从[AUR](/index.php/AUR "AUR")安装软件包[emacs-arduino-mode-git](https://aur.archlinux.org/packages/emacs-arduino-mode-git/)，以便在emacs中启用`arduino-mode`。

添加到初始化脚本：

 `~/.emacs` 
```
;; arduino-mode
(require 'cl)
(autoload 'arduino-mode "arduino-mode" "Arduino editing mode." t)
(add-to-list 'auto-mode-alist '("\.ino$" . arduino-mode))
```

您可以使用`M-x compile` `make upload`和`Arduino-mk`（见上文）来编译和上传程序。

参见: [[3]](http://www.emacswiki.org/emacs/ArduinoSupport).

## Troubleshooting

### Version 1.6

一些老的第三方工具可能仅适用于Arduino 1.0 ([arduino10](https://aur.archlinux.org/packages/arduino10/))。部分工具可能只会工作在Arduino version 1.6 ([arduino](https://www.archlinux.org/packages/?name=arduino))及更高版本。 如果工具不起作用，请检查版本。请注意，某些较新的开发板不适用于旧的Arduino IDE。

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

### 使用Uno/Mega2560

Arduino Uno和Mega2560具有一个板载USB接口（Atmel 8U2），用来接收串口数据，因此，在USB插入后，可以通过cdc-acm内核模块创建的/dev/ttyACM0来访问它们。

您可以通过将Uno置于环回模式并在115200波特的arduino串行监视器中键入字符来对Uno进行常规功能测试。它应将字符回显给您。要将其置于回送状态，请在数字端短接引脚0->1，并在键入时按住复位按钮或将GND->RESET引脚短路。

### Mega2560无法识别USB端口

安装驱动: [i2c-ch341-dkms](https://aur.archlinux.org/packages/i2c-ch341-dkms/).

### Application not resizing with WM, menus immediately closing

see [Java#Gray window, applications not resizing with WM, menus immediately closing](/index.php/Java#Gray_window,_applications_not_resizing_with_WM,_menus_immediately_closing "Java")

### 上传失败

将处理器设置从`ATmega328P`更改为`ATmega328P (Old Bootloader)` （请参阅Arduino IDE中的“工具”->“处理器”）可能有助于解决上传失败的问题。

## See also

*   [Official website](https://www.arduino.cc/)
*   [https://bbs.archlinux.org/viewtopic.php?pid=295312](https://bbs.archlinux.org/viewtopic.php?pid=295312)
*   [https://bbs.archlinux.org/viewtopic.php?pid=981348](https://bbs.archlinux.org/viewtopic.php?pid=981348)
*   [http://answers.ros.org/question/9097/how-can-i-get-a-unique-device-path-for-my-arduinoftdi-device/](http://answers.ros.org/question/9097/how-can-i-get-a-unique-device-path-for-my-arduinoftdi-device/)
*   [https://www.reddit.com/r/archlinux/comments/8j53dq/how_do_i_install_ch340_chip_drivers_on_arch/](https://www.reddit.com/r/archlinux/comments/8j53dq/how_do_i_install_ch340_chip_drivers_on_arch/)