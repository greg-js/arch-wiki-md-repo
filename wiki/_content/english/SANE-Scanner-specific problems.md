This article contains scanner or manufacturer-specific instructions for [SANE](/index.php/SANE "SANE").

## Contents

*   [1 Agfa](#Agfa)
    *   [1.1 Snapscan e40](#Snapscan_e40)
*   [2 BenQ/Acer](#BenQ.2FAcer)
*   [3 Brother](#Brother)
    *   [3.1 Network Scanning](#Network_Scanning)
    *   [3.2 Invalid argument](#Invalid_argument)
    *   [3.3 Scan-key-tool](#Scan-key-tool)
    *   [3.4 xsane crashes](#xsane_crashes)
*   [4 Canon](#Canon)
    *   [4.1 Scanning over the network with Canon Pixma all-in-one printer/scanners](#Scanning_over_the_network_with_Canon_Pixma_all-in-one_printer.2Fscanners)
*   [5 Epson](#Epson)
    *   [5.1 Image Scan v3](#Image_Scan_v3)
    *   [5.2 Epson Perfection V550 Photo](#Epson_Perfection_V550_Photo)
    *   [5.3 Epson Perfection 1270](#Epson_Perfection_1270)
    *   [5.4 Epson Perfection 1670/2480/2580/3490/3590](#Epson_Perfection_1670.2F2480.2F2580.2F3490.2F3590)
*   [6 Fujitsu](#Fujitsu)
    *   [6.1 S300M](#S300M)
*   [7 HP](#HP)
    *   [7.1 Alternative way to scan with network HP scanner](#Alternative_way_to_scan_with_network_HP_scanner)
*   [8 Medion](#Medion)
*   [9 Mustek](#Mustek)
    *   [9.1 BearPaw 2400CU](#BearPaw_2400CU)
*   [10 Samsung](#Samsung)

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

In order to install a Brother scanner or printer/scanner combo you need the right driver. To find the right one, search for your model at the [Brother Linux scanner page](http://support.brother.com/g/s/id/linux/en/download_scn.html), or see the information below for scanners that aren't listed on that page.

Then, install the appropriate package:

*   [brscan2](https://aur.archlinux.org/packages/brscan2/)
*   [brscan3](https://aur.archlinux.org/packages/brscan3/)
*   [brscan4](https://aur.archlinux.org/packages/brscan4/) (MFC-J5620DW)
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

The output should narrow down the problem. Most likely the connection isn't setup correctly. In case of a network scanner check if the IP address is right by opening the `/etc/opt/brother/scanner/brscan4//brsanenetdevice4.cfg` with an editor. In case of a USB connection check if the path to the scanner in the configuration file is setup correctly. For that compare the values of the `lsusb` command with your configuration file and change them if necessary.

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

## Epson

With Epson scanners, you can use "Image Scan! for Linux".

*   Install the [iscan](https://www.archlinux.org/packages/?name=iscan) package
*   Install the appropriate iscan-plugin package for your scanner (for example, [iscan-plugin-gt-x820](https://aur.archlinux.org/packages/iscan-plugin-gt-x820/) for the Epson Perfection Photo V600)
*   Reboot, so that udev will recognize the device as a scanner and apply appropriate permissions

For network (including Wi-Fi) scanners, install [iscan](https://www.archlinux.org/packages/?name=iscan) and [iscan-plugin-network](https://aur.archlinux.org/packages/iscan-plugin-network/), then edit `/etc/sane.d/epkowa.conf` and add the line:

```
net {IP_OF_SCANNER}

```

### Image Scan v3

Some models require "Image Scan 3", which is different from "Image Scan! for Linux" and is not available in the official repositores. Install [imagescan](https://aur.archlinux.org/packages/imagescan/) for the base program. It should detect supported USB scanners automatically by default. If you want to make use of a network scanner you also have to install [imagescan-plugin-networkscan](https://aur.archlinux.org/packages/imagescan-plugin-networkscan/). Then edit `/etc/utsushi/utsushi.conf`, and enter the ip address of your scanner to it.

```
[devices]
myscanner.udi    = esci:networkscan://<ip-address-here>:1865
myscanner.vendor = Epson
myscanner.model  = Model-name

```

When you then start Image Scan v3, the name of the scan should be visible in the top left corner. If a connection problem happened, an error dialog will be shown.

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

### S300M

For the operation of the scanner S300M a firmware file `/usr/share/sane/epjitsu/300M_0C00.nal` is required, which can be downloaded [here](http://sange.fi/~atehwa/cgi-bin/piki.cgi/fujitsu%20scansnap%20s300%20firmware), or extracted from the Windows driver.

## HP

If your HP device [is supported by hplip](http://hplipopensource.com/hplip-web/supported_devices/index.html), [install](/index.php/Install "Install") the [hplip](https://www.archlinux.org/packages/?name=hplip) package.

The latter comes with 3 tools:

*   *hp-setup* to add and setup the device
*   *hp-plugin* is the 'HPLIP Plugin Download and Install Utility'.
*   *hp-scan* is the 'HPLIP Scan Utility'. If you need that tool, you will need to install [python-pillow](https://www.archlinux.org/packages/?name=python-pillow).

*hp-setup* requires Python Qt4 when run using the GUI (which is the default). To avoid installing the old Qt4 toolchain, you can run the CLI interface of hp-setup using `-i` as argument.

If the device is connected by USB, run *hp-setup* as root and follow the on screen instructions.

If your device is connected on the network, use `# hp-setup <printer ip>` instead.

### Alternative way to scan with network HP scanner

*   Find out IP address of your network HP scanner, for example *192.168.1.8*
*   Make device URI using hp-makeuri utility:

```
   hp-makeuri 192.168.1.8

```

*   Output should look like *hpaio:/net/DeskJet_3630_series?ip=192.168.1.8*
*   This URI could be given to xsane or scanimage tools, for example:

```
   xsane "hpaio:/net/DeskJet_3630_series?ip=192.168.1.8"
   scanimage --device "hpaio:/net/DeskJet_3630_series?ip=10.12.129.6" --format=png --resolution 300 >scan01.png

```

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