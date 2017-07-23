This article covers all non-specific (ie, not related to any one printer) troubleshooting of CUPS and printing drivers (but not problems related to printer sharing), including methods of determining the exact nature of the problem, and of solving the identified problem.

## Contents

*   [1 Introduction](#Introduction)
*   [2 Problems resulting from upgrades](#Problems_resulting_from_upgrades)
    *   [2.1 CUPS stops working](#CUPS_stops_working)
    *   [2.2 All jobs are "stopped"](#All_jobs_are_.22stopped.22)
    *   [2.3 All jobs are "The printer is not responding"](#All_jobs_are_.22The_printer_is_not_responding.22)
    *   [2.4 The PPD version is not compatible with gutenprint](#The_PPD_version_is_not_compatible_with_gutenprint)
    *   [2.5 Printers are not present in the print dialog for GTK3 applications](#Printers_are_not_present_in_the_print_dialog_for_GTK3_applications)
*   [3 Networking issues](#Networking_issues)
    *   [3.1 Unable to locate printer](#Unable_to_locate_printer)
    *   [3.2 Old CUPS server](#Old_CUPS_server)
    *   [3.3 CUPS identifies printer but cannot connect to it](#CUPS_identifies_printer_but_cannot_connect_to_it)
    *   [3.4 Shared printer works locally but remote machine fails to print](#Shared_printer_works_locally_but_remote_machine_fails_to_print)
*   [4 USB printers](#USB_printers)
    *   [4.1 Conflict with SANE](#Conflict_with_SANE)
    *   [4.2 Conflict with usblp](#Conflict_with_usblp)
*   [5 HP issues](#HP_issues)
    *   [5.1 CUPS: "/usr/lib/cups/backend/hp failed"](#CUPS:_.22.2Fusr.2Flib.2Fcups.2Fbackend.2Fhp_failed.22)
    *   [5.2 CUPS: Job is shown as complete but the printer does nothing](#CUPS:_Job_is_shown_as_complete_but_the_printer_does_nothing)
    *   [5.3 CUPS: '"foomatic-rip" not available/stopped with status 3'](#CUPS:_.27.22foomatic-rip.22_not_available.2Fstopped_with_status_3.27)
    *   [5.4 CUPS: "Filter failed"](#CUPS:_.22Filter_failed.22)
        *   [5.4.1 Missing foomatic-db](#Missing_foomatic-db)
        *   [5.4.2 Bad permissions](#Bad_permissions)
        *   [5.4.3 Avahi not enabled](#Avahi_not_enabled)
        *   [5.4.4 Out-of-date plugin](#Out-of-date_plugin)
    *   [5.5 CUPS: prints only an empty and an error-message page on HP LaserJet](#CUPS:_prints_only_an_empty_and_an_error-message_page_on_HP_LaserJet)
    *   [5.6 HPLIP 3.13: Plugin is installed, but HP Device Manager complains it is not](#HPLIP_3.13:_Plugin_is_installed.2C_but_HP_Device_Manager_complains_it_is_not)
    *   [5.7 hp-toolbox: "Unable to communicate with device"](#hp-toolbox:_.22Unable_to_communicate_with_device.22)
        *   [5.7.1 Permission problem](#Permission_problem)
        *   [5.7.2 Virtual CDROM printers](#Virtual_CDROM_printers)
        *   [5.7.3 Networked printers](#Networked_printers)
    *   [5.8 hp-setup asks to specify the PPD file for the discovered printer](#hp-setup_asks_to_specify_the_PPD_file_for_the_discovered_printer)
    *   [5.9 hp-setup: "Qt/PyQt 4 initialization failed"](#hp-setup:_.22Qt.2FPyQt_4_initialization_failed.22)
    *   [5.10 hp-setup: finds the printer automatically but reports "Unable to communicate with device" when printing test page immediately afterwards](#hp-setup:_finds_the_printer_automatically_but_reports_.22Unable_to_communicate_with_device.22_when_printing_test_page_immediately_afterwards)
*   [6 Other](#Other)
    *   [6.1 Printer "Paused" or "Stopped" with Status "Rendering completed"](#Printer_.22Paused.22_or_.22Stopped.22_with_Status_.22Rendering_completed.22)
        *   [6.1.1 Low ink](#Low_ink)
        *   [6.1.2 Permission issue](#Permission_issue)
    *   [6.2 Printing fails with unauthorised error](#Printing_fails_with_unauthorised_error)
    *   [6.3 Unknown supported format: application/postscript](#Unknown_supported_format:_application.2Fpostscript)
    *   [6.4 Print-Job client-error-document-format-not-supported](#Print-Job_client-error-document-format-not-supported)
    *   [6.5 Unable to get list of printer drivers](#Unable_to_get_list_of_printer_drivers)
    *   [6.6 lp: Error - Scheduler Not Responding](#lp:_Error_-_Scheduler_Not_Responding)
    *   [6.7 "Using invalid Host" error message](#.22Using_invalid_Host.22_error_message)
    *   [6.8 Cannot print from LibreOffice](#Cannot_print_from_LibreOffice)
    *   [6.9 Printer output shifted](#Printer_output_shifted)
    *   [6.10 Printer becomes stuck after a problem](#Printer_becomes_stuck_after_a_problem)

## Introduction

The best way to get printing working is to set 'LogLevel' in `/etc/cups/cupsd.conf` to:

```
LogLevel debug

```

And then viewing the output from `/var/log/cups/error_log` like this:

```
# tail -n 100 -f /var/log/cups/error_log

```

The characters at the left of the output stand for:

*   D=Debug
*   E=Error
*   I=Information
*   And so on

These files may also prove useful:

*   `/var/log/cups/page_log` - Echoes a new entry each time a print is successful
*   `/var/log/cups/access_log` - Lists all cupsd http1.1 server activity

Of course, it is important to know how CUPS works if wanting to solve related issues:

1.  An application sends a .ps file (PostScript, a script language that details how the page will look) to CUPS when 'print' has been selected (this is the case with most programs).
2.  CUPS then looks at the printer's PPD file (printer description file) and figures out what filters it needs to use to convert the .ps file to a language that the printer understands (like PJL, PCL), usually GhostScript.
3.  GhostScript takes the input and figures out which filters it should use, then applies them and converts the .ps file to a format understood by the printer.
4.  Then it is sent to the back-end. For example, if the printer is connected to a USB port, it uses the USB back-end.

Print a document and watch `error_log` to get a more detailed and correct image of the printing process.

## Problems resulting from upgrades

*Issues that appeared after CUPS and related program packages underwent a version increment*

### CUPS stops working

The chances are that a new configuration file is needed for the new version to work properly. Messages such as "404 - page not found" may result from trying to manage CUPS via localhost:631, for example.

To use the new configuration, copy `/etc/cups/cupsd.conf.default` to `/etc/cups/cupsd.conf` (backup the old configuration if needed) and restart CUPS to employ the new settings.

### All jobs are "stopped"

If all jobs sent to the printer become "stopped", delete the printer and add it again. Using the [CUPS web interface](http://localhost:631), go to Printers > Delete Printer.

To check the printer's settings go to *Printers*, then *Modify Printer*. Copy down the information displayed, click 'Modify Printer' to proceed to the next page(s), and so on.

### All jobs are "The printer is not responding"

On networked printers, you should check that the hostname in the printer's URI resolves to the printer's IP address via DNS, e.g. if your printer's connection looks like this:

```
lpd://BRN_020554/BINARY_P1

```

then the hostname 'BRN_020554' needs to resolve to the printer's IP from the server running CUPS. If [Avahi](/index.php/Avahi "Avahi") is being used, ensure that [Avahi's hostname resolution](/index.php/Avahi#Hostname_resolution "Avahi") is working.

Alternatively, replace the hostname used in the URI with the printer's IP address.

### The PPD version is not compatible with gutenprint

Run:

```
# /usr/bin/cups-genppdupdate

```

And restart CUPS (as pointed out in gutenprint's post-install message)

### Printers are not present in the print dialog for GTK3 applications

A recent upgrade of GTK3 (3.22) requires the [gtk3-print-backends](https://www.archlinux.org/packages/?name=gtk3-print-backends) package for printers to be listed in GTK3 print dialogs. This stops printing from applications like [gedit](/index.php/Gedit "Gedit"), [Chromium](/index.php/Chromium "Chromium"), and [Firefox](/index.php/Firefox "Firefox"), but printers still appear in the CUPS web interface and lpstat, and you can print from the command line and GTK2 applications like GIMP.

## Networking issues

### Unable to locate printer

Even if CUPS can detect networked printers, you may still end up with an "Unable to locate printer" error when trying to print something. The solution to this problem is to enable Avahi's [.local hostname resolution](/index.php/Avahi#Hostname_resolution "Avahi"). See [CUPS#Network](/index.php/CUPS#Network "CUPS") for details.

### Old CUPS server

As of CUPS version 1.6, the client defaults to IPP 2.0\. If the server uses CUPS <= 1.5 / IPP <= 1.1, the client does not downgrade the protocol automatically and thus cannot communicate with the server. A workaround is to append the `version=1.1` option documented at [[1]](https://www.cups.org/doc/network.html#TABLE2) to the URI.

### CUPS identifies printer but cannot connect to it

Enable debug logging. If you see `Executing backend "/usr/lib/cups/backend/dnssd"...` over and over switch from dnssd to socket in the printer configuration.

Example: `socket://192.168.11.6:9100`. The port number can be confirmed via [nmap](/index.php/Nmap "Nmap") or `telnet *your-printer-ip* 9100`.

### Shared printer works locally but remote machine fails to print

This is caused by a print job being sent through a filter twice, once on the local machine and once on the remote. See also the warning on the main [CUPS](/index.php/CUPS#Network_2 "CUPS") page.

## USB printers

### Conflict with SANE

If you are also running [SANE](/index.php/SANE "SANE"), it's possible that it is conflicting with CUPS. To fix this create a [Udev](/index.php/Udev "Udev") rule marking the device as matched by libsane:

 `/etc/udev/rules.d/99-printer.rules`  `ATTRS{idVendor}=="*vendor id*", ATTRS{idProduct}=="*product id*", MODE="0664", GROUP="lp", ENV{libsane_matched}="yes"` 

### Conflict with usblp

USB printers can be accessed using two methods: The usblp kernel module and libusb. The former is the classic way. It is simple: data is sent to the printer by writing it to a device file as a simple serial data stream. Reading the same device file allows bi-di access, at least for things like reading out ink levels, status, or printer capability information (PJL). It works very well for simple printers, but for multi-function devices (printer/scanner) it is not suitable and manufacturers like HP supply their own backends. Source: [here](http://lists.linuxfoundation.org/pipermail/printing-architecture/2012/002412.html).

**Warning:** As of [cups](https://www.archlinux.org/packages/?name=cups) version 1.6.0, it should no longer be necessary to blacklist the `usblp` kernel module. If you find out this is the only way to fix a remaining issue please report this upstream to the CUPS bug tracker and maybe also get in contact with Till Kamppeter (Debian CUPS maintainer). See [upstream bug](http://cups.org/str.php?L4128) for more info.

If you have problems getting your USB printer to work, you can try [blacklisting](/index.php/Blacklisting "Blacklisting") the `usblp` [kernel module](/index.php/Kernel_module "Kernel module"):

 `/etc/modprobe.d/blacklistusblp.conf` 
```
blacklist usblp

```

Custom kernel users may need to manually load the `usbcore` [kernel module](/index.php/Kernel_module "Kernel module") before proceeding.

Once the modules are installed, plug in the printer and check if the kernel detected it by running the following:

```
# journalctl -e

```

or

```
# dmesg

```

If you are using `usblp`, the output should indicate that the printer has been detected like so:

```
Feb 19 20:17:11 kernel: printer.c: usblp0: USB Bidirectional
printer dev 2 if 0 alt 0 proto 2 vid 0x04E8 pid 0x300E
Feb 19 20:17:11 kernel: usb.c: usblp driver claimed interface cfef3920
Feb 19 20:17:11 kernel: printer.c: v0.13: USB Printer Device Class driver

```

If you blacklisted `usblp`, you will see something like:

```
usb 3-2: new full speed USB device using uhci_hcd and address 3
usb 3-2: configuration #1 chosen from 1 choice

```

## HP issues

See also [CUPS/Printer-specific problems#HP](/index.php/CUPS/Printer-specific_problems#HP "CUPS/Printer-specific problems").

### CUPS: "/usr/lib/cups/backend/hp failed"

Make sure dbus is installed and running. If the error persists, try starting avahi-daemon.

Try adding the printer as a Network Printer using the http:// protocol.

**Note:** There might need to set permissions issues right.

### CUPS: Job is shown as complete but the printer does nothing

This happens on HP printers when you select the (old) hpijs driver (e.g. the Deskjet D1600 series). Use the hpcups driver instead.

Some HP printers require their firmware to be downloaded from the computer every time the printer is switched on. If there is an issue with udev (or equivalent) and the firmware download rule is never fired, you may experience this issue. As a workaround, you can manually download the firmware to the printer. Ensure the printer is plugged in and switched on, then run

```
hp-firmware -n

```

### CUPS: '"foomatic-rip" not available/stopped with status 3'

If receiving any of the following error messages in `/var/log/cups/error_log` while using a HP printer, with jobs appearing to be processed while they all end up not being completed with their status set to 'stopped':

```
Filter "foomatic-rip" for printer *printer_name* not available: No such file or director

```

or:

```
PID *pid* (/usr/lib/cups/filter/foomatic-rip) stopped with status 3!

```

make sure [hplip](https://www.archlinux.org/packages/?name=hplip) has been [installed](/index.php/Installed "Installed").

### CUPS: "Filter failed"

A "filter failed" error can be caused by any number of issues. The CUPS error log should record which filter failed and why.

#### Missing foomatic-db

Install [foomatic-db](https://www.archlinux.org/packages/?name=foomatic-db) and [foomatic-db-ppds](https://www.archlinux.org/packages/?name=foomatic-db-ppds). This fixes it in some cases.

#### Bad permissions

Change the permissions of the printer USB port. Get the bus and device number from `lsusb`, then set the permission using:

 ` lsusb `  ` Bus <BUSID> Device <DEVID>: ID <PRINTERID>:<VENDOR> Hewlett-Packard DeskJet D1360` 

Then substitute the provided device information to the

```
# chmod 0666 /dev/bus/usb/<BUSID>/<DEVID>

```

To make the persistent permission change that will be triggered automatically each time the computer is rebooted, add the following line.

 `/etc/udev/rules.d/10-local.rules`  `SUBSYSTEM=="usb", ATTRS{idVendor}=="<VENDOR>", ATTRS{idProduct}=="<PRINTERID>", GROUP="lp", MODE:="666"` 

Each system may vary, so consult [udev#List attributes of a device](/index.php/Udev#List_attributes_of_a_device "Udev") wiki page.

#### Avahi not enabled

[Start](/index.php/Start "Start"), and [enable](/index.php/Enable "Enable") the `avahi-daemon` service.

#### Out-of-date plugin

This error can also indicate that the plugin is out of date (version is mismatched). If you have installed [hplip-plugin](https://aur.archlinux.org/packages/hplip-plugin/), you will need to update the package.

### CUPS: prints only an empty and an error-message page on HP LaserJet

There is a bug that causes CUPS to fail when printing images on HP LaserJet (in my case 3380). The bug has been reported and fixed by [Ubuntu](https://bugs.launchpad.net/ubuntu/+source/cups-filters/+bug/998087). The first page is empty, the second page contains the following error message:

```
 ERROR:
 invalidaccess
 OFFENDING COMMAND:
 filter
 STACK:
 /SubFileDecode
 endstream
 ...

```

In order to fix the issue, run the following command as root:

```
# lpadmin -p *printer* -o pdftops-renderer-default=pdftops

```

### HPLIP 3.13: Plugin is installed, but HP Device Manager complains it is not

The issue might have to do with the file permission change that had been made to `/var/lib/hp/hplip.state`. To correct the issue, a simple `chmod 644 /var/lib/hp/hplip.state` and `chmod 755 /var/lib/hp` should be sufficient. For further information, please read this [link](https://bugs.launchpad.net/hplip/+bug/1131596).

### hp-toolbox: "Unable to communicate with device"

```
# hp-toolbox
# error: Unable to communicate with device (code=12): hp:/usb/*printer id*

```

#### Permission problem

It may be needed to add the user to the `lp` and `sys` [groups](/index.php/Group "Group").

#### Virtual CDROM printers

This can also be caused by printers such as the P1102 that provide a virtual CD-ROM drive for MS Windows drivers. The lp dev appears and then disappears. In that case, try the **usb-modeswitch** and **usb-modeswitch-data** packages, that lets one switch off the "Smart Drive" (udev rules included in said packages).

#### Networked printers

This can also occur with network attached printers using dynamic hostnames if the [avahi-daemon](/index.php/Avahi "Avahi") is not running. Another possibility is that *hp-setup* failed to locate the printer because the IP address of the the printer changed due to DHCP. If this is the case, consider adding a DHCP reservation for the printer in the DHCP server's configuration.

### hp-setup asks to specify the PPD file for the discovered printer

Install and start CUPS before running hp-setup.

### hp-setup: "Qt/PyQt 4 initialization failed"

[Install](/index.php/Install "Install") [python-pyqt4](https://www.archlinux.org/packages/?name=python-pyqt4), which is an optdepend of [hplip](https://www.archlinux.org/packages/?name=hplip). Alternatively, to run hp-setup with the command line interface, use the `-i` flag.

### hp-setup: finds the printer automatically but reports "Unable to communicate with device" when printing test page immediately afterwards

This at least happens to hplip 3.13.5-2 for HP Officejet 6500A through local network connection. To solve the problem, specify the IP address of the HP printer for hp-setup to locate the printer.

## Other

### Printer "Paused" or "Stopped" with Status "Rendering completed"

#### Low ink

When low on ink, some printers will get stuck in "Rendering completed" status and, if it is a network printer, the printer may even become unreachable from CUPS' perspective despite being properly connected to the network. Replacing the low/depleted ink cartridge(s) in this setting will return the printer to "Ready" status and, if it is a network printer, will make the printer available to CUPS again.

**Note:** If you use third-party ink cartridges, the ink levels reported by the printer may be inaccurate. If you use third-party ink and your printer used to work fine but is now getting stuck on "Rendering completed" status, replace the ink cartridges regardless of the reported ink levels before trying other fixes.

#### Permission issue

Prior to [cups](https://www.archlinux.org/packages/?name=cups) 2.0.0-2, if the group set in the `Group` directive is also listed in the `SystemGroup` directive in `/etc/cups/cups-files.conf`, `cupsd` will instead run any helper programs with a group of `nobody`. However, the helpers may need to write to printer devices, which are created with user `root` and group `lp`, and will be unable to if they are run with a group of `nobody`, causing the print queue to become "Paused" or "Stopped".

To fix this, ensure that the the `Group` directive is set to `lp`, and the `SystemGroup` directive does not include `lp`.

Fixed in Arch with [[2]](https://git.archlinux.org/svntogit/packages.git/commit/trunk?h=packages/cups&id=c20b22f4f996cb08b1aa856d4c8991e869459eb2).

### Printing fails with unauthorised error

If a remote printer requests authentication CUPS will automatically add an `AuthInfoRequired` directive to the printer in `/etc/cups/printers.conf`. However, some graphical applications (for instance, some versions of [LibreOffice](/index.php/LibreOffice "LibreOffice") [[3]](https://bugs.documentfoundation.org/show_bug.cgi?id=53029)) have no way to prompt for credentials, so printing fails. To fix this include the required username and password in the URI. See [[4]](https://bugs.launchpad.net/ubuntu/+source/cups/+bug/283811), [[5]](https://bbs.archlinux.org/viewtopic.php?id=61826),

### Unknown supported format: application/postscript

Comment the lines:

```
application/octet-stream        application/vnd.cups-raw        0      -

```

from `/etc/cups/mime.convs`, and:

```
application/octet-stream

```

in `/etc/cups/mime.types`.

### Print-Job client-error-document-format-not-supported

Try installing the foomatic packages and use a foomatic driver.

### Unable to get list of printer drivers

(Also applicable to error "-1 not supported!")

Try to remove Foomatic drivers or refer to [CUPS/Printer-specific problems#HPLIP Driver](/index.php/CUPS/Printer-specific_problems#HPLIP_Driver "CUPS/Printer-specific problems") for a workaround.

### lp: Error - Scheduler Not Responding

If you get this error, ensure [CUPS](/index.php/CUPS "CUPS") is running, the environmental variable `CUPS_SERVER` is unset, and that `/etc/cups/client.conf` is correct.

### "Using invalid Host" error message

Try adding `ServerAlias *` into `/etc/cups/cupsd.conf`.

### Cannot print from LibreOffice

If you can print a test page from the [CUPS](/index.php/CUPS "CUPS") web interface, but not from [LibreOffice](/index.php/LibreOffice "LibreOffice"), try to [install](/index.php/Install "Install") the [a2ps](https://www.archlinux.org/packages/?name=a2ps) package.

### Printer output shifted

This seems to be caused by the wrong page size being set in [CUPS](/index.php/CUPS "CUPS").

### Printer becomes stuck after a problem

When an issue arises during printing, the printer in CUPS may become unresponsive. `lpq` reports that the printer `is not ready`. It can be reactivated using `cupsenable`. To automatically have CUPS reactivate the printer, change [ErrorPolicy](https://www.cups.org/doc/man-cupsd.conf.html?TOPIC=Man+Pages#ErrorPolicy) from the default `stop-printer` to `retry-this-job`.