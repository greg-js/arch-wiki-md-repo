This article contains scanner or manufacturer-specific instructions for [SANE](/index.php/SANE "SANE").

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Agfa](#Agfa)
    *   [1.1 Snapscan e40](#Snapscan_e40)
*   [2 BenQ/Acer](#BenQ/Acer)
*   [3 Brother](#Brother)
    *   [3.1 Network Scanning](#Network_Scanning)
    *   [3.2 Invalid argument](#Invalid_argument)
    *   [3.3 Scan-key-tool](#Scan-key-tool)
    *   [3.4 xsane crashes](#xsane_crashes)
*   [4 Canon](#Canon)
    *   [4.1 Scanning over the network with Canon Pixma all-in-one printer/scanners](#Scanning_over_the_network_with_Canon_Pixma_all-in-one_printer/scanners)
    *   [4.2 CanoScan LiDE 200 and black stripe in the middle of the scanned image](#CanoScan_LiDE_200_and_black_stripe_in_the_middle_of_the_scanned_image)
*   [5 Epson](#Epson)
    *   [5.1 Driver-Backends](#Driver-Backends)
        *   [5.1.1 Image Scan! for Linux](#Image_Scan!_for_Linux)
        *   [5.1.2 Image Scan v3](#Image_Scan_v3)
    *   [5.2 Epson DS-6500](#Epson_DS-6500)
    *   [5.3 Epson Perfection V550 Photo](#Epson_Perfection_V550_Photo)
    *   [5.4 Epson Perfection 1270](#Epson_Perfection_1270)
    *   [5.5 Epson Perfection 1670/2480/2580/3490/3590](#Epson_Perfection_1670/2480/2580/3490/3590)
*   [6 Fujitsu](#Fujitsu)
    *   [6.1 ScanSnap S300/S300M](#ScanSnap_S300/S300M)
*   [7 HP](#HP)
    *   [7.1 Alternative way to scan with network HP scanner](#Alternative_way_to_scan_with_network_HP_scanner)
*   [8 Lexmark](#Lexmark)
    *   [8.1 Warning](#Warning)
    *   [8.2 Process](#Process)
        *   [8.2.1 Option 1 : using DPKG](#Option_1_:_using_DPKG)
        *   [8.2.2 Option 2 : manual installation](#Option_2_:_manual_installation)
    *   [8.3 Supported devices](#Supported_devices)
    *   [8.4 To do](#To_do)
*   [9 Medion](#Medion)
*   [10 Mustek](#Mustek)
    *   [10.1 BearPaw 2400CU](#BearPaw_2400CU)
*   [11 Samsung](#Samsung)

## Agfa

### Snapscan e40

Firmware `Snape40.bin` from [here](https://sites.google.com/site/rameyarnaud/media/books/agfa-scanners-with-linux) is required.

If USB autosuspend is enabled, the printer may need to be turned off and on again before each scan. USB autosuspend can be disabled using [powertop](/index.php/Powertop "Powertop").

## BenQ/Acer

If you own an USB scanner from Acer (now BenQ), you need to download a suitable firmware binary and configure `/etc/sane.d/snapscan.conf`.

*   Find out which model you own and take note of the USB ID:

 `$ lsusb`  `Bus 002 Device 010: ID 04a5:20b0 Acer Peripherals Inc. (now BenQ Corp.) S2W 3300U/4300U` 

*   Go to [snapscan](http://snapscan.sourceforge.net/) main page and see whether your scanner is supported and which firmware you need (e.g, `u176v046.bin`).
*   Search the firmware image on the Internet and download it to `/usr/share/sane/snapscan/`.
*   Edit the head of `/etc/sane.d/snapscan.conf` and configure the following two lines:

```
firmware /usr/share/sane/snapscan/u176v046.bin
/dev/usb/scanner0 bus=usb

```

## Brother

In order to install a Brother scanner or printer/scanner combo you need the right driver. To find the right one, search for your model at the [Brother Linux scanner page](http://support.brother.com/g/s/id/linux/en/download_scn.html). That list is not exhaustive. You can also search the web. Or see the information below for more scanners. Or extract each of the [AUR](/index.php/AUR "AUR") packages below. Each package seems to contain an exhaustive list of the models it is suitable to.

Then, install the appropriate package:

*   [brscan2](https://aur.archlinux.org/packages/brscan2/)
*   [brscan3](https://aur.archlinux.org/packages/brscan3/)
*   [brscan4](https://aur.archlinux.org/packages/brscan4/) (MFC-J5620DW)
*   [brscan5](https://aur.archlinux.org/packages/brscan5/)
*   [libsane-dsseries](https://aur.archlinux.org/packages/libsane-dsseries/)

Now, the scanner should be recognized by SANE.

For network scanners, Brother provides a different configuration tool for each brscan version (eg. brsaneconfig2 for brscan2 compatible devices):

```
# brsaneconfig2 -a name=<ScannerName> model=<ScannerModel> ip=<ScannerIP>

```

Example:

```
# brsaneconfig2 -a name=SCANNER_DCP770CW model=DCP-770CW ip=192.168.0.110

```

### Network Scanning

In case of network scanning, e.g. by WiFi, Sane may still be unable to find the scanner. If so, you need to specify the IP address of the scanner in the `/etc/sane.d/net.conf` file.

Now use `scanimage --list-devices` to check whether sane is able to find your scanner. If not, further check that Sane expects this device through the network (see [[1]](http://neithere.net/2013/02/18/archlinux_brother_7860.html)). Check that `/etc/sane.d/dll.conf` contains `brother*X*`, where the `*X*` stands for the brscan version from above. If nothing was found, add `brother*X*` to the end of the file.

### Invalid argument

If all the necessary packages are installed but you still get the "invalid argument" error this could mean that the configuration file has been corrupted. Run the following command (in case of brscan4):

```
 # brsaneconfig4 -d 

```

The output should narrow down the problem. Most likely the connection isn't setup correctly. In case of a network scanner check if the IP address is right by opening the `/etc/opt/brother/scanner/brscan4//brsanenetdevice4.cfg` with an editor. In case of a USB connection check if the path to the scanner in the configuration file is setup correctly. For that compare the values of the `lsusb` command with your configuration file and change them if necessary. You might also try to follow the `brother*X*` suggestion from [Network Scanning above](/index.php/SANE/Scanner-specific_problems#Network_Scanning "SANE/Scanner-specific problems") even for non networked scanners.

### Scan-key-tool

Brother has released a tool to enable scanning to be triggered by user interaction with the scanner itself (e.g. by selecting one of "Scan to email", "Scan to image", etc. on the scanner keypad) rather than by an attached computer. This can be set up by installing the [brscan-skey](https://aur.archlinux.org/packages/brscan-skey/) package and starting `brscan-skey.service` [using systemd](/index.php/Systemd#Using_units "Systemd"). Note that by default this service runs as the **brscan-skey** user which is created by the package, whose home directory is located at `/srv/brscan-skey`.

Brother supplies some default scripts that are executed when a scan type is selected on the keypad. These may require the installation of some optional dependencies of the [brscan-skey](https://aur.archlinux.org/packages/brscan-skey/) package. For all options apart from "Scan to email" the resulting output can be found inside `$HOME/brscan`, with `$HOME` the home directory of the user running this tool (so `/srv/brscan-skey` if started via systemd as a systemwide process).

It is possible to change what action takes place when a given type of scan is selected on the keypad. This is done by editing `/opt/brother/scanner/brscan-skey/brscan-skey-0.2.4-0.cfg`. For each variable `SCAN_COMMAND` in `IMAGE`, `OCR`, `EMAIL`, `FILE`, the command

```
 $ $SCAN_COMMAND $SCANNER_DEVICE $SCANNER_FRIENDLY_NAME

```

is executed when the corresponding scan type is selected. Note that `$SCAN_COMMAND` is not quoted so may specify more than one positional parameter in the final command that is executed. `$SCANNER_DEVICE` refers to the name of the device that should be specified to a sane frontend (e.g. via the `--device-name` flag when using `scanimage`), for example `brother3:bus4;dev2`. `$SCANNER_FRIENDLY_NAME` is the human-readable name of the scanner.

### xsane crashes

If xsane crashes with message "`=bugchk_free(ptr==(nil))@brother_modelinf.c(482)`", then you need to create the link `/usr/local/Brother -> /usr/share/brother`.

## Canon

### Scanning over the network with Canon Pixma all-in-one printer/scanners

Find out your printer/scanner's IP address, and add it on a new line to `/etc/sane.d/pixma.conf` in the format `bjnp://10.0.0.20`.

**Tip:** Instead of a IP address you can use the [mDNS](/index.php/MDNS "MDNS") `.local` address, e.g. `bjnp://*MyPixmaPrinter*.local`.

Sane should now find your device. For more details refer to [sane-pixma(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/sane-pixma.5).

Alternative: for some Canon Pixma all-in-one printer/scanners, which are not detected over network, can be used [scangearmp2](https://aur.archlinux.org/packages/scangearmp2/) package from AUR.

### CanoScan LiDE 200 and black stripe in the middle of the scanned image

Bug affects [sane](https://www.archlinux.org/packages/?name=sane) 1.0.26, 1.0.27 and related to the GENESYS backend [1](https://bbs.archlinux.org/viewtopic.php?id=233725), [2](https://bugs.launchpad.net/prj20071101/+bug/1731459). Install [sane-git](https://aur.archlinux.org/packages/sane-git/) and run `scanimage --clear-calibration`. On next scan image will be clear.

## Epson

### Driver-Backends

For Epson scanners, you can choose between two different backends: "**Image Scan! for Linux**" ([iscan](https://www.archlinux.org/packages/?name=iscan)/epkowa) or "**Image Scan v3**" ([imagescan](https://www.archlinux.org/packages/?name=imagescan)/utsushi). You can check [here](http://www.sane-project.org/lists/sane-backends-external.html#S-EPKOWA) for all supported **iscan/epkowa** devices and [here](http://www.sane-project.org/lists/sane-backends-external.html#S-UTSUSHI) for all **imagescan/utsushi** devices.

#### Image Scan! for Linux

*   Install the [iscan](https://www.archlinux.org/packages/?name=iscan) package
*   Install the appropriate iscan-plugin package for your scanner (for example, [iscan-plugin-gt-x820](https://aur.archlinux.org/packages/iscan-plugin-gt-x820/) for the Epson Perfection Photo V600)
*   Reboot, so that udev will recognize the device as a scanner and apply appropriate permissions

For network (including Wi-Fi) scanners, install [iscan](https://www.archlinux.org/packages/?name=iscan) and [iscan-plugin-network](https://aur.archlinux.org/packages/iscan-plugin-network/), then edit `/etc/sane.d/epkowa.conf` and add the line:

```
net {IP_OF_SCANNER}

```

Upstream version of [iscan](https://www.archlinux.org/packages/?name=iscan) does not support 16bpc color depth scanning. Choosing any bit depth other than 8 makes iscan stop without warning, leaving the scanner stuck until restarted. To enable 16bpc scanning, iscan requires to be patched. Use [ABS](/index.php/ABS "ABS") and apply patch found in [this forum thread](https://bbs.archlinux.org/viewtopic.php?pid=1841337#p1841337) to enable 16bpc depth mode.

#### Image Scan v3

If you have to use Image Scan v3-backend you can install [imagescan](https://www.archlinux.org/packages/?name=imagescan). It should detect supported USB scanners automatically by default. If you want to make use of a network scanner you also have to install [imagescan-plugin-networkscan](https://aur.archlinux.org/packages/imagescan-plugin-networkscan/). Then edit `/etc/utsushi/utsushi.conf` and enter the ip address of your scanner to it.

```
[devices]
myscanner.udi    = esci:networkscan://<ip-address-here>:1865
myscanner.vendor = Epson
myscanner.model  = Model-name

```

When you then start Image Scan v3 by typing in the command

```
$ utsushi

```

the name of the scanner should be visible in the top left corner. If a connection problem happened, an error dialog will be shown.

### Epson DS-6500

Usually this device works with the epsonds-backend. However, there may be an error "Error during device I / O" when scanning multiple pages. If this error occurs, the Image Scan v3 backend can be used and [imagescan](https://www.archlinux.org/packages/?name=imagescan) needs to be installed. If you want to use the network module, the scanner can be configured in the `/etc/utsushi/utsushi.conf` after installing [imagescan-plugin-networkscan](https://aur.archlinux.org/packages/imagescan-plugin-networkscan/) as described above.

### Epson Perfection V550 Photo

Install [iscan-plugin-perfection-v550](https://aur.archlinux.org/packages/iscan-plugin-perfection-v550/)

### Epson Perfection 1270

For Epson Perfection 1270, you also need a firmware named `esfw3e.bin`. It can be obtained by installing the Windows driver.

Modify the configuration file of the snapscan backend, `/etc/sane.d/snapscan.conf`. Change the firmware path line with yours:

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

You can get such code information (`usb 0x04b8 0x0120`) by *sane-find-scanner* command.

Also add such information lines to `/etc/hotplug/usb/libsane.usermap` to setup your privilege, like:

```
# Epson Perfection 1270
libusbscanner 0x0003 0x04b8 0x0120 0x0000 0x0000 0x00 0x00 0x00 0x00 0x00 0x00 0x00000000

```

Replug scanner, you have a working Epson Perfection 1270 now.

**Note:** I can scan image if I define the X and Y value, but without that error message occurs like: `scanimage: sane_start: Error during device I/O`, if anyone knows any other reasons, please add them to this section.

*   To prevent `scanimage: sane_start: Error during device I/O` and hangup of the scanner itself, when trying to scan with ADF (automatic document feed) enabled, I had to remove or comment out all Backends from `/etc/sane.d/dll.conf` and instead just add this to the file: `snapscan` 

If you still get the `Error during device I/O` messages check that the transportation lock of the scanner (on the bottom of the scanner) is open.

### Epson Perfection 1670/2480/2580/3490/3590

**Note:** Installation instructions were only tested for Epson Perfection 3590 but should be similar to the other models. Check the instructions above and the links below and edit this wiki page if you can verify that your scanner works.

Make sure to download the correct firmware for your Epson model. You can get an overview of some models and their drivers [here](https://wiki.ubuntuusers.de/Scanner/Epson%20Perfection/#Unterstuetze-Geraete) and [here](http://snapscan.sourceforge.net/). The download links of the firmware are broken, but you can use [this link](https://wiki.ubuntuusers.de/Scanner/Epson_Perfection/Esfw52.bin/) as alternative instead. Make sure to change the firmware filename of the link suiting your model. If you want to download and extract the firmware sources from the official epson sites yourself you can use [this guide](https://forum.ubuntuusers.de/topic/epson-perfection-3490-photo-on-ubuntu-9-04-64/).

As an alternative you can also install the AUR package [sane-epson-perfection-firmware](https://aur.archlinux.org/packages/sane-epson-perfection-firmware/) which will download the firmware from the official sources, extract the binary and install those to `/usr/share/sane/snapscan/`.

Modify the configuration file of the snapscan backend, `/etc/sane.d/snapscan.conf`. Change the firmware path line with yours:

```
# Change to the fully qualified filename of your firmware file, if
# firmware upload is needed by the scanner
firmware /usr/share/sane/snapscan/esfw52.bin

```

Other modifications were not needed for the Epson Perfection 3590 and might not be for other models as well. If you still have problems it can also help if you [completely remove](/index.php/SANE#Multiple_backends_claim_scanner "SANE") the [iscan](https://www.archlinux.org/packages/?name=iscan) package.

## Fujitsu

### ScanSnap S300/S300M

For the operation of the ScanSnap scanners S300 and S300M a firmware file `/usr/share/sane/epjitsu/300M_0C00.nal` is required, which can be downloaded [here](http://sange.fi/~atehwa/cgi-bin/piki.cgi/fujitsu%20scansnap%20s300%20firmware) or extracted from the Windows driver. The `300M_0C00.nal` and `300_0C00.nal` files are interchangeable; the S300 device can use the `300M_0C00.nal` file and the S300M device can use the `300_0C00.nal` file. The file can be renamed to fit the entry in `/etc/sane.d/epjitsu.conf`, or that entry can be edited to match the file name.

## HP

If your HP device [is supported by hplip](http://hplipopensource.com/hplip-web/supported_devices/index.html), [install](/index.php/Install "Install") the [hplip](https://www.archlinux.org/packages/?name=hplip) package.

The latter comes with 3 tools:

*   *hp-setup* to add and setup the device
*   *hp-plugin* is the 'HPLIP Plugin Download and Install Utility' (plugin also available from [hplip-plugin](https://aur.archlinux.org/packages/hplip-plugin/)).
*   *hp-scan* is the 'HPLIP Scan Utility'. If you need that tool, you will need to install [python-pillow](https://www.archlinux.org/packages/?name=python-pillow).

*hp-setup* requires Python Qt5 when run using the GUI (which is the default). As an alternative, you can run the CLI interface of hp-setup using `-i` as argument.

If the device is connected by USB, run *hp-setup* as root and follow the on screen instructions.

If your device is connected on the network, use `hp-setup *printer_ip*` instead.

### Alternative way to scan with network HP scanner

*   Find out IP address of your network HP scanner, for example *192.168.1.8*
*   Make device URI using hp-makeuri utility:

 `$ hp-makeuri 192.168.1.8`  `hpaio:/net/DeskJet_3630_series?ip=192.168.1.8` 

*   This URI could be given to xsane or scanimage tools, for example:

```
$ xsane "hpaio:/net/DeskJet_3630_series?ip=192.168.1.8"
$ scanimage --device "hpaio:/net/DeskJet_3630_series?ip=10.12.129.6" --format=png --resolution 300 >scan01.png

```

## Lexmark

For Lexmark devices printing issues, please read [CUPS/Printer-specific_problems#Lexmark](/index.php/CUPS/Printer-specific_problems#Lexmark "CUPS/Printer-specific problems").

Most Lexmark scanners are still (2019) not supported by SANE, and thus cannot be detected either by `sane-find-scanner` or by `scanimage -L`. Lexmark provides a non-free driver for GNU/Linux, which is supposed to support *all* its scanners. Nevertheless, the driver is only distributed for Debian, OpenSUSE, Fedora and RedHat, but not for Arch. Here is a way to install it.

### Warning

Before following these steps, note that :

*   This driver is non-free (copyrighted by Lexmark)
*   This hasn’t been widely tested yet (but the driver is supposed to work for all Lexmark scanners)
*   The tree does not respect Arch standards — namely, all will be installed in `/usr/local`; you’ll get a `/usr/lexmark/` symbolic link; and get symbolic links to the files installed in `/usr/local/lexmark`.
*   This process might generate conflicts if you’ve already installed some Lexmark drivers.

### Process

1.  Ensure [Java](/index.php/Java "Java") is installed.
2.  Download the [`.deb` file](https://downloads.lexmark.com/downloads/drivers/lexmark_network-scan-linux-glibc2_04082019_x86_64.deb) containing the driver and save it (eg at `~/lexmark.deb`).

#### Option 1 : using DPKG

[dpkg](https://aur.archlinux.org/packages/dpkg/) is the standard package-manager for [Debian](/index.php/Debian "Debian")-based distributions. **It should not be used to replace `[pacman](/index.php/Pacman "Pacman")`** unless you precisely know what you’re doing. Simply run as root

```
# dpkg -i lexmark.deb

```

Your scanner should be detected after reboot.

#### Option 2 : manual installation

Alternatively, if you dont want to install dpkg or wish to control exactly what is done during install, you can follow these instructions (assuming you’re working in `~`). Please note that `md5` sums will not be checked, which could cause security issues.

1.  Extract the `~/lexmark.deb` archive, running `ar x lexmark.deb`. File `debian-binary` can be dropped.
2.  Extract both `~/control.tar.gz` and `~/data.tar.gz` archives.
3.  `data.tar.gz` gives a `~/usr/` directory. As root, move `~/usr/local/lexmark` to `/usr/local/lexmark`.
4.  As root, run `~/control/postinst` to perform install. This script will automatically set all files owners an `chmod`, then set some fonts, drivers and docs tricks. It will also eventually run `/usr/local/lexmark/network-scan.link`, creating several symbolic links in your Arch architecture.
5.  Your scanner should be detected after reboot.

### Supported devices

This process has been successfully tested for the following devices:

*   Lexmark MB2236 (USB only; network untested).

It does not work fot the following:

*   …

### To do

In order to improve Lexmark scanners support, you can:

*   Check whether this process works for your computer and device
*   Help defining the list of dependencies required for this process
*   Create an AUR package with this driver which installation would not mess architecture up. Namely, such a package should not need to create a `/usr/lexmark` symlink, and should be containerized (eg in `/opt/lexmark`).

## Medion

If you own the USB scanner MD 9705 from Medion, you need to download a suitable firmware binary. This firmware file is in the device driver for Windows.

Find out which model you own and take note of the USB ID:

 `$ lsusb` 
```
Bus 006 Device 007: ID 05d8:4003 Ultima Electronics Corp. Artec E+ 48U

```

Download the windows driver from [http://download.medion.com/downloads/treiber/scamd9705w9xxp.exe](http://download.medion.com/downloads/treiber/scamd9705w9xxp.exe)

Then enter the following commands to extract the firmware file, and copy it to the location SANE expects it:

```
$ unzip scamd9705w9xxp.exe Win2000/Artec48.usb
# cp Win2000/Artec48.usb /usr/share/sane/artec_eplus48u/Artec48.usb

```

## Mustek

### BearPaw 2400CU

Works with sane-gt68xx ([sane-gt68xx-firmware](https://www.archlinux.org/packages/?name=sane-gt68xx-firmware))

## Samsung

For some Samsung MFP printers you may need to edit `/etc/sane.d/xerox_mfp.conf`.

example entry:

```
#Samsung SCX-3200
usb 0x04e8 0x3441

```

Change the printer model as needed. You can get the idVendor and idProduct code with `lsusb`. See [this thread](https://bbs.archlinux.org/viewtopic.php?id=123934).

To access the scanner over the network rather than the usb interface, add a line to `/etc/sane.d/xerox_mfp.conf` such as

```
#Samsung scx4500w wireless ip network address
tcp xx.xx.xx.xx

```

where xx.xx.xx.xx is the static ip address of the printer.