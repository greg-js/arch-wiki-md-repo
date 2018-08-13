Related articles

*   [SANE/Scanner-specific problems](/index.php/SANE/Scanner-specific_problems "SANE/Scanner-specific problems")
*   [Scanner Button Daemon](/index.php/Scanner_Button_Daemon "Scanner Button Daemon")

[SANE](http://www.sane-project.org/) ([Scanner Access Now Easy](https://en.wikipedia.org/wiki/Scanner_Access_Now_Easy "wikipedia:Scanner Access Now Easy")) provides a library and a command-line tool to use scanners under GNU/Linux. See [[1]](http://www.sane-project.org/sane-supported-devices.html) to check if sane supports your scanner.

## Contents

*   [1 Installation](#Installation)
*   [2 Verification](#Verification)
*   [3 Installing a scanner driver](#Installing_a_scanner_driver)
    *   [3.1 Firmware](#Firmware)
*   [4 Install a frontend](#Install_a_frontend)
*   [5 Network scanning](#Network_scanning)
    *   [5.1 Sharing your scanner over a network](#Sharing_your_scanner_over_a_network)
    *   [5.2 Accessing your scanner from a remote workstation](#Accessing_your_scanner_from_a_remote_workstation)
    *   [5.3 Windows clients](#Windows_clients)
*   [6 Troubleshooting](#Troubleshooting)
    *   [6.1 Invalid argument](#Invalid_argument)
        *   [6.1.1 Missing firmware file](#Missing_firmware_file)
        *   [6.1.2 Wrong firmware file permissions](#Wrong_firmware_file_permissions)
        *   [6.1.3 Multiple backends claim scanner](#Multiple_backends_claim_scanner)
        *   [6.1.4 Communication via xHCI not working (older scanner models)](#Communication_via_xHCI_not_working_.28older_scanner_models.29)
    *   [6.2 Slow startup](#Slow_startup)
    *   [6.3 Device busy](#Device_busy)
    *   [6.4 Permission problem](#Permission_problem)
        *   [6.4.1 Parallel port scanners](#Parallel_port_scanners)

## Installation

[Install](/index.php/Install "Install") the [sane](https://www.archlinux.org/packages/?name=sane) package.

## Verification

Now you can try to see if sane recognizes your scanner

```
$ scanimage -L

```

If that fails, run the command again as root to check for permission problems. If that fails as well, check that your scanner is plugged into the computer. You also might have to unplug/plug your scanner for `/usr/lib/udev/rules.d/49-sane.rules` to recognize your scanner.

Now you can see if it actually works

```
$ scanimage --format=png > test.png

```

If the scanning fails with the message `scanimage: sane_start: Invalid argument` you may need to specify the device.

 `$ scanimage -L` 
```
device `v4l:/dev/video0' is a Noname Video WebCam virtual device
device `pixma:04A91749_247936' is a CANON Canon PIXMA MG5200 multi-function peripheral

```

Then you would need to run

```
$ scanimage --device "pixma:04A91749_247936" --format=tiff > test.tiff

```

Sane provides many special backend options for numerous scanner types. To see what these are for your device:

```
$ scanimage -A

```

## Installing a scanner driver

Most scanners should work out of the box. If yours does not, see [SANE/Scanner-specific problems](/index.php/SANE/Scanner-specific_problems "SANE/Scanner-specific problems") for installation instructions.

### Firmware

**Note:** This section is only needed if you need to upload firmware to your scanner.

Firmwares usually have the **`.bin`** extension.

Firstly you need to put the firmware someplace safe, it is recommended to put it in a subdirectory of `/usr/share/sane/`.

Then you need to tell sane where the firmware is:

*   Find the name of the backend for your scanner from the [sane supported devices list](http://www.sane-project.org/sane-supported-devices.html).
*   Open the file `/etc/sane.d/*<backend-name>*.conf`.
*   Make sure the firmware entry is uncommented and let the file-path point to where you put the firmware file for your scanner. Be sure that members of the group `scanner` can access the `/etc/sane.d/*<backend-name>*.conf` file.

If the backend of your scanner is not part of the sane package (such as `hpaio.conf` which is part of [hplip](https://www.archlinux.org/packages/?name=hplip)), you need to uncomment the relevant entry in `/etc/sane.d/dll.d` or in `/etc/sane.d/dll.conf`.

## Install a frontend

Many frontends exist for SANE, a non-exhaustive list of which can be found on the [sane-project website](http://www.sane-project.org/sane-frontends.html).

*   **[gscan2pdf](https://en.wikipedia.org/wiki/Scanner_Access_Now_Easy#gscan2pdf "wikipedia:Scanner Access Now Easy")** — Scans, runs an OCR engine, minor post-processing, creates a document.

	[http://gscan2pdf.sourceforge.net/](http://gscan2pdf.sourceforge.net/) || [gscan2pdf](https://www.archlinux.org/packages/?name=gscan2pdf)

*   **[OCRFeeder](https://en.wikipedia.org/wiki/OCRFeeder "wikipedia:OCRFeeder")** — Python GUI for Gnome which performs document analysis and rendition, and can use either CuneiForm, GOCR, Ocrad or Tesseract as OCR engines. It can import from PDF or image files, and export to HTML or OpenDocument.

	[https://wiki.gnome.org/Apps/OCRFeeder](https://wiki.gnome.org/Apps/OCRFeeder) || [ocrfeeder](https://www.archlinux.org/packages/?name=ocrfeeder)

*   **[Simple Scan](https://en.wikipedia.org/wiki/Scanner_Access_Now_Easy#Simple_Scan "wikipedia:Scanner Access Now Easy")** — Simplified GUI that is intended to be easier to use and better integrated into the [GNOME](/index.php/GNOME "GNOME") desktop than XSane. It was initially written for Ubuntu and is maintained by Robert Ancell of Canonical Ltd. for GNU/Linux.

	[https://launchpad.net/simple-scan](https://launchpad.net/simple-scan) || [simple-scan](https://www.archlinux.org/packages/?name=simple-scan)

*   **[Skanlite](https://en.wikipedia.org/wiki/Skanlite "wikipedia:Skanlite")** — Simple image scanning application that does nothing more than scan and save images, based on the KSane backend.

	[https://www.kde.org/applications/graphics/skanlite](https://www.kde.org/applications/graphics/skanlite) || [skanlite](https://www.archlinux.org/packages/?name=skanlite)

*   **[XSane](https://en.wikipedia.org/wiki/Scanner_Access_Now_Easy#XSane "wikipedia:Scanner Access Now Easy")** — Full-featured GTK-based frontend looking a bit old but providing extended functionalities.

	[http://www.xsane.org/](http://www.xsane.org/) || [xsane](https://www.archlinux.org/packages/?name=xsane)

**Note:** Scanning directly to PDF using XSane in 16bit color depth mode is known to produces [corrupted files](https://bugs.launchpad.net/ubuntu/+source/xsane/+bug/539162) and a note in `pacman` output warns so. 8bit mode is known to work.

**Note:** Using a frontend doesn't mean you do not have to apply some tricks. This is especially true with devices configured via [mDNS](/index.php/MDNS "MDNS"). For example, `skanlite` needs to have additional info specified on the command line in order to detect a network scanner properly as it can't handle mDNS. Here is an example with an HP Officejet Pro L7590: `skanlite --device "hpaio:/net/Officejet_Pro_L7500?ip=192.168.0.17"`.

## Network scanning

### Sharing your scanner over a network

You can share your scanner with other hosts on your network who use *sane*, *xsane* or xsane-enabled *GIMP*. To set up the server, first indicate which hosts on your network are allowed access.

Change the `/etc/sane.d/saned.conf` file to your liking, for example:

```
# required
localhost
# allow local subnet
192.168.0.0/24

```

If you use [iptables](/index.php/Iptables "Iptables"), [insert](/index.php/Kernel_modules "Kernel modules") the `nf_conntrack_sane` module to let the firewall track `saned` connections.

Now [start/enable](/index.php/Start/enable "Start/enable") `saned.socket`. Your scanner is now available over the network. For more information, see [saned(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/saned.8).

**Note:** saned intentionally refuses to share scanners that use the net: backend (which includes some USB scanners). There is a crude patch to allow this in [FS#54786](https://bugs.archlinux.org/task/54786), but note it may cause problems on some networks. Check output of `scanimage -L` on the server to see the scanner url.

### Accessing your scanner from a remote workstation

**Note:** Some network scanners require a different approach. See [SANE/Scanner-specific problems](/index.php/SANE/Scanner-specific_problems "SANE/Scanner-specific problems").

You can access your network-enabled scanner from a remote Arch Linux workstation.

First, specify the server's host name or IP address in the `/etc/sane.d/net.conf` file:

```
# static IP address
192.168.0.1
# or host name
stratus

```

Now test your workstation's connection:

```
$ scanimage -L

```

The network scanner should now also show up in any [front-end](#Install_a_frontend).

### Windows clients

Since the Windows port of SANE seems to be [unsupported, outdated and difficult to get](http://www.xsane.org/xsane-download.html), you can try [SaneTwain](http://sanetwain.ozuzo.net/) instead.

## Troubleshooting

	See also: [SANE/Scanner-specific problems](/index.php/SANE/Scanner-specific_problems "SANE/Scanner-specific problems")

### Invalid argument

If you get an "Invalid argument" error with xsane or another sane front-end, this could be caused by one of the following reasons:

#### Missing firmware file

No firmware file was provided for the used scanner (see [#Firmware](#Firmware) for details).

#### Wrong firmware file permissions

The permissions for the used firmware file are wrong. Correct them using

```
# chown root:scanner /usr/share/sane/*SCANNER_MODEL*/*FIRMWARE_FILE*
# chmod ug+r /usr/share/sane/*SCANNER_MODEL*/*FIRMWARE_FILE*

```

#### Multiple backends claim scanner

It may happen, that multiple backends support (or pretend to support) your scanner, and sane chooses one that does not do after all (the scanner will not be displayed by `scanimage -L` then). This has happened with older Epson scanners and the `epson2` resp. `epson` backends. In this case, the solution is to comment out the unwanted backend in `/etc/sane.d/dll.conf`. In the Epson case, that would be to change

```
epson2
#epson

```

to

```
#epson2
epson

```

It may also be possible that the independent [iscan](https://www.archlinux.org/packages/?name=iscan) `epkowa` backend interferes with your `snapscan` backend (epson scanners). You may get this error right after using the `scanimage -L` command. Starting the scanner app (like [xsane](https://www.archlinux.org/packages/?name=xsane)) twice can also solve the problem. Otherwise check your `/etc/sane.d/epkowa.conf` for wrong configurations or remove the [iscan](https://www.archlinux.org/packages/?name=iscan) package.

#### Communication via xHCI not working (older scanner models)

Some older scanner models do not work when connected via an USB3 port. If you experience this issue, try setting the `SANE_USB_WORKAROUND=1` [environment variable](/index.php/Environment_variable "Environment variable") before starting your frontend.[[2]](https://lists.alioth.debian.org/pipermail/sane-announce/2017/000036.html)[[3]](https://anonscm.debian.org/cgit/sane/sane-backends.git/commit/?id=1207ce5a40664c04b934bd0a6babbc1575361356)

If that does not work, try one of the following workarounds:

*   Use an USB2 port instead of an USB3 port, if available.
*   Disable xHCI via BIOS/EFI. eHCI will consequently be used and communication with the scanner will work. On the downside, USB3 speed can not be reached on any port.
*   On (some) intel chipsets the `setpci` command can be used to route specific usb ports to either the xHCI or the eHCI controller. See [here](https://forums.opensuse.org/showthread.php/507627-Suse-13-2-scanner-no-longer-working-on-64-bit-version?p=2714695#post2714695) and [here](https://superuser.com/questions/812022/force-a-single-usb-3-0-port-to-work-as-usb-2-0) (scroll down to where it says "setpci") for further information. With this it is possible to toggle single USB ports with a simple shell script.
*   Connect the scanner over the network instead if it is supported.

### Slow startup

If you encounter slow startup issue (e.g. `xsane` or `scanimage -L` take a lot to find scanner) it may be that more than one driver supporting it is available.

Have a look at `/etc/sane.d/dll.conf` and try commenting out one (e.g. you may have `epson`, `epson2` and `epkowa` enabled at the same time, try leaving only `epson` or `epkowa` uncommented).

You can also try to comment out `net` driver, if there are no network scanners.

Your [webcam](/index.php/Webcam "Webcam") might also be listed as scanning device and slow down detection at startup. To blacklist webcam, try commenting out all the lines in `/etc/sane.d/v4l.conf`.

### Device busy

If your USB device is listed with `scanimage -L` but launching the test `scanimage pixma:04A9173E_11DAD1 --format=tiff > test.tiff` always return the 'Device busy' error, you might try to add your username to the scanner group `usermod -a -G scanner yourusername` then blacklist the `usblp` kernel module by writing `blacklist usblp` in `/etc/modprobe.d/no-usblp.conf` (it prevents `usblp` from loading to support scanning, not needed by either CUPS or xsane and related tools). Reboot to finish. [[4]](http://cromwell-intl.com/linux/canon-pixma-printer-scanner.html)

### Permission problem

After systemd, the `scanner` and `lp` groups are deprecated. No need to add your user to those groups. See [Users and groups#Pre-systemd groups](/index.php/Users_and_groups#Pre-systemd_groups "Users and groups") for detail.

You can also try to change permissions of usb device but this is not recommended, a better solution is to fix the [Udev rules](/index.php/Udev_rules "Udev rules") so that your scanner is recognized.

First check connected usb devices with `lsusb`:

```
Bus 006 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub
Bus 005 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub
Bus 004 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub
Bus 003 Device 003: ID 04d9:1603 Holtek Semiconductor, Inc.
Bus 003 Device 002: ID 04fc:0538 Sunplus Technology Co., Ltd
Bus 003 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub
Bus 002 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub
Bus 001 Device 006: ID 03f0:2504 Hewlett-Packard
Bus 001 Device 002: ID 046d:0802 Logitech, Inc. Webcam C200
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub

```

In our example we see the scanner: `Bus 001 Device 006: ID 03f0:2504 Hewlett-Packard`. Here `03f0` is the *vendorID* and `2504` is the *productID*.

Now open `/usr/lib/udev/rules.d/49-sane.rules` and see if there is there is a line with the *vendorID* and *productID* of your scanner. If there is not any, create the new file `/etc/udev/rules.d/49-sane-missing-scanner.rules`, with the following contents:

```
ATTRS{idVendor}=="**vendorID**", ATTRS{idProduct}=="**productID**", MODE="0664", GROUP="scanner", ENV{libsane_matched}="yes"

```

Save the file, plug out and back in your scanner and the file permissions should be now correct.

Another tip, is that you can add your device (scanner) in backend file:

Add `usb 0x03f0 0x2504` to `/etc/sane.d/hp4200.conf` so it looks like this:

```
#
# Configuration file for the hp4200 backend
#
#
# HP4200
#usb 0x03f0 0x0105
usb 0x03f0 0x2504

```

#### Parallel port scanners

All devices attached to a parallel port are assumed to be printers, and are given a `lp` group. Either create a [udev](/index.php/Udev "Udev") rule to mark the relevant parallel port as `libsane_matched`, or add your user to the `lp` [group](/index.php/Group "Group"). CUPS also uses the `lp` group for read-only access to configuration files, so there are potential security implications to adding users to the `lp` group - see [CUPS#Connection Interfaces](/index.php/CUPS#Connection_Interfaces "CUPS") for more information.