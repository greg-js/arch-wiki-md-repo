This article contains scanner or manufacturer-specific instructions for [SANE](/index.php/SANE "SANE").

## Contents

*   [1 BenQ/Acer](#BenQ.2FAcer)
*   [2 Brother](#Brother)
    *   [2.1 Network Scanning](#Network_Scanning)
    *   [2.2 Invalid argument](#Invalid_argument)
    *   [2.3 Scan-key-tool](#Scan-key-tool)
    *   [2.4 xsane crashes](#xsane_crashes)
*   [3 Canon](#Canon)
    *   [3.1 Scanning over the network with Canon Pixma all-in-one printer/scanners](#Scanning_over_the_network_with_Canon_Pixma_all-in-one_printer.2Fscanners)
    *   [3.2 Cannot read scanner make and model](#Cannot_read_scanner_make_and_model)
*   [4 Epson](#Epson)
    *   [4.1 Epson Perfection 1270](#Epson_Perfection_1270)
*   [5 Fujitsu](#Fujitsu)
    *   [5.1 S300M](#S300M)
*   [6 HP](#HP)
*   [7 Mustek](#Mustek)
    *   [7.1 BearPaw 2400CU](#BearPaw_2400CU)
*   [8 Samsung](#Samsung)

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

In order to install a Brother scanner or printer/scanner combo you need the right driver. To find the right one, search for your model at the [Brother Linux scanner page](http://support.brother.com/g/s/id/linux/en/download_scn.html).

Then, install the appropriate package:

*   [brscan2](https://aur.archlinux.org/packages/brscan2/)
*   [brscan3](https://aur.archlinux.org/packages/brscan3/)
*   [brscan4](https://aur.archlinux.org/packages/brscan4/)
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

In case of network scanning, e.g. by WiFi, Sane is still unable to find the scanner. You need to specify the IP address of the scanner in the corresponding net.conf file of sane. So for instance if the scanner is at IP address 192.168.1.100 do:

```
   echo 192.168.1.100 | sudo tee -a /etc/sane.d/net.conf

```

Now use `scanimage --check-devices` do check whether sane is able to find your scanner. If not, further check that Sane expects this device through the network (see [http://neithere.net/2013/02/18/archlinux_brother_7860.html](http://neithere.net/2013/02/18/archlinux_brother_7860.html)).

Check it:

```
   $ grep brother /etc/sane.d/dll.conf
      brother4

```

If nothing was found (it must fit exactly brother4), add it:

```
   $ echo brother4 | sudo tee -a /etc/sane.d/dll.conf
   $ scanimage -L

```

The scanner should now appear in the list.

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

Sane should now find your device. For more details refer to `man sane-pixma`.

### Cannot read scanner make and model

If you have a Canon multi function printer/scanner and get an error message of the following kind:

```
Cannot read mac address, skipping this scanner
Cannot read scanner make & model: bjnp://

```

and the scanner refuses to connect, then it may be because you have a newer scanner using the mfnp, and not the bjnp protocol. Unfortunately, this scanner may not be supported (yet) by the current sane version. However, you can install [sane-git](https://aur.archlinux.org/packages/sane-git/) to get a version supporting mfnp reasonably well. (And make sure that the scanner is in "remote" scanning mode - otherwise it will not communicate it's scanning capabilities over the network at all)

## Epson

With Epson scanners, you can use "Image Scan! for Linux".

*   Install the [iscan](https://www.archlinux.org/packages/?name=iscan) package
*   Install the appropriate iscan-plugin package for your scanner (for example, [iscan-plugin-gt-x820](https://aur.archlinux.org/packages/iscan-plugin-gt-x820/) for the Epson Perfection Photo V600)
*   Add your user to the "scanner" group
*   Reboot, so that udev will recognize the device as a scanner and apply appropriate permissions

For network (including Wi-Fi) scanners, install [iscan](https://www.archlinux.org/packages/?name=iscan) and [iscan-plugin-network](https://aur.archlinux.org/packages/iscan-plugin-network/), then edit `/etc/sane.d/epkowa.conf` and add the line:

```
net {IP_OF_SCANNER}

```

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

Finally. If you still get the `Error I/O` messages try to check the transportation lock of the scanner. It is on the bottom of the scanner. It must be opened.

## Fujitsu

### S300M

For the operation of the scanner S300M a firmware file `/usr/share/sane/epjitsu/300M_0C00.nal` is required, which can be downloaded [here](http://sange.fi/~atehwa/cgi-bin/piki.cgi/fujitsu%20scansnap%20s300%20firmware), or extracted from the Windows driver.

## HP

If your HP device [is supported by hplip](http://hplipopensource.com/hplip-web/supported_devices/index.html), install the [install](/index.php/Install "Install") the [hplip](https://www.archlinux.org/packages/?name=hplip) package.

The latter comes with 3 tools:

*   `hp-setup` to add and setup the device
*   `hp-plugin` is the 'HPLIP Plugin Download and Install Utility'.
*   `hp-scan` is the 'HPLIP Scan Utility'. If you need that tool, you will need to install [python-pillow](https://www.archlinux.org/packages/?name=python-pillow).

`hp-setup` requires Python Qt4 when run using the GUI (which is the default). To avoid installing the old Qt4 toolchain, you can run hp-setup in CLI using `-i` as argument.

If your device is plugged as USB, run `hp-setup` as root and follow the on screen instructions.

If your devices is connected on the network, run `hp-setup` like this:

```
# hp-setup <printer ip>

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

When plugging in a usb2 printer/scanner to a usb3 interface there is currently a bug in the xhci kernel code that causes the xsane process to hang when the scanner is connected. In the event of a multi-function Samsung printer having an ethernet or wireless interface then it is possible to access the scanner over the network rather than the usb interface by adding in a line to the file /etc/sane.d/xerox_mfp.conf such as

```
#Samsung scx4500w wireless ip network address
tcp xx.xx.xx.xx

```

where xx.xx.xx.xx is the static ip address of the printer.

Then when xsane starts up you can choose the network tcp access option instead of the usb line, and the scanner will be accessed via the network instead of the usb port and avoid the current usb3 issues.