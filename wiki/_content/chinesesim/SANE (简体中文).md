Sane provides a library and a command-line tool to use scanners under GNU/Linux. [Here](http://www.sane-project.org/sane-supported-devices.html) you can check if sane supports your scanner.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 For HP hardware](#For_HP_hardware)
    *   [2.2 For Brother hardware](#For_Brother_hardware)
    *   [2.3 For Epson hardware](#For_Epson_hardware)
    *   [2.4 For Samsung hardware](#For_Samsung_hardware)
    *   [2.5 For plustek scanners](#For_plustek_scanners)
*   [3 Firmware](#Firmware)
*   [4 Install a frontend](#Install_a_frontend)
*   [5 Network scanning](#Network_scanning)
    *   [5.1 Sharing Your Scanner Over a Network](#Sharing_Your_Scanner_Over_a_Network)
    *   [5.2 Accessing Your Scanner from a Remote Workstation](#Accessing_Your_Scanner_from_a_Remote_Workstation)
*   [6 Troubleshooting](#Troubleshooting)
    *   [6.1 Invalid argument](#Invalid_argument)
        *   [6.1.1 Missing firmware file](#Missing_firmware_file)
        *   [6.1.2 Wrong firmware file permissions](#Wrong_firmware_file_permissions)
        *   [6.1.3 Multiple backends claim scanner](#Multiple_backends_claim_scanner)
    *   [6.2 Slow startup](#Slow_startup)
    *   [6.3 Permission problem](#Permission_problem)
    *   [6.4 Epson Perfection 1270](#Epson_Perfection_1270)

## Installation

[Install](/index.php/Pacman "Pacman") [sane](https://www.archlinux.org/packages/?name=sane) from the [official repositories](/index.php/Official_repositories "Official repositories").

## Configuration

Now you can try to see if sane recognizes your scanner

```
$ scanimage -L

```

If that fails, check that your scanner is plugged into the computer. You also might have to unplug/plug your scanner for `/etc/udev/rules.d/sane.rules` to recognize your scanner.

Now you can see if it actually works

```
$ scanimage --format=tiff > test.tiff

```

### For HP hardware

For HP hardware you may also need to install [hplip](https://www.archlinux.org/packages/?name=hplip) from the [official repositories](/index.php/Official_repositories "Official repositories") and/or [hpoj](https://aur.archlinux.org/packages/hpoj/) from the [AUR](/index.php/Arch_User_Repository "Arch User Repository").

*   Uncomment or add `hpaio` and `hpoj` to a new line in `/etc/sane.d/dll.conf`.
*   Running `hp-setup` as root may help you add your device.
*   `hp-plugin` is the 'HPLIP Plugin Download and Install Utility'.
*   `hp-scan` is the 'HPLIP Scan Utility'.

For Hewlett-Packard OfficeJet, PSC, LaserJet, and PhotoSmart printer multi-function peripherals, run ptal-init setup as root and follow instructions:

```
# ptal-init setup

```

Then start the **ptal-init** daemon.

### For Brother hardware

In order to install a Brother Scanner or Printer/Scanner Combo you need the right driver (which can be found in the AUR). There are only four drivers to choose from (brscan1-4). In order to find the right one you should search for your model at the [brother linux scanner page](http://welcome.solutions.brother.com/bsc/public_s/id/linux/en/download_scn.html).

After you installed the driver you need to run

```
# /usr/local/Brother/sane/setupSaneScan1 -i

```

so the drivers/scanner are recognized by sane.

For network scanners, Brother provides a configuration tool:

```
$ brsaneconfig2 -a name=<ScannerName> model=<ScannerModel> ip=<ScannerIP>

```

Example:

```
$ brsaneconfig2 -a name=SCANNER_DCP770CW model=DCP-770CW ip=192.168.0.110

```

### For Epson hardware

For Wi-Fi and/or network scanners, you can use "Image Scan! for Linux".

Install [iscan](https://www.archlinux.org/packages/?name=iscan) and [iscan-plugin-network](https://aur.archlinux.org/packages/iscan-plugin-network/) from the [AUR](/index.php/AUR "AUR"), then update `/etc/sane.d/epkowa.conf` and add the line:

```
net {IP_OF_SCANNER}

```

### For Samsung hardware

For some Samsung MFP printers you may need to edit /etc/sane.d/xerox_mfp.conf.

example entry:

```
#Samsung SCX-3200
usb 0x04e8 0x3441

```

Change the printer model as needed. You can get the ipVendor and idProduct code with lsusb. See [this thread](https://bbs.archlinux.org/viewtopic.php?id=123934).

### For plustek scanners

Some plustek scanners (noticeably Canoscan ones), require a lock directory. Make sure that /var/lock/sane directory exists, that its permissions are 660, and that it is owned by <user>:scanner. If the directory permissions are wrong, only root will be able to use the scanner. Seems (at least on x86-64) that some programs using libusb (noticeably xsane and kooka) need scanner group rw permissions also for accessing /proc/bus/usb to work for a normal user.

## Firmware

**Note:** This section is only needed if you need to upload firmware to your scanner.

Firmwares usually have the **`.bin`** extension.

Firstly you need to put the firmware someplace safe, it is recommended to put it in a subdirectory of `/usr/share/sane`.

Then you need to tell sane where the firmware is:

*   Find the name of the backend for your scanner from the [sane supported devices list](http://www.sane-project.org/sane-supported-devices.html).
*   Open the file `/etc/sane.d/<backend-name>.conf`.
*   Make sure the firmware entry is uncommented and let the file-path point to where you put the firmware file for your scanner. Be sure that members of the group `scanner` can access the `/etc/sane.d/<backend-name>.conf` file.

If the backend of your scanner is not part of the sane package (such as hpaio.conf which is part of hplip), you need to uncomment the relevant entry in /etc/sane.d/dll.d/hplip.

## Install a frontend

XSane provides a GTK-based frontend to Sane. It is available in the `extra` repository.

```
# pacman -S xsane

```

**Note:** Scanning directly to pdf using Xsane in 16bit color depth mode is known to produces [corrupted files](https://bugs.launchpad.net/ubuntu/+source/xsane/+bug/539162). 8bit mode should work.

Other frontends exist, to find them you can:

*   use `pacman -Ss` to search for keywords such as "sane" or "scanner"
*   see the [list of frontends](http://www.sane-project.org/sane-frontends.html) on the sane-project website

## Network scanning

### Sharing Your Scanner Over a Network

You can share your scanner with other hosts on your network who use sane, xsane or xsane-enabled Gimp. To set up the server, first indicate which hosts on your network are allowed access.

Change the `/etc/sane.d/saned.conf` file to your liking, for example:

```
# required
localhost
# allow local subnet
192.168.0.0/24

```

Ensure xinetd is installed:

```
# pacman -S xinetd

```

Next, make sure the a file called `/etc/xinetd.d/sane` exists and disabled is set to no:

```
service sane-port
{
   port        = 6566
   socket_type = stream
   wait        = no
   user        = root
   group       = scanner
   server      = /usr/sbin/saned
   disable     = no
}

```

Add the following line to `/etc/services`:

```
sane-port 6566/tcp

```

Start the **xinetd** [daemon](/index.php/Daemons "Daemons").

Your scanner can now be used by other workstations, across your local area network.

### Accessing Your Scanner from a Remote Workstation

You can access your network-enabled scanner from a remote Arch Linux workstation.

To set up your workstation, begin by installing xsane:

```
# pacman -S xsane

```

Next, specify the server's host name or IP address in the `/etc/sane.d/net.conf` file:

```
# static IP address
192.168.0.1
# or host name
stratus

```

Now test your workstation's connection, from a non-root login prompt:

```
$ xsane

```

or

```
$ scanimage -L

```

After a short while, xsane should find your remote scanner and present you with the usual windows, ready for network scanning delight!

For HP All in one network printer/scanner/fax you need to configure it via:

```
$ hp-setup <printer ip>

```

## Troubleshooting

### Invalid argument

If you get an "Invalid argument" error with xsane or another sane front-end, this could be caused by one of the following reasons:

#### Missing firmware file

No firmware file was provided for the used scanner (see above for details).

#### Wrong firmware file permissions

The permissions for the used firmware file are wrong. Correct them using

```
# chown root:scanner /usr/share/sane/SCANNER_MODEL/FIRMWARE_FILE
# chmod ug+r /usr/share/sane/SCANNER_MODEL/FIRMWARE_FILE

```

#### Multiple backends claim scanner

It may happen, that multiple backends support (or pretend to support) your scanner, and sane chooses one that does not do after all (the scanner will not be displayed by scanimage -L then). This has happend with older Epson scanners and the `epson2` resp. `epson` backends. In this case, the solution is to comment out the unwanted backend in `/etc/sane.d/dll.conf`. In the Epson case, that would be to change

```
 epson2
 #epson

```

to

```
 #epson2
 epson

```

### Slow startup

If you encounter slow startup issue (e.g. xsane or scanimage -L take a lot to find scanner) it may be that more than one driver supporting it is available.

Have a look at /etc/sane.d/dll.conf and try commenting out one (e.g. you may have epson, epson2 and epkowa enabled at the same time, try leaving only epson or epkowa uncommented)

### Permission problem

You can try to change permissions of usb device but this is not recommended, a better solution is to fix the Udev rules so that your scanner is recognized.

Example:

First, as root, check connected usb devices with `lsusb`:

```
#Bus 006 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub
#Bus 005 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub
#Bus 004 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub
#Bus 003 Device 003: ID 04d9:1603 Holtek Semiconductor, Inc. 
#Bus 003 Device 002: ID 04fc:0538 Sunplus Technology Co., Ltd 
#Bus 003 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub
#Bus 002 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub
#Bus 001 Device 006: ID 03f0:2504 Hewlett-Packard 
#Bus 001 Device 002: ID 046d:0802 Logitech, Inc. Webcam C200
#Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub

```

In our example we see scanner - '**Bus 001 Device 006: ID 03f0:2504 Hewlett-Packard'**

Now edit `/lib/udev/rules.d/53-sane.rules` and look for the first part of the ID number found previously and check if there is a line that also reports the second part of the number (model numer), in this example 2504\. If not found change or copy a line and enter the idVendor and idProduct of your scanner, in this example it would be:

```
# Hewlett-Packard ScanJet 4100C
ATTRS{idVendor}=="03f0", ATTRS{idProduct}=="2504", MODE="0664", GROUP="scanner",
  ENV{libsane_matched}="yes"

```

Save the file, plug out and back in your scanner and the file permissions should be now correct.

Another tip, is that you can add your device (scanner) in backend file:

Add '**usb 0x03f0 0x2504'** to `/etc/sane.d/hp4200.conf` so it looks like this:

```
#
# Configuration file for the hp4200 backend
#
#
# HP4200
#usb 0x03f0 0x0105
usb 0x03f0 0x2504

```

### Epson Perfection 1270

For Epson Perfection 1270, you also need a firmware named esfw3e.bin. It can be obtained by installing the Windows driver.

Modify configuration file of snapscan backend:

```
vi /etc/sane.d/snapscan.conf 

```

Change the firmware path line with yours. :

```
   # Change to the fully qualified filename of your firmware file, if
   # firmware upload is needed by the scanner
   firmware /mnt/mydata/Backups/firmware/esfw3e.bin

```

And add the following line in the end or anywhere you like

```
  # Epson Perfection 1270
  usb 0x04b8 0x0120

```

You can get such code information (_usb 0x04b8 0x0120_) by "sane-find-scanner" command.

Also add such information lines in your libsane.usermap file to setup your privilage, like:

```
vi /etc/hotplug/usb/libsane.usermap

 #Epson Perfection 1270
 libusbscanner 0x0003 0x04b8 0x0120 0x0000 0x0000 0x00 0x00 0x00 0x00 0x00 0x00 0x00000000

```

Replug scanner, you have a working Epson Perfection 1270 now.

NOTE: I can scan image if I define the X and Y value, but without that error meassage occors like: "scanimage: sane_start: Error during device I/O", if anyone know why, please complete the section. ".