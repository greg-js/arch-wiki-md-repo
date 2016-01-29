# Launchpad MSP430G2

Follow these steps in order to use Energia for the [Launchpad MSP-EXP430G2](http://www.ti.com/tool/MSP-EXP430G2) board.

[Install](/index.php/Install "Install") package [java-rxtx](https://www.archlinux.org/packages/?name=java-rxtx) from the [official repositories](/index.php/Official_repositories "Official repositories").

Create a udev rule:

 `/etc/udev/rules.d/10-launchpad.rules`  `SUBSYSTEM=="usb",ATTR{idVendor}=="0451",ATTR{idProduct}=="f432",GROUP="dialout",MODE="0660"` 

Create `dialout` group:

```
# groupadd dialout

```

Add your user to groups `lock`, `uucp` and `dialout`:

```
# usermod -a -G lock,uucp,dialout $(whoami)

```

Download energia for your architecture (32bit or 64bit) from [www.energia.nu](http://www.energia.nu) and decompress it.

Change directory to the folder `lib`:

```
$ cd ./energia-0101E0012/lib/

```

Create a backup of these files (or delete them):

```
$ mv librxtxSerial.so librxtxSerial.so.bak
$ mv librxtxSerial64.so librxtxSerial64.so.bak
$ mv RXTXcomm.jar RXTXcomm.jar.bak

```

Create links to the Arch Linux version of java-rxtx:

```
$ ln -s /usr/lib/librxtxSerial.so "librxtxSerial.so"
$ ln -s /usr/lib/librxtxSerial.so "librxtxSerial64.so"
$ ln -s /usr/share/java/rxtx/RXTXcomm.jar "RXTXcomm.jar"

```

Reboot (or restart udev, log out and log in).

Plug your launchpad and start energia.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Launchpad_MSP430G2&oldid=412119](https://wiki.archlinux.org/index.php?title=Launchpad_MSP430G2&oldid=412119)"