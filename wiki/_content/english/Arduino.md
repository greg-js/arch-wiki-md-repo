[Arduino](https://www.arduino.cc/) is an open-source electronics prototyping platform based on flexible, easy-to-use hardware and software. It is intended for artists, designers, hobbyists, and anyone interested in creating interactive objects or environments.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 AVR Boards](#AVR_Boards)
    *   [1.2 Pinoccio Scout](#Pinoccio_Scout)
    *   [1.3 Intel Galileo](#Intel_Galileo)
    *   [1.4 On Arm7 devices](#On_Arm7_devices)
    *   [1.5 RedBear Duo](#RedBear_Duo)
*   [2 Configuration](#Configuration)
    *   [2.1 Accessing serial](#Accessing_serial)
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
        *   [5.8.1 Installation](#Installation_2)
        *   [5.8.2 Usage](#Usage)
    *   [5.9 Emacs](#Emacs)
*   [6 Troubleshooting](#Troubleshooting)
    *   [6.1 Version 1.6](#Version_1.6)
    *   [6.2 Consistent naming of Arduino devices](#Consistent_naming_of_Arduino_devices)
    *   [6.3 Error opening serial port](#Error_opening_serial_port)
    *   [6.4 Working with Uno/Mega2560](#Working_with_Uno.2FMega2560)
    *   [6.5 Application not resizing with WM, menus immediately closing](#Application_not_resizing_with_WM.2C_menus_immediately_closing)
*   [7 See also](#See_also)

## Installation

*   Install [arduino](https://www.archlinux.org/packages/?name=arduino) and [arduino-docs](https://www.archlinux.org/packages/?name=arduino-docs) for its offline documentation.
*   Add yourself to the `uucp` and `lock` [groups](/index.php/Groups "Groups") (more information in the [#Accessing serial](#Accessing_serial) section).
*   You may need to [load](/index.php/Kernel_modules "Kernel modules") the `cdc_acm` module.

### AVR Boards

To use AVR boards such as the Arduino Uno you can install [arduino-avr-core](https://www.archlinux.org/packages/?name=arduino-avr-core) optionally to use archlinux upstream avr-gcc instead of the bundled older avr-core. If you still want to use the older arduino-core you need to [install it in the board manager](https://www.arduino.cc/en/Guide/Cores). You can always switch between the different cores in the "Tools>Board" menu.

### Pinoccio Scout

[Pinoccio Scouts](https://pinocc.io/) can also be programmed using the Arduino IDE. Instructions can be found [here](https://pinocc.io/solo). Alternative you can install [arduino-pinoccio](https://aur.archlinux.org/packages/arduino-pinoccio/) from the [AUR](/index.php/AUR "AUR").

### Intel Galileo

To use the Intel Galileo boards with Archlinux install the Arduino IDE and download the Galileo tools package via "Tools->Board->Boards Manager". To fix the installation you can follow [this github post](https://github.com/arduino/Arduino/issues/5523).

### On Arm7 devices

See [here](http://blog.tklee.org/2014/10/arduino-ide-158-on-banana-pi.html) for a work around.

### RedBear Duo

You might need to install [perl-archive-zip](https://www.archlinux.org/packages/?name=perl-archive-zip) or you'll get an error about missing crc32.

## Configuration

### Accessing serial

The arduino board communicates with the computer via a serial connection or a serial over USB connection. So the user needs read/write access to the serial device file. [Udev](/index.php/Udev "Udev") creates files in `/dev/tts/` owned by group `uucp` so adding the user to the `uucp` group gives the required read/write access. If you are planning to use the default Java IDE, add your user to the lock group for `/var/lock/lockdev` access.

```
# gpasswd -a $USER uucp
# gpasswd -a $USER lock

```

**Note:** You will have to logout and login again for this to take effect.

Before uploading to the Arduino, be sure to set the correct serial port, board, and processor from the Tools menu.

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

Using [arduino-cmake](https://github.com/queezythegreat/arduino-cmake) and [CMake](http://www.cmake.org/cmake/resources/software.html) you can build Arduino firmware from the command line using multiple build systems. CMake lets you generate the build system that fits your needs, using the tools you like. It can generate any type of build system, from simple Makefiles, to complete projects for Eclipse, Visual Studio, XCode, etc.

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
ARDUINO_CORE_PATH = /usr/share/arduino/hardware/arduino/avr/cores/arduino
BOARDS_TXT = /usr/share/arduino/hardware/arduino/avr/boards.txt
ARDUINO_VAR_PATH = /usr/share/arduino/hardware/arduino/avr/variants
BOOTLOADER_PARENT = /usr/share/arduino/hardware/arduino/avr/bootloaders

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

### Consistent naming of Arduino devices

If you have more than one arduino you may have noticed that they names /dev/ttyUSB[0-9] are assigned in the order of connection. In the IDE this is not so much of a problem, but when you have programmed your own software to communicate with an arduino project in the background this can be annoying. Use the following udev rules to assign static symlinks to your arduino's:

 `/etc/udev/rules.d/52-arduino.rules` 
```
SUBSYSTEMS=="usb", KERNEL=="ttyUSB[0-9]*", ATTRS{idVendor}=="0403", ATTRS{idProduct}=="6001", SYMLINK+="sensors/ftdi_%s{serial}"

```

Your arduino's will be available under names like "/dev/sensors/ftdi_A700dzaF". If you want you can also assign more meaningfull names to several devices like this:

 `/etc/udev/rules.d/52-arduino.rules` 
```
SUBSYSTEMS=="usb", KERNEL=="ttyUSB[0-9]*", ATTRS{idVendor}=="0403", ATTRS{idProduct}=="6001", ATTRS{serial}=="A700dzaF", SYMLINK+="arduino/nano"

```

which will create a symlink in /dev/arduino/nano to the device with the specified serialnumber. You do need to unplug and replug your arduino for this to take effect or run

```
udevadm trigger

```

Common `idVendor`/`idProduct` pairs can be found in `hardware/arduino/avr/boards.txt` in the distribution package. Note that some of them (notably [FTDI](https://en.wikipedia.org/wiki/FTDI "wikipedia:FTDI") ones) are not unique to the Arduino platform. Using `serial` attribute is a good way to distinguish between various devices.

### Error opening serial port

You may see the serial port initially when the IDE starts, but the TX/RX leds do nothing when uploading. You may have previously changed the baudrate in the serial monitor to something it does not like. Edit ~/.arduino/preferences.txt so that serial.debug_rate is a different speed, like 115200.

### Working with Uno/Mega2560

The Arduino Uno and Mega2560 have an onboard USB interface (an Atmel 8U2) that accepts serial data, so they are accessed through /dev/ttyACM0 created by the cdc-acm kernel module when it is plugged in.

The 8U2 firmware may need an update to ease serial communications. See [[1]](http://www.arduino.cc/cgi-bin/yabb2/YaBB.pl?num=1286350399) for more details and reply #11 for a fix. The original arduino bbs, where you can find an image explaining how to get your Uno into DFU, is now in a read-only state. If you do not have an account to view the image, see [[2]](http://www.scribd.com/doc/45913857/Arduino-UNO).

You can perform a general function test of the Uno by putting it in loopback mode and typing characters into the arduino serial monitor at 115200 baud. It should echo the characters back to you. To put it in loopback, short pins 0 -> 1 on the digital side and either hold the reset button or short the GND -> RESET pins while you type.

### Application not resizing with WM, menus immediately closing

see [Java#Applications not resizing with WM, menus immediately closing](/index.php/Java#Applications_not_resizing_with_WM.2C_menus_immediately_closing "Java")

## See also

*   [https://bbs.archlinux.org/viewtopic.php?pid=295312](https://bbs.archlinux.org/viewtopic.php?pid=295312)
*   [https://bbs.archlinux.org/viewtopic.php?pid=981348](https://bbs.archlinux.org/viewtopic.php?pid=981348)
*   [http://answers.ros.org/question/9097/how-can-i-get-a-unique-device-path-for-my-arduinoftdi-device/](http://answers.ros.org/question/9097/how-can-i-get-a-unique-device-path-for-my-arduinoftdi-device/)