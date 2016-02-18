Arduino is an open-source electronics prototyping platform based on flexible, easy-to-use hardware and software. It is intended for artists, designers, hobbyists, and anyone interested in creating interactive objects or environments. More information is available on the [Arduino HomePage](http://www.arduino.cc/).

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Arduino Due / Yun](#Arduino_Due_.2F_Yun)
    *   [1.2 Pinoccio Scout](#Pinoccio_Scout)
    *   [1.3 Intel Galileo](#Intel_Galileo)
    *   [1.4 On Arm7 devices](#On_Arm7_devices)
*   [2 Configuration](#Configuration)
    *   [2.1 Accessing serial](#Accessing_serial)
*   [3 stty](#stty)
*   [4 Alternatives for IDE](#Alternatives_for_IDE)
    *   [4.1 ArduIDE](#ArduIDE)
    *   [4.2 gnoduino](#gnoduino)
    *   [4.3 Arduino-CMake](#Arduino-CMake)
    *   [4.4 Ino](#Ino)
    *   [4.5 Makefile](#Makefile)
    *   [4.6 Arduino-mk](#Arduino-mk)
    *   [4.7 Scons](#Scons)
    *   [4.8 PlatformIO](#PlatformIO)
        *   [4.8.1 Installation](#Installation_2)
        *   [4.8.2 Usage](#Usage)
    *   [4.9 Emacs](#Emacs)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 Version 1.6](#Version_1.6)
    *   [5.2 Consistent naming of Arduino devices](#Consistent_naming_of_Arduino_devices)
    *   [5.3 Error opening serial port](#Error_opening_serial_port)
    *   [5.4 Permissions to open serial port and create lockfile](#Permissions_to_open_serial_port_and_create_lockfile)
    *   [5.5 Missing twi.o](#Missing_twi.o)
    *   [5.6 Working with Uno/Mega2560](#Working_with_Uno.2FMega2560)
    *   [5.7 error compiling](#error_compiling)
    *   [5.8 avrdude missing libtinfo.so.5](#avrdude_missing_libtinfo.so.5)
    *   [5.9 Application not resizing with WM, menus immediately closing](#Application_not_resizing_with_WM.2C_menus_immediately_closing)
*   [6 See also](#See_also)

## Installation

*   Install [arduino](https://aur.archlinux.org/packages/arduino/) from the [AUR](/index.php/AUR "AUR").
*   Add yourself to the `uucp` and `lock` [groups](/index.php/Groups "Groups"). (More information in the next section: "Accessing serial")
*   You may need to load the cdc_acm module.

```
 # modprobe cdc_acm

```

*   Can be built on a Raspberry Pi by adding 'armv6h' to the arch=('i686' 'x86_64') line like so arch=('i686' 'x86_64' 'armv6h') in the PKGBUILD

### Arduino Due / Yun

The [Arduino Due](http://arduino.cc/en/Main/arduinoBoardDue) and the [Arduino Yun](http://arduino.cc/en/Main/ArduinoBoardYun) need the version 1.5 or newer of the Arduino IDE.

### Pinoccio Scout

[Pinoccio Scouts](https://pinocc.io/) can also be programmed using the Arduino IDE. Instructions can be found [here](https://pinocc.io/solo). Alternative you can install [arduino-pinoccio](https://aur.archlinux.org/packages/arduino-pinoccio/) from the [AUR](/index.php/AUR "AUR").

### Intel Galileo

The version of the Arduino IDE that supports the [Intel Galileo](http://arduino.cc/en/ArduinoCertified/IntelGalileo) board can be downloaded [here](https://communities.intel.com/community/makers/software/drivers).

### On Arm7 devices

See [here](http://blog.tklee.org/2014/10/arduino-ide-158-on-banana-pi.html) for a work around.

## Configuration

### Accessing serial

The arduino board communicates with the computer via a serial connection or a serial over USB connection. So the user needs read/write access to the serial device file. [Udev](/index.php/Udev "Udev") creates files in `/dev/tts/` owned by group `uucp` so adding the user to the `uucp` group gives the required read/write access. If you are planing to use the default Java IDE, add your user to the lock group for `/var/lock/lockdev` access.

```
# gpasswd -a $USER uucp
# gpasswd -a $USER lock

```

**Note:** You will have to logout and login again for this to take effect.

The arduino board appears as `/dev/ttyACMx` so if the above does not work try adding the user to the group `tty`:

```
# gpasswd -a $USER tty

```

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

**Note:** As autoreset on serial connection is activated by default on most boards, you need to disable this feature if you want to communicate directly with your board with the last command instead of a terminal emulator (arduino IDE, screen, picocom...). If you have a Leonardo board, you are not concerned by this, because it does not autoreset. If you have a Uno board, connect a 10 µF capacitor between the RESET and GND pins. If you have another board, connect a 120 ohms resistor between the RESET and 5V pins. See [http://playground.arduino.cc/Main/DisablingAutoResetOnSerialConnection](http://playground.arduino.cc/Main/DisablingAutoResetOnSerialConnection) for more details.

Reading what your Arduino has to tell you

```
$ cat /dev/ttyACM0

```

## Alternatives for IDE

### ArduIDE

ArduIDE is a Qt-based IDE for Arduino. [arduide-git](https://aur.archlinux.org/packages/arduide-git/) is available in the [AUR](/index.php/AUR "AUR").

### gnoduino

[gnoduino](https://aur.archlinux.org/packages/gnoduino/) is an implementation of original Arduino IDE for GNOME available in the [AUR](/index.php/AUR "AUR"). The original Arduino IDE software is written in Java. This is a Python implementation and it is targeted at GNOME but will work on xfce4 and other WM. Its purpose is to be light, while maintaining compatibility with the original Arduino IDE. The source editor is based on gtksourceview.

If you prefer working from terminal, below there are some other options to choose from.

### Arduino-CMake

Using [arduino-cmake](https://github.com/queezythegreat/arduino-cmake) and [CMake](http://www.cmake.org/cmake/resources/software.html) you can build Arduino firmware from the command line using multiple build systems. CMake lets you generate the build system that fits your needs, using the tools you like. It can generate any type of build system, from simple Makefiles, to complete projects for Eclipse, Visual Studio, XCode, etc.

Requirements:

*   [CMake](https://www.archlinux.org/packages/?sort=&q=cmake)
*   [Arduino SDK](https://aur.archlinux.org/packages/arduino/)
*   [avr-gcc](https://www.archlinux.org/packages/?sort=&q=avr-gcc)
*   [avr-binutils](https://www.archlinux.org/packages/?sort=&q=avr-binutils)
*   [avr-libc](https://www.archlinux.org/packages/?sort=&q=avr-libc)
*   [avrdude](https://www.archlinux.org/packages/?sort=&q=avrdude)

### Ino

[Ino](https://github.com/amperka/ino) is a command line toolkit for working with arduino hardware. [ino](https://aur.archlinux.org/packages/ino/) is available in the [AUR](/index.php/AUR "AUR").

Note that `Ino` looks for the file `avrdude.conf` in `/etc/avrdude/avrdude.conf`, while [pacman](/index.php/Pacman "Pacman") appears to place this file (upon installation of [avrdude](https://www.archlinux.org/packages/?name=avrdude)) in `/etc/avrdude.conf`. If `Ino` gives you troubles create the directory `/etc/avrdude` and make the symlink:

```
ln -s /etc/avrdude.conf /etc/avrdude/avrdude.conf

```

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

Its recommended to use a virtual environment because platformio uses python2 because its based on SCons which does not support python3\.

```
$ virtualenv --python=python2 venv
$ source ./venv/bin/activate
$ pip install platformio

```

#### Usage

```
$ platformio install atmelavr
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

As of Oct 5, 2014, most of the 3rd party tools only work for Arduino 1.0 ([arduino10](https://aur.archlinux.org/packages/arduino10/)). Some of the tools may partially work for Arduino version 1.6 ([arduino](https://aur.archlinux.org/packages/arduino/)) and after. Check the version if the tools do not work.

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

### Error opening serial port

You may see the serial port initially when the IDE starts, but the TX/RX leds do nothing when uploading. You may have previously changed the baudrate in the serial monitor to something it does not like. Edit ~/.arduino/preferences.txt so that serial.debug_rate is a different speed, like 115200.

### Permissions to open serial port and create lockfile

Arduino uses java-rxtx to do the serial communications. It expects to create lock files in `/var/lock/lockdev`, so you need to be in the <tt>lock</tt> group. USB serial devices such as /dev/ttyUSB0 or /dev/ttyACM0 will often be assigned to the <tt>uucp</tt> group, so as long as you are adding yourself to groups, you should add that one too.

### Missing twi.o

If the file `/usr/share/arduino/lib/targets/libraries/Wire/utility/twi.o` does not exist arduino may try to create it. Normal users do not have permission to write there so this will fail. Run arduino as root so it can create the file, after the file has been created arduino can be run under a normal user.

### Working with Uno/Mega2560

The Arduino Uno and Mega2560 have an onboard USB interface (an Atmel 8U2) that accepts serial data, so they are accessed through /dev/ttyACM0 created by the cdc-acm kernel module when it is plugged in.

The 8U2 firmware may need an update to ease serial communications. See [[1]](http://www.arduino.cc/cgi-bin/yabb2/YaBB.pl?num=1286350399) for more details and reply #11 for a fix. The original arduino bbs, where you can find an image explaining how to get your Uno into DFU, is now in a read-only state. If you do not have an account to view the image, see [[2]](http://www.scribd.com/doc/45913857/Arduino-UNO).

You can perform a general function test of the Uno by putting it in loopback mode and typing characters into the arduino serial monitor at 115200 baud. It should echo the characters back to you. To put it in loopback, short pins 0 -> 1 on the digital side and either hold the reset button or short the GND -> RESET pins while you type.

### error compiling

if you get following message (in verbose mode)

```
/usr/share/arduino/hardware/tools/avr/bin/../lib/gcc/avr/4.3.2/../../../avr/bin/ld: cannot find -lm

```

see this fix [[3]](https://bbs.archlinux.org/viewtopic.php?pid=1343402#p1343402)

*   install package avr-gcc
*   Replace build-in avr-gcc compiler by same from package installed on previous step:

1.  cd /usr/share/arduino/hardware/tools/avr/bin
2.  mv ./avr-gcc ./avr-gcc-backup
3.  ln -s /usr/bin/avr-gcc ./

To use the avr tools that are system installed, remove the avr directory as per the Arduino Linux install page: "If you want to use your system's compiler, delete the folder `./hardware/tools/avr` in your arduino IDE installation"

An alternate approach to take is to download the corresponding Linux install from Arduino.cc and replace the `/usr/share/arduino/hardware/tools/avr` directory with the avr directory that comes in the stock installation archive.

### avrdude missing libtinfo.so.5

When uploading a sketch to the Arduino, the following message is thrown in the Arduino UI concole:

```
 /usr/share/arduino/hardware/tools/avr/bin/avrdude: error while loading shared libraries: libtinfo.so.5: cannot open shared object file: No such file or directory

```

Solve the dependency problem by creating a symbolic link

```
# ln -s /usr/lib/libncurses.so.5 /usr/lib/libtinfo.so.5

```

For more info: [https://bbs.archlinux.org/viewtopic.php?pid=1108717#p1108717](https://bbs.archlinux.org/viewtopic.php?pid=1108717#p1108717)

### Application not resizing with WM, menus immediately closing

see [Java#Applications not resizing with WM, menus immediately closing](/index.php/Java#Applications_not_resizing_with_WM.2C_menus_immediately_closing "Java")

## See also

*   [https://bbs.archlinux.org/viewtopic.php?pid=295312](https://bbs.archlinux.org/viewtopic.php?pid=295312)
*   [https://bbs.archlinux.org/viewtopic.php?pid=981348](https://bbs.archlinux.org/viewtopic.php?pid=981348)
*   [http://answers.ros.org/question/9097/how-can-i-get-a-unique-device-path-for-my-arduinoftdi-device/](http://answers.ros.org/question/9097/how-can-i-get-a-unique-device-path-for-my-arduinoftdi-device/)